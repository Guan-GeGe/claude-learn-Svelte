<script>
  // 统一的副作用管理
  import Fuzoyong from "./01-副作用管理.svelte";
  // $effect.pre() - DOM 更新前执行
  import EffectPre from "./02-DOM更新前执行.svelte";

  // $effect.root() - 手动控制 Effect 生命周期

  import EffectRoot from "./03-手动控制 Effect.svelte";

  // untrack() - 不追踪依赖
  import Untrack from "./04-untrack-不追踪依赖.svelte";
</script>

<!-- 统一的副作用管理 -->
<!-- <Fuzoyong /> -->

<!-- // $effect.pre() - DOM 更新前执行 -->
<!-- <EffectPre /> -->

<!-- $effect.root() - 手动控制 Effect 生命周期 -->
<!-- <EffectRoot /> -->


<!-- untrack() - 不追踪依赖 -->
<Untrack />