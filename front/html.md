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

### HTML 基本语法

```html
<!-- 标签结构 -->
<标签名 属性="值">内容</标签名>
<h1 class="title">Hello World</h1>
<img src="image.jpg" alt="描述">
<br>
<input type="text">
```

### 常用属性

```html
<div id="header"></div>
<p class="text-large highlight"></p>
<span style="color: red;">红色文字</span>
<article data-id="123"></article>
```

---

## 第二部分：HTML 文档结构

### 完整 HTML 文档

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

### 语义化标签

| 标签 | 用途 |
|------|------|
| header | 页眉 |
| nav | 导航 |
| main | 主要内容 |
| article | 独立文章 |
| section | 章节 |
| aside | 侧边栏 |
| footer | 页脚 |

---

## 第三部分：文本内容标签

### 标题标签

```html
<h1>最重要的标题（每页一个）</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>最不重要的标题</h6>
```

### 段落与换行

```html
<p>这是一个段落。</p>
第一行<br>
第二行
<hr>
```

### 文本格式化

```html
<strong>重要文本</strong>
<b>粗体</b>
<em>强调文本</em>
<i>斜体</i>
<u>下划线</u>
<s>删除线</s>
E = mc²
H₂O
<code>代码</code>
<pre>预格式化文本</pre>
<kbd>Ctrl + C</kbd>
<blockquote>引用</blockquote>
<cite>书名</cite>
```

---

## 第四部分：链接与图像

### 超链接

```html
<a href="https://example.com">访问网站</a>
<a href="https://example.com" target="_blank">新窗口</a>
<a href="./about.html">关于</a>
<a href="#section1">跳转到第一节</a>
<a href="file.pdf" download>下载</a>
<a href="mailto:test@example.com">发邮件</a>
<a href="tel:+8613800138000">打电话</a>
```

### 图像

```html
<img src="image.jpg" alt="图片描述">
<img src="photo.jpg" alt="风景" width="800" height="600" loading="lazy">
<picture>
    <source srcset="image.webp" type="image/webp">
    <img src="image.jpg" alt="备选">
</picture>
```

**图片格式：** JPEG(照片), PNG(透明), GIF(动画), WebP(现代), SVG(矢量)

---

## 第五部分：列表与表格

### 列表

```html
<ul>
    <li>项目 1</li>
    <li>项目 2</li>
</ul>

<ol>
    <li>第一步</li>
    <li>第二步</li>
</ol>

<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言</dd>
</dl>
```

### 表格

```html
<table>
    <thead>
        <tr>
            <th>姓名</th>
            <th>年龄</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>张三</td>
            <td>25</td>
        </tr>
    </tbody>
</table>
```

---

## 第六部分：表单与输入

```html
<form action="/submit" method="POST">
    <label for="username">用户名：</label>
    <input type="text" id="username" name="username" required>
    
    <label for="password">密码：</label>
    <input type="password" id="password" name="password" required>
    
    <label for="email">邮箱：</label>
    <input type="email" id="email" name="email">
    
    <fieldset>
        <legend>性别</legend>
        <label><input type="radio" name="gender" value="male">男</label>
        <label><input type="radio" name="gender" value="female">女</label>
    </fieldset>
    
    <label for="city">城市：</label>
    <select id="city" name="city">
        <option value="beijing">北京</option>
        <option value="shanghai">上海</option>
    </select>
    
    <label for="message">留言：</label>
    <textarea id="message" name="message" rows="5"></textarea>
    
    <button type="submit">提交</button>
</form>
```

**其他输入类型：** number, range, date, color, search, tel, url

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
