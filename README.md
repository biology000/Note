# Note
日常学习笔记
一：自定义注解(@interface)学习
@interface 

   关键字表示本类为注解类，类结构：
            public @interface 自定义注解名 { 自定义注解体 }
    注解体中支持的元素类型：
　　　　1.所有基本数据类型（int,float,boolean,byte,double,char,long,short)

　　　　2.String类型

　　　　3.Class类型

　　　　4.enum类型

　　　　5.Annotation类型

　　　　6.以上所有类型的数组
简单示例：

public @interface SecurityCheck {
 
	boolean open() default false;
 
	SecurityCheckType[] checkTypes();
 
	boolean justLimitFailure() default false;
 
	String rule() default "";
 
 }
 
 定义好注解后即使用，使用示例：
 @SecurityCheck(open = true, justLimitFailure = true, checkTypes = SecurityCheckType.IP)
 
 1.@Target 主要用于规定注解使用的位置
 取值	注解使用范围
METHOD	可用于方法上
TYPE	可用于类或者接口上
ANNOTATION_TYPE	可用于注解类型上（被@interface修饰的类型）
CONSTRUCTOR	可用于构造方法上
FIELD	可用于域上
LOCAL_VARIABLE	可用于局部变量上
PACKAGE	用于记录java文件的package信息
PARAMETER	可用于参数上
例子：@Target({ ElementType.METHOD })   表示该注解用于方法上

2.@Retention 主要功能是定义注解保留时间的长短，可以设置的三个值都出自RetentionPolicy


public enum RetentionPolicy
{
  SOURCE,  CLASS,  RUNTIME;
  
  private RetentionPolicy() {}
}
SOURCE:在源文件中有效（即源文件保留）
　　CLASS:在class文件中有效（即class保留，默认策略）
　　RUNTIME:在运行时有效（即运行时保留，可以通过此级别获取注解信息）

      例子：@Retention(RetentionPolicy.RUNTIME)   也是一般用法

3.@Documented

    仅仅作为一个标记注解，说明该注解类应该被javadoc工具记录(默认情况下是不记录的)，不在代码运行时产生影响。
 二：
 Spring AOP - 使用@Aspect注解
 2 注解说明
2.1 @Aspect

作用是把当前类标识为一个切面供容器读取

2.2 @Before
标识一个前置增强方法，相当于BeforeAdvice的功能，相似功能的还有

2.3 @AfterReturning

后置增强，相当于AfterReturningAdvice，方法正常退出时执行

2.4 @AfterThrowing

异常抛出增强，相当于ThrowsAdvice

2.5 @After

final增强，不管是抛出异常或者正常退出都会执行

2.6 @Around

环绕增强，相当于MethodInterceptor

2.7 @DeclareParents

引介增强，相当于IntroductionInterceptor

3 execution切点函数
 

execution函数用于匹配方法执行的连接点，语法为：

execution(方法修饰符(可选)  返回类型  方法名  参数  异常模式(可选)) 

 

参数部分允许使用通配符：

*  匹配任意字符，但只能匹配一个元素

.. 匹配任意字符，可以匹配任意多个元素，表示类时，必须和*联合使用

+  必须跟在类名后面，如Horseman+，表示类本身和继承或扩展指定类的所有类

 

示例中的* chop(..)解读为：

方法修饰符  无

返回类型      *匹配任意数量字符，表示返回类型不限

方法名          chop表示匹配名称为chop的方法

参数               (..)表示匹配任意数量和类型的输入参数

异常模式       不限
