<script>
  let { items ,children  } = $props();
</script>

<ul>
  {#each items as item}
    <li>
      {@render children?.(item)}
    </li>
  {/each}
</ul>
