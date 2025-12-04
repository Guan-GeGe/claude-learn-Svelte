<script>
  import { onMount } from "svelte";
  // 对象
  let user = $state({
    name: "张三",
    age: 18,
  });

  // 数组
  let arrItems = $state([1, 2, 3]);

  function updateUser() {
    user.age++;
  }
  function addItem() {
    arrItems.push(Math.random());
  }

  //  $derived
  // 使用场景：基于现有状态计算新值

  let count = $state(0);
  let doubleCount = $derived(count * 2);
  let arrNames = [
    {
      name: "张三",
      age: 18,
      active: true,
    },
    {
      name: "李四",
      age: 138,
      active: true,
    },
    {
      name: "王五",
      age: 14,
      active: false,
    },
  ];
  let searchName = $state("");
  let filterName = $derived(
    arrNames.filter((item) => item.name.includes(searchName) && item.active)
  );
  let activeNum = $derived(arrNames.filter((item) => item.active).length);
  let avgAge = $derived(
    arrNames.reduce((pre, cur) => pre + cur.age, 0) / arrNames.length
  );

  // $derived.by - 复杂派生逻辑
  // 使用场景：需要多行代码或临时变量的计算
  let orders = $state([
    { id: 1, items: [10, 20, 30], status: "paid" },
    { id: 2, items: [15, 25], status: "pending" },
    { id: 3, items: [50], status: "paid" },
  ]);
  let summary = $derived.by(() => {
    const paid = orders.filter((order) => order.status === "paid");
    const totalRevenue = orders.reduce(
      (pre, cur) => pre + cur.items.reduce((pre, cur) => pre + cur, 0),
      0
    );
    const avgOrderValue = totalRevenue / paid.length;
    return {
      paidOrders: paid.length,
      totalRevenue,
      avgOrderValue,
    };
  });

  // $effect - 副作用
  let count1 = $state(0);
  $effect(() => {
    // 只有在里面的值才会被监听到，当把 count1 去掉，则方法不会执行了
    console.log("count1", count1);
  });
  let formData = $state({
    name: "",
    email: "",
    message: "",
  });

  let lastSaved = $state(null);

  // 自动保存（防抖）
  $effect(() => {
    localStorage.setItem("draft", JSON.stringify(formData));
    lastSaved = new Date();
  });

  // 加载草稿
  $effect(() => {
    const draft = localStorage.getItem("draft");
    if (draft) {
      formData = JSON.parse(draft);
    }
  });

  // $state.raw - 非响应式状态
  // 使用场景：大数据或不需要响应式的数据
  // 使用 raw：普通对象，无响应式开销
  let bigList = $state.raw(
    new Array(10000).fill(0).map((_, i) => ({
      id: i,
      data: Math.random(),
    }))
  );

  // 手动触发更新
  let version = $state(0);

  function updateItem(index) {
    bigList[index].data = Math.random();
    version++;
  }

  // $state.snapshot - 获取快照
  let usersnap = $state({
    name: "张三",
    profile: {
      age: 25,
      city: "北京",
    },
  });

  // ✅ 保存到 localStorage
  function save() {
    console.log(usersnap);

    const snapshot = $state.snapshot(usersnap);
    console.log(snapshot);
    // 会变成普通的，没有代理了，但是不影响最开始数据
    localStorage.setItem("user", JSON.stringify(snapshot));
  }

  // ✅ 发送到服务器
  async function sync() {
    const snapshot = $state.snapshot(usersnap);
    await fetch("/api/user", {
      method: "POST",
      body: JSON.stringify(snapshot),
    });
  }

  // ✅ 深度比较
  let originalUser = $state.snapshot(usersnap);

  let hasChanges = $derived(() => {
    const current = $state.snapshot(usersnap);
    return JSON.stringify(current) !== JSON.stringify(originalUser);
  });

  // 练习
  let cart = $state([
    { id: 1, name: "商品1", price: 100, quantity: 1 },
    { id: 2, name: "商品2", price: 200, quantity: 2 },
    { id: 3, name: "商品3", price: 300, quantity: 3 },
  ]);
  // 总价
  let totalPrice = $derived(
    cart.reduce((pre, cur) => pre + cur.price * cur.quantity, 0)
  );

  // 同步到 localStorage
  $effect(() => {
    localStorage.setItem("cart", JSON.stringify(cart));
  });

  function updateQty(id, qty) {
    cart.find((item) => item.id === id).quantity = qty;
  }
</script>

<div>
  <button onclick={updateUser}>增加年龄</button>
  <button onclick={addItem}>增加数组</button>
  <div>{user.name}---{user.age}</div>
  {#each arrItems as item (item)}
    <p>{item}</p>
  {/each}
  <h1>$derived</h1>
  <p>{doubleCount}</p>
  <input bind:value={searchName} placeholder="搜索用户" />
  {#each filterName as item}
    <p>{item.name} - {item.age} - {item.active}</p>
  {/each}
  <p>activeNum {activeNum}</p>
  <p>avgAge {avgAge.toFixed(2)}</p>

  <h1>$derived.by</h1>
  <p>已付款订单: {summary.paidOrders}</p>
  <p>总收入: ¥{summary.totalRevenue}</p>
  <p>平均订单: ¥{summary.avgOrderValue.toFixed(2)}</p>

  <h1>$effect</h1>
  <input bind:value={count1} />
  <button onclick={() => count1++}>增加count1</button>
  <h2>自动保存form</h2>
  <input bind:value={formData.name} placeholder="姓名" />
  <input bind:value={formData.email} placeholder="邮箱" />
  <textarea bind:value={formData.message}></textarea>

  {#if lastSaved}
    <p>最后保存: {lastSaved.toLocaleTimeString()}</p>
  {/if}

  <h1>$state.raw</h1>
  <button onclick={() => updateItem(Math.floor(Math.random() * 10000))}
    >更新</button
  >
  <!-- {#each bigList as item}
    <p>{item.id} - {item.data}</p>
  {/each} -->
  <p>{version}</p>
  <h1>$state.snapshot</h1>
  <input bind:value={usersnap.name} />
  <input bind:value={usersnap.profile.age} type="number" />

  {#if hasChanges}
    <button onclick={save}>保存更改</button>
  {/if}

  <h1>购物车</h1>
  {#each cart as item}
    <p>{item.name} - {item.price} - {item.quantity}</p>
    <input
      type="number"
      bind:value={item.quantity}
      oninput={() => updateQty(item.id, item.quantity)}
    />
  {/each}
  <p>总价: {totalPrice}</p>
</div>
