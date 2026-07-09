<script lang="ts">
  import { Button } from 'bits-ui';
  import MaterialIcon from '../internal/MaterialIcon.svelte';

  let {
    canContinue = false,
    backLabel = '返回',
    nextLabel = '下一步',
    onBack = () => {},
    onNext = () => {}
  } = $props<{
    canContinue?: boolean;
    backLabel?: string;
    nextLabel?: string;
    onBack?: () => void;
    onNext?: () => void;
  }>();
</script>

<nav
  class="fixed bottom-0 left-0 z-50 flex w-full items-center justify-between bg-[rgb(249_249_249/0.64)] px-(--container-margin) py-(--stack-gap-md) shadow-[0_-4px_20px_rgb(0_0_0/0.05)] backdrop-blur-sm"
  aria-label="问卷导航"
>
  <Button.Root
    type="button"
    class="inline-flex min-h-(--touch-target) items-center gap-(--unit) rounded-lg bg-transparent px-2 font-semibold text-(--secondary) transition-[color,opacity,transform] duration-150 hover:text-(--primary-container) active:scale-95 focus-ring"
    onclick={onBack}
  >
    <MaterialIcon name="chevron_left" />
    <span class="nav-label-capsize">{backLabel}</span>
  </Button.Root>

  <Button.Root
    type="button"
    class="group relative inline-flex min-h-(--touch-target) items-center gap-(--unit) overflow-hidden rounded-full border border-(--outline-variant) bg-(--surface-container-lowest) px-4 py-2 font-semibold text-(--primary) shadow-sm transition-[color,opacity,transform] duration-150 hover:text-(--primary-container) active:scale-95 disabled:cursor-not-allowed disabled:opacity-50 focus-ring"
    disabled={!canContinue}
    onclick={onNext}
  >
    <span class="nav-label-capsize">{nextLabel}</span>
    <MaterialIcon name="chevron_right" class="transition-transform duration-150 group-hover:translate-x-1" />
  </Button.Root>
</nav>
