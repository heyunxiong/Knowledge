谁还不是从菜鸟开始学JS /JSP
Javascript 结构
![](_assets/谁还不是从菜鸟开始学JS%20JSP/image-谁还不是从菜鸟开始学JS%20JSP-20221017-162437131.jpeg)
原生ajax写法: POST请求
![](_assets/谁还不是从菜鸟开始学JS%20JSP/image-谁还不是从菜鸟开始学JS%20JSP-20221017-162457360.jpeg)
原生ajax写法: GET请求
![](_assets/谁还不是从菜鸟开始学JS%20JSP/image-谁还不是从菜鸟开始学JS%20JSP-20221017-162503330.jpeg)
JSP 九大内置对象
![](_assets/谁还不是从菜鸟开始学JS%20JSP/image-谁还不是从菜鸟开始学JS%20JSP-20221017-162514382.jpeg)

## jQuery 库 - 特性

jQuery 是一个 JavaScript 函数库。

jQuery 库包含以下特性：

-   HTML 元素选取
    
-   HTML 元素操作
    
-   CSS 操作
    
-   HTML 事件函数
    
-   JavaScript 特效和动画
    
-   HTML DOM 遍历和修改
    
-   AJAX
    
-   Utilities
    

  

## jQuery 语法

jQuery 语法是为 HTML 元素的选取编制的，可以对元素执行某些操作。

基础语法是：$(selector).action()

-   美元符号定义 jQuery
    
-   选择符（selector）“查询”和“查找” HTML 元素
    
-   jQuery 的 action() 执行对元素的操作
    

### 示例

$(this).hide() - 隐藏当前元素

$("p").hide() - 隐藏所有段落

$(".test").hide() - 隐藏所有 class="test" 的所有元素

$("#test").hide() - 隐藏所有 id="test" 的元素

提示：jQuery 使用的语法是 XPath 与 CSS 选择器语法的组合。在本教程接下来的章节，您将学习到更多有关选择器的语法。


```javascript

如何用jquery获取<input id="test" name="test" type="text"/>中输入的值？

$(" #test ").val()

$(" input[ name='test' ] ").val()

$(" input[ type='text' ] ").val()

$(" input[ type='text' ]").attr("value")
```

```html
问：html中去掉文本框(input type="text")的边框或只显示下边框

去掉文本框：<input   type="text"   name="textfield"   style="border:0px;">

只留下边框：<input type="text" style="BORDER-TOP-STYLE: none; BORDER-RIGHT-STYLE: none; BORDER-LEFT-STYLE: none; BORDER-BOTTOM-STYLE: solid">
```


