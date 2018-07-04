# 第九章 对象和类

## 9.1 引言
面向对象编程可以有效的帮助开发大规模的软件以及图形用户界面(GUI)

## 9.2 对象定义类
1. 类为对象定义属性和行为
	1. 一个对象的属性：是由具有当前值的数据域来表示的
	2. 一个对象的行为：是由方法定义的，调用一个方法就是要对对象完成一个动作
	3. Java类用【变量】定义【数据域】
	4. Java类用【方法】定义【动作】	
2. UML类图
	1. 类：ClassName(parameterName: parameterType)
	2. 数据域：dataName：dataType
	3. 方法：methodName（parameterName：parameterType）：returnType
3. 包含Main（）的类称为主类
## 9.3 定义类和创建对象
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
3. 类的构造方法和其他方法定义为公共(public)，因此可以从其他类中访问
## 9.4 使用构造方法构造对象

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

1. 对象的数据和方法可以通过点操作符(.)通过对象的引用变量来进行访问


</> abernathy
MK-42
