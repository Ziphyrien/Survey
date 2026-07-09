<script lang="ts">
  import { Progress } from 'bits-ui';
  import ShaderStrip from '../internal/ShaderStrip.svelte';

  let { value = 0 } = $props<{ value?: number }>();
  let clampedValue = $derived(Math.min(100, Math.max(0, value)));
  let width = $derived(`${clampedValue}%`);
</script>

<Progress.Root
  class="fixed top-0 left-0 z-50 h-2 w-full overflow-hidden bg-(--surface-variant)"
  aria-label="问卷进度"
  value={clampedValue}
>
  <div
    class="relative h-full overflow-hidden rounded-r-full bg-linear-to-r from-(--primary) to-(--primary-container) transition-[width] duration-400 ease-in-out"
    style={`width: ${width}`}
  >
    <ShaderStrip />
  </div>
</Progress.Root>
