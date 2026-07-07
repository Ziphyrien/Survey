<script lang="ts">
  import '../app.css';

  let { children } = $props();
</script>

<svelte:head>
  <title>问卷</title>
</svelte:head>

{@render children()}
