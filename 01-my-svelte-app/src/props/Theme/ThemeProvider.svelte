<script>
  let { children } = $props();
  import { setContext } from "svelte";

  let theme = $state("light");

  setContext("theme", {
    get current() {
      return theme;
    },
    toggle() {
      theme = theme === "light" ? "dark" : "light";
    },
  });
</script>

<div class={theme}>
  {@render children()}
</div>
