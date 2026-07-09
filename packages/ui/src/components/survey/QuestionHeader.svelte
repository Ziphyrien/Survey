<script lang="ts">
  let { progressLabel, title } = $props<{
    progressLabel: string;
    title: string;
  }>();
</script>

<div class="mb-8">
  <p class="mb-(--unit) text-[13px] leading-4.5 font-medium tracking-[0.02em] text-(--secondary)">
    {progressLabel}
  </p>
  <h1 class="text-2xl leading-8 font-semibold tracking-[-0.01em] text-(--on-background)">{title}</h1>
</div>
