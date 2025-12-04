<script>
  import { onMount, onDestroy } from "svelte";

  onMount(() => {
    console.log("组件挂载");

    return () => {
      console.log("在 onMount 中卸载组件");
    };
  });

  onDestroy(() => {
    console.log("组件卸载");
  });
</script>

<div>内容</div>
