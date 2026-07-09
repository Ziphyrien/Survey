<script lang="ts">
  let {
    name,
    fill = false,
    class: className = ''
  } = $props<{
    name: string;
    fill?: boolean;
    class?: string;
  }>();
</script>

<span class={`material-symbols-outlined${fill ? ' fill' : ''}${className ? ` ${className}` : ''}`}>{name}</span>
