<script>
  import { untrack } from "svelte";

  let count = $state(0);
  let dbCount = $state(0);

  $effect(() => {
    console.log(count, "count");
    // 读取 doubled 但不追踪
    const currentDoubled = untrack(() => dbCount);
    console.log("当前 doubled:", currentDoubled);
  });

  function updateBoth() {
    count++;
    dbCount = count * 2;
  }
</script>

<button onclick={updateBoth}>更新</button>
