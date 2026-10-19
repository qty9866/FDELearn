# JavaScript 完整学习指南：从零到一

> 💡 让网页'动'起来的编程语言

## 📚 目录

### 入门篇 (1-8)
1. JavaScript 是什么
2. 第一个 JS 程序
3. 变量与数据类型
4. 运算符
5. 条件判断
6. 循环
7. 函数
8. 数组

### 基础篇 (9-16)
9. 对象
10. 字符串操作
11. 日期与时间
12. Math 对象
13. DOM 操作
14. 事件处理
15. BOM 操作
16. 表单验证

### 进阶篇 (17-24)
17. 作用域
18. 闭包
19. this 关键字
20. 原型与继承
21. ES6+新特性
22. 异步编程
23. Promise
24. async/await

### 高级篇 (25-32)
25. 模块化
26. AJAX 与 Fetch
27. JSON
28. 本地存储
29. 正则表达式
30. 错误处理
31. 调试技巧
32. 实战项目

---

## 第一部分：JavaScript 是什么

### 什么是 JavaScript？

JavaScript (简称 JS) 是一种运行在浏览器中的编程语言，用于让网页动起来。

**HTML、CSS、JavaScript 的关系：**
- HTML = 骨架（结构）
- CSS = 皮肤（样式）
- JavaScript = 肌肉（行为）

---

## 第三部分：变量与数据类型

变量就像一个盒子，用来存储数据。

```javascript
// 声明变量
let name = "张三";
let age = 25;
const PI = 3.14;

// 使用变量
console.log(name);
```

### 数据类型

```javascript
// 字符串
let str = "Hello";

// 数字
let num = 42;

// 布尔值
let isTrue = true;

// undefined
let undef;

// null
let empty = null;
```

---

## 第四部分：运算符

### 算术运算符

```javascript
let a = 10;
let b = 3;

a + b   // 加：13
a - b   // 减：7
a * b   // 乘：30
a / b   // 除：3.333...
a % b   // 取余：1
a ** b  // 幂：1000
a++     // 自增：11
a--     // 自减：9
```

### 比较运算符

```javascript
5 == 5    // 相等：true
5 === "5"  // 全等（类型和值）：false
5 != 3    // 不相等：true
5 !== "5"  // 不全等：true
5 > 3     // 大于：true
5 < 3     // 小于：false
5 >= 5    // 大于等于：true
```

### 逻辑运算符

```javascript
true && false   // 与：false
true || false   // 或：true
!true           // 非：false
```

---

## 第五部分：条件判断

### if...else 语句

```javascript
let age = 18;

if (age >= 18) {
    console.log("成年人");
} else {
    console.log("未成年人");
}
```

### if...else if...else

```javascript
let score = 85;

if (score >= 90) {
    console.log("优秀");
} else if (score >= 80) {
    console.log("良好");
} else if (score >= 60) {
    console.log("及格");
} else {
    console.log("不及格");
}
```

### switch 语句

```javascript
let day = 1;

switch(day) {
    case 1:
        console.log("星期一");
        break;
    case 2:
        console.log("星期二");
        break;
    default:
        console.log("其他");
}
```

### 三元运算符

```javascript
let age = 20;
let result = age >= 18 ? "成年" : "未成年";
console.log(result);  // 输出：成年
```

---

## 第六部分：循环

### for 循环

```javascript
// 从 1 数到 5
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
// 输出：1, 2, 3, 4, 5
```

### while 循环

```javascript
let i = 1;
while (i <= 5) {
    console.log(i);
    i++;
}
```

### do...while 循环

```javascript
let i = 1;
do {
    console.log(i);
    i++;
} while (i <= 5);
```

### break 和 continue

```javascript
// break - 跳出循环
for (let i = 1; i <= 10; i++) {
    if (i === 5) {
        break;  // 到 5 就停止
    }
    console.log(i);  // 输出：1, 2, 3, 4
}

// continue - 跳过本次
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        continue;  // 跳过 3
    }
    console.log(i);  // 输出：1, 2, 4, 5
}
```

---

## 第七部分：函数

### 什么是函数？

函数是一段可以重复使用的代码。

```javascript
// 声明函数
function sayHello() {
    console.log("你好！");
}

// 调用函数
sayHello();  // 输出：你好！
```

### 带参数的函数

```javascript
function greet(name) {
    console.log("你好，" + name + "！");
}

greet("张三");  // 输出：你好，张三！
greet("李四");  // 输出：你好，李四！
```

### 返回值

```javascript
function add(a, b) {
    return a + b;
}

let result = add(3, 5);
console.log(result);  // 输出：8
```

### 箭头函数（ES6）

```javascript
// 传统函数
function add(a, b) {
    return a + b;
}

// 箭头函数
const add2 = (a, b) => {
    return a + b;
};

// 简写
const add3 = (a, b) => a + b;
```

---

## 第八部分：数组

### 创建数组

```javascript
// 方法 1
let fruits = ["苹果", "香蕉", "橙子"];

// 方法 2
let numbers = new Array(1, 2, 3, 4, 5);
```

### 访问数组元素

```javascript
let fruits = ["苹果", "香蕉", "橙子"];

fruits[0];  // "苹果"
fruits[1];  // "香蕉"
fruits[2];  // "橙子"
fruits.length;  // 3（数组长度）
```

### 数组方法

```javascript
let arr = [1, 2, 3, 4, 5];

// 添加元素
arr.push(6);      // 末尾添加：[1,2,3,4,5,6]
arr.unshift(0);   // 开头添加：[0,1,2,3,4,5,6]

// 删除元素
arr.pop();        // 删除末尾
arr.shift();      // 删除开头

// 查找
arr.indexOf(3);   // 找到 3 的位置
arr.includes(3);  // 是否包含 3：true

// 转换
arr.join("-");    // "1-2-3-4-5"
arr.toString();   // "1,2,3,4,5"

// 切片
arr.slice(1, 3);  // [2, 3]（不包含 3）

// 遍历
arr.forEach(item => console.log(item));
```

---

## 第九部分：对象

### 什么是对象？

对象是键值对的集合。

```javascript
// 创建对象
let person = {
    name: "张三",
    age: 25,
    city: "北京",
    isStudent: false
};
```

### 访问对象属性

```javascript
let person = {
    name: "张三",
    age: 25
};

// 方法 1：点表示法
person.name;  // "张三"

// 方法 2：方括号
person["age"];  // 25

// 修改属性
person.age = 26;
person.city = "上海";

// 添加新属性
person.job = "工程师";

// 删除属性
delete person.city;
```

### 对象方法

```javascript
let person = {
    name: "张三",
    sayHello: function() {
        console.log("你好，我是" + this.name);
    }
};

person.sayHello();  // 输出：你好，我是张三
```

---

## 第十部分：字符串操作

```javascript
let str = "Hello World";

// 长度
str.length;  // 11

// 大小写
str.toUpperCase();  // "HELLO WORLD"
str.toLowerCase();  // "hello world"

// 查找
str.indexOf("World");  // 6
str.includes("Hello");  // true

// 截取
str.slice(0, 5);   // "Hello"
str.substring(6);  // "World"

// 替换
str.replace("World", "JS");  // "Hello JS"

// 分割
str.split(" ");  // ["Hello", "World"]

// 去除空格
let trimStr = "  hello  ";
trimStr.trim();  // "hello"
```

---

## 第十一部分：DOM 操作

### 什么是 DOM？

DOM（文档对象模型）是 HTML 的编程接口。

### 获取元素

```javascript
// 通过 ID
document.getElementById("myId");

// 通过类名
document.getElementsByClassName("myClass");

// 通过标签名
document.getElementsByTagName("div");

// CSS 选择器
document.querySelector(".myClass");      // 第一个
document.querySelectorAll(".myClass");   // 所有
```

### 修改内容

```javascript
let elem = document.getElementById("demo");

elem.textContent = "新文本";     // 纯文本
elem.innerHTML = "<b>加粗</b>";  // HTML
elem.innerText = "新文本";       // 可见文本
```

### 修改样式

```javascript
let elem = document.getElementById("demo");

elem.style.color = "red";
elem.style.fontSize = "20px";
elem.style.backgroundColor = "yellow";
```

### 添加/删除元素

```javascript
// 创建元素
let newDiv = document.createElement("div");
newDiv.textContent = "我是新元素";

// 添加到页面
document.body.appendChild(newDiv);

// 删除元素
elem.remove();
```

---

## 第十二部分：事件处理

### 什么是事件？

事件是用户或浏览器执行的操作。

### 常见事件

```javascript
// 鼠标事件
click       // 点击
dblclick    // 双击
mouseover   // 鼠标移入
mouseout    // 鼠标移出
mousemove   // 鼠标移动

// 键盘事件
keydown     // 按键按下
keyup       // 按键释放
keypress    // 按键按下并释放

// 表单事件
submit      // 提交
change      // 改变
focus       // 聚焦
blur        // 失焦
input       // 输入

// 页面事件
load        // 加载完成
resize      // 窗口调整
scroll      // 滚动
```

### 添加事件监听器

```javascript
// 方法 1：HTML 中
<button onclick="alert(\"点击了！\")">按钮</button>

// 方法 2：直接绑定
let btn = document.getElementById("myBtn");
btn.onclick = function() {
    console.log("点击了！");
};

// 方法 3：addEventListener（推荐）
btn.addEventListener("click", function() {
    console.log("点击了！");
});

// 带参数的箭头函数
btn.addEventListener("click", (event) => {
    console.log(event.target);
});
```

### 阻止默认行为

```javascript
link.addEventListener("click", (e) => {
    e.preventDefault();  // 阻止跳转
});

form.addEventListener("submit", (e) => {
    e.preventDefault();  // 阻止提交
});
```

---

## 第十三部分：ES6+ 新特性

### let 和 const

```javascript
// var - 函数作用域（不推荐）
var x = 1;

// let - 块级作用域，可修改
let y = 2;
y = 3;  // OK

// const - 块级作用域，不可修改
const z = 4;
z = 5;  // Error!
```

### 模板字符串

```javascript
let name = "张三";
let age = 25;

// 传统方式
console.log("我叫" + name + "，今年" + age + "岁");

// 模板字符串
console.log(\`我叫${name}，今年${age}岁\`);
```

### 解构赋值

```javascript
// 数组解构
let [a, b, c] = [1, 2, 3];
console.log(a);  // 1

// 对象解构
let person = {name: "张三", age: 25};
let {name, age} = person;
console.log(name);  // "张三"
```

### 展开运算符

```javascript
// 合并数组
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = [...arr1, ...arr2];

// 复制数组
let copy = [...arr1];

// 对象展开
let obj1 = {a: 1};
let obj2 = {...obj1, b: 2};
```

### 默认参数

```javascript
function greet(name = "朋友") {
    console.log(\`你好，${name}！\`);
}

greet();           // 你好，朋友！
greet("张三");     // 你好，张三！
```

---

## 第十四部分：异步编程

### 同步 vs 异步

```javascript
// 同步：按顺序执行
console.log("1");
console.log("2");
console.log("3");
// 输出：1, 2, 3

// 异步：不阻塞后续代码
console.log("1");
setTimeout(() => {
    console.log("2");
}, 1000);
console.log("3");
// 输出：1, 3, 2（2 延迟 1 秒）
```

### setTimeout 和 setInterval

```javascript
// 延迟执行
setTimeout(() => {
    console.log("1 秒后执行");
}, 1000);

// 定时执行
let timer = setInterval(() => {
    console.log("每 2 秒执行一次");
}, 2000);

// 清除定时器
clearInterval(timer);
```

---

## 第十五部分：Promise

### 什么是 Promise？

Promise 是异步编程的解决方案。

```javascript
let promise = new Promise((resolve, reject) => {
    // 异步操作
    let success = true;
    
    if (success) {
        resolve("成功！");
    } else {
        reject("失败！");
    }
});

// 使用 Promise
promise
    .then(result => {
        console.log(result);  // 成功时调用
    })
    .catch(error => {
        console.log(error);   // 失败时调用
    });
```

### Promise 链式调用

```javascript
fetchData()
    .then(data => {
        console.log(data);
        return processData(data);
    })
    .then(processed => {
        console.log(processed);
    })
    .catch(error => {
        console.error(error);
    });
```

---

## 第十六部分：async/await

### async 函数

```javascript
// 声明 async 函数
async function fetchData() {
    return "数据";
}

// 箭头函数
const getData = async () => {
    return "数据";
};
```

### await 关键字

```javascript
async function loadData() {
    try {
        let result1 = await fetch(url1);
        let data1 = await result1.json();
        
        let result2 = await fetch(url2);
        let data2 = await result2.json();
        
        console.log(data1, data2);
    } catch (error) {
        console.error(error);
    }
}
```

### Promise + async/await

```javascript
async function getUserData() {
    const response = await fetch("https://api.example.com/user");
    const user = await response.json();
    return user;
}

getUserData().then(user => console.log(user));
```

---

## 第十七部分：AJAX 与 Fetch

### 什么是 AJAX？

AJAX 允许网页与服务器交换数据而不刷新页面。

### Fetch API（推荐）

```javascript
// GET 请求
fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));

// POST 请求
fetch("https://api.example.com/data", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({name: "张三", age: 25})
})
.then(response => response.json())
.then(data => console.log(data));

// async/await 方式
async function getData() {
    try {
        const response = await fetch(url);
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

---

