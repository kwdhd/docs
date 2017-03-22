# CSS笔记
---
## 1.CSS 基础

### 基本语法
CSS 语法由三部分构成：选择器、属性和值：
```css
selector {property: value}
```

### 筛选器分组
你可以对选择器进行分组，这样，被分组的选择器就可以分享相同的声明。用逗号将需要分组的选择器分开。
```css
h1,h2,h2,h3,h5,h6 {
color: green
}
```

### 派生选择器
只有 `<li><strong></strong></li>` 中的内容受影响。
```css
li strong {
	font-style: italic;
	font-weight: normal;
	}
}
```

###id 选择器
id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式，使用了id选择器也可以继续使用派生选择器。
```css
#red {color:red;}
#green {color:green;}

#sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}
```


### 类选择器
在 CSS 中，类选择器以一个点号显示，指定class为center的样式。
```css
.center {text-align: center}
```
和 id 一样，class 也可被用作派生选择器：
```css
.fancy td {
	color: #f60;
	background: #666;
	}
```
元素也可以基于它们的类而被选择：
```css
td.fancy {
	color: #f60;
	background: #666;
	}
```

### 插入样式表
```css
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

---
## 2.CSS 高级

### CSS 伪类 (Pseudo-classes)
CSS 伪类用于向某些选择器添加特殊的效果。
语法：
```css
selector:pseudo-class {property: value}
```
**伪类**

| 伪类 | 作用 |
|:----:|:----|
|:active |将样式添加到被激活的元素| 
|:focus| 将样式添加到被选中的元素 |
|:hover |当鼠标悬浮在元素上方时，向元素添加样式|
|:link |将特殊的样式添加到未被访问过的链接 |
|:visited |将特殊的样式添加到被访问过的链接 |
|:first-child |将特殊的样式添加到元素的第一个子元素| 
|:lang |允许创作者来定义指定的元素中使用的语言   |


### CSS 伪元素 (Pseudo-elements)
语法：
```
选择器 : 伪元素 { 属性: 值 }
```
CSS 类也可以与伪元素配合使用：
```
选择器 . 类: 伪元素 { 属性: 值 }
```

**伪元素**

|伪元素 |作用 | 
|:---:|:---:|
|:first-letter |将特殊的样式添加到文本的首字母 |
|:first-line |将特殊的样式添加到文本的首行 |
|:before |在某元素之前插入某些内容   |
|:after |在某元素之后插入某些内容  |
