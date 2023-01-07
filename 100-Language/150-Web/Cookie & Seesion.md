> Web Knowledge: 会话管理

## Cookie & Session 概述
HTTP是无状态的，默认情况下，web服务器是无法区分一个http请求是否为第一次访问
Cookie和Session的作用都是为了保持访问用户与后端服务器的交互状态。
![image.png](_assets/Cookie%20&%20Seesion/1637565097012-4c1af18d-e5ea-44a1-b1ba-33fab3f7cbb4.png)
> [图片来源](https://mt5718214.medium.com/cookie-%E5%92%8C-session-%E7%A9%B6%E7%AB%9F%E6%98%AF%E4%BB%80%E9%BA%BC-%E4%BB%A5%E5%8F%8A%E5%A6%82%E4%BD%95%E5%9C%A8express%E4%B8%AD%E5%AF%A6%E4%BD%9C-9697934ca24f)

## 保持状态的技术
### URL重写（了解）
将一个或多个token添加到url的字符查询字符串中，每个token以key=value形式传递
`url?key1=value1&key2=value2...keyn=valuen`
局限性

- url字符长度限制
- 传递值困难
- 信息时可见的，不安全
### 隐藏域 hidden （了解）
不放在url，而是用html表单隐藏，但是局限性依旧有，不适合跨多个界面
`<input type='hidden' name='id' value='1'/>`
### Cookie 技术
Cookie是一个较少的信息片段，可在浏览器和web服务器交互使用，因此能存储在多个页面之间传递的信息
Cookie作为Http协议 header的一部分，自然支持http协议，受该协议的控制
Cookie中重要的类和对象 **javax.servlet.http.Cookie**类以及**HttpServletRequest**和**HttpServletResponse**接口
```java
public class Cookie implements Cloneable, Serializable {....}
```
**Cookie属性**

| 属性项 | 属性介绍 |
| --- | --- |
| NAME=VALUE | 键值对，可以设置要保存的key/value，name不能和其他属性项的名字一样 |
| version | Cookie的版本信息，目前有0和1，默认是0 |
| expires | 过期时间，在设置的某个时间点后该Cookie就会失效。如expires=Wednesday, 11-Nov-21 23:00:00 GMT |
| Max-Age | 最大失效时间，设置多少秒后失效 |
| domain | 生成该Cookie的域名。如domain="123.com" |
| path | 该cookie是在当前哪个路径下生成的，如path=/wp-admin/ |
| secure | 如果设置了该属性，那么只会在SSH连接时才会回传该Cookie |
| comment | 注释。说明该cookie用途 |
| commentURL | 服务器为此Cookie提供注释 |
| discard | 会话结束是否丢弃该cookie，默认是false |
| port | 该cookie在什么端口下可以回传服务器，如port="8080,8081,8082" |

**Cookie的示例**
```java
// 创建cookie对象
Cookie cookie = new Cookie("name","sean");

//cookie可以添加超时属性等
cookie.setMaxAge(0);

// 添加cookie到请求中, 浏览器请求时一同带出
httpServletRequest.addCookie(cookie);

// 服务端读取请求中的cookie
Cookie[] cookies = request.getCookies();

// 遍历cookies数组，获取到自己要的cookie
for(Cookie cookie: cookies){
    if(cookie.getName().equals("name")){
    	....
    }
}
```
**Cookie的限制**
Cookie最终还是存储在浏览器中，所以不同浏览器对于Cookie的大小和数量有限制
### Session 技术
**Session概述**
Cookie可以让服务端程序跟踪每个客户端的访问，但是每次客户端的访问都必须回传这些cookie，如果这些cookie很多，则会增加传输的数据量，于是可以用session
同一个客户端每次和服务端交互式，不需要每次都传回所有的cookie值，只需要传回一个ID，这个ID是客户端第一次访问服务端时生成的，而且每个客户端是唯一的。客户端只需要回传这个ID即可，ID通常是NAME为
JSESSIONID的一个Cookie

**Seesion创建**
HttpSession对象在用户第一次访问时自动被创建，可以通过HttpServletRequest的getSession方法获取该对象
```java
public interface HttpSession {...}
```
HttpSession getSession( )
**设置和获取session属性**
void setAtrribute(String name, Object value)
getAttribute(String name)
```java
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setCharacterEncoding("UTF-8");
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        request.setCharacterEncoding("UTF-8");
        request.getRequestDispatcher("link.html").include(request, response);

        String username = request.getParameter("username");
        String password = request.getParameter("password");

        if (username.equals("admin") && password.equals("admin123")) {
            out.print("Welcome, " + username);
            HttpSession session = request.getSession(); // 获取会话
            session.setAttribute("username", username);
            session.setAttribute("nickname", "苏小牛");
            session.setAttribute("age", "21");
        } else { 
            request.getRequestDispatcher("login.html").include(request, response);
        }
        out.close();
    }
}
```
## Cookie和Session的区别

- Session是将数据保存在服务器上；而Cookie是将数据以文本的形式保存在客户端浏览器上，由浏览器进行管理的维护
- Session对象可以存放多个name和多个Object；而一个cookie只能放一个name和一个value

