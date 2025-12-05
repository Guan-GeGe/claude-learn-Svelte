<!-- Parent.svelte -->
<script>
  import Form from "./Form.svelte";
  import FormField from "./FormField.svelte";
  let formData = {};
  function formHandleSubmit(data) {
    console.log(data);
    formData = data;
  }
</script>

<Form onSubmit={formHandleSubmit}>
  {#snippet children()}
    <FormField name="name" label="姓名" type="text" />
    <FormField name="age" label="年龄" type="number" />
    <button>提交</button>
  {/snippet}
</Form>

<p>表单数据: {JSON.stringify(formData)}</p>
