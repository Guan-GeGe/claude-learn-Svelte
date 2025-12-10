<script>
  let items = $state([1, 2, 3]);
  let listElement;

  // DOM 更新前执行
  $effect.pre(() => {
    if (listElement) {
      console.log("更新前的高度:", listElement.scrollHeight);
    }
  });

  // DOM 更新后执行
  $effect(() => {
    if (listElement) {
      console.log("更新后的高度:", listElement.scrollHeight);
    }
  });

  // 实战：保持滚动位置
  let messages = $state([]);
  let container;
  let shouldScrollToBottom = $state(true);
  let previousScrollHeight = 0;

  // DOM 更新前记录状态
  $effect.pre(() => {
    console.log(container);

    if (container) {
      previousScrollHeight = container.scrollHeight;
      const isAtBottom =
        container.scrollTop + container.clientHeight >=
        container.scrollHeight - 10;
      console.log(isAtBottom);

      shouldScrollToBottom = isAtBottom;
    }
  });

  // DOM 更新后调整滚动
  $effect(() => {
    if (container && shouldScrollToBottom && messages.length) {
      container.scrollTop = container.scrollHeight;
    }
  });

  function addMessage(text) {
    messages = [...messages, { id: Date.now(), text }];
  }
</script>

<ul bind:this={listElement}>
  {#each items as item}
    <li>{item}</li>
  {/each}
</ul>
<h1>实战：保持滚动位置</h1>
<div bind:this={container} class="chat-container">
  {#each messages as msg (msg.id)}
    <div class="message">{msg.text}</div>
  {/each}
</div>

<button onclick={() => addMessage("新消息")}>发送</button>

<style>
  .chat-container {
    height: 300px;
    overflow-y: auto;
  }
</style>
