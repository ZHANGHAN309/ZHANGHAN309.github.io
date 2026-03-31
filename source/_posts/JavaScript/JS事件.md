---
title: JS事件
date: 2025-11-13 10:51:03
tags: JavaScript
categories: 技术篇
---

# 事件描述

事件相当于产生一个动作或者是某个对象状态发生改变，比如点击按钮就是一个事件。当事件发生后会触发某种信号，并提供某种事件处理方式，之后就会按照预先设定好的事件处理方式进行。

# 怎么使用事件

## `addEventListener()`

```javascript
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function changeBackground() {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
}

btn.addEventListener("click", changeBackground);
```

用这样的方式可以为某个事件添加多个处理函数

```javascript
btn.addEventListener("click", function1);
btn.addEventListener("click", function2);
```

- `removeEventListener()`可以删除已经添加的事件监听器

```javascript
btn.removeEventListener("click", function1);
```

- 通过传递`AbortSignal`到`addEventListener()`，在拥有`AbortSignal`的控制器上调用`abort()`，从而删除事件处理器

```javascript
const controller = new AbortController();

btn.addEventListener("click",
  () => {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    document.body.style.backgroundColor = rndCol;
  },
  { signal: controller.signal } // 向该处理器传递 AbortSignal
);

controller.abort();
```

## 事件处理器属性

推荐使用`addEventListener()`来注册事件处理器，但是也有其他方法

```javascript
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

btn.onclick = () => {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
};
```

类似

```javascript
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function bgChange() {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
}

btn.onclick = bgChange;
```

但是这种方式添加的处理器会被下一个函数覆盖

## 内联事件处理器--不推荐

```html
<button onclick="bgChange()">按下我</button>
```

这种方式添加的处理器会不方便管理

# 事件对象

有时候在事件处理函数内部，可能会看到一个固定指定名称的参数，例如event、evt或e，这被称为事件对象，它会被自动传递给事件处理函数作为第一个参数。

```javascript
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function bgChange(e) {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  e.target.style.backgroundColor = rndCol;
  console.log(e);
}

btn.addEventListener("click", bgChange);
```

## 事件对象的核心属性

| 属性             | 描述             |
| ------------------- | ------------------------------------------------------------ |
| `type`              | 事件类型（如 `click`、`mouseover`、`keydown`）。             |
| `target`            | 触发事件的**原始元素**（事件最初发生的元素）。               |
| `currentTarget`     | 绑定事件处理函数的**当前元素**（与 `this` 指向一致）。       |
| `bubbles`           | 布尔值，指示事件是否会冒泡（向上传播）。                     |
| `cancelable`        | 布尔值，指示事件是否可以取消默认行为（通过 `preventDefault()`）。 |
| `clientX`/`clientY` | 鼠标事件中，鼠标相对于浏览器可视区域的坐标（不含滚动条偏移）。 |
| `pageX`/`pageY`     | 鼠标事件中，鼠标相对于文档页面的坐标（含滚动条偏移）。       |
| `key`               | 键盘事件中，按下的键对应的字符（如 `a`、`Enter`）。          |
| `code`              | 键盘事件中，按下的物理键的编码（如 `KeyA`、`Enter`）。       |

## 事件对象的常用方法

| 方法                         | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| `preventDefault()`           | 取消事件的默认行为（如阻止链接跳转、表单提交、右键菜单弹出等）。 |
| `stopPropagation()`          | 阻止事件冒泡（阻止事件向父元素传播，避免父元素的事件处理函数被触发）。 |
| `stopImmediatePropagation()` | 不仅阻止事件冒泡，还会阻止当前元素上后续的事件处理函数执行。 |

示例1：阻止默认行为

```html
<!-- 阻止链接跳转 -->
<a href="https://example.com" id="link">点击不跳转</a>

<script>
  const link = document.getElementById("link");
  link.addEventListener("click", function(e) {
    e.preventDefault(); // 取消默认跳转行为
    console.log("链接被点击，但不会跳转");
  });
</script>
```

示例2：阻止事件冒泡

```html
<div id="parent" style="padding: 50px; background: lightgray;">
  父元素
  <button id="child">子元素</button>
</div>

<script>
  const parent = document.getElementById("parent");
  const child = document.getElementById("child");
  
  child.addEventListener("click", function(e) {
    e.stopPropagation(); // 阻止事件冒泡到父元素
    console.log("子元素被点击");
  });
  
  parent.addEventListener("click", function() {
    console.log("父元素被点击"); // 若不阻止冒泡，点击子元素时会同时触发此函数
  });
</script>
```

在事件冒泡中，事件是按照从里面的元素冒泡而出

```html
<body>
  <div id="container">
    <button>点我！</button>
  </div>
  <pre id="output"></pre>
</body>
```

```javascript
const output = document.querySelector("#output");
function handleClick(e) {
  output.textContent += `你在 ${e.currentTarget.tagName} 元素上进行了点击\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

document.body.addEventListener("click", handleClick);
container.addEventListener("click", handleClick);
button.addEventListener("click", handleClick);
```

```
你在 BUTTON 元素上进行了点击
你在 DIV 元素上进行了点击
你在 BODY 元素上进行了点击
```

事件捕获可以让事件先在最小嵌套元素上发生，然后在连续更多的嵌套元素上发生，直到达到目标。

事件捕获默认是禁用的，你需要在`addEventListener()`的`capture`选项中启用它

```html
<body>
  <div id="container">
    <button>点我！</button>
  </div>
  <pre id="output"></pre>
</body>
```

```js
const output = document.querySelector("#output");
function handleClick(e) {
  output.textContent += `你在 ${e.currentTarget.tagName} 元素上进行了点击\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

document.body.addEventListener("click", handleClick, { capture: true });
container.addEventListener("click", handleClick, { capture: true });
button.addEventListener("click", handleClick);
```

```
你在 BODY 元素上进行了点击
你在 DIV 元素上进行了点击
你在 BUTTON 元素上进行了点击
```

# 参考

[事件介绍 - 学习 Web 开发 | MDN](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/Events)
