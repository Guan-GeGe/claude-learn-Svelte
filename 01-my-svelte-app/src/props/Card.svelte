<script>
  let { title } = $props();
</script>

<div class="card">
  <h2>{title}</h2>
  <div class="content">
    <slot />
  </div>
</div>

<style>
  .card {
    border: 1px solid #ccc;
    padding: 20px;
  }
</style>
