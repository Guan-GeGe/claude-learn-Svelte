<script>
  import { getContext } from "svelte";
  let { name, label, type = "text" } = $props();
  let value = $state("");
  const form = getContext("form");
  const handleInput = (e) => {
    value = e.target.value;
    form?.update(name, value);
  };
  $effect(() => {
    form.register(name, value);
  });
  let error = $derived(form.getError(name));
</script>

<div>
  <label for={name}>{label}</label>
  <input {type} {name} bind:value oninput={handleInput} />
  {#if error}
    <span class="error">{error}</span>
  {/if}
</div>
