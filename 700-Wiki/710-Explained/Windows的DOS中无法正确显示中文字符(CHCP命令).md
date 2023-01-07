在中文Windows系统中，如果一个文本文件是UTF-8编码的，那么在CMD.exe命令行窗口（所谓的DOS窗口）中不能正确显示文件中的内容。

**问题：windows的DOS中无法正确显示中文字符**
![image.png](_assets/Windows的DOS中无法正确显示中文字符(CHCP命令)/1623659956595-c8f36c58-4fc0-4708-bc20-746a36a042b1.png)
解决方法：
chcp 65001 就是换成UTF-8代码页
chcp 936 可以换回默认的GBK （中文）
chcp 437 是美国英语
结果：
![image.png](_assets/Windows的DOS中无法正确显示中文字符(CHCP命令)/1623660049842-b47a024c-da01-47d7-ba3a-ce28b2069fa2.png)
