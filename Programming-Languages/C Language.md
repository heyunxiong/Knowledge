
指针
图-->实现-->涉及到指针-->关系到内存地址（十六进制）

  

指针：一个变量

&hyx        //hyx的内存地址，可以理解成住哪里

int  *hyx         就是一个空的地址，可以理解成空房子，里面住的是别人

  

所有指针的值的实际数据类型，不管是整型、浮点型、字符型，还是其他的数据类型，都是一样的，都是一个代表内存地址的长的十六进制数。

不同数据类型的指针之间唯一的不同是，指针所指向的变量或常量的数据类型不同

  

一个简单的示例：

int var=10;      //定义一个整型变量，这个变量的值是10

int *p ;            //定义一个指针变量，现在这个指针变量还没有值（需要注意的一点就是指针自身也有地址，只是现在不需要关注指针变量的地址）p=&var         //&取地址的符号，该语句表示把var的内存地址存入指针p中,记住，指针的值就是地址

printf("i 存放的内容的值: %d, i 自己所在的地址: %p\n", i, &i);   

printf("p 存放的地址的值: %p; p 自己所在的地址: %p; p 存放的地址所指所存放内容的值: %d", p, &p, *p); 

                     //p输入var的地址值，&p是指针本身的值，*p是存放的地址所指向的数值

  

指针数组 ，数组指针 ，函数指针 ，函数指针数组 ，指向函数指针数组的指针

函数指针，顾名思义，就是一个指向函数的指针。函数指针的目的就是为了实现方法的回调

基本的简单的指针

指针的指针 int **p,

  

int *p1; int **p2;

*p2=&p1; //指针的指针：存放指针的地址。

---

```c
## C语言如何定义结构体

1. struct与typedef struct区别

struct是[结构体](http://wenwen.soso.com/z/Search.e?sp=S%E7%BB%93%E6%9E%84%E4%BD%93&ch=w.search.yjjlink&cid=w.search.yjjlink)的[关键字](http://wenwen.soso.com/z/Search.e?sp=S%E5%85%B3%E9%94%AE%E5%AD%97&ch=w.search.yjjlink&cid=w.search.yjjlink)，用来声明结构体[变量](http://wenwen.soso.com/z/Search.e?sp=S%E5%8F%98%E9%87%8F&ch=w.search.yjjlink&cid=w.search.yjjlink)如

struct  student

{   char  num[10];

     char   name[20];

     int    age;

};

struct student  stu[10]来声明一个结构体[数组](http://wenwen.soso.com/z/Search.e?sp=S%E6%95%B0%E7%BB%84&ch=w.search.yjjlink&cid=w.search.yjjlink)

-------------------------------------------------------------------------------

typedef是用来定义新的类型名来代替已有的类型名，

可将上面的结构体定义为

typedef struct  student

{   char  num[10];

     char   name[20];

     int    age;

}stud;

也就是说，将原来的struct student 重新定义为 stud;

可以直接用  stud stu[10]来声明一个结构体[数组](http://wenwen.soso.com/z/Search.e?sp=S%E6%95%B0%E7%BB%84&ch=w.search.yjjlink&cid=w.search.yjjlink)

2. 结构体的自引用 / 相互引用

 结构体的自引用(self reference)，就是在结构体内部，包含指向自身类型结构体的指针。

 结构体的相互引用（mutual reference），就是说在多个结构体中，都包含指向其他结构体的指针。

1. 自引用 结构体

 (1.1) 不使用typedef时

  struct tag_1{  

      struct tag_1 A;   /* 结构体 */  

      int value;  

  };  

     这种声明是错误的，因为这种声明实际上是一个无限循环，成员b是一个结构体，b的内部还会有成员是结构体，

    依次下去，无线循环。

     在分配内存的时候，由于无限嵌套，也无法确定这个结构体的长度，所以这种方式是非法的。

  正确的方式： （使用指针）：

  struct tag_1{

      struct tag_1 *A;  /* 指针 */

      int value;

  };       

   由于指针的长度是确定的（在32位机器上指针长度为4），所以编译器能够确定该结构体的长度。

 (1.2) 使用typedef 时

  typedef struct {

      int value;

      NODE *link;  /* 虽然也使用指针，但这里的问题是：NODE尚未被定义 */

  } NODE;

  这里的目的是使用typedef为结构体创建一个别名NODEP。

  但是这里是错误的，因为类型名的作用域是从语句的结尾开始，而在结构体内部是不能使用的，因为还没定义。

  正确的方式：有三种，差别不大，使用哪种都可以。

  /*  方法一  */

  typedef struct tag_1{

      int value;

      struct tag_1 *link;  

  } NODE;

  /*  方法二  */

  struct tag_2;

  typedef struct tag_2 NODE;

  struct tag_2{

      int value;

      NODE *link;    

  };

  /*  方法三  */

  struct tag_3{

      int value;

      struct tag *link;  

  };

  typedef struct tag_3 NODE;

2. 相互引用 结构体

 错误的方式：

 typedef struct tag_a{

     int value;

     B *bp;  /* 类型B还没有被定义 */

 } A;

 typedef struct tag_b{

     int value;

     A *ap;

 } B;         错误的原因和上面一样，这里类型B在定义之 前 就被使用。

 正确的方式：（使用“不完全声明”）

/* 方法一   */   

struct tag_a{  

    struct tag_b *bp;  /* 这里struct tag_b 还没有定义，但编译器可以接受 */  

    int value;  

}; 

struct tag_b{  

    struct tag_a *ap;  

    int value;  

}; 

typedef struct tag_a A;  

typedef struct tag_b B;  

/*  方法二   */   

struct tag_a;   /* 使用结构体的不完整声明（incomplete declaration）,此句省略也是对的 */  

struct tag_b;   // 此句省略也是对的

typedef struct tag_a A;   

typedef struct tag_b B;  

struct tag_a{  

    struct tag_b *bp;  /* 这里struct tag_b 还没有定义，但编译器可以接受 */  

    int value;  

};  

struct tag_b{  

    struct tag_a *ap;  

    int value;  

};  

===========================================================

2. 一篇关于结构体声明的有用文档

[原文地址：[http://hi.baidu.com/gubuntu/blog/item/70d8d16079535eda8cb10d8e.html](http://hi.baidu.com/gubuntu/blog/item/70d8d16079535eda8cb10d8e.html)]

C 中使用：

  

struct test

{

    int x, y;

};

就可以定义一个名为test的结构体，但C中很可能编译通不过。

C语言并不支持在struct后使用标示符定义结构体的名字，test将会被忽略，这相当于定义了一个没有名字的结构体。

若定义一个该结构体对象test mt; 将会提示未定义的test错误信息。

所以，在C语言中，一般使用typedef来定义结构体，上面的例子可以改为：

  

typedef struct _test{

    int x, y;

}test;

  

_test要不要都可以。

并且，第一个大括号不能像原来那样随便的换行写（因为是typedef）。

------------------------------------------------------------------------------

#define S(s) printf("%s\n", #s); s

typedef struct _TS1{

    int x, y;

} TS1, *PTS1, ***PPPTS1; // TS1是结构体的名称，PTS1是结构体指针的名称

// 也就是将结构体struct _TS1 命名为TS1,

// 将struct _TS1 * 命名为 PTS1

// 将struct _TS1 *** 命名为 PPPTS1

typedef struct { // struct后面的结构体说明也可以去掉

    int x, y;

} TS2, *PTS2;

typedef PTS1 *PPTS1; // 定义PPTS1是指向PTS1的指针

typedef struct _TTS1{

    typedef struct ITTS1 {

        int x, y;

    } iner;

    iner i;

    int x, y;

} TTS1;

//结构体内部的结构体也一样可以定义

typedef TTS1::ITTS1 ITS1;

void test_struct()

{

    // 基本结构体重定义的使用

    TS1 ts1 = {100, 200};

    PTS1 pts1 = &ts1; // 完全等价于TS1* pts1 = &ts1;

    PPTS1 ppts1 = &pts1; // 完全等价于TS1** ppts1 = &pts1;

    PPPTS1 pppts1 = &ppts1; // 完全等价于 TS1*** pppts1 = &ppts1;

    TS2 ts2 = {99, 88};

    PTS2 pts2 = &ts2;   // 完全等价于 TS2* pts2 = &ts2;

    TTS1 itts1 = {{110, 220}, 10, 20};

    Its1* rits1 = &itts1.i;

    ITS1* &its1 = rits1; // 等价于 TTS1::ITTS1 *its1 = &(itts1.i);

    printf("ts1\t = (%d, %d)\n*pts1\t = (%d, %d)\n"

           "**ppts1\t = (%d, %d)\n***pppts1= (%d, %d)\n\n",

            ts1.x, ts1.y, pts1->x, pts1->y,

            (**ppts1).x, (**ppts1).y, (***pppts1).x, (***pppts1).y);

    printf("ts2\t = (%d, %d)\n*pts2\t = (%d, %d)\n\n",

        ts2.x, ts2.y, pts2->x, pts2->y);

    printf("itts1\t = [(%d, %d), %d, %d]\n*its1\t = (%d, %d)\n\n",

        itts1.i.x, itts1.i.y, itts1.x, itts1.y, its1->x, its1->y);

    S(pts1->x = 119);

    S(pts2->y = 911);

    S(its1->x = 999);

    printf("ts1\t = (%d, %d)\n*pts1\t = (%d, %d)\n"

           "**ppts1\t = (%d, %d)\n***pppts1= (%d, %d)\n\n",

            ts1.x, ts1.y, pts1->x, pts1->y,

            (**ppts1).x, (**ppts1).y, (***pppts1).x, (***pppts1).y);

    printf("ts2\t = (%d, %d)\n*pts2\t = (%d, %d)\n\n",

        ts2.x, ts2.y, pts2->x, pts2->y);

    printf("itts1\t = [(%d, %d), %d, %d]\n*its1\t = (%d, %d)\n\n",

        itts1.i.x, itts1.i.y, itts1.x, itts1.y, its1->x, its1->y);

    S((*ppts1)->y = -9999);

    printf("ts1\t = (%d, %d)\n**ppts1\t = (%d, %d)\n\n",

        ts1.x, ts1.y, (*ppts1)->x, (*ppts1)->y);

    S((**pppts1)->x = -12345);

    S((***pppts1).y = -67890);

    printf("ts1\t = (%d, %d)\n*pts1\t = (%d, %d)\n"

           "**ppts1\t = (%d, %d)\n***pppts1= (%d, %d)\n\n",

            ts1.x, ts1.y, pts1->x, pts1->y,

            (**ppts1).x, (**ppts1).y, (***pppts1).x, (***pppts1).y);

}
```

