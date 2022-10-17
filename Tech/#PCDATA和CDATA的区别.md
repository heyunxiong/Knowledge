# \#PCDATA和CDATA的区别
https://blog.csdn.net/czh500/article/details/79822920

1）在DTD中，指定标签中某个属性的类型为字符型时，使用CDATA。因为XML解析器会去分析这段字符内容，因而里面如果需要使用>, <, &, ', "这5个特殊字符，应当用对应的替代替代字符来表示(必须以&开始，以;结束)。具体如下：
< - <   (less than)
> - > (greater than)
& - &  (ampersand)
' - '  (apostrophe)
" - "  (straight double quotation mark)

例如在DTD中声明：
  <!ATTLIST author period CDATA> 它表示在author这个标签中，period属性应该是字符类型。


2) 在XML中，指定某段内容不必被XML解析器解析时，使用<![CDATA[...]]>。也就是说中括号中的内容解析器不会去分析。所以其中可以包含>, <, &, ', "这5个特殊字符。经常把一段程序代码嵌入到<![DATA[...]]>中。 因为代码中可能包含大量的 >, <, &, "这样的特殊字符。

例如在XML中声明：
 <![CDATA[
  if(i<10){
  System.out.println("i<10");
  }
  ]]>

3) 在DTD中，指定某个标签中的内容是字符数据时，使用(#PCDATA)。由于它的内容也是需要解析器来解析的，所有仍然需要转换>, <, &, ', "这5个特殊字符。

例如在DTD中声明：
 <!ELEMENT name (#PCDATA)> 它表示在<name>和</name>标签之间可以插入字符或者子标签。