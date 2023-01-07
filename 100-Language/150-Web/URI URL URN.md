##### URI，URL，URN
http://www.jianshu.com/writer#/notebooks/20574510/notes/21978567/preview

![](_assets/URI%20URL%20URN/image-URI%20URL%20URN-20221019-132303109.png)


从上面的那幅图可以看出来，一共有三个不同的概念URI,URL,URN。这讨论这样的问题时，最好的方法就是回到原点啊，这里我们在[RFC 3986: Uniform Resource Identifier (URI): Generic Syntax](http://tools.ietf.org/html/rfc3986)里面收集了点资料：

“A Uniform Resource Identifier (URI) 是一个紧凑的字符串用来标示抽象或物理资源。”

“A URI 可以进一步被分为定位符、名字或两者都是. 术语“Uniform Resource Locator” (URL) 是URI的子集, 除了确定一个资源,还提供一种定位该资源的主要访问机制(如其网络“位置”)。“

那我们无所不知的维基百科把这段消化的很好，并描述的更加形象了：

“URI可以分为URL,URN或同时具备locators 和names特性的一个东西。URN作用就好像一个人的名字，URL就像一个人的地址。换句话说：URN确定了东西的身份，URL提供了找到它的方式。”

通过这些描述我们可以得到一些结论：

-   首先，URL是URI的一种（通过那个图就看的出来吧）。所以有人跟你说URL不是URI，他就错了呗。但也不是所有的URI都是URL哦，就好像蝴蝶都会飞，但会飞的可不都是蝴蝶啊，你让苍蝇怎么想！
    
-   让URI能成为URL的当然就是那个“访问机制”，“网络位置”。e.g. http:// or ftp://.。
    
-   URN是唯一标识的一部分，就是一个特殊的名字。
    

下面就来看看例子吧，当来也是来自权威的RFC：

-   [ftp://ftp.is.co.za/rfc/rfc1808.txt](ftp://ftp.is.co.za/rfc/rfc1808.txt) (also a URL because of the protocol)
    
-   [http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt) (also a URL because of the protocol)
    
-   ldap://[2001:db8::7]/c=GB?objectClass?one (also a URL because of the protocol)
    
-   mailto:[John.Doe@example.com](mailto:John.Doe@example.com) (also a URL because of the protocol)
    
-   news:comp.infosystems.[www.servers.unix](http://www.servers.unix/) (also a URL because of the protocol)
    
-   tel:+1-816-555-1212
    
-   telnet://192.0.2.16:80/ (also a URL because of the protocol)
    
-   urn:oasis:names:specification:docbook:dtd:xml:4.1.2
    

这些全都是URI, 其中有些事URL. 哪些? 就是那些提供了访问机制的.

##### 总结

下面到了回答问题的时候了：

当我们替代web地址的时候，URI和URL那个更准确？

基于我读的很多的文章，包括RFC，我想说URI更准确。

别急，我有我的理由：

我们经常使用的URI不是严格技术意义上的URL。例如：你需要的文件在[files.hp.com](http://files.hp.com/). 这是URI，但不是URL--系统可能会对很多协议和端口都做出正

确的反应。

你去[http://files.hp.com](http://files.hp.com/) 和[[ftp://files.hp.com](ftp://files.hp.com/)]([ftp://files.hp.com/](ftp://files.hp.com/)).可能得到完全不同的内容。这种情况可能更加普遍，想想不同谷歌域名上的不同服务啊。

所以，用URI吧，这样你通常技术上是正确的，URL可不一定。最后“URL”这个术语正在被弃用。所以明智吧少年！

##### 结语

If you don’t mind being “that guy”, URI is probably the more accurate term to use. But if you are in the linguist / “use what’s understood” camp, feel free to go with URL.

参考：

[https://en.wikipedia.org/wiki/Uniform_Resource_Identifier](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)

[https://danielmiessler.com/study/url_vs_uri/](https://danielmiessler.com/study/url_vs_uri/ "https://danielmiessler.com/study/url_vs_uri/")

首先，URI，是uniform resource identifier，统一资源标识符，用来唯一的标识一个资源。而URL是uniform resource locator，统一资源定位器，它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。而URN，uniform resource name，统一资源命名，是通过名字来标识资源，比如[mailto:java-net@java.sun.com](mailto:java-net@java.sun.com)。也就是说，URI是以一种抽象的，高层次概念定义统一资源标识，而URL和URN则是具体的资源标识的方式。URL和URN都是一种URI。

在Java的URI中，一个URI实例可以代表绝对的，也可以是相对的，只要它符合URI的语法规则。而URL类则不仅符合语义，还包含了定位该资源的信息，因此它不能是相对的，schema必须被指定。