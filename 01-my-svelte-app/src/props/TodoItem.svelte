<script>
  let { todo, onDelete, onToggle } = $props();
</script>

<ul>
  {#each todo as item (item.id)}
    <li>
      <input
        type="checkbox"
        checked={item.done}
        onchange={() => onToggle?.(item.id)}
      />
      <span>{item.text}</span>
      <button onclick={() => onDelete?.(item.id)}>删除</button>
    </li>
  {/each}
</ul>
