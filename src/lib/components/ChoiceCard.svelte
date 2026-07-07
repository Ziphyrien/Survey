<script lang="ts">
  import { RadioGroup } from 'bits-ui';

  let { value, label } = $props<{
    value: string;
    label: string;
  }>();
</script>

<RadioGroup.Item
  class="group flex min-h-20 w-full cursor-pointer items-center justify-between rounded-xl border border-(--outline-variant) bg-(--surface-container-lowest) p-6 text-left text-(--on-surface) shadow-sm transition-[border-color,transform] duration-150 hover:border-(--outline) data-[state=checked]:border-(--primary) focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-(--primary)"
  {value}
>
  <span class="text-lg leading-7 font-normal">{label}</span>
  <span
    class="material-symbols-outlined fill scale-50 text-(--primary) opacity-0 transition-[opacity,transform] duration-200 group-data-[state=checked]:scale-100 group-data-[state=checked]:opacity-100"
  >check_circle</span>
</RadioGroup.Item>
