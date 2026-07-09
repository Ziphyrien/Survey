<script lang="ts">
  import { RadioGroup } from 'bits-ui';
  import MaterialIcon from '../internal/MaterialIcon.svelte';

  let { value, label } = $props<{
    value: string;
    label: string;
  }>();
</script>

<RadioGroup.Item
  class="group flex min-h-20 w-full cursor-pointer items-center justify-between rounded-xl border border-(--outline-variant) bg-(--surface-container-lowest) p-6 text-left text-(--on-surface) shadow-sm transition-[border-color,transform] duration-100 hover:border-(--outline) data-[state=checked]:border-(--primary) focus-ring"
  {value}
>
  <span class="text-lg leading-7 font-normal">{label}</span>
  <MaterialIcon
    name="check_circle"
    fill
    class="scale-50 text-(--primary) opacity-0 transition-all duration-200 group-data-[state=checked]:scale-100 group-data-[state=checked]:opacity-100"
  />
</RadioGroup.Item>
