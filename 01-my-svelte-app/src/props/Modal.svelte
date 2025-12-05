<script>
  let { children } = $props();

  let visilbe = $state(false);

  export function open() {
    visilbe = true;
  }

  export function close() {
    visilbe = false;
  }
</script>

{#if visilbe}
  <div class="modal">
    <div class="modal-content">
      {@render children?.()}
      <button onclick={close}>关闭</button>
    </div>
  </div>
{/if}
