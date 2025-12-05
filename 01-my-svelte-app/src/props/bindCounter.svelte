<script>
  let { bindCount=$bindable(0) } = $props();
</script>

<button onclick={() => bindCount++}>
  {bindCount}
</button>