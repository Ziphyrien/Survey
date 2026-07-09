<script lang="ts">
  let { title, evidence, onRestart } = $props<{
    title: string;
    evidence: string[];
    onRestart: () => void;
  }>();
</script>

<section class="flex min-h-screen flex-col bg-(--surface) px-(--container-margin) py-10 text-(--on-background)">
  <div class="mx-auto flex w-full max-w-md flex-1 flex-col justify-center">
    <p class="mb-(--unit) text-[13px] leading-4.5 font-medium tracking-[0.02em] text-(--secondary)">检测结果</p>
    <h1 class="mb-6 text-3xl leading-10 font-semibold tracking-[-0.02em]">{title}</h1>

    <div class="mb-10 rounded-xl border border-(--outline-variant) bg-(--surface-container-lowest) p-6 shadow-sm">
      <h2 class="mb-4 text-lg leading-7 font-semibold">证据链</h2>
      <ul class="flex flex-col gap-3 text-base leading-6 text-(--on-surface)">
        {#each evidence as item}
          <li>· {item}</li>
        {/each}
      </ul>
    </div>

    <button
      type="button"
      class="inline-flex min-h-(--touch-target) items-center justify-center rounded-full border border-(--outline-variant) bg-(--surface-container-lowest) px-5 py-3 font-semibold text-(--primary) shadow-sm transition-[color,transform] duration-150 hover:text-(--primary-container) active:scale-95 focus-ring"
      onclick={onRestart}
    >
      再测一次
    </button>
  </div>
</section>
