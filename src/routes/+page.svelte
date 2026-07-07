<script lang="ts">
  import ChoiceGroup from '$lib/components/ChoiceGroup.svelte';
  import SurveyCanvas from '$lib/components/SurveyCanvas.svelte';

  const choices = [
    { value: 'A', label: '选项 A' },
    { value: 'B', label: '选项 B' },
    { value: 'C', label: '选项 C' },
    { value: 'D', label: '选项 D' }
  ];

  let selected = $state('');

  function choose(value: string) {
    selected = value;

    if (navigator.vibrate) {
      navigator.vibrate(50);
    }
  }
</script>

<SurveyCanvas progress={25} canContinue={Boolean(selected)}>
  <ChoiceGroup name="survey_option" choices={choices} value={selected} onchange={choose} />
</SurveyCanvas>
