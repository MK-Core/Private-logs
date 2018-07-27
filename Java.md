# 第九章 对象和类

## 9.1 面向对象优势
面向对象编程可以有效的帮助开发大规模的软件以及图形用户界面(GUI)

## 9.2 对象的介绍
1. 类为对象定义属性和行为
	1. 对象的两要素
		1. 属性：是由具有当前值的数据域来表示的
		2. 行为：是由方法定义的，调用一个方法就是要对对象完成一个动作
	2. Java类
		1. 用 变量 定义 数据域
		2. 用 方法 定义 动作	
		
2. UML类图
	1. 类：ClassName(parameterName: parameterType)
	2. 数据域：dataName：dataType
	3. 方法：methodName（parameterName：parameterType）：returnType

## 9.3 类的介绍
1. 可以把两个类放在同一个文件中，但是文件中只能有一个类是公共类(public)
	* 此外公共类(public)必须与文件同名
2. 包含Main（）函数的类称为主类，结构如下：
```
	public class mainClass
	{
		public static void main(String[] args)
		{
			//Main Method Area
		}
		
		/* Main Class Content*/
		
		//Data Area
		
		// Constructor Method
		
		// Methods		
	}
```

3. 类的「构造方法」和其他方法定义为公共(public)，因此可以从其他类中访问

## 9.4 构造方法
1. 构造方法的必备要素：
	1. 构造方法名和类名相同
	2. 构造方法没有返回值类型，连void也没有
		* 构造方法函数头：public className()
	3. 构造方法创建一个对象，在使用new操作符时被调用
		* 调用方式：new className(arguments);
2. 构造方法可以重载：可以定义多个同名的构造方法，它们要有不同的签名
3. 一个类可以不定义构造方法，这种情况下，类中隐含定义一个方法体为空的无参构造方法
	* 当且仅当类中没有明确定义任何构造方法时，才会自动提供它

## 9.5 通过引用变量访问对象
1. 对象通过“.”来调用类中的方法和数据域
	1. object1.method1(arguments);
	2. object1.data1;
2. 对象是通过「引用变量」来访问的
	1. ClassName object1;
		* 引用变量为object1，此符号此时代表ClassName类下的该对象
	2. object1 = new ClassName();
		* 新生成了一个ClassName类的对象，并将它赋给引用变量object1
	3. ClassName object1 = new ClassName();
		* 以上两步整合
3. 静态(static) 与 实例
	1. 「实例变量」只能通过实例调用的数据域变量
		* object1.dataField;
	2. 「实例方法」只能通过实例调用的方法
		* object1.method1(arguments);
	3. 「静态方法(static)」通过类名调用的方法
		* className.method2(arguments);
	4. 静态方法的定义方式
		* public static void methodName(arguments);
			1. public 代表类外是否可访问，不可访问为 private
			2. static 代表是否可用"类名.方法名()"的方式调用
			3. void 代表返回值类型
4. Math类下的方法都是静态方法
	* Math.pow(3,2.5);
5. String 类型
	1. String 是一个预定义的 Java 类
	2. String 类型属于 引用类型
		* String name;
	3. 引用类型不属于 Java 基本类型，String 不属于 Java 基本类型
	
6. 类中的数据域也可能是「引用类型」的
	```
		Class student
		{
			/* data field */
			String name;// 引用类型数据域 
			int age;
			boolean isMajor;
			char grade;
		}
	```
	
7. 如果一个「引用类型」的变量没有赋初值，默认初值为 null
	* ClassName var;// var is null
 	
8. 在类中数据域不赋初值，系统会自动赋默认值
	1. 数值类型 default 0 
	2. boolean default false
	3. char default '\u0000'
	4. 引用类型 default null
	
9. Java 没有给方法中的局部变量赋默认值
	* 此处的局部变量指定义在方法内部的变量，包括
		1. 数值类型
		2. boolean
		3. char
		4. 引用类型
	* 下面的程序会报错
	
	```
		public static void main(String[] args)
		{
			// x y 是局部变量
			int x;
			String y;
			System.out.println("print"+ x + y);
		}
	```
	
10. 基本类型 与 引用类型 区别
	* 变量 代表 存储值的内存位置
	
	1. 基本类型：对应内存存储的是基本类型的值
	2. 引用类型：对应内存存储的是对象的地址
		* className c,"c"内存存储的是 对象c的地址
		* 对象c的地址：对象c的内容存储在内存中的什么位置
	3. 变量互相赋值
		1. 基本类型：实际值的传递
		2. 引用类型：地址的传递
			* c1 指向对象1，c2指向对象2
			* c1=c2后，c1和c2指向同一个对象
			* 原c1指向的对象被「垃圾回收」
			
11. 如果 不需要 某个对象时，可以显式给它的 引用变量 赋值为 null

## 9.6 Java库中的类
1. Date 类
	1. 定义 Date 对象：
		`java.util.Date object1 = new java.util.Date();`
	2. 构造方法：
		1. `java.util.Date();`表示从GMT点流逝至今的时间
		2. `java.util.Date(t0:long)`表示从GMT点流逝t0毫秒的时间
	2. `object1.toString();` 以字符形式返回object1对应的时间
	3. `object1.getTime();` 返回从GMT:1970年1月1日起到object1对象表示时间点之间流逝的毫秒
	4. `object1.setTime();` 为object1设定一个新的流逝时间
2. Random 类
	1. `Math.random()`：得到一个 0.0-0.1(!=1.0) 的double类型值
	
	2. java.util.Random类
		1. 创建Random对象，必须指定一个种子
			1. 默认种子是当前流逝的时间
			2. 两个Random对象具有相同的种子，它们将产生相同的数列
				* 软件测试常用一组固定顺序的随机数来重复生成测试案例
		2. `Random(seed: long)`：构造函数
		3. `nextInt()`：返回一个随机int值
		4. `nextInt(n: int)`：返回一个0到n(!=n)之间的随机int值
		5. `nextLong()`：返回一个随机long值
		6. `nextDouble()`：返回一个0.0至1.0(!=1.0)的随机double值
		7. `nextFloat()`：返回一个0.0至1.0F(!=1.0)的随机double值
		8. `nextBoolean()`：返回一个随机boolean值
3. Point2D类
	1. 用于表示二维平面的点
	2. `Point2D(x: double,y: double)`：构造函数
	3. `distance(x1: double,y1: doulbe): double`：返回(x,y)到(x1,y1)的距离
	4. `distance(p: Point2D): double`返回该点到对象p点的距离
	5. `getX(): double`返回该点x坐标
	6. `getY(): double`返回该点y坐标
	7. `toString(): String`以字符串形式返回该点

## 9.7 静态变量、常量和方法
1. 要点
	1. 静态变量可以被类下的所有对象调用
	2. 静态方法不能访问类下的任何对象
	
	
	
	
	
	
	
	
	


	
