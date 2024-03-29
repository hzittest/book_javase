# day08笔记_封装

## 一、回顾

``` xml
1.封装与隐藏
	封装：隐藏内部实现细节，对对外提供统一访问的接口;
	具体表现:
		a.就属性进行私有化,提供get/set方法进行访问;
		b.具体的方法(函数)进行封装。封装一个 计算工资的方法。

2.访问修饰符
	private:私有的  本类
	default(无修饰符):默认的 本类  本包
 	protected:受保护的 本类  本包  子类
	public:公共的 本项目中任何的地方

3.get/set方法
	看成普通方法,作用:get 用来提供数据   set:用来设置数据
	方法名规范:  get属性名()   getName();
			    set属性名()   setName();

		public String getName(){
			return name;
		}
	
		public void setName(String name){
			this.name = name;
		}


4.构造方法
	a.特点
		i:方法的名称和类名一致;
		ii:放方法没有返回值，也不需要使用void修饰。如果使用void变成了普通方法
	b.作用
		创建对象，并且对对象进行初始化操作(给属性赋值)
	c.注意
		a.每个类都至少一个构造方法;
		b.默认都是有一个无参的构造方法;
		c.如果定义有其他有参的构造方法，那么无参的构造就会自动消失。如果需要自己显示定义
		d.构造方法也可以重载。
	d.构造方法的调用
		是使用 new + 构造方法([参数]);
		无法使用 obj.构造方法(不支持)
	
		public Person(){

		}

		public Person(String name){

		}


5.方法的重载
	同名不同参的方法，称为方法的重载;
	
	语法:
		a.参数的顺序、个数、类型至少有一个不一样;
		b.返回值可以相同，也可以不同
	多个方法如何调用:
		a.通过传递的实参类型，顺序，及个数来决定调用哪一个方法。如果都不符合,语法会报错;
	
	可变参数: 定义方法的时候，在形参列表中 使用 ... 
			可变参数 必须放在形参列表的最后一个参数位

6.package和import
	package:创建包  可以使用 . 进行目录的分层;
	import:导入其他包中需要使用的类
```



## 二、继承

``` xml
1.基本概念
	子类自动享有父类中所有非私有的属性和方法。子类可以对父类进行扩充。
2.继承的优点
	a.提高代码的可重用性及扩展性;
	b.设计应用程序变得更加简单;
	c.可以轻松的自定义子类;公共的属性和方法交给父类统一处理;
3.继承的语法
	a.关键字  : extends
	b.语法结构  [修饰符] class 类名 [extends 父类]{} 
```

``` java
//定义父类：将公共的属性和方法，放入父类中，让子类自动继承
public class Person {
	public String name;
	public int age;
	public Date birthDate;
	public String sex;
}

public class Student extends Person {
	public String school; //继承父类属性之外，自己定义的属性
	public void getInfo() {
		System.out.println(
				"name:" + name + " age:" + age + " birthDate:" + birthDate + " school:" + school + " sex:" + sex);
	}
}
```

``` xml
4.java继承的特点
	a.java只支持单继承,一个子类只能有一个直接的父类;
	b.一个父类可以同时派生出多个子类

5.总结
	子类继承了父类，就继承了父类的方法和属性。
	在子类中，可以使用父类中定义的方法和属性，也可以创建新的数据和方法。
	因而，子类通常比父类的功能更多。
	在Java 中，继承的关键字用的是“extends”，即子类不是父类的子集，而是对父类的“扩展”。

6.子类不能继承父类的内容:
	a.被private修饰的属性和方法
	b.不同包中，使用默认修饰符修饰的属性和方法
	c.构造方法不能被继承

7.多重继承的执行顺序
	父类的属性---->父类的构造方法---->子类的属性----->子类的构造方法

8.成员变量的隐藏
	当子类中定义的成员变量只要和父类中的成员变量同名时，子类就隐藏了继承的成员变量
```

![1553046433735](img\1553046433735.png)



### 2.1 方法的重写（覆盖）

override(重写)和overload(重载)的区别

``` xml
1.概念
	a.在子类中可以根据需要对从父类中继承来的方法进行改造—覆盖方法(方法的重置、重写)，在程序执行时，子类		的方法将覆盖父类的方法。
	b.覆盖方法必须和被覆盖方法具有相同的方法名称、参数列表和返回值类型。
		注意:返回值类型,除了本身的类型之外，也支持子类的类型
	c.覆盖方法不能使用比被覆盖方法更严格的访问权限。
	
	可以使用 	@Override 注解 判断是否是重写方法
	@Override //如果不是重写方法，出现错误
	public void show() {
		System.out.println("son....show");
	}


2.重写和重载的区别
	a.重载同名不同参，至少有一个参数不一样。重写同名同参。所有的参数必须一样
	b.重载的返回值可以一样，也可以不一样。重写必须一样
	c.重写的访问修饰符号不能比被重写的权限更低
	d.重载可以在一个类中，也可以在父子类。重写必须子类重写父类的方法。
```



### 2.2 super

``` xml
在Java类中使用super来引用父类的成分
	super可用于访问父类中定义的属性   ---->super.name
	super可用于调用父类中定义的成员方法 ---->super.findArea()
	super可用于在子类构造方法中调用父类的构造方法
	super的追溯不仅限于直接父类

调用构造方法:
	a.在子类的构造方法中可使用super(参数列表)语句调用父类的构造方法
	b.如果子类构造方法中既未显式调用父类构造方法，而父类中又没有无参的构造方法，则编译出错
	c.如果子类的构造方法中没有显示地调用父类构造方法，也没有使用this关键字调用重载的其它构造方法，则系统		默认调用父类无参数的构造方法



```



































