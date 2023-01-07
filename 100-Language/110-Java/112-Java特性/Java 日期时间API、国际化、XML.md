> Java 基础知识： jdk1.8新的时间api使用、国际化概念、xml基本使用处理

## jdk1.8引入的日期时间API
jdk1.8新引入关于日期和时间处理api。java.time.*
而以前关于日期时间处理的api在 java.util.*  [待添加：java日期api的使用](#)
**新引入主要的一些类：**

- Instant：时间戳 
- Duration：持续时间，时间差 
- LocalDate：只包含日期，比如：2016-10-20 
- LocalTime：只包含时间，比如：23:12:10 
- LocalDateTime：包含日期和时间，比如：2016-10-20 23:14:21 
- Period：时间段 
- ZoneOffset：时区偏移量，比如：+8:00 
- ZonedDateTime：带时区的时间 
- Clock：时钟，比如获取目前美国纽约的时间
### Instant、Duration 类
时间线的原点被设置为穿过伦敦格林威治皇家天文台的本初子午线所处时区1970年1月1日的零点

- Instant.now( )				可以获得当前时刻
- Duration.between(start,end)  计算时间差
```java
public static void main(String[] args) throws  Exception{
        Instant start = Instant.now();
        System.out.println(start);
        Thread.sleep(5000);
        Instant end = Instant.now();
        System.out.println(end);
        System.out.println("=====时间差=====");
        System.out.println(Duration.between(start, end));
    }
```
### 本地日期 LocalDate
Java中有两种时间，本地日期/时间 和 时区日期/时间
本地日期/时间包含日期和当天的时间，但是没有时区相关的信息
本地日期/时间：1999/12/12 14:03:12
时区日期/时间：1969/07/16 09:32:00 EDT
LocalDate是带有年月日的日期，
创建LocalDate对象：now或者of静态方法
```java
LocalDate.now();
LocalDate.of(1993,1,1);

LocalDate localDate = LocalDate.of(2017, 1, 4);     // 初始化一个日期：2017-01-04
int year = localDate.getYear();                     // 年份：2017
Month month = localDate.getMonth();                 // 月份：JANUARY
int dayOfMonth = localDate.getDayOfMonth();         // 月份中的第几天：4
DayOfWeek dayOfWeek = localDate.getDayOfWeek();     // 一周的第几天：WEDNESDAY
int length = localDate.lengthOfMonth();             // 月份的天数：31
boolean leapYear = localDate.isLeapYear();          // 是否为闰年：false
```
### 本地时间 LocalTime
LocalTime表示当日时刻，例如15:40:00；使用now或者of创建对象
```java
LocalTime.now( );
LocalTime.of(15,40);

LocalTime localTime = LocalTime.of(17, 23, 52);     // 初始化一个时间：17:23:52
int hour = localTime.getHour();                     // 时：17
int minute = localTime.getMinute();                 // 分：23
int second = localTime.getSecond();                 // 秒：52
```
### 日期时间 LocalDateTime
是LocalDate和LocalTime的合体
```javascript
LocalDateTime ldt1 = LocalDateTime.of(2017, Month.JANUARY, 4, 17, 23, 52);

LocalDate localDate = LocalDate.of(2017, Month.JANUARY, 4);
LocalTime localTime = LocalTime.of(17, 23, 52);
LocalDateTime ldt2 = localDate.atTime(localTime);
```
### 日期时间的格式化 DateTimeFormatter
使用DateTimeFormatter类
`DateTimeFormatter.ofPattern("yyyy/MM/dd");`
```javascript
public class Main {
    public static void main(String[] args) {
        // 自定义格式化:
        DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm:ss");
        System.out.println(dtf.format(LocalDateTime.now()));

        // 用自定义格式解析:
        LocalDateTime dt2 = LocalDateTime.parse("2019/11/30 15:16:17", dtf);
        System.out.println(dt2);
    }
}

LocalDateTime dateTime = LocalDateTime.now();
String strDate1 = dateTime.format(DateTimeFormatter.BASIC_ISO_DATE);    // 20170105
String strDate2 = dateTime.format(DateTimeFormatter.ISO_LOCAL_DATE);    // 2017-01-05
String strDate3 = dateTime.format(DateTimeFormatter.ISO_LOCAL_TIME);    // 14:20:16.998
String strDate4 = dateTime.format(DateTimeFormatter.ofPattern("yyyy-MM-dd"));   // 2017-01-05
String strDate5 = dateTime.format(DateTimeFormatter.ofPattern("今天是：YYYY年 MMMM DD日 E", Locale.CHINESE)); // 今天是：2017年 一月 05日 星期四
```
### 时区 ZoneId
```javascript
ZoneId shanghaiZoneId = ZoneId.of("Asia/Shanghai");
ZoneId systemZoneId = ZoneId.systemDefault();
```
### 时区时间 ZonedDateTime
创建ZoneDateTime对象：
ZonedDateTime对象由两部分构成，LocalDateTime和ZoneId，
其中2017-01-05T15:26:56.147部分为LocalDateTime，+08:00[Asia/Shanghai]部分为ZoneId
```java
ZonedDateTime.of(1969,7,16,32,0,0);

LocalDateTime localDateTime = LocalDateTime.now();
ZonedDateTime zonedDateTime = ZonedDateTime.of(localDateTime, shanghaiZoneId);

```
日期处理 参考资料：

- [https://www.cnblogs.com/huanshilang/p/12013386.html](https://www.cnblogs.com/huanshilang/p/12013386.html)
- [https://lw900925.github.io/java/java8-newtime-api.html](https://lw900925.github.io/java/java8-newtime-api.html)
- [https://www.liaoxuefeng.com/wiki/1252599548343744/1303871087444002](https://www.liaoxuefeng.com/wiki/1252599548343744/1303871087444002)
- [https://www.jianshu.com/p/51ccbe1d34b0](https://www.jianshu.com/p/51ccbe1d34b0)
## 国际化 i18n
### Locale
Locale对象代表具体的地理，政治或文化地区。 
```java
java.lang.Object 
	-->java.util.Locale 

public final class Locale extends Object implements Cloneable, Serializable
```
一个需要的操作Locale执行任务被称为语言环境敏感和使用Locale定制信息的用户。
例如，显示一个数字是一个区域设置敏感的操作 - 该数字应该根据用户的本地国家，地区或文化的习惯和惯例进行格式化
### ResourceBundle 
包含本地化的文本或对象。
```javascript
public abstract class ResourceBundle extends Object
```
国际化资源文件的命名规范规定资源名称采用以下的方式进行命名：
<资源名>_<语言代码>_<国家/地区代码>.properties

国际化 参考资料：

- [https://cloud.tencent.com/developer/article/1633910](https://cloud.tencent.com/developer/article/1633910)
- [https://www.yiibai.com/java_i18n/java_i18n_locale_details.html#article-start](https://www.yiibai.com/java_i18n/java_i18n_locale_details.html#article-start)
- [https://www.javatpoint.com/internationalization-in-java](https://www.javatpoint.com/internationalization-in-java)
- [https://docs.oracle.com/javase/8/docs/technotes/guides/intl/index.html](https://docs.oracle.com/javase/8/docs/technotes/guides/intl/index.html)
## XML处理
四种方法：

- DOM
- SAX
- JDOM
- DOM4J

XML处理 参考资料：

- [http://www.51gjie.com/java/80](http://www.51gjie.com/java/80)
- [https://bbs.huaweicloud.com/blogs/detail/232737](https://bbs.huaweicloud.com/blogs/detail/232737)
- [https://www.cnblogs.com/JavaArchitect/p/12243296.html](https://www.cnblogs.com/JavaArchitect/p/12243296.html)
- [https://segmentfault.com/a/1190000016114761](https://segmentfault.com/a/1190000016114761)
