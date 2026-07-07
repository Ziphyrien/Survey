<script lang="ts">
  import ShaderStrip from './ShaderStrip.svelte';

  let { value = 25 } = $props<{ value?: number }>();
  let width = $derived(`${Math.min(100, Math.max(0, value))}%`);
</script>

<div
  class="fixed top-0 left-0 z-50 h-2 w-full overflow-hidden bg-(--surface-variant)"
  aria-label="问卷进度"
  aria-valuemin="0"
  aria-valuemax="100"
  aria-valuenow={value}
  role="progressbar"
>
  <div
    class="relative h-full overflow-hidden rounded-r-full bg-linear-to-r from-(--primary) to-(--primary-container) transition-[width] duration-400 ease-in-out"
    style={`width: ${width}`}
  >
    <ShaderStrip />
  </div>
</div>
