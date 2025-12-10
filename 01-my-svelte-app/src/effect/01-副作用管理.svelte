<script>
  // 基本概念
  let count = $state(0);

  $effect(() => {
    console.log(count, "count变化");
  });

  // 执行时机

  let name = $state("Svelte");
  let age = $state(18);
  // 首次渲染后执行，依赖变化时重新执行
  $effect(() => {
    console.log("effect 执行");
    console.log("name:", name);
    console.log("age:", age);
  });
  // 只在 name 变化时执行（因为只读取了 name）
  $effect(() => {
    console.log("name 变化:", name);
  });

  // 清理函数
	let count1 = $state(0);
	let milliseconds = $state(1000);

	// $effect(() => {
	// 	// This will be recreated whenever `milliseconds` changes
	// 	const interval = setInterval(() => {
	// 		count1 += 1;
	// 	}, milliseconds);

	// 	return () => {
	// 		// if a teardown function is provided, it will run
	// 		// a) immediately before the effect re-runs
	// 		// b) when the component is destroyed
  //     console.log('清除');
      
	// 		clearInterval(interval);
	// 	};
	// });
</script>

<h1>$effect() - 统一的副作用管理</h1>
<h2>基本概念</h2>
<button onclick={() => count++}>
  Clicks: {count}
</button>
<h2>执行时机</h2>
<p>{name}</p>
<p>{age}</p>

<h2>清理函数</h2>
<h3>{count1}</h3>

<button onclick={() => (milliseconds *= 2)}>slower</button>
<button onclick={() => (milliseconds /= 2)}>faster</button>
<p>{milliseconds}</p>