# 面向对象
## 成员变量和局部变量的区别：
1. 有效区域
	1. 成员变量定义在类中，整个类中都可以访问
	2. 局部变量定义在函数语句局部代码块中，只在所属的区域有效
2. 所在内存
	1. 成员变量存在于堆内存的对象中
	2. 局部变量存在于栈内存的方法中
3. 生命周期
	1. 成员变量随着对象的创建而出现，随着对象的消失而释放
	2. 局部变量随着所属区域的执行而存在，随着所属区域的结束而释放
4. 成员变量有默认初始化值，局部变量没有默认初始化值

## 当局部变量与成员变量同名时:
1. 局部变量的值会覆盖成员变量的值
2. 当方法在栈内运行时，由于局部变量也存储在栈内，所以优先取得局部变量的值
3. 当栈中不存在该变量名时，才选择去堆内存中对象下查找是否有该名字的变量

## 类类型参数
* 指方法的参数为类的对象
* 该方法的功能：用于改变对象的属性
* 类类型变量一定指向对象，或者为null，不能赋值为其他

## 匿名对象
* 形式：new className();
* 定义对象的简写格式
1. 使用方式
	1. 当对象对方法「只进行一次调用时」就可以简化成匿名对象
	2. 匿名对象可以作为「方法参数」传递

## (一) 基本数据类型参数传递
	```
		classDemo
		{
			public static void main(String[] args)
			{
				int x = 3;
				show(x);
				System.out.println("x=" + x);
			}
			public static void show (int x)
			{
				x = 4;
			}
		}
	```
	
* show()方法改变的是show代码段内的x值
* show()方法弹栈后对main代码段内的x值无影响
* 系统依然输出main代码段中的x值，为3

## (二) 引用数据类型参数传递
	```
		class Demo
		{
			int x = 3;
			public static void main(String[] args)
			{
				Demo d = new Demo();
				d.x = 9;
				show(d);
				System.out.println(d.x);
			}
			public static void show(Demo d)
			{
				d.x = 4;
			}
		}
	```
	
* 对象的数据域只要被改变，均为堆内存的数据被改变
	
## 封装
	```
		class Person
		{
			private int age; //封装属性
			
			public void setAge(int a)
			{
				age = a;
			}// 设置属性
			
			public int getAge()
			{
				return age;
			}// 获得属性
		}
	```

## 权限修饰符
1. private
	1. 只能用于修饰成员，不能修饰局部
	2. 私有的内容只在类中有效 
2. public
	* 被修饰后可以在类外访问
		
## 构造函数
 1. 一个类中如果没有定义过构造函数，该类中会有一个默认的空参数构造函数
 2. 如果在类中定义了指定的构造函数，那么类中的默认构造函数便不存在
 3. 构造函数允许重载，重载构造函数间参数列表不同
 	1. 参数个数
 	2. 参数类型
 	3. 参数顺序
 		* 参数个数、类型相同，参数顺序不同也构成重载
 4. 构造函数名通常首字母大写，容易区分
 5. 构造函数包含`return;`语句，只起结束函数的作用
 
## 什么时候定义构造函数？
1. 描述事物时，该事物已存在就具备一些内容，这些内容就定义在构造函数中

## 静态工具类，实现阻止类创建对象的方法
1. `private 构造函数名(){}`
2. 工具类的所有方法都是静态的，为了阻止其创建对象浪费堆内存空间，可以将构造函数私有化

## 文档注释导出-应用程序说明书
1. 格式
```
	程序整体
	/**
		建立一个用于操作数组的工具类
		其中包含了常见对数组操作的函数，如：最值、排序等
		@author Mark
		@version V1.0
	*/
	单个函数
	/**
		获取整型数组的最大值
		@param arr 接收一个元素为int类型的数组
		@return 该数组中的最大元素值
	*/
```

2. 如果把一个类文档化导出，该类必须是public类
	* 文档注释也只会提供出public方法信息，不提供private方法信息
3. javadoc 只会导出文档注释`/**...*/`，不会导出多行注释`/*...*/`
	

## 将数组以String形式全部打印
```
	public static String arrayToString(int[] arr)
	{
		String str = "[";
		
		for (int i = 0; i < arr.length; i++)
		{
			if(x!=arr.length-1)
				str = str + arr[x]+",";
			else
				str = str + arr[x]+"]";
		}
		
		return str;
	}
```

* 采用字符串相加的方式，将数组内容合并在一起

## this关键字
1. this调用变量	
	1. 问题：局部变量和成员变量重名

	2. 解决方法：`this.name = name;`
		1. `this.name`代表堆内存中的成员变量name
		2. `name`代表局部变量name
		3. 该动作将局部变量取得的值赋给成员变量
	
	3. 哪个对象调用了this所在的函数，this就代表了哪个对象  
2. this调用构造方法
	1. 关键字this可以用于在同一个类的构造方法中「调用另一个重载构造方法」
		```
			Person(String name)
			{
				this.name = name;
			}
			
			Person(String name,int age)
			{
				this(name); //此处调用的为上述构造方法
				this.age = age;
			}
		```	
		
		* 此处`this(args);`只能定义在构造函数的第一行，「初始化先执行」
		* 优势：提高代码复用率 
3. this 应用范围
	1. 在本类中用到本类的对象，通常用到this
		* 此时对象还没有被创建，this代表未被创建对象的位置
		```
			public boolean compare(Person p)
		 		{
		 			if(this.age == p.age)
		 				return true;
		 			else
		 				return false;
		 				
		 			// return this.age == p.age;
		 		}	
		 		
		 		p1.compare(p2);	
		```
		 	
# 静态变量、常量和方法
## 实例对象与静态变量的定义：

1. 实例变量-对象变量
	1. 指在数据域中没有被注明 static 的变量
	2. 实例变量不能被同一个类下的不同对象所共享
	3. 同类下的不同对象针对同一个实例变量做出的改变不互相影响
		* object1 中的 data 不会影响 object2 中的 data
	4. 如果想要同类下的所有对象共享数据域，就要使用static变量
	
	
2. 静态变量-类变量
	1. 静态变量可以被类下的所有对象共享
		* 共享意味着：改变值后相互影响
		*  静态变量可以用来==统计创建对象的个数==
	2.	静态方法使用注意事项 
		1. 静态方法不能访问类下的任何==对象==
		2. ==静态方法只能访问静态成员(成员=成员函数+成员变量)==
		3. 非静态方法既可访问静态又可访问非静态
		4. ==静态方法中不可以使用 this 和 super 关键字==
		5. 主函数是静态的
			* 主函数只能调用 static 方法
			* ==可以采用用“对象.方法”的形式来调用非静态方法==
	
	
## 实例变量和静态变量的区别：

1. 变量生命周期不同
	1. ==实例变量随着对象的创建而存在，随着对象的回收而释放==
	2. ==静态变量随着类的加载而存在，随着类的消失而消失==
2. 调用方式不同
	1. 实例变量只能被对象调用
	2. 静态变量即可以被对象调用，又可以被类名调用
		* 不建议用对象调用static变量
3. 数据存储位置不同
	1. 成员变量存储在堆内存的对象中，也称对象的特有变量
	2. 静态变量存储在==方法区的静态区==下，也称对象的共享数据
4. ==静态变量前省略的是`类名.`==
5. ==非静态变量前省略的是`this.`==

## 什么时候用静态变量？
1. 静态变量
	1. 当对象中对于同一个成员变量的值都一样时，对象只需要访问，不需要修改，定义成静态的
	2. 若数据在对象中都是不同的，就是对象的特有数据，必须存储在对象中，定义成非静态的
	
2. 静态函数
	1. 该功能是否需要访问非静态的成员变量
		1. 需要：定义成非静态
		2. 不需要：定义成静态

## 静态代码块
```
	class ClassName
	{
		// 静态代码块
		static
		{
			System.out.println("the class is running");
		}
	}
```

1. 静态代码块没有函数名
2. 静态代码块==写在类内==
3. 静态代码块随着类的加载而执行
	* 而且只执行一次
4. ==作用：用于对类进行初始化==
	* 通常该类内全为静态成员
5. ==静态代码块在主类中时，先执行静态代码块，再执行主函数==

## 构造代码块
```
	class ClassName
	{
		// 构造代码块
		{
			System.out.println("object is running");
		}
	}
```

1. 写在类中的无名代码块称为构造代码块
2. ==「构造代码块」是给所有对象进行初始化==
3. ==「构造函数」是给对应的对象进行针对性初始化==
4. 构造代码块，==每创建一个新对象执行一次==
	* ==构造代码块在构造函数前执行==

## 局部代码块
```
	public void function()
	{
		// 函数代码块
		{
			System.out.println("funcition code area");
		}
	}
```

*  用于限制局部变量的生存周期


## 主函数是静态的：

1. 主函数`public static void main(String[] args)`
	1. 格式是固定的
		1. public : 权限必须是最大的
		2. static : 不需要“对象.”，直接用主函数所属类名调用即可
		3. void : 主函数没有具体的返回值
		4. main : 函数名，不是关键字，只是一个JVM识别的固定的名字
		5. String[] args : 一个数组类型的参数，元素都是字符串类型
			* Java虚拟机只识别参数()内的固定格式
			* 可以更改args名字
			* 不可更改String[] 类型
	2. 被JVM所识别和调用
	3. 虚拟机在调用主函数时给参数传递了一个"new String[0]"
	
# 设计模式
## 单例设计模式
* 解决的问题： 可以保证一个类在内存中对象的唯一性
* 比如：多个程序使用同一个配置信息对象时，就需要保证该对象的唯一性
	 
* 如何保证对象的唯一性？
	1. 不允许其它程序用new创建该类对象
	2. 在该类中创建一个本类实例
	3. 对外提供方法让其它程序可以获取该对象
	 	
* 实现步骤
	1. 私有化该类构造函数
	2. 通过new在本类内创建本类对象
	3. 定义一个public方法，将创建的对象返回
	```
	 //方案1-饿汉式
	 class Single
	 {
	 		private static Single s = new Single();
	 		private Single(){}
	 		public static Single getInstance() 
	 		{
	 			return s;
	 		}
	 }
	```
	 	
	* static修饰函数，以被类名调用
	* static修饰变量，以被static函数访问
	 	
	```
	 //方案2-懒汉式
	 class Single2
	 {
	 	private static Single2 s = null;
	 	private Single2(){}
	 	public static Single2 getInstance()
	 	{
	 		if(s == null)
	 			s = new Single2();
	 		return s;
	 	}
	 }
	```
	 	
	* 方案1与方案2 的区别
	 1. 方案1：随着类的加载，对象就已经生成，开发常用
	 2. 方案2：调用getInstance()函数，创建新对象
	 	* 是方案1的延迟加载形式，面试常用
	 	* 方案2被多线程并发访问时有安全隐患
	 			
# 继承
1. 格式
```
	class SonClass extends FatherClass
	{
		// 继承父类的全部方法
	}
```

2. Java支持单继承，不支持多继承
	* 单继承：一个子类只能有一个直接父类
	* 多继承：多个父类中有同名成员函数时，会产生调用的不确定性
		* 在Java中使用“多实现”的方式实现的
		* 对C++中的多继承机制进行了改良
3. Java支持多层继承

4. 子类和父类的变量名冲突时，子类变量有效
	* 当子类的变量和父类变量重名时，用super关键字区分父类
		* this代表一个本类对象的引用
		* super代表一个父类的空间
		
5. Java 中的所有类都是 Object 类的子类

## 什么时候用继承？
当类与类之间存在所属关系时，定义继承

所属关系：xxx 是 yyy 的一种	 

## super关键字
1. ==在子类中==，调用原父类中被覆写的方法`super.method();`
2. 在子类构造函数第一行调用父类构造方法
```
	class Father
	{
		public void method()
		{
			System.out.println("Father");
		}
		
	}
	
	class Son extends Father
	{
		public void method()
		{
			System.out.println("Son");
		}
		public void function()// 在主函数中调用
		{
			super.method();// 在子类中覆写
		}
	}
	
	public class MainClass
	{
		public static void main(String[] args)
		{
			Son s = new Son();
			s.method();// Print: Son
			s.function();// Print: Father
		}	
	}
```

## 子父类中「成员函数」的特点
1. 函数的两个特性
	1. overload-重载：两函数函数名与返回值一致，参数列表不同
	2. override-子类重写父类函数：两函数函数名、返回值和参数列表完全一致	
	3. **重写注意事项**
		1. 子类方法重写父类方法时，==子类方法权限必须大于等于父类权限==
			* 权限顺序：public > (none) > private
		2. 静态子类重写静态父类，两者其中有一个不是静态都不通过编译
	4. **什么时候用重写操作？**
		* 当对一个类进行子类扩展时，子类需要保留父类的功能声明，但是要定义父类中该功能的特有内容时，使用「重写」实现
			1. 用继承的方式进行程序的版本升级，而不是修改源代码
			2. ==保留父类原有功能，创建子类特有内容==
				* 父类保留原有功能「用super的方式调用原函数」
		
## 子父类中「构造函数」的特点
1. 在子类构造对象时，发现：访问子类构造函数时，父类构造函数也运行 ？
	* 原因是：==在子类构造函数中第一行有一个默认的隐式语句`super();`==
		* `super();`调用的是父类中的「空参构造函数」
		* ==父类中如没有空参数构造函数，会报错，需要用`super`明确调用==
2. 构造函数不发生重写，也没有被继承过来，只能在子类中通过`super`访问
3. 子类的实例化过程，子类构造函数默认都会访问父类空参构造函数
	```
		SonClassName(args or not)
		{
			//隐式访问super();
			System.out.println("son's contents");
		}
	```
	
4. **为什么子类实例化的时候要访问父类的构造函数 ？**
	* 子类有可能用到父类的成员变量，因此要事先了解父类如何对该变量初始化的
	* 因此子类在构造对象时会事先访问父类构造函数，即在子类构造函数中加入了`super();`语句
	* 如果父类中没有定义空参数构造函数，那么子类的构造函数必须使用super语句明确调用
	
	* ==`super`语句必须定义在子类构造函数的第一行==
		* 由于`super();`和`this();`都必须放在构造函数首行
		* ==因此有`this();`后，该构造函数中就不存在`super()`==
		* 但总会通过某个`this`访问到父类构造函数
	
	```
	/* 特殊例子 */
		Son()
		{
			//super();
		}
		
		Son(args)// 此构造函数中没有super();
		{
			this();
			//Son(args)的内容
		}
		
	```
	
	5. ==**父类初始化完毕，才执行子类显式初始化**==
		* 先在子类中执行`super();`
		* `super();`弹栈后再执行子类中第一条`int sonx = 42;`
		* int sonx 初值为 0
		
## 一个对象的实例化过程
`Person p = new Person();`

1. JVM读取指定路径下的Person.class文件，并加载进内存，并先加载Person的父类
2. 在堆内存中开辟空间分配地址
3. ==并在对象空间中，对对象中的属性进行默认初始化==
4. 调用对应的构造函数初始化对象
5. 在构造函数首行，先调用`super();`
6. ==父类初始化完毕后，在对子类的属性进行显式初始化== 
7. 再对对象进行子类构造函数的特定初始化
8. 初始化完毕后，将地址值赋给引用变量

## final关键字 
* 继承弊端：打破封装性

1. final是一个修饰符，可以修饰类、方法、变量
2. ==final修饰的类不可以被继承`final class Father`==
3. ==final修饰的方法不可以被重写`final void method()`==
4. final修饰的变量是常量，只能赋值一次`final int X = 42;`
	* 在类中final修饰的常量，不被默认初始化，需要主动显式初始化
	* ==在类中final常量，通常也被static修饰==
	* 常量名字母均大写，多个单词之间`_`连接

5. **为什么要用final修饰变量**
	* 创造一个阅读性好的固定数值
	
# 抽象类
1. 抽象：具体细节不能确定
2. 当一个类描述事物时，没有足够的信息用以描述，此类为抽象类
3. 格式：`abstract void method();`
```
	abstract class ClassName
	{
		abstract void method();
	}
```

	* ==抽象函数必须放在抽象类中==
	
## 抽象类的特点
1. 方法只有声明没有实现时，该方法就是抽象方法，需要被abstract修饰
2. 抽象方法只能定义在抽象类中，该类必须也被abstract修饰
3. 抽象类不可以被实例化(不能新建对象):因为调用抽象方法无意义 
4. 抽象类必须有==子类覆盖了所有的抽象方法==后，该子类才可以实例化。否则，该子类也是一个抽象类

## 抽象类的细节
1. 抽象类中有构造函数吗？
	* 有，用于给子类对象进行初始化
2. 抽象类可以不定义抽象方法吗？
	* 可以，但是很少见，==目的就是不让该类创建对象==(AWT适配器对象)
3. ==抽象关键字不可以和哪些关键字共存？== 
	1. `private`：抽象方法需要被子类覆盖，用private修饰的方法不能完成此动作
	2.  `static`：会导致类名直接调用抽象方法，这个操作没意义
	3. `final`：抽象一定需要覆盖，final一定不能被覆盖
4. 抽象类和一般类的区别
	* 相同点：抽象类和一般类都是用来描述事物的，都在内部定义了成员
	* 不同点：
		1. 一般类有足够的信息描述事物，而抽象类描述事物的信息可能不足
		2. ==一般类中不能定义抽象方法，只能定义非抽象方法==
		3. 抽象类中可以定义抽象方法，也可以定义非抽象方法
		4. 一般类可以被实例化，抽象类不可以被实例化
5. 抽象类一定是一个父类吗？
	* 是的，因为需要子类覆盖其方法后，才可以对子类实例化
	
# 接口 interface
1. 当一个抽象类中的方法全部为抽象方法，采用`接口interface`
	* 接口实际上就是抽象类，生成的也是`.classs`文件
2. 接口中常见的成员：
	1. 全局常量：public static final
	2. 抽象方法：public abstract
	
	* ==而且这些成员都有「固定」的修饰符== 
	```
		interface ClassName
		{
			public static final int NUM = 42;
			public abstract void method1();
			public abstract void method2();
		}
	```
	
	* ==接口内只能定义静态常量==
	* 接口中的成员都是公共权限
	* 由于成员格式是固定的，因此冗长的修饰符即使不写或是漏写，编译也会自动补全。但是不建议这样做，可读性差，函数重写时也容易出问题
	
## 接口类的实现`implements`
1. 类与类之间是继承关系，接口与类之间是实现关系
2. 接口的特点
	1. 接口不可以实例化
	2. 只能由实现了接口的子类，并覆盖了接口中的全部抽象方法，该子类才可以实例化
	3. ==在子类中重写`@override`方法，一定要前加`public`== 
		* 因为在接口中，抽象函数前一定用`public`修饰，重写权限必须大于等于`public`
	
3. **在java中不支持多继承**
	1. java对多继承机制进行了改良，在java中变成了**多实现**
	2. 一个类可以实现多个**接口**
	```
		interface A
		{
			public void method();
		}
		
		interface B
		{
			public void method();
		}
		
		class C_Impl implements A,B// 多实现
		{
			public void method();
			// 会覆盖A,B中的抽象方法，不产生不确定调用
		}
	```
	
4. **一个子类在继承一个父类的同时，还可以实现多个接口**
	```
			class Father
			{
				public void Fmethod(){}
			}
			
			interface A
			{
				public void method();
			}
			
			interface B
			{
				public void method();
			}
			
			class C_Impl extends Father implements A,B// 多实现
			{
				public void method(){}
				// 会覆盖A,B中的抽象方法，不产生不确定调用
				
				public void Fmethod(){}
				// 会覆盖 Father 中的方法，优先使用改写后的方法
			}
	```
	
	5. 接口与接口之间是`继承 extends`关系，==接口之间可以多继承==
	
## 接口的特点
1. 接口是对外暴露的规则
2. 接口是程序功能的扩展
3. 接口的出现降低耦合性	
	
## 接口与抽象类的区别
1. 关键字
	1. 抽象类需要被`继承 extends`，而且只能单继承
	2. 接口需要被`实现 implements`，而且可以多实现
2. 可直接使用的方法
	1. 抽象类中可以定义抽象方法和非抽象方法，子类继承后，可以直接使用非抽象类方法
	2. 接口中只能定义抽象方法，需要子类去实现
3. 使用接口? 还是使用抽象类?
	1. 抽象类的继承是`is-a 所属关系`，在定义体系的基本==共性内容==
	2. 接口的实现是`like-a`关系，在定义体系的==额外功能==
	
## 接口的应用
1. 对外暴露规则
	* 先定义接口及其内部抽象函数
```
	interface USB
	{
		public void open();
		public void close();
	}
```

2. 实现规则
	* 通过子类具体实现接口中定义的抽象函数
```
	class productUSB implements USB
	{
			public void open
			{
				System.out.println("open");
			}
		
			public void close
			{
				System.out.println("close");
			}
	}
```

3. 使用规则
	* 在主函数中用子类对象调用子类中实现的方法
```
	public class MainClass
	{
			public static void main(String[] args)
			{
				useProduct(new productUSB());
			}
		
			public static useProduct(USB u)// 接口类型引用
			{
				u.open();
				u.close();
			}
	}
```

* ==接口类型的引用指向其子类对象 多态== 

# 多态
```
	class Animal
	{}
	
	class Cat extends Animal
	{}
	
	class Dog extends Animal
	{}
	
	Cat x = new Cat();
	
	Animal x = new Cat();
	//父类类型 x = new 子类类型();
```

1. 多态：一个对象对应着不同类型
2. 多态在代码中的体现：父类或者接口的引用指向其子类对象

* ==多态下：父类引用作为函数参数时，任何被继承的子类对象都可以作为实参传递==

```
		public static useProduct(USB u)// 接口类型引用
		{
			u.open();
			u.close();
		}
```

* USB是接口类型：因此所有USB的子类对象都可以作为参数调用此函数
4. **多态的弊端**：只能调用父类中抽象方法声明过的内容，不能调用子类中的特有内容
	* ==多态下不能调用子类特有方法== 

5. 多态的前提：
	1. 必须要有如右子父类关系：继承、实现
	2. 必须要有对父类抽象方法的覆盖 
	
6. ==多态下使用子类下的特有方法==
	1. `Animal a = new Cat();`
		1. 向上转型：将Cat类型向上转换为Animal类型
		2. 为了限制对特有功能的访问
		3. 为了提高扩展性
	2. ==向下转型==：通过强制类型转换，使用子类中的特有方法
	```
		Cat c = (Cat)a;
		c.catchMouse();// Cat中的特有函数catchMouse();
	```
	
	3. ==注意事项：不构成子父类关系的不要使用转型== 
	
## 对于对象类型的判断
- 格式：`对象 instanceof 类名`：当前对象是后类的实例时，返回true

- 只能用于==引用数据类型==判断 
```
	class Animal
	{	
	}
	class Cat extends Animal
	{
	}
	public class MainClass
	{
		public static void main(String[] args)
		{
			Animal dog = new Animal();
				Cat cat = new Cat();
			System.out.println(dog instanceof Animal);//true
			System.out.println(cat instanceof Animal);//true
		}	
	}
```
	
## 多态下成员的特点
1. ==成员变量==
	1. `Father f = new Son();` 
	2. 编译看左边，==运行看左边==
		1. f 现在是Father类型，具有 Father 的属性，调用的变量在 Father 类中寻找，有就使用其值，没有就报错
		2. 和 Son 类中的同名变量无关 
			* 开发时Son中不会出现定义和父类同名变量，面试时会出现此情况 
2. ==成员函数==
	1. `Father f = new Son();` 
	2. `非静态函数时`	
		* f 调用方法，由于 f 指向 Son 类对象，因此先在 Son 类中查找，Son中没有就从父类中继承
			* 前提也是父类中有被覆写的同名方法，没有就报错
		* 编译看左边，==运行看右边==
	3. `static 函数时` 
		* 由于静态函数随类加载而加载，f 此时属于 Father 类型，因此调用Father 类中的 static 方法,父类中有就调用，没有就报错
		* 编译看左边，==运行看左边==
		* 通常静态方法不涉及多态性，因为多态是对象的性质，而静态不需要对象来调用
	
	
		```		
			// 非静态函数时
			
			class Father
			{
				public void show()// 父类中有被覆写的同名方法
				{
					System.out.println("Father");
				}
			}
			class Son extends Father
			{
				public void show()
				{
					System.out.println("Son");
				}
			}
			public class MainClass
			{
				public static void main(String[] args)
				{
					Father f = new Son();
					f.show();// 打印：Son
				}	
			}
		```

		
# 内部类
1. 定义：在类中定义新类	
	```
	class Outer
	{
		class Inner
		{
			void method()
			{
				System.out.println("method runn");
			}
		}
	}
	```
	
2. 内部类的访问特点：
	1. 可以直接访问外层内的`private 成员`
	2. 外部类想要访问内部类，必须建立类的对象
	3. ==内部类可以被成员修饰符所修饰==

3. 一般用于类的设计：
	* 分析事物时，发现事物的内部还有事物，而且外部事物还在访问内部事务，此时就需要定义内部类
	
4. 直接访问外部类中的内部类
	```
	public static void main(String[] args)
	{
		// 内部类是非静态
		Outer.Inner in = new Outer().new Inner();
		in.method();// 引用变量直接访问方法
		
		// 内部类 Inner 是 static
		Outer.Inner in = new Outer.Inner();
		in.method();
		
		// 内部类是static，method() 也是 static
		Outer.Inner.method();
	}
	```
	
	* ==记住格式==
	
	* ==静态成员只能访问静态数据==
	
	* 如果内部类中定义了静态成员: ==如果内部类方法被定义成static，那么内部类也必须被定义成static==
	
5. ==当内部类想要直接访问外部类的成员时：==
	* 格式：外部类名.this
	* ==外部类名，意在注明是谁的this==
	```
		class Outer
		{
			int num = 3;
			class Inner
			{
				int num = 4;
				void show()
				{
					int num = 5
					System.out.println(Outer.this.num); // <--
				}	
			}
			
			void method()
			{
				new Inner().show();
			}
		}
		
		class MainClass
		{
			public static void main(String[] args)
			{
				new Outer().method();
			}
		}
	```
	
	1. 当--> num前为空，结果为5: 因为局部变量优先
	2. 当--> num前为this，结果为4: 此时调用的是内部类的数据域
	3. 当--> num前为Outer.this，结果为3: 此时调用的是外部类的数据域
	
6. ==内部类可以在局部位置上==
	```
		class Outer
		{
			int num = 3;
			void method()
			{
				final int x =9;// <--
				
				class Inner
				{
					void show()
					{
						System.out.println("Inner is running"+x);
					}
				}
				
				Inner in = Inner();
				in.show();// 此时调用method()就可以调用show()了
			}
		}
	```
	
	* ==在内部类中访问局部变量时(<--)，该局部变量必须被定义成final==
	

# 匿名内部类
* 内部类的简写格式
	* 前提：内部类==必须继承一个外部类==，或者实现一个外部接口
	* ==匿名内部类其实是一个带着类内容的对象==
	```
		abstract class Father
		{
			abstract void show();
		}
		
		class Outer
		{
			/*
				class Inner extends Father
				{
					void show()
					{
						System.out.println("override show");
					}
				}
			*/
			
			void method()
			{
				// 此处代替了 class Inner extends Father
				new Father()
				{
					void show()
					{
						System.out.println("匿名内部类正常运行");
					}
				}.show();
				// 此处new Father()是一个对象，可以直接调用show()
			}
		}
		
		// 调用方式
		public class MainClass
		{
			public static void main(String[] args)
			{
				new Outer().method();
			}
		}
	```
	
	* ==此处new Father()是一个对象，可以直接尾部调用show()==
	
	* 类的成员：可以是方法，可以是变量，但是==不可以是匿名对象==
		* `new Father()`不可以直接作为类的成员
## 匿名内部类的应用
*  当函数的参数是接口类型，且接口中的方法不超过三个，此时可以用匿名内部类作为实参传递
	```
		interface Inter
		{
			public void show1();
			public void show2();
		}
		
		public class MainClass
		{
			public static void main(String[] args)
			{
				show(new Inter()
				{
					public void show1(){}
					public void show2(){}
				}); // 实现接口的匿名内部类
			}
			
			// 参数是接口类型的函数
			public static show(Inter in)
			{
				in.show1();
				in.show2();
			}
		}
	```	
	
	* 匿名内部类就是==继承外部类==或==实现外部接口==的一个==有内容的对象==
	
## 匿名内部类实际是外类下的成员
```
	public class MainClass
	{
		class Inner
		{
		}
		public static void main(String[] args)
		{
			new Inner();// 此处会报错
		}
	}
```

* 在主类中，==Inner相当于一个非静态成员==，主函数是静态的，静态方法不能访问类下的非静态成员

* 应该对 Inner类做如下改动：
```
	static /*静态成员*/class Inner
	{
	}
```

## 匿名内部类与向上转型
1. 代码块-1
```
	class Outer
	{
		void method()
		{
			new Object()// <--
			{
				public void show()
				{
					System.out.println("show run");
				}
			}.show();		
		}
	}	
	
	public class MainClass
	{
		public static void main(String[] args)
		{
			new Outer().method();
		}	
	}
```
	
* Object是所有类的父类
* `new Object(){...};`是创建一个继承Object类的匿名子类

2. 代码块-2
```
	class Outer
	{
		void method()
		{
			Object obj = new Object()
			{
				public void show()
				{
					System.out.println("show run");
				}
			};	
			
			obj.show();		
		}
	}	
	
	public class MainClass
	{
		public static void main(String[] args)
		{
			new Outer().method();
		}	
	}
```

* 此时会报错，原因是：
* `new Object(){...};`匿名子类向上转型成了父类`Object`
* 父类`Object`中没有`show()`方法

## 对象的初始化过程
```
	class Father
	{
		{
			System.out.println("Father construct");// 1
		}
		Father()
		{
			// super();
			// 显式初始化
			// 构造代码块初始化
			show();
		}
		
		void show()
		{
			System.out.println("Father");// 运行覆写后的子类内容
		}
	}
	
	class Son extends Father
	{
		int num = 9;
		{
			System.out.println("Son construct" + num);// 3,num = 9
			num = 10;
		}
		Son()
		{
			// super();
			// 显式初始化
			// 构造代码块初始化
			System.out.println("Son" + num);// 4,num = 10
		}
		void show()
		{
			System.out.println("Son" + num);// 2 ,num = 0;
		}
	}
	
	public class MainClass
	{
		public static void main(String[] args)
		{
			new Son();
		}
	}
	/*
		运行结果：
			Father construct
			Son0
			Son construct9
			Son10
	*/
```

* ==构造函数内运行顺序==
	1. 运行`super();`先跳至父类构造函数
	2. 显式初始化
	3. 构造代码块运行
	4. 构造函数内特有内容执行
	
# 异常 Exception
1. 定义：==运行时期==发生的不正常情况
2. 异常类：在java中==用类的形式==对不正常的情况进行了描述和封装，描述不正常情况的类，就称为==异常类==
	*  不同的问题用不同的类进行具体的描述
3. 异常体系
	- 父类：Throwable 类，==该类及其子类==具有==可抛性==
		1. Error类：不可处理的问题
			* 由JVM抛出的严重性的问题
		2. Exception异常：可处理的问题
4. 可抛性：`throw(s)`凡是被这两个关键字所操作的==类==和==对象==都具备可抛性

```
class ArrayError
{
	public int method(int[] arr,int index)
	{
		// 异常判断部分
		if(index >= arr.length)
		{
			throw new ArrayIndexOutOfBoundsException();
			// 括号内可自定义异常显示信息
		}
		return arr[index];
	}
}

class MainClass
{
	public static void main(String[] args)
	{
		ArrayError a = new ArrayError();
		a.method(arr,30);// 此处数组脚标越界
	}
}
```

## 自定义异常
1. 如果让一个类成为异常类，必须要==继承==异常体系，具备可抛性`throw`
2. 自定义异常在`throw`前，要在==所有使用过==的函数体上做标识
	`public int method(int[] arr,int index)throws customizeException`
	
# Java 数据库程序设计

## 关系型数据库系统

1. 关系结构
	1. 每一行表示：相互关联的数据构成一行，称为元组
	2. 每一列表示一个属性
 	
2. 完整性
	1. 域约束：规定一个属性的允许值
	2. 主键约束：
		1. 超键：表格中所有属性对应值的集合
		2. 键：最小单元
		3. 候选键：除主键之外的其它最小单元
			* 主键：数据库设计者指定的候选键之一
	3. 外键约束
		1. 不同表格中的记录通过它们「共同属性」也是相互关联的
		2. 共同属性即为外键
			* 数据库管理系统强制执行完整性约束
3. 语言：
	* SQL：结构化查询语言
 		
## SQL
 1. 进入根账户`mysql -uroot -p`，输入根密码
 2. 在MySQL创建用户账户
 	1. 输入`use mysql`
 	2. 创建账户名和密码：
 	`create user 'scott'@'localhost' identified by 'tiger'`
 	3. 授权给scott
 	```
 	grant select,insert,update,delete,create,create view,drop,execute,references on *.* to 'scott'@'localhost';
 	```
 	
 		1. 如果希望该账号可以从任意IP远程登录
 	```
 	grant all privileges on *.* to 'scott'@'%'identified by 'tiger';`
 	```
 	
 		2. 将 % 改为特定IP地址，即设为只能从该IP远程登录
 	4. 输入`exit;`退出MySQL控制台
 	
 	* Windows中`net start/stop mysql`启动/终止 MySQL
 	
 3. 默认状态下服务器包含mysql和test两个数据库
 	1. mysql：
 		1. 可以使用它创建用户账户
 		2. 可以使用授予撤销用户权限
 		* ==不能用mysql创建用户表==
 	2. test：
 		1. 可以创建新数据库
 		`create database Name`
 		2. 可以删除已存在数据库
 		`drop database Name`
 		
### 创建数据库
1. 进入在根用户下创建的账户
	`mysql -uscott -ptiger`
2. 出现`mysql>`输入：
	`create database javabook`
	* javabook是在该账户下创建的新数据库名
3. 转到javabook数据库
	`use javabook;`
	
### 创建和删除表
1. 创建表
```
create table 表名(
	arg1 char(5),
	arg2 char(4) not null,
	arg3 varchar(50),
	arg4 integer,
	primary key (couseId)
	foreign key (arg1) references 表2(arg1)
	foreign key (arg2) references 表3(arg2)
);
```

2. 参数后跟类型(可注明个数，非空)
	* varchar 是可变长字符串
3. 外键约束`foreign key (arg1) references 表2(arg1)`
4. `primary key (arg)`注明主键
5. SQL关键字不区分大小写
	1. 表名 命名规则同 Java类
	2. 属性 命名规则同 Java变量
6. 删除表：`drop table 表名`
	* 如果创建的表被其它表引用，必须先删除引用表
7. ==从文件中运行SQL命令==
	1. 将命令写入txt，改后缀为`.sql`
	2. mysql> `source 路径 test.sql`

### 插入、更新和删除
1. 插入
```
insert into 表名 (column1,column2,...)
values (value1,value2,...)
```
 
 * column是可选的，如果省略了colunm，必须输入记录中所有属性值
2. 更新
```
update 表名
set column1 = newValue1,column2 = newValue2...
where column3 = 'xxx';
```

3. 从表中删除记录
```
delete from 表名
where column = 'xxx';
```

* 删除表中所有记录`delete from 表名;`

### 查询
```
select column1,column2....
from 表名
where column3 = 'xxx';
```

* 预览整表
```
select *
from 表名;
```

### MySQL中的布尔运算符
1. 与 and
2. 或 or
3. 非 not

### 操作符like、between-and和is null
1. 通配符
	1. `%` 匹配==零个==或多个字符
	2. `_` 匹配单个字符
2. `A like B`：在A内容里查找符合B的部分
3. `A not like B`：在A内容里==排除==含有B的部分
	* 例：`lastName not like '_mi%'`
	* 表示排除第二第三个字母分别是m和i的任意字符串
4. `between v1 and v2`：筛选出值在v1和v2间的部分
5. `A is null`：筛选出A下表格为null的内容

### 列的别名
1. 通常用户对列名采用缩写，显示查询结果时，SQL使用列名作为标题，有时希望在结果中列名给出更具描述性的名字。
 ```
 select LN as "Last Name"	,ZC as "Zip Code"
 from Student;
 ```
 
 * 注意：==此处字符串用的是双引号==
 * 输出结果：
 
```
 +-------+---------+
 |LN     |Last Name|
 +-------+---------+
 |Heintz |Heintz   |
 |Kennedy|Kennedy  |
 +-------+---------+
```
 
 
### 算数运算符 	
 - 用于输出对表格计算后的结果
 ```
 select title,50 * numOfCredits as "Lecture Minutes"
 from Course
 where subjectId = 'CSCI';
 ```
 
 - 每一节课50分钟，输出CSCI学科每门课的总时长
 
### 显示互不相同的记录

1. 关键字：`distinct`
```
select distinct subjectId as "Subject ID"
from Course;
```

* 去除 列subjectId 下重复的元组

2. `select distinct subjectId,title`
	* 筛除两个列下内容==完全相同==的部分，显示剩余部分 
	
### 显示排序好的记录
1. 关键字`order by column`
```
select column1,column2....
from 表名
where column3 = 'xxx';
order by column1 desc,column2 asc;
```
	1. desc 表示降序排列，asc 表示升序排列
	2. ==当指定多列时==：先按第一行排序，然后对第一行具有相同值的行按第二行排列
	
### 联结表
1. 将多个表联合起来，获取完整信息
```
select distinct lastName,firstName,courseId
from Student,Enrollment
where Student.ssn = Enrollment.ssn and
	lastName = 'Smith' and firstName = 'Jacob';
```
 
* 要在一个查询中区==区分==ssn，可以用Student.ssn 和 Enrollment.ssn


