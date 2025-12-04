<script>
  import Child from './Child.svelte'
  function handleMessage(){
    alert('hello')
  }
</script>

<Child name="张三" age={20} onMessage={handleMessage} />