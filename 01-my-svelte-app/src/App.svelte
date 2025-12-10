<!-- <script>
  let count = 0
  function increment() {
    count++
  }
</script>

<button onclick={increment}>
  点击次数 {count}
</button> -->

<!-- 响应式声明 -->

<!-- <script>
  let count = 0
// 类似 Vue 的 computed
  $: doubled = count * 2

  // 响应式语句 watch
  $: if(count >10){
    alert('count > 10')
  }
</script>
<p>count {count}</p>
<p>doubled {doubled}</p>
<button onclick={() => count++}>点击</button> -->

<!-- Props 和事件 -->
<!-- <script>
  import Parent from './parent.svelte'
 </script>
 <Parent /> -->

<!-- 条件和循环 -->
<!-- <script>
  let show = true;
  let items = ["香蕉", "苹果", "橙子"];
</script>


{#if show}
  <p>显示内容 {show}</p>
{:else}
  <p>不显示内容 {show}</p>
{/if}

 {#each items as item}
  <p>{item}</p>
 {/each} -->

<!-- 双向绑定 -->
<!-- <script>
  let name = "";
  let checked = false;
  let selected = "1";
</script>
<div>{name}</div>
<div>{checked}</div>
<div>{selected}</div>
<input bind:value={name} />
<input type="checkbox" bind:checked />
<select bind:value={selected}>
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3">3</option>
</select> -->

<!-- 生命周期 -->
<!-- 
<script>
  import Smzq from './smzq.svelte'
  let show = true
</script>
{#if show}
<Smzq />
{/if}
<button onclick={() => show = !show}>卸载组件</button> -->

<!-- 状态管理 -->
<!-- <script>
  import { count } from "./store/index";

  // 自动订阅，使用 $ 前缀
  $: console.log($count);
</script>

<p>count {$count}</p>
<button onclick={() => $count++}>点击</button> -->

<!-- 响应式深入 -->
<!-- <script>
  import Responsive from "./responsive/index.svelte";
</script>

<Responsive /> -->

<!-- 组件通信（Props 和 Events） 详细用法 -->
<!-- <script>
  import Parent from './props/Parent.svelte'
</script>
<Parent /> -->

<!-- Svelte 5 生命周期核心变化 -->
<!-- <script>
  import Effect from "./effect/index.svelte";
</script>

<Effect /> -->

<!-- Svelte 5 动画与过渡核心变化 -->

<script>
  import AppTransition from "./transition/index.svelte";
</script>

<AppTransition />
