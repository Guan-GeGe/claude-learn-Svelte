<script>
  let { value = $bindable(0), min = 0, max = 100 } = $props();
</script>

<input type="range" bind:value {min} {max} />
<span>{value}</span>
