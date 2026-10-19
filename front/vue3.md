## 第一部分：Vue 是什么

### 什么是 Vue？

Vue (读音 /vjuː/，类似 view) 是一个用于构建用户界面的 **渐进式 JavaScript 框架**。

**特点：**
- ✅ 易上手：有 HTML 基础就能开始
- ✅ 灵活：可以只用在页面的一部分
- ✅ 高效：虚拟 DOM，性能优秀
- ✅ 生态丰富：路由、状态管理、UI 库齐全

### Vue 能做什么？

```
✅ 单页应用 (SPA)
✅ 移动端应用 (配合 Uni-app)
✅ 桌面应用 (配合 Electron)
✅ 小程序 (配合 Taro)
✅ 静态网站生成 (配合 VitePress)
```

### Vue 2 vs Vue 3

| 特性 | Vue 2 | Vue 3 |
|------|-------|-------|
| API 风格 | Options API | Options + Composition API |
| 性能 | 好 | 更好 (快 1.3-2 倍) |
| TypeScript 支持 | 一般 | 优秀 |
| 体积 | 较大 | 更小 (Tree-shaking) |
| 新特性 | - | Fragment, Teleport, Suspense |

**建议：直接学 Vue 3！**

---

## 第二部分：第一个 Vue 应用

### 方式一：CDN 引入（快速体验）

```html
<!DOCTYPE html>
<html>
<head>
    <title>Vue 3 示例</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{ message }}</h1>
        <button @click="reverseMessage">反转消息</button>
    </div>

    <script>
        const { createApp } = Vue;

        createApp({
            data() {
                return {
                    message: 'Hello Vue 3!'
                }
            },
            methods: {
                reverseMessage() {
                    this.message = this.message.split('').reverse().join('');
                }
            }
        }).mount('#app');
    </script>
</body>
</html>
```

### 方式二：Vite 创建项目（推荐）

```bash
# 安装 Node.js 后执行
npm create vue@latest my-vue-app
cd my-vue-app
npm install
npm run dev
```

### 项目结构

```
my-vue-app/
├── public/          # 静态资源
├── src/
│   ├── assets/      # 图片、样式等
│   ├── components/  # 组件
│   ├── views/       # 页面
│   ├── App.vue      # 根组件
│   └── main.js      # 入口文件
├── index.html
├── package.json
└── vite.config.js
```

---

## 第三部分：模板语法

**插值：** `{{ message }}` `{{ number + 1 }}`

**指令：**
- `v-text="msg"` - 文本
- `v-html="html"` - HTML

---

## 第四部分：计算属性

```vue
computed: {
  fullName() {
    return this.firstName + this.lastName;
  }
}
```
特点：有缓存，性能更好

---

## 第五部分：条件渲染

```vue
<p v-if="seen">存在</p>
<div v-else>不存在</div>
<p v-show="ok">显示</p>
```
v-if 切换 DOM，v-show 切换 display

---

## 第六部分：列表渲染

```vue
<li v-for="item in items" :key="item.id">
  {{ item.name }}
</li>
```
⚠️ 必须使用 :key！

---

## 第七部分：事件处理

```vue
<button @click="count++">{{ count }}</button>
<button @click.stop="doSomething">停止冒泡</button>
<form @submit.prevent="onSubmit">表单</form>
<input @keyup.enter="submit" />
```
修饰符：.prevent .stop .self .once .enter

---

## 第八部分：表单绑定

```vue
<input v-model="message" />
<textarea v-model="desc"></textarea>
<input type="checkbox" v-model="checked" />
<select v-model="selected"><option>A</option></select>
```
修饰符：.lazy .number .trim

---

## 第九部分：组件基础

```vue
<!-- 定义 -->
<template><button @click="c++">{{ c }}</button></template>
<script>export default { data(){return {c:0}} }</script>

<!-- 使用 -->
<script>
import Btn from './Btn.vue';
export default { components: { Btn } }
</script>
```

---

## 第十部分：Props

```vue
<!-- 子接收 -->
props: {
  title: String,
  author: { type: String, default: '未知' }
}

<!-- 父传递 -->
<child title="标题" :author="'张三'" />
```

---

## 第十一部分：自定义事件

```vue
<!-- 子触发 -->
<button @click="$emit('del', id)">删除</button>

<!-- 父监听 -->
<child @del="removeTodo" />
```

---

## 第十二部分：生命周期

created -> mounted -> updated -> unmounted

---

## 第十三部分：watch

```vue
watch: {
  question(val) {
    console.log('变了', val);
  }
}
```

---

## 第十四部分：ref

```vue
<input ref="inputRef" />
<button @click="$refs.inputRef.focus()">聚焦</button>
```

---

## 第十五部分：组件通信

1. 父子：Props / emit
2. 兄弟：父中转
3. 跨级：provide/inject
4. 全局：Pinia

---

## 第十六部分：插槽

```vue
<!-- 子 -->
<slot>默认</slot>
<slot name="header"></slot>

<!-- 父 -->
<child>
  <template #header>自定义</template>
</child>
```

---

## 第十七部分：组合式 API

```vue
<script setup>
import { ref } from 'vue';
const count = ref(0);
const inc = () => count.value++;
</script>
```

---

## 第十八部分：ref vs reactive

```vue
const count = ref(0);       // 基本类型，用 .value
const obj = reactive({});   // 对象，直接用
```

---

## 第十九 - 二十四部分：进阶

详见官方文档

---

## 第二十五部分：Vue Router

```bash
npm install vue-router@4
```

```js
const routes = [
  { path: '/', component: Home },
  { path: '/user/:id', component: User }
];
```

```vue
<router-link to="/">首页</router-link>
<router-view />
```

获取参数：`route.params.id`

---

## 第二十六部分：Pinia

```bash
npm install pinia
```

```js
// store
export const useStore = defineStore('main', {
  state: () => ({ count: 0 }),
  actions: { inc() { this.count++; } }
});

// 使用
const store = useStore();
store.inc();
```

---

## 第三十二部分：实战项目

待办事项应用（添加、删除、筛选、持久化）

---

## 总结

**学习路线：**
模板 → 计算属性 → 条件/列表 → 事件 → 表单 → 组件 → Props/Events → 生命周期 → 组合式 API → Router/Pinia

**下一步：**
- UI 库：Element Plus
- TypeScript
- 全栈开发

**资源：**
- 官方文档：https://cn.vuejs.org/
- Vue School

祝学习顺利！🎉
