<script>
  let count = $state(0);
  let cleanup;

  function startTracking() {
    cleanup = $effect.root(() => {
      $effect(() => {
        console.log("count", count);
      });
    });
  }

  function stopTracking() {
    cleanup();
  }
</script>

<button onclick={startTracking}>开始追踪</button>
<button onclick={stopTracking}>停止追踪</button>
<button onclick={() => count++}>Count: {count}</button>
