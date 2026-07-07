<script lang="ts">
  import BottomNav from './BottomNav.svelte';
  import ProgressBar from './ProgressBar.svelte';

  let {
    progress = 25,
    canContinue = false,
    onBack = () => {},
    onNext = () => {},
    children
  } = $props<{
    progress?: number;
    canContinue?: boolean;
    onBack?: () => void;
    onNext?: () => void;
    children: import('svelte').Snippet;
  }>();
</script>

<div class="flex min-h-screen flex-col bg-(--surface)">
  <ProgressBar value={progress} />

  <main class="mx-auto flex w-full max-w-md flex-1 flex-col justify-center px-(--container-margin) pt-24 pb-32">
    {@render children()}
  </main>

  <BottomNav {canContinue} {onBack} {onNext} />
</div>
