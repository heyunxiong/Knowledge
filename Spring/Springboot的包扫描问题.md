Springboot的包扫描问题
由于SpringBoot默认包扫描机制是：从启动类所在包开始，扫描当前包及其子包下的所有文件。

![](_assets/Springboot的包扫描问题/image-Springboot的包扫描问题-20221017-143559868.png)

启动类RuoYiApplication当前是在web包下，那么默认情况下，会扫描web下的类和子包（controller、core）