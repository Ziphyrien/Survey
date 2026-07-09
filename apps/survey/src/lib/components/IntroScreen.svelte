<script lang="ts">
  let { onStart } = $props<{ onStart: () => void }>();
</script>

<section class="relative flex min-h-screen flex-col bg-(--surface) px-(--container-margin) py-10 text-(--on-background)">
  <a
    href="https://github.com/Ziphyrien/Survey"
    target="_blank"
    rel="noreferrer"
    aria-label="在 GitHub 查看源码"
    class="absolute top-6 right-6 rounded-full p-2 text-(--secondary) transition-colors hover:text-(--primary) focus-ring"
  >
    <svg class="size-5" viewBox="0 0 24 24" aria-hidden="true" fill="currentColor">
      <path d="M12 2C6.48 2 2 6.58 2 12.25c0 4.53 2.87 8.37 6.84 9.73.5.1.68-.22.68-.49v-1.9c-2.78.62-3.37-1.22-3.37-1.22-.45-1.18-1.1-1.49-1.1-1.49-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.3.1-2.71 0 0 .84-.28 2.75 1.05A9.28 9.28 0 0 1 12 7c.85 0 1.71.12 2.51.34 1.91-1.33 2.75-1.05 2.75-1.05.55 1.41.2 2.45.1 2.71.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.79-4.57 5.05.36.32.68.94.68 1.9v2.79c0 .27.18.59.69.49A10.16 10.16 0 0 0 22 12.25C22 6.58 17.52 2 12 2Z" />
    </svg>
  </a>
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
