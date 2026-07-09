<script lang="ts">
  import { onDestroy } from 'svelte';
  import { ChoiceGroup, QuestionHeader, SurveyLayout } from '@survey/ui';
  import IntroScreen from '$lib/components/IntroScreen.svelte';
  import LoadingScreen from '$lib/components/LoadingScreen.svelte';
  import ResultScreen from '$lib/components/ResultScreen.svelte';

  type Choice = {
    value: string;
    label: string;
  };

  type Question = {
    id: string;
    title: string;
    choices: Choice[];
  };

  type Result = {
    title: string;
    evidence: string[];
  };

  const requiredQuestions: Question[] = [
    {
      id: 'gender',
      title: '您的性别是？',
      choices: [
        { value: 'female', label: '女' },
        { value: 'male', label: '男' },
        { value: 'walmart_bag', label: '沃尔玛购物袋' },
        { value: 'attack_helicopter', label: '武装直升机' }
      ]
    },
    {
      id: 'breakfast',
      title: '今天吃早餐了吗？',
      choices: [
        { value: 'yes', label: '吃了' },
        { value: 'no', label: '没吃' },
        { value: 'coffee', label: '咖啡算早餐' }
      ]
    },
    {
      id: 'lunch',
      title: '今天吃午餐了吗？',
      choices: [
        { value: 'yes', label: '吃了' },
        { value: 'no', label: '没吃' },
        { value: 'late', label: '下午才想起来' }
      ]
    },
    {
      id: 'dinner',
      title: '今天吃晚餐了吗？',
      choices: [
        { value: 'yes', label: '吃了' },
        { value: 'no', label: '还没' },
        { value: 'snack', label: '零食顶上了' }
      ]
    }
  ];

  const bonusQuestions: Question[] = [
    {
      id: 'socks',
      title: '今天袜子状态如何？',
      choices: [
        { value: 'same', label: '成双成对' },
        { value: 'odd', label: '看起来不是一家的' },
        { value: 'none', label: '拒绝袜子' }
      ]
    },
    {
      id: 'elevator',
      title: '电梯到了您会先看哪里？',
      choices: [
        { value: 'floor', label: '楼层数字' },
        { value: 'mirror', label: '镜子里的自己' },
        { value: 'door', label: '门缝，防止被剧情选中' }
      ]
    },
    {
      id: 'charger',
      title: '手机电量低于多少会紧张？',
      choices: [
        { value: '50', label: '50%' },
        { value: '20', label: '20%' },
        { value: '1', label: '1% 还能聊' }
      ]
    },
    {
      id: 'noodle',
      title: '泡面调料包应该怎么放？',
      choices: [
        { value: 'before', label: '先放' },
        { value: 'after', label: '后放' },
        { value: 'half', label: '只放一半，保持神秘' }
      ]
    }
  ];

  let screen = $state<'intro' | 'question' | 'loading' | 'result'>('intro');
  let questions = $state<Question[]>([]);
  let answers = $state<Record<string, string>>({});
  let currentIndex = $state(0);
  let result = $state<Result | null>(null);
  let timer: ReturnType<typeof setTimeout> | undefined;

  let currentQuestion = $derived(questions[currentIndex]);
  let selected = $derived(currentQuestion ? (answers[currentQuestion.id] ?? '') : '');
  let progress = $derived(questions.length ? ((currentIndex + 1) / questions.length) * 100 : 0);
  let progressLabel = $derived(`第 ${currentIndex + 1} 题，共 ${questions.length} 题`);
  let isLastQuestion = $derived(currentIndex === questions.length - 1);

  function shuffle<T>(items: T[]) {
    return items
      .map((item) => ({ item, sort: Math.random() }))
      .sort((a, b) => a.sort - b.sort)
      .map(({ item }) => item);
  }

  function start() {
    const bonusCount = 1 + Math.floor(Math.random() * 3);

    questions = [...requiredQuestions, ...shuffle(bonusQuestions).slice(0, bonusCount)];
    answers = {};
    currentIndex = 0;
    result = null;
    screen = 'question';
  }

  function choose(value: string) {
    answers = { ...answers, [currentQuestion.id]: value };
    navigator.vibrate?.(50);
  }

  function back() {
    if (currentIndex === 0) {
      screen = 'intro';
      return;
    }

    currentIndex -= 1;
  }

  function next() {
    if (!selected) return;

    if (!isLastQuestion) {
      currentIndex += 1;
      return;
    }

    screen = 'loading';
    timer = setTimeout(() => {
      result = getResult();
      screen = 'result';
    }, 1400);
  }

  function restart() {
    if (timer) clearTimeout(timer);
    start();
  }

  function choiceLabel(questionId: string) {
    const question = questions.find((item) => item.id === questionId);
    return question?.choices.find((choice) => choice.value === answers[questionId])?.label ?? '未记录';
  }

  function getResult(): Result {
    const skippedMeals = ['breakfast', 'lunch', 'dinner'].filter((id) => answers[id] !== 'yes').length;
    const oddScore = Object.values(answers).join('').length + skippedMeals * 3;
    const titles = [
      '父亲是男性，母亲是女性',
      '父亲是女性，母亲是男性',
      '父亲是母亲，母亲是父亲',
      '父亲是男性，母亲也是男性',
      '父亲是女性，母亲也是女性',
      '父亲是母亲，母亲还是母亲'
    ];

    return {
      title: titles[oddScore % titles.length],
      evidence: [
        `性别输入为「${choiceLabel('gender')}」，先作为第一层线索。`,
        `三餐里有 ${skippedMeals} 项没有正常吃，亲属关系开始发生偏转。`,
        `早餐：「${choiceLabel('breakfast')}」；午餐：「${choiceLabel('lunch')}」；晚餐：「${choiceLabel('dinner')}」。三餐顺序决定父母顺序。`,
        `附加题选到了「${questions.slice(4).map((question) => choiceLabel(question.id)).join('」「')}」，用于确认父亲是否同时也是母亲。`
      ]
    };
  }

  onDestroy(() => {
    if (timer) clearTimeout(timer);
  });
</script>

{#if screen === 'intro'}
  <IntroScreen onStart={start} />
{:else if screen === 'loading'}
  <LoadingScreen />
{:else if screen === 'result' && result}
  <ResultScreen title={result.title} evidence={result.evidence} onRestart={restart} />
{:else if currentQuestion}
  <SurveyLayout
    {progress}
    canContinue={Boolean(selected)}
    nextLabel={isLastQuestion ? '提交检测' : '下一步'}
    onBack={back}
    onNext={next}
  >
    <QuestionHeader {progressLabel} title={currentQuestion.title} />
    <ChoiceGroup name={currentQuestion.id} choices={currentQuestion.choices} value={selected} onchange={choose} />
  </SurveyLayout>
{/if}
