<script lang="ts">
  let { onStart } = $props<{ onStart: () => void }>();
</script>

<section class="flex min-h-screen flex-col bg-(--surface) px-(--container-margin) py-10 text-(--on-background)">
  <div class="mx-auto flex w-full max-w-md flex-1 flex-col justify-center">
    <p class="mb-(--unit) text-[13px] leading-4.5 font-medium tracking-[0.02em] text-(--secondary)">今日可测</p>
    <h1 class="mb-10 text-3xl leading-10 font-semibold tracking-[-0.02em]">父母性别检测器</h1>
    <button
      type="button"
      class="inline-flex min-h-(--touch-target) items-center justify-center rounded-full border border-(--outline-variant) bg-(--surface-container-lowest) px-5 py-3 font-semibold text-(--primary) shadow-sm transition-[color,transform] duration-150 hover:text-(--primary-container) active:scale-95 focus-ring"
      onclick={onStart}
    >
      开始检测
    </button>
  </div>
</section>
