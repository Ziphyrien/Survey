<script lang="ts">
  import { ChoiceGroup, QuestionHeader, SurveyLayout } from '@survey/ui';

  const currentStep = 3;
  const totalSteps = 10;
  const progress = (currentStep / totalSteps) * 100;
  const progressLabel = `第 ${currentStep} 题，共 ${totalSteps} 题`;
  const question = {
    title: '您的设计偏好是什么？',
    choices: [
      { value: 'A', label: '选项 A' },
      { value: 'B', label: '选项 B' },
      { value: 'C', label: '选项 C' },
      { value: 'D', label: '选项 D' }
    ]
  };

  let selected = $state('');

  function choose(value: string) {
    selected = value;

    navigator.vibrate?.(50);
  }
</script>

<SurveyLayout {progress} canContinue={Boolean(selected)}>
  <QuestionHeader {progressLabel} title={question.title} />
  <ChoiceGroup name="survey_option" choices={question.choices} value={selected} onchange={choose} />
</SurveyLayout>
