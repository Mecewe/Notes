# sass、scss、和css的关系

说到css，相信大家都知道，css样式是用来修饰网页页面结构的。那么sass、scss又是做什么的呢？接下来我们来一起了解一下。

要了解css、sacc和scss的关系就要从css预处理器开始说起。

什么是css预处理器？css预处理器是用一种专门的语言，进行网页的样式设计，之后在被编译为正常的css文件，以供项目使用。

**使用css预处理语言的好处：**是css更加简洁、方便修改、可读性强、适应新强并且更易于代码的维护。

####**css和sass的关系：**

sass是由buby语言编写的一款css预处理语言，和html一样有严格的缩进风格，和css编写规范有着很大的出入，是不使用花括号和分号的，所以不被广为接受。

####**sass和scss的关系：**

sass和scss其实是一样的css预处理语言，其后缀名是分别为 .sass和.scss两种。

SASS版本3.0之前的后缀名为.sass，而版本3.0之后的后缀名.scss。

两者是有不同的，继sass之后scss的编写规范基本和css一致，sass时代是有严格的缩进规范并且没有‘{}’和‘；’。而scss则和css的规范是一致的。

**示例代码:**

sass

```text
#sidebar
  width: 30%
  background-color: #faa
```

scss

```text
#sidebar {
  width: 30%;
  background-color: #faa;
}
```

SCSS 和 CSS 写法无差别：

SCSS 和 CSS 写法无差别，这也是 Sass 后来越来越受大众喜欢原因之一。简单点说，把你现有的“.css”文件直接修改成“.scss”即可使用。



**SASS是一个具有语法改进的CSS预处理器**。高级语法中的样式表由程序处理，并转换为常规的CSS样式表。但是，它们并没有扩展CSS标准本身。

支持CSS变量，可以使用，但不能使用预处理器变量。

SCSS和SASS之间的区别，SASS文档页面上的此文本应回答以下问题：

> There are two syntaxes available for Sass. The first, known as SCSS (Sassy CSS) and used throughout this reference, is an extension of the syntax of CSS. This means that every valid CSS stylesheet is a valid SCSS file with the same meaning. This syntax is enhanced with the Sass features described below. Files using this syntax have the .scss extension.
>
> The second and older syntax, known as the indented syntax (or sometimes just"Sass"), provides a more concise way of writing CSS. It uses indentation rather than brackets to indicate nesting of selectors, and newlines rather than semicolons to separate properties. Files using this syntax have the .sass extension.

然而，所有这些只适用于SASS预编译器，它最终创建了CSS。它不是CSS标准本身的扩展。



