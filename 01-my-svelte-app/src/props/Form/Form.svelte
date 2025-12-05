<!-- Form.svelte -->
<script>
  import { setContext } from "svelte";
  let { onSubmit, children } = $props();

  let formData = $state({});
  let errors = $state({});

  setContext("form", {
    register(name, value) {
      formData[name] = value;
    },
    update(name, value) {
      formData[name] = value;
    },
    setError(name, error) {
      errors[name] = error;
    },
    getError(name) {
      return errors[name];
    },
    getData() {
      return formData;
    },
  });

  const handleSubmit = (event) => {
    event.preventDefault();
    onSubmit?.(formData);
  };
</script>

<form onsubmit={handleSubmit}>
  {@render children?.()}
</form>
