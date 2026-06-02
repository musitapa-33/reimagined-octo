# 1.1 Vue3 简介

- **渐进式 JavaScript 框架**：按需使用，不用一次性学完所有 API
- **作者**：尤雨溪（华人开发者）
- **核心特点**：
  - 更快（性能优化、diff 算法升级）
  - 更小（打包体积更小）
  - 更好的 TS 支持
  - **组合式 API（Composition API）** 是 Vue3 最大升级
- 支持**组件化开发**：把页面拆成独立、可复用的组件

***

# 1.2. 使用 Vite 创建 Vue3 项目（推荐）

Vite 是 Vue 官方推荐的极速构建工具

```bash
npm create vue@latest
```

创建步骤：

1. 输入项目名
2. 选择 **TypeScript和vue**（可选）
3. 其他默认即可 no

进入项目：

```bash
cd 项目名
npm install
npm run dev
```

***

# 1.3. Vue3 项目核心结构

项目最重要的两个文件：

- `main.ts`：入口文件
- `App.vue`：根组件

### main.ts（入口）

```ts
// 从 vue 中导入创建应用的方法
import { createApp } from 'vue'
// 导入根组件
import App from './App.vue'

// 创建应用并挂载到 #app 元素上
createApp(App).mount('#app')
```

### App.vue（根组件）

Vue 单文件组件（SFC）三部分：

1. `<template>`：HTML 结构
2. `<script>`：JS/TS 逻辑
3. `<style>`：CSS 样式

```vue
<template>
  <!-- 模板：写 HTML -->
  <div class="app">
    <h1>Hello Vue3</h1>
  </div>
</template>

<script lang="ts">
// JS/TS 代码
export default {
  name: 'App',
}
</script>

<style>
/* 样式 */
.app {
  background-color: #0fa;
  padding: 20px;
  border-radius: 10px;
}
</style>
```

***

# 1.4. Vue2 写法（选项式 API）

创建组件：`src/components/Person.vue`

插值表达式 + 点击事件

```vue
<template>
  <div class="person">
    <!-- 插值：{{ 变量名 }} 渲染数据 -->
    <h2>姓名：{{ name }}</h2>
    <h2>年龄：{{ age }}</h2>

    <!-- @click 绑定点击事件 -->
    <button @click="showTel">查看电话</button>
    <button @click="changeName">改名</button>
    <button @click="changeAge">加一岁</button>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Person',
  // data 存放数据
  data() {
    return {
      name: '张三',
      age: 18,
      tel: '13458888888',
    }
  },
  // methods 存放方法
  methods: {
    showTel() {
      alert(this.tel)
    },
    changeName() {
      this.name = '喜羊羊'
    },
    changeAge() {
      this.age++
    },
  },
}
</script>
```

### 在 App.vue 中使用组件

```vue
<template>
  <div class="app">
    <h1>hello vue3</h1>
    <Person />
  </div>
</template>

<script lang="ts">
import Person from './components/Person.vue'

export default {
  name: 'App',
  components: { Person }, // 注册组件
}
</script>
```

***

> 2026.4.27

## 2.1 optionsAPI 和 compositionAPI

1. Options API（Vue2 写法，选项式）
   代码分散：数据放 data，方法放 methods，计算属性放 computed…
   适合简单页面，复杂逻辑会跳来跳去，难维护
2. Composition API（Vue3 写法，组合式）
   代码聚合：一个功能的变量、函数写在一起
   逻辑复用强、代码清晰、适合复杂项目
   入口就是：setup

***

# 2.2 setup

**setup是compositionAPI的入口函数**

## 01 setup概述

```vue
<script lang="ts">
export default {
  name: 'PersonCard',
  beforeCreate() {
    console.log('beforeCreate')
    console.log('setup')
  },
  setup() {
    let name = '喜羊羊'
    let age = 18
    const tel = '13588888888'
    //不需要改的值 → 用 const
    //需要改的值 → 用 let
    //函数 → const

    function changeName() {
      name = 'musitapa'
      console.log(name)
    }
    function changeAge() {
      age += 1
      console.log(age)
    }
    function showtel() {
      alert(tel)
      console.log(tel)
    }

    return { name, age, showtel, changeName, changeAge }
  },
}
</script>
```

## 02 setup返回值

```vue
<script>
return () => '嗯嗯' // 直接返回渲染函数 → 整个模板都会被覆盖
</script>
```

## 03 setup和compositionAPI

```vue
<template>
 <h2>测试1:{{ a }}</h2>
    <h2>测试2:{{ c }}</h2>
    <h2>测试3:{{ d }}</h2>
    <button @click="b">测试</button>
</template>

<script lang="ts">
data() {
    return {
      a: 100,
      c: this.name,
      d: 900
    }
  },
  methods: {
    b() {
      console.log('b')
    }
  }
  //let x = d
<script>
```

## 04 setup语法糖

```vue
<script lang="ts" setup name="person234">
let name = '喜羊羊'
let age = 21
const tel = '13588888888'
const address = '新疆建设职业技术学院'

function changeName() {
  name = 'musitapa'
  console.log(name)
}
function changeAge() {
  age += 1
  console.log(age)
}
function showtel() {
  alert(tel)
  console.log(tel)
}
</script>
```

```bash
npm i vite-plugin-vue-setup-extend -D
```

在vite.config.ts 写 import vuesetup from 'vite-plugin-vue-setup-extend'

***

# 2.3 ref 和 reactive

**ref：基本类型，对象类型的响应式数据**

### 1.ref的基本类型

```vue
<script lang="ts" setup>
import { ref } from 'vue'

let name = ref('喜羊羊')
let age = ref(21)

function changeName() {
  name.value = 'musitapa'
  console.log(name.value)
}
function changeAge() {
  age.value += 1
  console.log(age.value)
}
</script>
```

### 2.ref的对象类型

```vue
<script lang="ts" setup>
import { ref } from 'vue'
const games = ref([
  { id: 1, name: '王者荣耀' },
  { id: 2, name: '和平精英' },
  { id: 3, name: '英雄联盟' },
  { id: 4, name: '绝地求生' },
])
const obj = ref({ x: 999 })
const car = ref({ brand: '奔驰', price: 100 })
console.log(car)
console.log(obj)
function changeprice() {
  car.value.price += 10
  console.log(car.value.price)
}
function addGame() {
  games.value[2].name = '洛克王国：世界'
}
</script>
```

### 3.reactive：对象类型的响应式数据

```vue
<template>
  <div class="person">
    <h2>一辆{{ car.brand }}车,价值{{ car.price }}万</h2>
    <button @click="changeprice">修改汽车的价格</button>
    <br />
    <h2>游戏列表:</h2>
    <ul>
      <li v-for="game in games" :key="game.id">
        {{ game.name }}
      </li>
    </ul>
    <button @click="addGame">添加游戏</button>
    <hr />
    <h2>测试:{{ obj.a.b.c }}</h2>
    <button @click="changeobj">测试</button>
  </div>
</template>
<script lang="ts" setup>
//定义数据
import { reactive } from 'vue'
const games = reactive([
  { id: 1, name: '王者荣耀' },
  { id: 2, name: '和平精英' },
  { id: 3, name: '英雄联盟' },
  { id: 4, name: '绝地求生' },
])

const obj = reactive({
  a: {
    b: {
      c: 666,
    },
  },
})

const car = reactive({ brand: '奔驰', price: 100 })

function changeprice() {
  car.price += 10
}

function addGame() {
  games[2].name = '洛克王国：世界'
}

function changeobj() {
  obj.a.b.c = 999
}
</script>
```

### 4.对比

```vue
<template>
  <div class="person">
    <h2>一辆{{ car.brand }}车,价值{{ car.price }}万</h2>
    <button @click="changeprice">修改汽车的价格</button>
    <button @click="changebrand">修改汽车的品牌</button>
    <button @click="changcar">修改汽车</button>
    <hr />
    <h2>求和为：{{ sum }}</h2>
    <button @click="changesum">sum+1</button>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
const obj = ref({ x: 999 })
const car = ref({ brand: '奔驰', price: 100 })
const sum = ref(0)

function changeprice() {
  car.value.price += 10
}
function changebrand() {
  car.value.brand = '宝马'
}
function changesum() {
  sum.value += 1
}
function changcar() {
  //car = { brand: '奥迪', price: 200 }
  //car.value = reactive({ brand: '奥迪', price: 200 })
  //Object.assign(car.value, { brand: '奥迪', price: 200 })
  car.value = { brand: '奥迪', price: 200 }
}
</script>
```

***

# 3.1 torefs 和 toref

**将一个响应式对象中的每一个属性，转换ref对象**

**torefs 和 toref 功能一致，但torefs批量转换**

```vue
<template>
  <div class="person">
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }},{{ nl }}</h2>
    <button @click="changeName">改名</button>
    <button @click="changeAge">加一岁</button>
  </div>
</template>

<script lang="ts" setup>
import { reactive, toRefs, toRef } from 'vue'
const person = reactive({
  name: '喜羊羊',
  age: 21,
})
const { name, age } = toRefs(person)
let nl = toRef(person, 'age')
console.log(nl.value)

function changeName() {
  name.value += '~'
  console.log(name.value, person.name)
}
function changeAge() {
  age.value += 1
  console.log(age.value)
}
</script>
```

***

# 3.2 computed 计算属性

计算属性的 get 和 set

```vue
<template>
  <div class="person">
    姓:<input type="text" v-model="firstname" /><br />
    名:<input type="text" v-model="lastname" /><br />
    全名：<span>{{ fullname }}</span>
    <button @click="changefullname">li-si</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue'
const firstname = ref('zhang')
const lastname = ref('san')

// const fullname = computed(() => {
//   return firstname.value.slice(0, 1).toUpperCase() + firstname.value.slice(1) + '-' + lastname.value
// })
const fullname = computed({
  get() {
    return (
      firstname.value.slice(0, 1).toUpperCase() + firstname.value.slice(1) + '-' + lastname.value
    )
  },
  set(val) {
    const [str1, str2] = val.split('-')
    firstname.value = str1
    lastname.value = str2
  },
})
function changefullname() {
  fullname.value = 'li-si'
}
</script>

<style scoped>
.person {
  background-color: rgb(180, 166, 13);
  box-shadow: 0 0 10px;
  border-radius: 10px;
  padding: 20px;
}

button {
  margin: 0 5px;
}
</style>
```

# 3.3 watch 监视

• 作用: **监视数据的变化 (和 Vue2 中的 watch 作用一致)**

• 特点: Vue3 中的 watch 只能监视

以下四种数据:

> 1 `ref` 定义的数据。
>
> 2 `reactive` 定义的数据。
>
> 3 函数返回一个值（`getter`函数=返回值函数）。
>
> 4 一个包含上述内容的数组。

### 情况一 监视 ref 定义的【基本类型】

**数据: 直接写数据名即可, 监视的是其 value 值的改变。**

```vue
<template>
  <div class="person">
    <h1>情况一 监视 ref 定义的【基本类型】数据</h1>
    <h2>求和为：{{ sum }}</h2>
    <button @click="changesum">sum+1</button>
  </div>
</template>

<script lang="ts" setup>
  import { ref, watch } from 'vue'
  const sum = ref(0)
  function changesum() {
    sum.value += 1
  }

  const stopwatch = watch(sum, (newvalue, oldvalue) => {
    console.log(`sum变化了`, newvalue, oldvalue)
    if (newvalue >= 10) {
      stopwatch()
    }
  })
```

### 情况二 监视 ref 定义的【对象类型】数据

```vue
<template>
  <div class="person">
    <h1>情况二 监视 ref 定义的【对象类型】数据</h1>
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="changeName">改名</button>
    <button @click="changeAge">加一岁</button>
    <button @click="changeperson">人</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch } from 'vue'
const person = ref({
  name: '喜羊羊',
  age: 21,
})

function changeName() {
  person.value.name += '~'
}
function changeAge() {
  person.value.age += 1
}
function changeperson() {
  person.value = { name: 'musitapa', age: 30 }
}
watch(
  person,
  (newvalue, oldvalue) => {
    console.log(`person变化了`, newvalue, oldvalue)
  },
  { deep: true, immediate: true },
)
</script>
```

### 情况三 监视 reactive 定义的【对象类型】数据

```vue
<template>
  <div class="person">
    <h1>情况二 监视 reactive 定义的【对象类型】数据</h1>
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <button @click="changeName">改名</button>
    <button @click="changeAge">加一岁</button>
    <button @click="changeperson">人</button>
  </div>
</template>

<script lang="ts" setup>
import { reactive, watch } from 'vue'
const person = reactive({
  name: '喜羊羊',
  age: 21,
})

function changeName() {
  person.name += '~'
}
function changeAge() {
  person.age += 1
}
function changeperson() {
  Object.assign(person, { name: 'musitapa', age: 30 })
}

watch(person, (newvalue, oldvalue) => {
  console.log('person变化了', newvalue, oldvalue)
})
</script>
```

### 情况四 监视 ref或reactive 定义的【对象类型】数据中的某个属性

> _1.若该属性值不是【对象类型】，需要写成函数形式。_
>
> _2.若该属性值是依然是【对象类型】，可直接编，也可写成函数，不过建议写成函数_

```vue
<template>
  <div class="person">
    <h2>姓名：{{ person.name }}</h2>
    <h2>年龄：{{ person.age }}</h2>
    <h2>汽车：{{ person.car.c1 }},{{ person.car.c2 }}</h2>
    <button @click="changeName">改名</button>
    <button @click="changeAge">加一岁</button>
    <button @click="changec1">修改第一车</button>
    <button @click="changec2">修改第二车</button>
    <button @click="changecar">修改整个车</button>
  </div>
</template>

<script lang="ts" setup>
import { reactive, watch } from 'vue'

const person = reactive({
  name: '喜羊羊',
  age: 18,
  car: {
    c1: '奔驰',
    c2: '宝马',
  },
})

function changeName() {
  person.name += '~'
}
function changeAge() {
  person.age += 1
}
function changec1() {
  person.car.c1 = '奥迪'
}
function changec2() {
  person.car.c2 = '大众'
}
function changecar() {
  person.car = { c1: '爱玛', c2: '雅迪' }
}
watch(
  () => {
    return person.name
  },
  (newvalue, oldvalue) => {
    console.log('person.name变化了', newvalue, oldvalue)
  },
)
watch(
  () => {
    return person.age
  },
  (newvalue, oldvalue) => {
    console.log('person.age变化了', newvalue, oldvalue)
  },
)
watch(
  () => person.car,
  (newvalue, oldvalue) => {
    console.log('person变化了', newvalue, oldvalue)
  },
  { deep: true },
)
</script>
```

![alt text](image.png)

### 情况五 监视上述的多个数据

```vue
<script lang="ts" setup>
watch(
  [() => person.name, person.car, () => person.age],
  (newvalue, oldvalue) => {
    console.log('person变化了', newvalue, oldvalue)
  },
  { deep: true },
)
</script>
```

***

# 4.1 watchEffect

**核心是：自动收集副作用函数内的响应式依赖，依赖变化时自动重执行，且默认立即执行。**

```vue
<template>
  <div class="person">
    <h2>当前水温：{{ temp }}℃</h2>
    <h2>当前水位：{{ height }}cm</h2>
    <button @click="changeTemp">水温+10</button>
    <button @click="changeHeight">水位+10</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch, watchEffect } from 'vue'

// 数据
const temp = ref(10)
const height = ref(0)

// 方法
function changeTemp() {
  temp.value += 10
}
function changeHeight() {
  height.value += 10
}
watchEffect(() => {
  console.log(temp.value, height.value)
  if (temp.value >= 60 || height.value >= 80) {
    console.log('水温过高！', '水位过高！')
  }
})
</script>
```

***

# 4.2 标签的ref属性

作用：注册模板引用，用于获取 DOM 节点或组件实例。

> 用在普通 DOM 标签上 → 获取的是 DOM 节点对象
>
> 用在组件标签上 → 获取的是 组件实例对象

App.vue（父组件）

```vue
<template>
  <h2 ref="title2">hello</h2>
  <button @click="showLog">点击获取内容</button>
  <personcard ref="ren" />
</template>

<script lang="ts" setup name="App">
import { ref } from 'vue'
import personcard from './components/preson.vue'

// 获取 DOM
const title2 = ref()
// 获取子组件实例
const ren = ref()

function showLog() {
  console.log('DOM节点：', title2.value)
  console.log('子组件实例：', ren.value)
  console.log('子组件暴露的 a：', ren.value.a)
  console.log('子组件暴露的 b：', ren.value.b)
  console.log('子组件暴露的 c：', ren.value.c)
}
</script>
```

preson.vue（子组件）

```vue
<template>
  <div class="person">
    <h1>中国</h1>
    <h2 ref="title2">北京</h2>
    <h3>天安门</h3>
    <button @click="showLogh2">子组件点击h2</button>
  </div>
</template>

<script lang="ts" setup name="personcard">
import { ref, defineExpose } from 'vue'

const title2 = ref()
const a = ref(0)
const b = ref(1)
const c = ref(2)

function showLogh2() {
  console.log('子组件内部获取h2：', title2.value)
}

// 父组件能访问的只有这里暴露的
defineExpose({
  a,
  b,
  c,
})
</script>
```

***

### 4.3 TS 接口 & 数组类型

1. 接口（interface）的作用：用来定义对象的结构，比如 personlnter 规定了一个人必须有 id(string)、name(string)、age(number) 这三个属性，少一个或类型不对，TS 都会报错。
2. 类型 \[] 更常用的简写方式 Array&#x20;

   <类型> 泛型写法，和上面完全等价

```ts
// types/index.ts
export interface personlnter {
  id: string
  name: string
  age: number
}

// 数组类型，两种写法等价
export type persons = personlnter[]
// export type persons = Array<personlnter>
```

```vue
<script lang="ts" setup name="personcard">
// 从类型文件导入
import { type personlnter, type persons } from '@/types/person'

// 单个对象
const person: personlnter = { id: 'asyud7asfd01', name: '喜羊羊', age: 20 }

// 数组，类型用 persons 或 Array<personlnter> 都可以
let personlist: persons = [
  { id: 'asyud7asfd01', name: '喜羊羊', age: 20 },
  { id: 'asyud7asfd02', name: '张三', age: 30 },
  { id: 'asyud7asfd03', name: '李四', age: 40 },
]
</script>
```
---

### 4.4 props