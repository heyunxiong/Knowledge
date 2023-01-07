> Java 基础知识： 网络、套接字
> 网络详细文章：[计算机网络 - Yunxiong's语雀](https://www.yuque.com/heyunxiong/knowledge/01a4db22bf199424402453b4ea58f70e)

所谓网络，简单来说，也不过是一台机器/应用发起请求服务，另一台机器/应用提供对应请求的服务。
![](_assets/Java%20网络/1636722828871-8110e75e-89ff-405d-9437-6cddb607b659.jpeg)

## Java Socket编程
基于TCP编程，在Java中一般指基于Socket编程，即套接字
java.net 包内有相关网络的api信息
客户端 Socket
服务端 ServerSocket
通信要求：IP地址 + 端口号
### ServerSocket 类
ServerSocket类用于在服务器上开一个端口，被动地等待数据（使用 accept() 方法）并建立连接进行数据交互
`ServerSocket serverSocket = **new **ServerSocket(8888);`
accept方法是阻塞方法, 监听并接收到此套接字的连接。

| 方法 | 描述 |
| --- | --- |
| Socket accept( ) | 监听并接收到此套接字的连接 |
| void bind(SocketAddress endpoint) | 将 ServerSocket 绑定到指定地址（IP 地址和端口号） |
| void close( ) | 关闭此套接字 |
| InetAddress getInetAddress( ) | 返回此服务器套接字的本地地址 |
| int getLocalPort( ) | 返回此套接字监听的端口 |
| SocketAddress getLocalSoclcetAddress( ) | 返回此套接字绑定的端口的地址，如果尚未绑定则返回 null |
| int getReceiveBufferSize( ) | 获取此 ServerSocket 的 SO_RCVBUF 选项的值，该值是从 ServerSocket 接收的套接字的建议缓冲区大小 |

### Socket类
Socket 类表示通信双方中的客户端，用于呼叫远端机器上的一个端口，主动向服务器端发送数据
`Socket socket = new Socket(serverIP,port); //建立连接`

| 方法 | 描述 |
| --- | --- |
| void bind(SocketAddress bindpoint) | 将套接字绑定到本地地址 |
| void close( ) | 关闭此套接字 |
| void connect(SocketAddress endpoint) | 将此套接字连接到服务器 |
| InetAddress getInetAddress( ) | 返回套接字的连接地址 |
| InetAddress getLocalAddress( ) | 获取套接字绑定的本地地址 |
| InputStream getInputStream( ) | 返回此套接字的输入流 |
| OutputStream getOutputStream( ) | 返回此套接字的输出流 |
| SocketAddress getLocalSocketAddress( ) | 返回此套接字绑定的端点地址，如果尚未绑定则返回 null |

### 简单的请求
除此之外还有其他的场景：多个客户端响应、上传文件到服务器等 [参考链接：使用场景案例](https://blog.csdn.net/u011035397/article/details/105151928)
```java
public class Server {
    public static void main(String[] args) throws Exception {

        ServerSocket serverSocket = new ServerSocket(8866);
        System.out.println("服务端已启动，等待请求中");
        Socket server = serverSocket.accept();

        InputStream inputStream = server.getInputStream();
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"));
        System.out.println("收到来自客户端的信息：" + bufferedReader.readLine());

//        OutputStream outputStream = server.getOutputStream();
//        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream, "UTF-8"));
//        bufferedWriter.write("服务端响应");
//        bufferedWriter.close();
//        outputStream.close();

        bufferedReader.close();
        inputStream.close();

        server.close();
        serverSocket.close();
    }
}

```
```java
public class Client {
    public static void main(String[] args) throws Exception{
        Socket client = new Socket("127.0.0.1",8866);
        OutputStream outputStream = client.getOutputStream();
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream, "UTF-8"));
        bufferedWriter.write("你好！我是client！");

//        InputStream inputStream = client.getInputStream();
//        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"));
//        System.out.println("收到来自服务端的信息："+bufferedReader.readLine());
//        bufferedReader.close();
//        inputStream.close();
        
        bufferedWriter.close();
        outputStream.close();
        client.close();
    }
}

//结果
服务端已启动，等待请求中
收到来自客户端的信息：你好！我是client！

Process finished with exit code 0
```
## InetAddress类
该类表示互联网协议IP地址对象，封装了与该IP地址相关信息，并提供获取信息的方法
```java
public class InetAddress extends Object implements Serializable

// 子类 
Inet4Address 对应IPv4
Inet6Address 对应IPv6
```
| 方法 | 描述 |
| --- | --- |
| byte[ ] getAddress( ) | 返回此 InetAddress对象的原始IP地址。  |
| static InetAddress [ ] getAllByName(String host) | 给定主机的名称，根据系统上配置的名称服务返回其IP地址数组。  |
| static InetAddress  getByAddress(byte[ ] addr) | 给出原始IP地址的 InetAddress对象。  |
| static InetAddress getByAddress(String  host, byte[ ] addr) | 根据提供的主机名和IP地址创建InetAddress。  |
| static InetAddress getByName (String  host) | 确定主机名称的IP地址。  |
| String getCanonicalHostName( ) | 获取此IP地址的完全限定域名。  |
| String getHostAddress( ) | 返回文本显示中的IP地址字符串。  |
| String getHostName( ) | 获取此IP地址的主机名。  |
| static InetAddress getLocalHost ( ) | 返回本地主机的地址。  |

```java
public class InetAddressTest {
    public static void main(String[] args) throws Exception {
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost.getHostAddress());
        System.out.println(localHost.getHostName());
    }
}
```
## URL 类
Class URL表示统一资源定位符，指向万维网上的“资源”的指针。资源可以像文件或目录一样简单，或者可以是对更复杂的对象的引用，例如对数据库或搜索引擎的查询。
URL的组成
https://www.heyunxiong.com/index.html?language=cn#java
URL 解析：

- 协议为(protocol)：https
- 主机为(host:port)：www.heyunxiong.com
- 端口号为(port): 80 ，以上URL实例并未指定端口，因为 HTTP 协议默认的端口号为 80。
- 文件路径为(path)：/index.html
- 请求参数(query)：language=cn
- 定位位置(fragment)：java，定位到网页中 id 属性为 java的 HTML 元素位置 。
| URL构造方法 | 描述 |
| --- | --- |
| public URL(String protocol, String host, int port, String file)  | 通过给定的参数(协议、主机名、端口号、文件名)创建URL。 |
| public URL(String protocol, String host, String file)  | 使用指定的协议、主机名、文件名创建URL，端口使用协议的默认端口。 |
| public URL(String url)  | 通过给定的URL字符串创建URL |
| public URL(URL context, String url)  | 使用基地址和相对URL创建 |

常用方法：

| 方法 | 描述 |
| --- | --- |
| public String getPath( ) | 返回URL路径部分 |
| public String getQuery( ) | 返回URL查询部分 |
| public String getAuthority( ) | 获取此 URL 的授权部分 |
| public int getPort( ) | 返回URL端口部分 |
| public int getDefaultPort( ) | 返回协议的默认端口号 |
| public String getProtocol( ) | 返回URL的协议 |
| public String getHost( ) | 返回URL的主机 |
| public String getFile( ) | 返回URL文件名部分 |
| public String getRef( ) | 获取此 URL 的锚点（也称为"引用"） |
| public URLConnection openConnection() throws IOException | 打开一个URL连接，并运行客户端访问资源 |

```java
public class URLTest {
    public static void main(String[] args) throws Exception{
        URL url = new URL("https://www.heyunxiong.com/index.html?language=cn#java");
        System.out.println("URL 为：" + url.toString());
        System.out.println("协议为：" + url.getProtocol());
        System.out.println("验证信息：" + url.getAuthority());
        System.out.println("文件名及请求参数：" + url.getFile());
        System.out.println("主机名：" + url.getHost());
        System.out.println("路径：" + url.getPath());
        System.out.println("端口：" + url.getPort());
        System.out.println("默认端口：" + url.getDefaultPort());
        System.out.println("请求参数：" + url.getQuery());
        System.out.println("定位位置：" + url.getRef());
    }
}
```
