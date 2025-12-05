<script>
  let { count, onIncrement } = $props();
  // Props 自动响应，无需额外处理
  let doubled = $derived(count * 2);
  // ❌ 错误：不能直接修改 props
  // function increment() {
  //   count++;
  // }
  function increment() {
   onIncrement?.();
  }
</script>

<p>{count}</p>
<p>{doubled}</p>
<button onclick={increment}>点击</button>
