####为什么要使用babel-polyfill？

​       Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而可以在现有环境执行，所以我们可以用ES6编写，而不用考虑环境支持的问题；
​        有些浏览器版本的发布早于ES6的定稿和发布，因此如果在编程中使用了ES6的新特性，而浏览器没有更新版本，或者新版本中没有对ES6的特性进行兼容，那么浏览器就会无法识别ES6代码，例如IE9根本看不懂代码写的let和const是什么东西？只能选择报错，这就是浏览器对ES6的兼容性问题；

​       Babel默认只转换新的JavaScript语法（syntax），如箭头函数等，而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码；因此我们需要polyfill；
​        因为这是一个 polyfill （它需要在源代码之前运行），我们需要让它成为一个 **dependency（上线时的依赖）,而不是一个 devDependency（开发时的依赖）**



https://www.babeljs.cn/docs/

## Babel 是一个 JavaScript 编译器

Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。下面列出的是 Babel 能为你做的事情：

- 语法转换
- 通过 Polyfill 方式在目标环境中添加缺失的特性 (通过 [@babel/polyfill](https://www.babeljs.cn/docs/babel-polyfill) 模块)
- 源码转换 (codemods)

```js
// Babel 输入： ES2015 箭头函数
[1, 2, 3].map((n) => n + 1);

// Babel 输出： ES5 语法实现的同等功能
[1, 2, 3].map(function(n) {
  return n + 1;
});
```

> 有关编译器的精彩教程，请查看 [the-super-tiny-compiler](https://github.com/thejameskyle/the-super-tiny-compiler) 项目，它还高屋建瓴地解释了 Babel 的工作方式。