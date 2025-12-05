<!-- App.svelte -->
<script>
  import ThemeProvider from "./ThemeProvider.svelte";
  import ThemeButton from "./ThemeButton.svelte";
</script>

<ThemeProvider>
  <h1>我的应用</h1>
  <ThemeButton />
</ThemeProvider>
