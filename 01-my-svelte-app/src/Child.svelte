<script>
  export let name
  export let age = 18
  export let onMessage


  function handleClick(){
    onMessage('hello')
  }
</script>

<button onclick={handleClick}>
  {name}---{age} 岁
</button>