<script lang="ts">
  let {
    canContinue = false,
    onBack = () => {},
    onNext = () => {}
  } = $props<{
    canContinue?: boolean;
    onBack?: () => void;
    onNext?: () => void;
  }>();
</script>

<nav
  class="fixed bottom-0 left-0 z-50 flex w-full items-center justify-between bg-[rgb(249_249_249/0.64)] px-(--container-margin) py-(--stack-gap-md) shadow-[0_-4px_20px_rgb(0_0_0/0.05)] backdrop-blur-sm"
  aria-label="问卷导航"
>
  <button
    class="inline-flex min-h-(--touch-target) items-center gap-(--unit) rounded-lg bg-transparent px-2 font-semibold text-(--secondary) transition-[color,opacity,transform] duration-150 hover:text-(--primary-container) active:scale-95 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-(--primary)"
    onclick={onBack}
  >
    <span class="material-symbols-outlined">chevron_left</span>
    <span class="nav-label-capsize">返回</span>
  </button>

  <button
    class="group relative inline-flex min-h-(--touch-target) items-center gap-(--unit) overflow-hidden rounded-full border border-(--outline-variant) bg-(--surface-container-lowest) px-4 py-2 font-semibold text-(--primary) shadow-sm transition-[color,opacity,transform] duration-150 hover:text-(--primary-container) active:scale-95 disabled:cursor-not-allowed disabled:opacity-50 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-(--primary)"
    disabled={!canContinue}
    onclick={onNext}
  >
    <span class="nav-label-capsize">下一步</span>
    <span class="material-symbols-outlined transition-transform duration-150 group-hover:translate-x-1">chevron_right</span>
  </button>
</nav>
