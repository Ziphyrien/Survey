<script lang="ts">
  import { RadioGroup } from 'bits-ui';
  import ChoiceCard from './ChoiceCard.svelte';

  type Choice = {
    value: string;
    label: string;
  };

  let {
    name,
    choices,
    value = '',
    onchange = () => {}
  } = $props<{
    name: string;
    choices: Choice[];
    value?: string;
    onchange?: (value: string) => void;
  }>();
</script>

<RadioGroup.Root
  class="flex w-full flex-col gap-(--stack-gap-md)"
  {name}
  {value}
  onValueChange={onchange}
  orientation="vertical"
  aria-label="问卷选项"
>
  {#each choices as choice}
    <ChoiceCard value={choice.value} label={choice.label} />
  {/each}
</RadioGroup.Root>
