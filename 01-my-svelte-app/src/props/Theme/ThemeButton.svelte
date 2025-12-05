<script>
  import { getContext } from "svelte";
  let theme = getContext("theme");
</script>

<button onclick={() => theme.toggle()}>
  当前主题: {theme.current}
</button>
