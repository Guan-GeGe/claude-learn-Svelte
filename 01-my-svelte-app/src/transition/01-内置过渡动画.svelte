<script>
  import { fade, fly, slide, scale, blur } from "svelte/transition";

  let visible = $state(false);
</script>

<button onclick={() => (visible = !visible)}>切换</button>

{#if visible}
  <div transition:fade>淡入淡出</div>
{/if}

{#if visible}
  <div transition:fly={{ y: 200, duration: 300 }}>飞入飞出</div>
{/if}

{#if visible}
  <div transition:slide>滑动</div>
{/if}

{#if visible}
  <div transition:scale={{ start: 0.5 }}>缩放</div>
{/if}

{#if visible}
  <div transition:blur>模糊</div>
{/if}
