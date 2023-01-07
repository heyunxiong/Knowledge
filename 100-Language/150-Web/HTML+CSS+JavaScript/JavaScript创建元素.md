# JavaScript创建元素
> 为了自定义博客园导航栏的菜单
> from：[https://www.cnblogs.com/seanho/p/15386800.html](https://www.cnblogs.com/seanho/p/15386800.html)

# 使用js创建元素节点
```javascript
//创建<a>元素，并添加id，class，href的属性
var element_a = document.createElement("a");
var element_a_id = document.createAttribute("id");          element_a_id.value="about_me";
var element_a_class = document.createAttribute("class");    element_a_class.value="menu";
var element_a_href = document.createAttribute("href");      element_a_href.value="http://heyunxiong.com";

element_a.setAttributeNode(element_a_id);
element_a.setAttributeNode(element_a_class);
element_a.setAttributeNode(element_a_href);
// <a>显示的文本
element_a.innerHTML = "About Me";	

// 创建<li> 列表元素，并设置id属性
var new_element_li_1 = document.createElement("li");
var new_element_li_1_id = document.createAttribute("id");     new_element_li_1_id.value="add_nav_li";
new_element_li_1.setAttributeNode(new_element_li_1_id);
// 然后把刚才创建的<a>元素以子元素的形式添加到<li>中
new_element_li_1.appendChild(element_a);


// 对应的也有删除的方法
//parent_navList.removeChild(blog_nav_sitehome);
```
上述代码的形式效果：
```html
<li id = "add_nav_li">
	<a id="about_me" class="menu" href="http://heyunxiong.com">About Me</a>
</li>
```
# 添加新元素到已有元素上
```javascript
//先设定要创建的元素，然后直接添加

//比如想要新添加的元素如下：（当然，也可以用上面说的方法，使用纯js拼成下面的形式）
<li id = "add_nav_li">
	<a id="about_me" class="menu" href="http://heyunxiong.com">About Me</a>
</li>

// 添加到已有元素ul上, 相当于在无须列表中添加了一个新的项
var new_element_ul = document.getElementById("ul"); //获取到已有元素ul
new_element_ul.appendChild(add_nav_li); // 把li添加到ul里面，
```
# 修改元素属性
```css
//获取元素，修改属性。
// 修改id属性的值
document.getElementById("navList").id="navList_obs";
// 修改css样式，相当于 #blog_nav_sitehome{display：none}
document.getElementById("blog_nav_sitehome").style.display = "none";
```
# 实际使用
针对需求，自定义导航栏上的信息；在博客园的设置进行了一些代码修改。
## 定制CSS代码
```css
/* 隐藏整个导航栏 */
/* #navigator{display:none;} */

/* 隐藏导航栏的菜单栏 */
/* #navList{display: none;} */
/* 隐藏自带的官方顶部导航栏 */
#top_nav{display: none;}

/* 隐藏博文数据显示 */
.blogStats{display: none;}
/* 隐藏单篇博文底部推荐、新闻文章块 */
#under_post_card1{display:none;}
#under_post_card2{display:none;}
#cnblogs_c1{display: none;}
#cnblogs_c2{display: none;}

/* 隐藏广告快 */
#ad_t2{display: none;}

/* 隐藏点赞分享，太丑了 */
#blog_post_info{display: none;}

/* 修改评论框的高度，太高不协调 */
#tbCommentBody{height: 100px;}
#tbCommentBodyPreview{height: auto;}

/* 隐藏指定导航烂的菜单栏特定元素，以便添加自己想要的其他元素 */
a#blog_nav_sitehome{display: none;}
a#blog_nav_myhome{display: none;}
a#blog_nav_newpost{display: none;}
a#blog_nav_contact{display: none;}
a#blog_nav_rss{display: none;}
a#blog_nav_admin{display: none;}

/* 隐藏公告下面的一些粉丝关注信息，完全没必要显示对我来说 */
#profile_block{display: none;}
#p_b_follow{display: none;}
```
## 侧边栏公告
主要是为了放一个头像 ：）
```html
<img id="mypic" src="https://img2020.cnblogs.com/blog/914318/202110/914318-20211006170609278-1378141535.jpg" alt="Yunxiong" loading="lazy">
```
## 页首代码
```javascript
<script type="text/javascript">

//添加一个新的关于我导航节点
var element_a = document.createElement("a");
var element_a_id = document.createAttribute("id");          element_a_id.value="about_me";
var element_a_class = document.createAttribute("class");    element_a_class.value="menu";
var element_a_href = document.createAttribute("href");      element_a_href.value="http://heyunxiong.com";

element_a.setAttributeNode(element_a_id);
element_a.setAttributeNode(element_a_class);
element_a.setAttributeNode(element_a_href);
element_a.innerHTML = "About Me";	

var new_element_li_1 = document.createElement("li");
var new_element_li_1_id = document.createAttribute("id");     new_element_li_1_id.value="add_nav_li";
new_element_li_1.setAttributeNode(new_element_li_1_id);
new_element_li_1.appendChild(element_a);


var element_navList = document.getElementById("navList");
element_navList.appendChild(new_element_li_1);

</script>
```
## 效果图
![](_assets/JavaScript创建元素/914318-20211009171815606-233611510.png)
# 参考资料：

- [JavaScript HTML DOM - 改变CSS](https://www.runoob.com/js/js-htmldom-css.html)
- [通过JS脚本修改文本](https://www.runoob.com/try/try.php?filename=tryjs_change_innerhtml),
- [JavaScript HTML DOM 元素 (节点)](https://www.runoob.com/js/js-htmldom-elements.html)
