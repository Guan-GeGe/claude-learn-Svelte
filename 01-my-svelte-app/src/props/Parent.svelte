<script>
  import Child from "./Child.svelte";
  import Counter from "./Counter.svelte";
  import TodoItem from "./TodoItem.svelte";
  import Input from "./Input.svelte";
  // 1. 基本用法
  let name = "张三";
  let age = 2011;
  let rest = {
    id: 1,
    class: "test",
  };

  // 2.响应式 props
  let count = $state(0);
  function updateCount() {
    count++;
  }

  // 3. 传递参数
  let todo = $state([
    {
      id: 1,
      text: "学习 Svelte",
      done: false,
    },
    {
      id: 2,
      text: "学习 React",
      done: true,
    },
    {
      id: 3,
      text: "学习 Vue",
      done: false,
    },
  ]);
  function updateTodo(id) {
    todo.find((item) => item.id === id).done = !todo.find(
      (item) => item.id === id
    ).done;
  }
  function deleteTodo(id) {
    console.log(id);

    todo = todo.filter((item) => item.id !== id);
  }

  //  事件修饰符 (原生事件)
  let { onSubmit } = $props();
  function handleSubmit(event) {
    event.preventDefault();
    console.log("提交");
    onSubmit?.();
  }

  // 4. 双向绑定（bind:）
  let text = $state("");

  // $bindable() - 可绑定的 Props
  import BindCounter from "./bindCounter.svelte";
  let bindCount = $state(0);

  // 自定义绑定逻辑
  import Slider from "./Slider.svelte";
  let sliderValue = $state(50);

  // 5.插槽（Slots）

  import Card from "./Card.svelte";

  // 命名插槽
  import Layout from "./Layout.svelte";

  // 插槽 Props（作用域插槽）
  import List from "./List.svelte";
  let arrList = $state([
    { id: 1, name: "张三" },
    { id: 2, name: "李四" },
    { id: 3, name: "王五" },
  ]);

  //  6. 组件引用（bind:this）
  import Modal from "./Modal.svelte";
  let modal;

  // 7.Context API（跨层级通信）
  import ThemeContext from "./Theme/App.svelte";

  // 实战：表单 Context
  import FormParent from "./Form/Parent.svelte";
</script>

<!-- 1. 基本用法 -->
<Child {name} {age} title="标题" content="内容" {...rest} />

<!-- 2.响应式 props -->
<Counter {count} onIncrement={updateCount} />
<button onclick={updateCount}>点击</button>

<!-- 3.传递参数 -->
<TodoItem {todo} onToggle={updateTodo} onDelete={deleteTodo} />

<!-- 事件修饰符 -->
<form onsubmit={handleSubmit}>
  <button>提交</button>
</form>

<!-- 4. 双向绑定（bind:） -->
<Input bind:value={text}></Input>
<p>你输入了: {text}</p>
<h2>$bindable() - 可绑定的 Props</h2>
<BindCounter bind:bindCount />
<p>父组件中的值: {bindCount}</p>
<h2>自定义绑定逻辑</h2>
<Slider bind:value={sliderValue} min={0} max={200} />
<p>音量: {sliderValue}%</p>

<h2>插槽</h2>
<Card title="标题">
  <p>姓名: 张三</p>
  <p>年龄: 25</p>
</Card>

<h2>命名插槽</h2>
<Layout>
  <svelte:fragment slot="header">
    <h1>网站标题</h1>
  </svelte:fragment>

  <p>主要内容</p>

  <svelte:fragment slot="footer">
    <p>© 2024</p>
  </svelte:fragment>
</Layout>
{#snippet footer({ message })}
  <p>© 2024 {message}</p>
{/snippet}
<Layout>
  <p>主要内容</p>
  {@render footer({ message: "传参" })}
</Layout>

<h2>插槽 Props（作用域插槽）</h2>
<List items={arrList}>
  {#snippet children(item)}
    <p>{item.name}</p>
  {/snippet}
</List>

<h2>6. 组件引用（bind:this）</h2>
<Modal bind:this={modal}>
  <p>模态框内容</p>
</Modal>
<button onclick={() => modal.open()}>打开模态框</button>

<h2>Context API（跨层级通信）</h2>
<ThemeContext />

<h1>实战：表单 Context</h1>
<FormParent />