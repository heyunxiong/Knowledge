# Java 函数式接口 lambda表达式  函数式接口的demo
lambda表达式  函数式接口的demo


1.创建函数式接口

@FunctionalInterface //这个接口可以探测接口的方法数量，因为函数式接口的是抽象方法只允许有一个，如果加了这个注释，发现有多个函数的话就会编译报错

public interface MyFunctionalInterface <T>{

    public T getValue(T t );

}



2.创建一个函数，把函数式接口作为参数

public Integer  operate(Integer num, MyFunctionalInterface mfi){

    return mfi.getValue(num);

}

  

3.用lambda表达式实现函数式接口

public void myLambda(){

    // 调用使用函数式接口作为参数的方法  operate( )

Integer i = operate(100, x -> x * 2);

}