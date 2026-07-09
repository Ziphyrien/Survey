<script lang="ts">
  import '../app.css';

  let { children } = $props();
</script>

<svelte:head>
  <title>父母性别检测器</title>
</svelte:head>

{@render children()}
