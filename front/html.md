# HTML & CSS 完整学习指南

## 目录

### HTML 基础篇 (1-6)
1. HTML 基础概念
2. HTML 文档结构
3. 文本内容标签
4. 链接与图像
5. 列表与表格
6. 表单与输入

### CSS 基础篇 (7-11)
7. CSS 基础概念
8. 选择器详解
9. 盒模型
10. 文本与字体样式
11. 背景与边框

### CSS 进阶篇 (12-16)
12. Flexbox 弹性布局
13. Grid 网格布局
14. 定位与浮动
15. 响应式设计
16. 动画与过渡

### CSS 高级篇 (17-20)
17. CSS 变量与现代特性
18. 最佳实践
19. 实战项目
20. 总结

---

## 第一部分：HTML 基础概念

### 什么是 HTML？

HTML (HyperText Markup Language) 是用于创建网页的标准标记语言。

**核心特点：**
- 使用标签描述网页结构
- 所有网页的基础
- 易于学习和使用
- 支持响应式和多媒体

**通俗理解：** 
如果把网页比作一栋房子，HTML 就是这栋房子的**钢筋结构**。它决定了哪里是墙、哪里是门、哪里是窗户，但不负责装饰（那是 CSS 的工作）和功能（那是 JavaScript 的工作）。

### HTML 基本语法 - 超详细解析

```html
<!-- 完整的标签结构 -->
<标签名 属性 1="值 1" 属性 2="值 2">内容</标签名>

<!-- 示例拆解 -->
<h1 class="title" id="main-title">Hello World</h1>
```

**标签的组成部分：**

1. **开始标签** `<h1>` - 告诉浏览器"从这里开始"
2. **结束标签** `</h1>` - 告诉浏览器"到这里结束"（注意斜杠 `/`）
3. **内容** `Hello World` - 开始和结束标签之间的文字
4. **属性** `class="title"` - 给标签添加额外信息

**特殊标签类型：**
- **自闭合标签**：不需要结束标签，如 `<br>`（换行）、`<img>`（图片）、`<input>`（输入框）
- **有空标签**：可以有内容但通常为空，如 `<div></div>`

### 核心概念详解：div、class、id、span

#### 1. `<div>` 是什么？

**`<div>` 是最常用的容器标签**，可以把它理解为**一个没有样式的盒子**。

```html
<!-- div 就像一个空盒子，用来装其他东西 -->
<div>
    <h1>标题</h1>
    <p>这是一个段落</p>
    <button>点击我</button>
</div>
```

**为什么需要 div？**
- **分组**：把相关的元素放在一起
- **布局**：通过 CSS 控制这个盒子的位置、大小
- **结构化**：让页面更有层次感

**生活中的比喻：**
想象你在整理书桌，`<div>` 就像不同的收纳盒：
- 一个盒子装文具（笔、橡皮、尺子）
- 一个盒子装文件（作业、试卷）
- 一个盒子装电子产品（计算器、耳机）

网页也一样，用 div 把相关内容分组管理。

#### 2. `class` 是什么？

**`class` 是给标签起的"类别名"**，就像给人贴标签："学生"、"老师"、"医生"。

```html
<!-- 多个元素可以有相同的 class -->
<p class="text-large">这段文字很大</p>
<p class="text-large">这段文字也很大</p>
<div class="text-large">这个盒子里的文字也很大</div>
```

**class 的核心作用：**
- **批量样式**：一次定义，多处使用
- **分类管理**：相同类型的元素用同一个 class
- **JavaScript 操作**：通过 class 找到并操作元素

**一个重要规则：** 同一个 class 可以用在多个元素上！

```html
<!-- ✅ 正确：多个元素共享同一个 class -->
<button class="btn">按钮 1</button>
<button class="btn">按钮 2</button>
<button class="btn">按钮 3</button>

<!-- CSS 中可以这样写 -->
<style>
.btn {
    background-color: blue;
    color: white;
    padding: 10px 20px;
}
</style>
```

#### 3. `id` 是什么？

**`id` 是元素的"身份证号"**，每个 id 在页面中必须是**唯一**的。

```html
<!-- id 就像身份证号，不能重复 -->
<div id="header">页眉</div>
<!-- ❌ 错误：不能再有另一个 id="header" 的元素 -->
```

**id vs class 的区别：**

| 特性 | id | class |
|------|-----|-------|
| 唯一性 | 必须唯一 | 可重复使用 |
| 数量 | 一个元素只能有一个 id | 一个元素可以有多个 class |
| 优先级 | CSS 中优先级高 | CSS 中优先级较低 |
| 用途 | 标识唯一元素 | 分类相似元素 |
| 比喻 | 身份证号 | 职业标签 |

```html
<!-- 正确用法示例 -->
<div id="header" class="container highlight">
    <!-- id="header" 表示这是唯一的页眉 -->
    <!-- class="container highlight" 表示它同时属于两个类别 -->
</div>
```

#### 4. `<span>` 是什么？

**`<span>` 是行内容器**，和 `<div>` 类似，但有一个关键区别：

- `<div>` 是**块级元素**：独占一行，像一个大盒子
- `<span>` 是**行内元素**：不换行，只包裹里面的内容

```html
<!-- div 会独占一行 -->
<div>第一行</div>
<div>第二行</div>
<!-- 显示效果：
第一行
第二行
-->

<!-- span 不会换行 -->
<p>这是一段文字，<span style="color: red;">这部分是红色</span>，这后面还是正常颜色</p>
<!-- 显示效果：这是一段文字，这部分是红色，这后面还是正常颜色 -->
```

**什么时候用 span？**
当你只想改变一段文字中**某几个字**的样式时：

```html
<p>
    今天天气<span style="color: red;">很好</span>，
    我们一起去<span style="text-decoration: underline;">公园</span>玩吧！
</p>
```

### 常用属性详解

```html
<!-- id: 唯一标识符 -->
<div id="header"></div>

<!-- class: 类别名，可以有多个，用空格分隔 -->
<p class="text-large highlight important"></p>

<!-- style: 直接写 CSS 样式（不推荐大量使用） -->
<span style="color: red; font-size: 20px;">红色大字</span>

<!-- data-*: 自定义数据属性，用于存储额外信息 -->
<article data-id="123" data-author="张三"></article>

<!-- title: 鼠标悬停时显示的提示文字 -->
<a href="#" title="点击查看详细信息">链接</a>

<!-- hidden: 隐藏元素 -->
<div hidden>这段内容不会显示</div>
```

### 属性的多重值写法

```html
<!-- 一个元素可以有多个 class，用空格分开 -->
<div class="card card-large highlighted"></div>

<!-- 但不能有多个 id -->
<!-- ❌ 错误 -->
<div id="header main"></div>
```

---

---

## 第二部分：HTML 文档结构 - 超详细解析

### 完整 HTML 文档拆解

让我们逐行分析一个完整的 HTML 文档，每一行都代表什么：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>页面标题</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>页眉</header>
    <nav>导航</nav>
    <main>主要内容</main>
    <footer>页脚</footer>
</body>
</html>
```

### 逐行详解

#### 1. `<!DOCTYPE html>` - 文档类型声明

**这不是 HTML 标签**，而是一条指令，告诉浏览器：
> "我使用的是 HTML5 版本，请用 HTML5 的标准来解析这个页面"

**为什么需要它？**
- 没有它，浏览器可能进入"怪异模式"（Quirks Mode），导致页面显示异常
- 确保所有浏览器用同样的标准解析你的代码

**历史知识：** 在旧版 HTML 中，这行非常长：
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```
HTML5 简化成了 `<!DOCTYPE html>`

---

#### 2. `<html lang="zh-CN">` - 根元素

**`<html>` 是整个页面的根节点**，所有其他元素都在它里面。

**`lang="zh-CN"` 属性：**
- 告诉浏览器这个页面用的是**简体中文**
- 对搜索引擎优化（SEO）很重要
- 帮助屏幕阅读器选择正确的发音

```html
<!-- 不同语言的写法 -->
<html lang="zh-CN">      <!-- 简体中文 -->
<html lang="zh-TW">      <!-- 繁体中文 -->
<html lang="en">         <!-- 英语 -->
<html lang="ja">         <!-- 日语 -->
```

---

#### 3. `<head>` - 头部区域

**`<head>` 里的内容不会直接显示在页面上**，它是给浏览器和搜索引擎看的"元信息"。

可以把 `<head>` 理解为**产品的说明书**，`<body>` 是**产品本身**。

---

#### 4. `<meta charset="UTF-8">` - 字符编码

**这行非常重要！** 它告诉浏览器用什么"字典"来解读网页中的文字。

**UTF-8 是什么？**
- 一种字符编码标准，支持世界上几乎所有语言的文字
- 如果不写这行，中文可能显示成乱码：``

**生活中的比喻：**
就像你收到一封加密信件，`charset="UTF-8"` 告诉你用哪本密码本来解码。

---

#### 5. `<meta name="viewport" ...>` - 视口设置

**这行让网页在手机正常显示！**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**属性详解：**
- `width=device-width`：网页宽度 = 设备屏幕宽度
- `initial-scale=1.0`：初始缩放比例为 100%（不放大也不缩小）

**没有这行会怎样？**
手机浏览器会默认把网页当成桌面网页显示，然后整体缩小，导致字小到看不清。

---

#### 6. `<title>页面标题</title>` - 页面标题

**显示在哪里？**
- 浏览器的标签页上
- 搜索引擎结果中
- 收藏夹/书签里

**重要提示：** 每个页面应该有独特的 title，有助于 SEO。

---

#### 7. `<link rel="stylesheet" href="style.css">` - 引入 CSS 文件

**这行连接外部样式表**，让 HTML 和 CSS 分离。

**属性详解：**
- `rel="stylesheet"`：表示关联的是样式表文件
- `href="style.css"`：CSS 文件的路径

```html
<!-- 可以引入多个 CSS 文件 -->
<link rel="stylesheet" href="reset.css">
<link rel="stylesheet" href="style.css">
<link rel="stylesheet" href="mobile.css">
```

---

#### 8. `<body>` - 主体区域

**`<body>` 里的所有内容都会显示在浏览器窗口中**，包括文字、图片、按钮等。

**简单理解：**
- `<head>` = 给浏览器看的信息（不显示）
- `<body>` = 给用户看的内容（会显示）

---

### 语义化标签详解

**什么是语义化？**
使用有明确含义的标签，让代码"自解释"。

**为什么要语义化？**
1. **可读性**：其他开发者一看就懂
2. **SEO**：搜索引擎能更好地理解页面结构
3. **无障碍**：屏幕阅读器能更好地帮助视障用户

### 常用语义化标签对比

```html
<!-- ❌ 不推荐：全部用 div -->
<div>
    <div>
        <div>Logo</div>
        <div>导航链接 1</div>
        <div>导航链接 2</div>
    </div>
    <div>主要内容</div>
    <div>版权信息</div>
</div>

<!-- ✅ 推荐：用语义化标签 -->
<header>
    <div>Logo</div>
    <nav>
        <a href="#">导航链接 1</a>
        <a href="#">导航链接 2</a>
    </nav>
</header>
<main>
    主要内容
</main>
<footer>
    版权信息
</footer>
```

### 语义化标签完整对照表

| 标签 | 含义 | 使用场景 | 生活比喻 |
|------|------|----------|----------|
| `<header>` | 页眉/头部 | 网站顶部、文章开头 | 书的封面和前言 |
| `<nav>` | 导航 | 菜单栏、面包屑 | 书的目录页 |
| `<main>` | 主要内容 | 页面的核心内容（唯一） | 书的正文部分 |
| `<article>` | 独立文章 | 博客文章、新闻、帖子 | 杂志中的一篇文章 |
| `<section>` | 章节 | 内容分区、主题分组 | 书中的章节 |
| `<aside>` | 侧边栏 | 相关链接、广告、注释 | 书页边缘的批注 |
| `<footer>` | 页脚 | 版权信息、联系方式 | 书的后记和版权页 |
| `<figure>` | 插图容器 | 图片 + 说明文字 | 书中的插图和图注 |
| `<figcaption>` | 插图说明 | 图片的标题或说明 | 图注文字 |
| `<time>` | 时间 | 发布日期、活动时间 | 日历上的日期标记 |

### 实际案例：博客文章结构

```html
<article>
    <header>
        <h1>如何学习 HTML</h1>
        <p>作者：张三</p>
        <time datetime="2024-01-15">2024 年 1 月 15 日</time>
    </header>
    
    <section>
        <h2>第一部分：基础概念</h2>
        <p>HTML 是...</p>
    </section>
    
    <section>
        <h2>第二部分：常用标签</h2>
        <p>div 是...</p>
    </section>
    
    <aside>
        <h3>相关文章</h3>
        <ul>
            <li><a href="#">CSS 入门</a></li>
            <li><a href="#">JavaScript 基础</a></li>
        </ul>
    </aside>
    
    <footer>
        <p>© 2024 我的博客</p>
    </footer>
</article>
```

---

---

## 第三部分：文本内容标签 - 超详细解析

### 标题标签 `<h1>` ~ `<h6>`

**标题标签用于定义页面中的标题**，从 `<h1>` 到 `<h6>` 重要性递减。

```html
<h1>最重要的标题（每页一个）</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>最不重要的标题</h6>
```

**关键规则：**

1. **每页只有一个 `<h1>`** 
   - `<h1>` 是页面的主标题，就像书的名称
   - 一篇文章/页面应该有且仅有一个 `<h1>`

2. **按层级使用**
   - 不要跳过级别（如从 h1 直接到 h3）
   - 像目录一样有层次结构

3. **SEO 重要性**
   - 搜索引擎特别重视 `<h1>` 的内容
   - 应该包含页面的核心关键词

**生活中的比喻：**
```
📖 一本书的结构
├─ 书名（h1）- 只有一个
│  ├─ 第 1 章（h2）
│  │  ├─ 1.1 节（h3）
│  │  │  ├─ 小节（h4）
│  ├─ 第 2 章（h2）
│  │  ├─ 2.1 节（h3）
```

**错误示例 vs 正确示例：**

```html
<!-- ❌ 错误：多个 h1 -->
<h1>欢迎访问我的网站</h1>
<h1>这是关于我们</h1>

<!-- ✅ 正确：层级清晰 -->
<h1>欢迎访问我的网站</h1>
<h2>关于我们</h2>
<h3>团队介绍</h3>
<h3>发展历程</h3>
<h2>联系我们</h2>
```

---

### 段落标签 `<p>` 

**`<p>` 用于包裹一段文字**，是最常用的文本容器。

```html
<p>这是第一段文字。它可以很长，也可以很短。</p>
<p>这是第二段文字。每个 p 标签会自动换行。</p>
```

**重要特性：**
- `<p>` 是**块级元素**：前后会自动换行
- 浏览器会忽略 HTML 中的多余空格和换行
- 不能在 `<p>` 里面放另一个 `<p>`

```html
<!-- ❌ 错误：p 里面不能嵌套 p -->
<p>第一段
    <p>这样不行</p>
</p>

<!-- ✅ 正确：用 br 换行 -->
<p>
    第一行<br>
    第二行<br>
    第三行
</p>
```

---

### 换行 `<br>` 和水平线 `<hr>`

#### `<br>` - 强制换行

**`<br>` 是自闭合标签**，表示"在这里换行"。

```html
<p>
    床前明月光<br>
    疑是地上霜<br>
    举头望明月<br>
    低头思故乡
</p>
```

**使用场景：**
- 诗歌、歌词
- 地址信息
- 需要精确控制换行的地方

**注意：** 不要用多个 `<br>` 来制造间距，应该用 CSS 的 `margin` 或 `padding`。

---

#### `<hr>` - 水平分割线

**`<hr>` 表示主题转换**，显示为一条水平线。

```html
<p>这是上一部分内容。</p>
<hr>
<p>这是下一部分内容，主题已经改变。</p>
```

**语义含义：** 
不仅仅是视觉上的线，更表示"内容的分隔"。

---

### 文本格式化标签详解

#### 1. 强调类标签

```html
<strong>重要文本</strong>  <!-- 强烈重要，通常显示为粗体 -->
<b>粗体</b>              <!-- 只是视觉上的粗体，无语义 -->

<em>强调文本</em>        <!-- 语气强调，通常显示为斜体 -->
<i>斜体</i>              <!-- 只是视觉上的斜体，无语义 -->
```

**`<strong>` vs `<b>` 的区别：**
- `<strong>`：**有语义**，表示"这段文字很重要"
- `<b>`：**无语义**，只是"让文字变粗"

**屏幕阅读器会重读 `<strong>` 和 `<em>` 的内容**，但不会特别处理 `<b>` 和 `<i>`。

```html
<!-- ✅ 推荐：用语义化标签 -->
<p>警告：<strong>高压危险，请勿靠近！</strong></p>

<!-- ❌ 不推荐：只用视觉标签 -->
<p>警告：<b>高压危险，请勿靠近！</b></p>
```

---

#### 2. 下划线和删除线

```html
<u>下划线</u>    <!-- underline -->
<s>删除线</s>    <!-- strikethrough -->
```

**使用场景：**
- `<u>`：标注专有名词、拼写错误等（慎用，容易和链接混淆）
- `<s>`：表示已删除/过时的内容，如价格折扣

```html
<p>原价：<s>¥999</s> 现价：¥599</p>
```

---

#### 3. 上标和下标

```html
<p>E = mc<sup>2</sup></p>      <!-- 上标：E = mc² -->
<p>H<sub>2</sub>O</p>          <!-- 下标：H₂O -->
```

**使用场景：**
- `<sup>`：数学公式、脚注标记
- `<sub>`：化学分子式、数学下标

---

#### 4. 代码相关标签

```html
<code>console.log("Hello")</code>     <!-- 行内代码 -->
<pre>                               <!-- 预格式化文本 -->
function hello() {
    console.log("Hello");
}
</pre>
<kbd>Ctrl + C</kbd>                   <!-- 键盘输入 -->
<samp>输出结果</samp>                 <!-- 程序输出 -->
```

**区别：**
- `<code>`：显示单个代码片段，字体变为等宽字体
- `<pre>`：保留空格和换行，适合多行代码
- `<kbd>`：表示用户键盘输入
- `<samp>`：表示程序的输出结果

```html
<p>按下 <kbd>Ctrl + C</kbd> 复制，然后 <kbd>Ctrl + V</kbd> 粘贴</p>
<p>程序输出：<samp>Hello World</samp></p>
```

---

#### 5. 引用标签

```html
<blockquote>这是一段长引用</blockquote>  <!-- 块级引用 -->
<q>这是一段短引用</q>                    <!-- 行内引用 -->
<cite>《HTML 权威指南》</cite>           <!-- 作品标题 -->
<abbr title="HyperText Markup Language">HTML</abbr>  <!-- 缩写 -->
```

**使用场景：**
- `<blockquote>`：大段引用，会缩进显示
- `<q>`：短引用，浏览器会自动添加引号
- `<cite>`：书籍、文章、电影等作品名称
- `<abbr>`：缩写词，`title` 属性显示全称

```html
<p>正如爱因斯坦所说：<q>想象力比知识更重要</q></p>

<p>这本书出自<cite>《JavaScript 高级程序设计》</cite></p>

<p><abbr title="World Health Organization">WHO</abbr>发布了最新指南</p>
```

---

### 文本标签完整对照表

| 标签 | 含义 | 默认样式 | 使用场景 |
|------|------|----------|----------|
| `<h1>`~`<h6>` | 标题 | 粗体，大小递减 | 页面/文章标题 |
| `<p>` | 段落 | 前后换行 | 文本段落 |
| `<br>` | 换行 | 换行 | 诗歌、地址 |
| `<hr>` | 分隔线 | 水平线 | 主题分隔 |
| `<strong>` | 重要 | 粗体 | 强调重要性 |
| `<b>` | 粗体 | 粗体 | 纯视觉加粗 |
| `<em>` | 强调 | 斜体 | 语气强调 |
| `<i>` | 斜体 | 斜体 | 纯视觉斜体 |
| `<u>` | 下划线 | 下划线 | 专有名词 |
| `<s>` | 删除 | 删除线 | 过期内容 |
| `<sup>` | 上标 | 上标 | 公式、脚注 |
| `<sub>` | 下标 | 下标 | 化学式 |
| `<code>` | 代码 | 等宽字体 | 代码片段 |
| `<pre>` | 预格式 | 等宽 + 保留空格 | 多行代码 |
| `<kbd>` | 键盘 | 等宽 + 边框 | 按键说明 |
| `<blockquote>` | 引用 | 缩进 | 大段引用 |
| `<q>` | 引用 | 加引号 | 短引用 |
| `<cite>` | 作品名 | 斜体 | 书名、文章名 |
| `<abbr>` | 缩写 | 无 | 缩写词 |

---

---

## 第四部分：链接与图像 - 超详细解析

### 超链接 `<a>` 标签详解

**`<a>` 标签用于创建超链接**，是网页之间跳转的核心。

```html
<a href="https://example.com">访问网站</a>
```

#### 属性完全解析

**1. `href` - 链接地址（必需）**

```html
<!-- 绝对 URL：完整网址 -->
<a href="https://www.google.com">谷歌</a>

<!-- 相对 URL：相对于当前页面 -->
<a href="./about.html">关于我们</a>      <!-- 同级目录 -->
<a href="../contact.html">联系</a>       <!-- 上级目录 -->
<a href="/home">首页</a>                 <!-- 网站根目录 -->

<!-- 锚点链接：页面内跳转 -->
<a href="#section1">跳到第一节</a>

<!-- 特殊协议 -->
<a href="mailto:test@example.com">发邮件</a>
<a href="tel:+8613800138000">打电话</a>
```

**路径详解：**
```
假设当前文件在：/website/pages/index.html

./about.html      → /website/pages/about.html（同目录）
../contact.html   → /website/contact.html（上一级）
/images/logo.png  → /website/images/logo.png（从 pages 进入 images）
/home             → /website/home（网站根目录）
```

**2. `target` - 在哪里打开链接**

```html
<!-- _self: 当前窗口打开（默认） -->
<a href="#" target="_self">当前窗口</a>

<!-- _blank: 新窗口/新标签页打开 -->
<a href="#" target="_blank">新窗口</a>

<!-- _parent: 父框架中打开 -->
<a href="#" target="_parent">父框架</a>

<!-- _top: 顶级窗口打开 -->
<a href="#" target="_top">顶级窗口</a>

<!-- 指定框架名 -->
<a href="#" target="myFrame">指定框架</a>
```

**安全提示：** 使用 `_blank` 时建议添加 `rel="noopener noreferrer"`
```html
<a href="https://external.com" target="_blank" rel="noopener noreferrer">
    外部链接
</a>
```

**3. `download` - 下载文件**

```html
<!-- 直接下载 -->
<a href="file.pdf" download>下载 PDF</a>

<!-- 指定下载文件名 -->
<a href="file.pdf" download="报告.pdf">下载</a>
```

**4. `title` - 悬停提示**

```html
<a href="help.html" title="点击查看帮助文档">帮助</a>
<!-- 鼠标放上去会显示"点击查看帮助文档" -->
```

**5. `rel` - 链接关系**

```html
<!-- nofollow: 告诉搜索引擎不要追踪此链接 -->
<a href="https://spam.com" rel="nofollow">垃圾网站</a>

<!-- noopener: 防止新窗口访问原窗口对象（安全） -->
<a href="https://external.com" rel="noopener" target="_blank">外部</a>

<!-- external: 表示外部链接 -->
<a href="https://github.com" rel="external">GitHub</a>
```

### 完整的链接示例

```html
<!-- 普通链接 -->
<a href="https://example.com">访问 Example</a>

<!-- 新窗口打开 + 安全增强 -->
<a href="https://example.com" 
   target="_blank" 
   rel="noopener noreferrer">
   访问 Example（新窗口）
</a>

<!-- 下载文件 -->
<a href="document.pdf" download="重要文档.pdf">
    下载文档
</a>

<!-- 页面内跳转 -->
<a href="#chapter1">跳转到第一章</a>

<!-- 发邮件 -->
<a href="mailto:support@example.com?subject=问题反馈">
    联系客服
</a>

<!-- 打电话（移动端） -->
<a href="tel:10086">拨打 10086</a>
```

---

### 图像 `<img>` 标签详解

**`<img>` 用于在网页中嵌入图片**，是自闭合标签。

```html
<img src="image.jpg" alt="图片描述">
```

#### 核心属性解析

**1. `src` - 图片来源（必需）**

```html
<!-- 相对路径 -->
<img src="logo.png">                    <!-- 同目录 -->
<img src="./images/logo.png">           <!-- 子目录 -->
<img src="../assets/logo.png">          <!-- 上级目录 -->

<!-- 绝对路径（从网站根目录开始） -->
<img src="/images/logo.png">

<!-- 完整 URL（外部图片） -->
<img src="https://example.com/image.jpg">

<!-- Base64 编码（小图标） -->
<img src="data:image/png;base64,iVBORw0KGgoAAAANS...">
```

**2. `alt` - 替代文字（强烈推荐）**

**`alt` 的作用：**
- 图片加载失败时显示的文字
- 屏幕阅读器读给视障用户听
- SEO 优化，帮助搜索引擎理解图片内容

```html
<!-- ✅ 好的 alt -->
<img src="cat.jpg" alt="一只橘色的猫在睡觉">
<img src="logo.png" alt="公司 Logo">
<img src="search-icon.svg" alt="搜索">

<!-- ❌ 不好的 alt -->
<img src="cat.jpg" alt="图片">         <!-- 太模糊 -->
<img src="cat.jpg" alt="img_001.jpg">  <!-- 文件名没意义 -->
<img src="cat.jpg">                    <!-- 缺少 alt -->

<!-- 装饰性图片用空 alt -->
<img src="decorative-line.png" alt="">
```

**3. `width` 和 `height` - 尺寸**

```html
<!-- 固定尺寸（不推荐，可能变形） -->
<img src="photo.jpg" width="800" height="600">

<!-- 只设置一个，另一个自动保持比例 -->
<img src="photo.jpg" width="800">

<!-- 推荐：用 CSS 控制，更灵活 -->
<img src="photo.jpg" style="width: 100%; height: auto;">
```

**4. `loading="lazy"` - 懒加载**

```html
<!-- 滚动到附近时才加载图片 -->
<img src="large-image.jpg" loading="lazy" alt="大图">
```

**好处：**
- 加快页面初始加载速度
- 节省流量
- 特别适合长页面、多图页面

**5. `srcset` 和 `sizes` - 响应式图片**

```html
<img src="medium.jpg"
     srcset="small.jpg 480w,
             medium.jpg 800w,
             large.jpg 1200w"
     sizes="(max-width: 600px) 480px,
            (max-width: 900px) 800px,
            1200px"
     alt="响应式图片">
```

**工作原理：**
浏览器根据屏幕宽度自动选择最合适的图片版本。

---

### `<picture>` 标签 - 高级图片控制

**当需要根据不同条件显示不同图片时使用**。

```html
<picture>
    <!-- WebP 格式（现代浏览器） -->
    <source srcset="image.webp" type="image/webp">
    
    <!-- JPEG 格式（备选） -->
    <source srcset="image.jpg" type="image/jpeg">
    
    <!-- 最终 fallback -->
    <img src="image-fallback.jpg" alt="描述">
</picture>
```

**使用场景：**
1. **格式降级**：WebP → JPEG → PNG
2. **艺术指导**：不同屏幕尺寸显示不同裁剪的图片
3. **分辨率适配**：Retina 屏幕用高清图

```html
<!-- 艺术指导示例：手机端显示竖版，桌面端显示横版 -->
<picture>
    <source media="(max-width: 768px)" 
            srcset="portrait.jpg">
    <source media="(min-width: 769px)" 
            srcset="landscape.jpg">
    <img src="landscape.jpg" alt="风景">
</picture>
```

---

### 图片格式对比

| 格式 | 全称 | 特点 | 使用场景 |
|------|------|------|----------|
| **JPEG/JPG** | Joint Photographic Experts Group | 有损压缩，不支持透明 | 照片、色彩丰富的图片 |
| **PNG** | Portable Network Graphics | 无损压缩，支持透明 | Logo、图标、需要透明的图片 |
| **GIF** | Graphics Interchange Format | 支持动画，颜色少 | 简单动画、表情包 |
| **WebP** | Web Picture | 高压缩率，支持透明和动画 | 现代网站首选 |
| **SVG** | Scalable Vector Graphics | 矢量图，无限放大不失真 | Logo、图标、简单图形 |
| **AVIF** | AV1 Image Format | 最新格式，压缩率最高 | 未来趋势，兼容性在提升 |

**选择建议：**
```
照片 → WebP（优先）或 JPEG
Logo/图标 → SVG 或 PNG
动画 → GIF 或 WebP
需要透明 → PNG 或 WebP
```

---

### 图片最佳实践

```html
<!-- ✅ 推荐的完整写法 -->
<img src="product.jpg"
     alt="红色运动鞋侧面展示"
     width="800"
     height="600"
     loading="lazy"
     srcset="product-400.jpg 400w,
             product-800.jpg 800w,
             product-1200.jpg 1200w"
     sizes="(max-width: 600px) 400px, 100vw">

<!-- ✅ 带 figure 和 figcaption -->
<figure>
    <img src="chart.png" alt="2024 年销售数据图表">
    <figcaption>图 1:2024 年各季度销售额对比</figcaption>
</figure>
```

---

---

## 第五部分：列表与表格 - 超详细解析

### 列表详解

HTML 中有三种列表类型，每种都有特定的使用场景。

---

#### 1. 无序列表 `<ul>` - Unordered List

**用于没有顺序关系的项目**，默认显示为圆点符号。

```html
<ul>
    <li>苹果</li>
    <li>香蕉</li>
    <li>橙子</li>
</ul>
```

**显示效果：**
```
• 苹果
• 香蕉
• 橙子
```

**常见使用场景：**
- 导航菜单
- 功能特性列表
- 购物车商品
- 标签云

```html
<!-- 导航菜单示例 -->
<nav>
    <ul>
        <li><a href="/">首页</a></li>
        <li><a href="/about">关于</a></li>
        <li><a href="/contact">联系</a></li>
    </ul>
</nav>
```

**修改列表符号样式（用 CSS）：**
```css
ul {
    list-style-type: disc;      /* 实心圆（默认） */
    list-style-type: circle;    /* 空心圆 */
    list-style-type: square;    /* 方块 */
    list-style-type: none;      /* 无符号（常用于导航） */
}
```

---

#### 2. 有序列表 `<ol>` - Ordered List

**用于有顺序关系的步骤**，默认显示为数字。

```html
<ol>
    <li>打开冰箱</li>
    <li>把大象放进去</li>
    <li>关上冰箱</li>
</ol>
```

**显示效果：**
```
1. 打开冰箱
2. 把大象放进去
3. 关上冰箱
```

**编号类型：**
```html
<!-- 数字（默认） -->
<ol>
    <li>第一步</li>
    <li>第二步</li>
</ol>
<!-- 1. 第一步  2. 第二步 -->

<!-- 大写字母 -->
<ol type="A">
    <li>第一项</li>
    <li>第二项</li>
</ol>
<!-- A. 第一项  B. 第二项 -->

<!-- 小写字母 -->
<ol type="a">
    <li>第一项</li>
    <li>第二项</li>
</ol>
<!-- a. 第一项  b. 第二项 -->

<!-- 大写罗马数字 -->
<ol type="I">
    <li>第一章</li>
    <li>第二章</li>
</ol>
<!-- I. 第一章  II. 第二章 -->

<!-- 小写罗马数字 -->
<ol type="i">
    <li>前言</li>
    <li>正文</li>
</ol>
<!-- i. 前言  ii. 正文 -->
```

**从指定数字开始：**
```html
<ol start="5">
    <li>第五步</li>
    <li>第六步</li>
</ol>
<!-- 5. 第五步  6. 第六步 -->
```

**常见使用场景：**
- 操作步骤教程
- 排行榜
- 目录章节
- 时间线

---

#### 3. 定义列表 `<dl>` - Definition List

**用于术语和解释的配对展示**，适合 FAQ、词汇表等。

```html
<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言，用于创建网页结构</dd>
    
    <dt>CSS</dt>
    <dd>层叠样式表，用于控制网页样式</dd>
    
    <dt>JavaScript</dt>
    <dd>编程语言，用于实现网页交互</dd>
</dl>
```

**结构说明：**
- `<dl>` (Definition List) - 定义列表容器
- `<dt>` (Definition Term) - 术语/名词
- `<dd>` (Definition Description) - 描述/解释

**一个术语可以有多个解释：**
```html
<dl>
    <dt>苹果</dt>
    <dd>一种水果，富含维生素 C</dd>
    <dd>一家科技公司，生产 iPhone</dd>
</dl>
```

**常见使用场景：**
- FAQ 问答
- 词汇表/字典
- 产品规格说明
- 元数据展示
```

#### 4. 嵌套列表

**列表里面可以包含另一个列表**。

```html
<ul>
    <li>水果
        <ul>
            <li>苹果</li>
            <li>香蕉</li>
        </ul>
    </li>
    <li>蔬菜
        <ul>
            <li>白菜</li>
            <li>萝卜</li>
        </ul>
    </li>
</ul>
```

**显示效果：**
```
• 水果
  • 苹果
  • 香蕉
• 蔬菜
  • 白菜
  • 萝卜
```

---

### 表格详解

**表格用于展示行列数据**，不适合用来做页面布局（那是 CSS 的工作）。

---

#### 基础表格结构

```html
<table>
    <tr>
        <td>单元格 1</td>
        <td>单元格 2</td>
    </tr>
    <tr>
        <td>单元格 3</td>
        <td>单元格 4</td>
    </tr>
</table>
```

**标签说明：**
- `<table>` - 表格容器
- `<tr>` (Table Row) - 表格行
- `<td>` (Table Data) - 表格单元格（数据格）
- `<th>` (Table Header) - 表头单元格（加粗居中）

---

#### 完整的语义化表格

```html
<table>
    <!-- 表头区域 -->
    <thead>
        <tr>
            <th>姓名</th>
            <th>年龄</th>
            <th>城市</th>
        </tr>
    </thead>
    
    <!-- 表格主体 -->
    <tbody>
        <tr>
            <td>张三</td>
            <td>25</td>
            <td>北京</td>
        </tr>
        <tr>
            <td>李四</td>
            <td>30</td>
            <td>上海</td>
        </tr>
    </tbody>
    
    <!-- 表格底部/汇总 -->
    <tfoot>
        <tr>
            <td><strong>总计</strong></td>
            <td>55</td>
            <td>2 人</td>
        </tr>
    </tfoot>
</table>
```

**为什么要用语义化分区？**
- `thead`、`tbody`、`tfoot` 让表格结构清晰
- 长表格分页打印时，表头表尾会重复显示
- 屏幕阅读器能更好地朗读表格内容

---

#### 合并单元格

**1. 跨列合并 `colspan`**

```html
<table border="1">
    <tr>
        <th colspan="2">个人信息（跨两列）</th>
    </tr>
    <tr>
        <td>姓名</td>
        <td>张三</td>
    </tr>
</table>
```

**2. 跨行合并 `rowspan`**

```html
<table border="1">
    <tr>
        <td rowspan="2">跨两行的单元格</td>
        <td>第一行</td>
    </tr>
    <tr>
        <td>第二行</td>
    </tr>
</table>
```

---

#### 表格样式（用 CSS）

```html
<style>
table {
    border-collapse: collapse;  /* 合并边框 */
    width: 100%;
}
th, td {
    border: 1px solid #ddd;
    padding: 12px;
    text-align: left;
}
th {
    background-color: #f5f5f5;
    font-weight: bold;
}
tr:nth-child(even) {
    background-color: #fafafa;  /* 斑马纹 */
}
tr:hover {
    background-color: #f0f0f0;  /* 悬停高亮 */
}
</style>
```

---

---

## 第六部分：表单与输入 - 超详细解析

**表单是用户与网站交互的主要方式**，用于登录、注册、搜索、留言等。

---

### 表单基础结构

```html
<form action="/submit" method="POST">
    <!-- 表单内容 -->
</form>
```

**`<form>` 标签的属性：**

| 属性 | 作用 | 示例 |
|------|------|------|
| `action` | 提交到哪里 | `action="/api/login"` |
| `method` | 提交方法 | `method="GET"` 或 `POST` |
| `enctype` | 编码类型 | `enctype="multipart/form-data"` |
| `target` | 在哪里打开响应 | `target="_blank"` |

---

### GET vs POST

```html
<!-- GET: 数据附在 URL 后面，适合搜索 -->
<form action="/search" method="GET">
    <input type="text" name="q" placeholder="搜索...">
</form>
<!-- 提交后：/search?q=关键词 -->

<!-- POST: 数据在请求体中，适合登录、注册 -->
<form action="/login" method="POST">
    <input type="text" name="username">
    <input type="password" name="password">
</form>
```

**区别：**
- **GET**：数据可见、有长度限制、可收藏、不适合敏感信息
- **POST**：数据不可见、无长度限制、不可收藏、适合敏感信息

---

### `<label>` - 表单标签

**`<label>` 用于描述输入框的作用**，点击 label 会自动聚焦到对应的输入框。

```html
<!-- 方式 1：使用 for 属性关联 -->
<label for="username">用户名：</label>
<input type="text" id="username" name="username">

<!-- 方式 2：包裹输入框 -->
<label>
    用户名：
    <input type="text" name="username">
</label>
```

**为什么要用 label？**
- 提高可访问性（屏幕阅读器会朗读 label）
- 扩大点击区域（用户点击文字也能聚焦）
- 语义清晰

---

### `<input>` - 输入框详解

**`<input>` 是最常用的表单元素**，通过 `type` 属性改变类型。

#### 1. 文本输入

```html
<!-- 单行文本 -->
<input type="text" name="username" placeholder="请输入用户名">

<!-- 密码（输入内容显示为圆点） -->
<input type="password" name="password" placeholder="请输入密码">

<!-- 邮箱（自动验证格式） -->
<input type="email" name="email" placeholder="example@mail.com">

<!-- 电话号码 -->
<input type="tel" name="phone" placeholder="138-0000-0000">

<!-- 网址 -->
<input type="url" name="website" placeholder="https://example.com">
```

#### 2. 数字和范围

```html
<!-- 数字输入（有上下箭头） -->
<input type="number" name="age" min="0" max="150" step="1">

<!-- 滑块 -->
<input type="range" name="volume" min="0" max="100" value="50">
```

#### 3. 日期和时间

```html
<!-- 日期选择器 -->
<input type="date" name="birthday">

<!-- 时间选择器 -->
<input type="time" name="meeting-time">

<!-- 日期 + 时间 -->
<input type="datetime-local" name="event-time">
```

#### 4. 选择和勾选

```html
<!-- 复选框（可以多选） -->
<input type="checkbox" name="hobby" value="reading"> 阅读
<input type="checkbox" name="hobby" value="music"> 音乐

<!-- 单选按钮（只能选一个） -->
<input type="radio" name="gender" value="male" id="male">
<label for="male">男</label>

<input type="radio" name="gender" value="female" id="female">
<label for="female">女</label>
```

**重要：** 同一组单选按钮必须有相同的 `name` 属性。

#### 5. 其他类型

```html
<!-- 颜色选择器 -->
<input type="color" name="favorite-color">

<!-- 文件上传 -->
<input type="file" name="avatar" accept="image/*">

<!-- 隐藏字段（用户看不到，但会提交） -->
<input type="hidden" name="token" value="abc123">
```

---

### 常用输入属性

```html
<!-- required: 必填 -->
<input type="text" name="username" required>

<!-- placeholder: 占位提示文字 -->
<input type="text" placeholder="请输入用户名">

<!-- value: 默认值 -->
<input type="text" value="默认用户名">

<!-- disabled: 禁用（不能编辑，不提交） -->
<input type="text" disabled value="不可编辑">

<!-- readonly: 只读（不能编辑，但会提交） -->
<input type="text" readonly value="只读内容">

<!-- autofocus: 自动聚焦 -->
<input type="text" autofocus>

<!-- pattern: 正则验证 -->
<input type="text" pattern="[A-Za-z]{3,}" title="至少 3 个字母">

<!-- min/max: 最小/最大值 -->
<input type="number" min="1" max="10">

<!-- maxlength: 最大长度 -->
<input type="text" maxlength="10">
```

---

### `<textarea>` - 多行文本框

```html
<textarea name="message" rows="5" cols="30" placeholder="请输入留言"></textarea>
```

**属性：**
- `rows` - 行数
- `cols` - 列数
- `placeholder` - 占位文字

---

### `<select>` - 下拉选择框

```html
<select name="city" id="city">
    <option value="">请选择城市</option>
    <option value="beijing">北京</option>
    <option value="shanghai">上海</option>
    <option value="guangzhou">广州</option>
</select>
```

**分组选项：**
```html
<select name="product">
    <optgroup label="水果">
        <option value="apple">苹果</option>
        <option value="banana">香蕉</option>
    </optgroup>
    <optgroup label="蔬菜">
        <option value="cabbage">白菜</option>
        <option value="carrot">胡萝卜</option>
    </optgroup>
</select>
```

---

### `<button>` - 按钮

```html
<!-- 提交按钮 -->
<button type="submit">提交</button>

<!-- 重置按钮（清空表单） -->
<button type="reset">重置</button>

<!-- 普通按钮（无默认行为） -->
<button type="button">点击我</button>
```

---

### 完整表单示例

```html
<form action="/register" method="POST">
    <!-- 账号信息 -->
    <fieldset>
        <legend>账号信息</legend>
        
        <div>
            <label for="username">用户名：</label>
            <input type="text" id="username" name="username" 
                   required minlength="3" maxlength="20">
        </div>
        
        <div>
            <label for="email">邮箱：</label>
            <input type="email" id="email" name="email" required>
        </div>
        
        <div>
            <label for="password">密码：</label>
            <input type="password" id="password" name="password" 
                   required minlength="6">
        </div>
    </fieldset>
    
    <!-- 个人信息 -->
    <fieldset>
        <legend>个人信息</legend>
        
        <div>
            <label>性别：</label>
            <label><input type="radio" name="gender" value="male"> 男</label>
            <label><input type="radio" name="gender" value="female"> 女</label>
        </div>
        
        <div>
            <label for="city">城市：</label>
            <select id="city" name="city">
                <option value="">请选择</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
            </select>
        </div>
    </fieldset>
    
    <!-- 提交按钮 -->
    <button type="submit">立即注册</button>
</form>
```

---

## 第七部分：CSS 基础概念

### CSS 引入方式

```html
<!-- 行内样式 -->
<p style="color: red;">红色文字</p>

<!-- 内部样式表 -->
<style>
    p { color: blue; }
</style>

<!-- 外部样式表（推荐） -->
<link rel="stylesheet" href="style.css">
```

### CSS 语法

```css
/* 选择器 { 属性：值；} */
p {
    color: red;
    font-size: 16px;
}

h1, h2, h3 {
    color: #333;
}
```

### 颜色和单位

```css
.element {
    /* 颜色 */
    color: #ff0000;
    color: rgb(255, 0, 0);
    color: rgba(255, 0, 0, 0.5);
    
    /* 单位 */
    width: 100px;
    width: 50%;
    font-size: 1.5rem;
    width: 50vw;
    height: 50vh;
}
```

---

## 第八部分：选择器详解

### 基础选择器

```css
* { margin: 0; padding: 0; }
p { color: #333; }
.class-name { color: blue; }
#unique-id { color: red; }
[target="_blank"] { color: green; }
```

### 关系选择器

```css
div p { color: blue; }      /* 后代 */
div > p { color: red; }     /* 子 */
h1 + p { color: green; }    /* 相邻兄弟 */
h1 ~ p { color: orange; }   /* 通用兄弟 */
```

### 伪类选择器

```css
a:hover { color: red; }
li:first-child { color: red; }
li:last-child { color: blue; }
li:nth-child(odd) { color: pink; }
input:focus { border-color: blue; }
input:disabled { opacity: 0.5; }
:not(.active) { opacity: 0.5; }
```

### 伪元素

```css
p::first-letter { font-size: 2em; }
p::before { content: "👉 "; }
p::after { content: " 👈"; }
::selection { background: yellow; }
```

### 优先级

!important > #id > .class > element > *

---

## 第九部分：盒模型

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid #000;
    margin: 10px;
    box-sizing: border-box;
}

/* 内边距简写 */
padding: 10px;              /* 上下左右 */
padding: 10px 20px;         /* 上下 左右 */
padding: 10px 20px 30px 40px; /* 上右下左 */

margin: 0 auto;             /* 水平居中 */
border-radius: 10px;        /* 圆角 */
border-radius: 50%;         /* 圆形 */

display: block;             /* 块级 */
display: inline;            /* 行内 */
display: inline-block;      /* 行内块 */
display: none;              /* 隐藏 */
```

---

## 第十部分：文本与字体样式

```css
.text {
    font-family: Arial, sans-serif;
    font-size: 16px;
    font-weight: bold;
    line-height: 1.5;
    color: #333;
    text-align: center;
    text-decoration: underline;
    letter-spacing: 2px;
}

/* 文本溢出省略号 */
.ellipsis {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

---

## 第十一部分：背景与边框

```css
.background {
    background: #f0f0f0 url("image.jpg") no-repeat center center / cover fixed;
    background: linear-gradient(to right, red, blue);
    background: radial-gradient(circle, red, blue);
}

.shadow {
    box-shadow: 5px 5px 10px rgba(0,0,0,0.5);
    box-shadow: inset 0 0 10px rgba(0,0,0,0.5);
}
```

---

## 第十二部分：Flexbox 弹性布局

```css
.container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}

.item {
    flex: 1;
    align-self: center;
    order: 1;
}

/* 垂直居中 */
.center {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
```

---

## 第十三部分：Grid 网格布局

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.item {
    grid-column: 1 / 3;
    grid-row: span 2;
}

/* 响应式网格 */
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
}
```

---

## 第十四部分：定位与浮动

```css
.position {
    position: relative;
    position: absolute;
    position: fixed;
    position: sticky;
    top: 0;
    z-index: 10;
}

.float {
    float: left;
    float: right;
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}
```

---

## 第十五部分：响应式设计

```css
@media (max-width: 768px) {
    .container { width: 100%; }
}

@media (prefers-color-scheme: dark) {
    body { background: #1a1a1a; color: #fff; }
}

.container {
    width: 90%;
    max-width: 1200px;
    margin: 0 auto;
}

img {
    max-width: 100%;
    height: auto;
}
```

---

## 第十六部分：动画与过渡

```css
.button {
    transition: all 0.3s ease;
}
.button:hover {
    background: red;
    transform: scale(1.1);
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.animated {
    animation: fadeIn 0.5s ease;
}

.transform {
    transform: translateX(50%);
    transform: scale(1.5);
    transform: rotate(45deg);
}
```

---

## 第十七部分：CSS 变量与现代特性

```css
:root {
    --primary-color: #3498db;
    --text-color: #333;
    --spacing-unit: 8px;
}

.button {
    background-color: var(--primary-color);
    color: var(--text-color);
    padding: calc(var(--spacing-unit) * 2);
}

.box {
    width: clamp(300px, 50%, 800px);
    aspect-ratio: 16 / 9;
}

img {
    object-fit: cover;
}
```

---

## 第十八部分：最佳实践

```css
/* CSS Reset */
* { margin: 0; padding: 0; box-sizing: border-box; }

/* BEM 命名 */
.card {}
.card__image {}
.card--featured {}

/* 属性顺序 */
.selector {
    position: relative;
    z-index: 1;
    display: block;
    width: 100%;
    font-size: 16px;
    color: #333;
    background: #fff;
}
```

---

## 第十九部分：实战项目 - 个人名片

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个人名片</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, sans-serif;
            background: linear-gradient(135deg, #667eea, #764ba2);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            max-width: 400px;
            width: 100%;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            text-align: center;
        }
        .avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            margin: 0 auto 20px;
            border: 4px solid #667eea;
        }
        .name { font-size: 24px; font-weight: bold; margin-bottom: 8px; }
        .title { color: #666; margin-bottom: 20px; }
        .info-item { margin: 10px 0; color: #555; }
        .social-link {
            width: 40px; height: 40px;
            background: #667eea;
            color: white;
            border-radius: 50%;
            text-decoration: none;
            line-height: 40px;
        }
    </style>
</head>
<body>
    <div class="card">
        <img src="avatar.jpg" alt="头像" class="avatar">
        <h1 class="name">张三</h1>
        <p class="title">前端开发工程师</p>
        <div class="info-item">📧 zhangsan@example.com</div>
        <div class="info-item">📱 138-0000-0000</div>
        <div class="social-links">
            <a href="#" class="social-link">G</a>
            <a href="#" class="social-link">H</a>
        </div>
    </div>
</body>
</html>
```

---

## 第二十部分：总结

### 核心知识点

**HTML:** 文档结构、语义化标签、表单、多媒体
**CSS:** 选择器、盒模型、Flexbox、Grid、响应式、动画

### 下一步学习

1. JavaScript - 交互逻辑
2. CSS 框架 - Bootstrap, Tailwind
3. 构建工具 - Webpack, Vite
4. 现代框架 - React, Vue

### 学习资源

- MDN Web Docs: https://developer.mozilla.org
- CSS-Tricks: https://css-tricks.com
- CodePen: https://codepen.io
- freeCodeCamp: https://freecodecamp.org

祝你前端学习顺利！🚀
