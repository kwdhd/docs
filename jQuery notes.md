# jQuery 笔记
---

## 1.选择器

### $
1.  根据元素ID
```javascript
$("#element id");
```
2. 根据元素class
```javascript
$(".myClass");
```
3. 根据标签
```
$("div");
```

4. 匹配所有元素
```
$("*")
```

5. 后代
````
$("form input")
```
6. 第一个后代
```
$("form > input")
```
7. 匹配所有紧接在 prev 元素后的 next 元素，只有紧接着的
```
$("label + input")
```
8. 匹配 prev 元素之后的所有 siblings 元素
```
$("form ~ input")
```
9. 获取第一个元素，获取最后个元素
```
$('li:first');
$('li:last')
```


## 2.属性

### attr(name|properties|key,value|fn)
设置或返回被选元素的属性值。

```
$("img").attr({ src: "test.jpg", alt: "Test Image" });
```

### removeAttr(name)
删除属性
```
$("img").removeAttr("src");
```
### toggleClass(class|fn[,sw])
如果存在（不存在）就删除（添加）一个类。
```
 var count = 0;
  $("p").click(function(){
      $(this).toggleClass("highlight", count++ % 3 == 0);
  });
```

### addClass(class|fn)
为每个匹配的元素添加指定的类名。

```
$("p").addClass("selected");

```

## html([val|fn])
用于设定HTML内容的值 or 此函数返回一个HTML字符串。
```
$("p").html("Hello <b>world</b>!");
```


##  text([val|fn])
用于设置元素内容的文本
```
$("p").text(function(i,e){
    console.log( "这个 p 元素的 index 是：" + i + '内容是：' + e);
    });
```

### val([val|fn|arr])
```
$('input:text.items').val(function() {
  return this.value + ' ' + this.className;
});
```
## 筛选

### eq 获取第index个元素
```
# 倒序从下标从1开始算，取倒数第二个p元素
$("p").eq(-2)
# 正序从0开始排
$("p").eq(1)
```

### first、last 
获取第一个、最后一个元素


### filter(expr|obj|ele|fn)
筛选出与指定表达式匹配的元素集合。

```
$('div').filter(
    function(i,v){
        return  v.innerText.match('记录');
    })
```

###   is(expr|obj|ele|fn)
根据选择器、DOM元素或 jQuery 对象来检测匹配元素集合，如果其中至少有一个元素符合这个给定的表达式就返回true。

如果没有元素符合，或者表达式无效，都返回'false'。 '''注意：'''在jQuery 1.3中才对所有表达式提供了支持。在先前版本中，如果提供了复杂的表达式，比如层级选择器（比如 + , ~ 和 > ），始终会返回true

### map
将一组元素转换成其他数组（不论是否是元素数组）
```
$("p").append( $("input").map(function(){
  return $(this).val();
}).get().join(", ") );
```


### has
保留包含特定后代的元素，去掉那些不含有指定后代的元素。
.has()方法将会从给定的jQuery对象中重新创建一组匹配的对象。提供的选择器会一一测试原先那些对象的后代，含有匹配后代的对象将得以保留。

```
$('li').has('ul').css('background-color', 'red');
```

### not
删除与指定表达式匹配的元素

### slice
选取一个匹配的子集


## CSS

### offset
获取匹配元素在当前视口的相对偏移。
返回的对象包含两个整型属性：top 和 left。此方法只对可见元素有效。
```
$("p:last").offset({ top: 10, left: 30 });
```


## 事件
在选择元素上绑定一个或多个事件的事件处理函数。


### on
在选择元素上绑定一个或多个事件的事件处理函数。

```
$('#header').on('click',function(){console.log('one');});
$('#header').on('click',function(){console.log('two');});
$('#header').on('click',function(){console.log('three');});
```

### hover
一个模仿悬停事件（鼠标移动到一个对象上面及移出这个对象）的方法。这是一个自定义的方法，它为频繁使用的任务提供了一种“保持在其中”的状态。
```
$("td").hover(
  function () {
    $(this).addClass("hover");
  },
  function () {
    $(this).removeClass("hover");
  }
);
```

###  toggle
用于绑定两个或多个事件处理器函数，以响应被选元素的轮流的 click 事件。
如果元素是可见的，切换为隐藏的；如果元素是隐藏的，切换为可见的。

```
$("td").toggle(
  function () {
    $(this).addClass("selected");
  },
  function () {
    $(this).removeClass("selected");
  }
);
```

## 动画

### show


<del>删除</del>
<span>span</span>
<cite>cite</cite>
<table>
    <tr>
        <td>td</td><br /><td>td2</td>
    </tr>
</table>

headline
==== 
headline2
---

> 行引用
> 第2行
>> 嵌套行
>
> 啦啦啦



## 工具

### each
each(object, [callback])
```
$.each( { name: "John", lang: "JS" }, function(i, n){
  alert( "Name: " + i + ", Value: " + n );
});
```

### extend
extend([deep], target, object1, [objectN])

```
```