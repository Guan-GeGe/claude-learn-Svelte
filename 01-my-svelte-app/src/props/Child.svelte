<script>
  // 1. 基本用法
  let { name, age, title,content,...rest } = $props();
  // 基本解构
  // let { title, content } = $props();
  // 默认值
  // let { count = 0, enabled = true } = $props();
  // 重命名
  // let { name: userName, id: userId } = $props();
  // 剩余属性
  // let { title, ...rest } = $props();
</script>

<p>{name}</p>
<p>{age}</p>
<h1>{title}</h1>
<div>{content}</div>
<div>{JSON.stringify(rest)}</div>
