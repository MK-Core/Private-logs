## 泛型

​	JDK1.5出现的安全机制

好处：
	1 将运行时期的问题ClassCastException转移到了编译时期
	2 避免了强制转换的麻烦

<>：什么时候用？当操作的引用数据类型不确定时，就使用<>，将要操作的引用数据类型传入即可，其实<>就是一个用于接收具体引用数据类型的参数范围。	

==引用数据类型==：不是类就是接口。

在程序用，只要用到了带有<>的类或接口，就要明确传入的具体引用数据类型。

```
void show(int x,double y)

class Tool<e1,e2,e3,e4>

Tool<String,Demo,Person,Integer> t = new Tool<String,Demo,Person,Integer>();
```



==P67==

## 内存加载过程 

栈：先进后出

1. 主函数最先进栈，运行到其他函数后，其他函数进栈。
2. 其他函数运算结束后自动出栈，释放内存。
3. 最终主函数执行结束后，主函数出栈，释放内存。

## 重载 

定义：在==同一个类中==，允许存在一个以上的==同名==函数，只要它们的==参数个数==`或者`==参数类型==不同。

重载函数通常会出现重复的代码，可以通过对功能最复杂的函数进行==复用==，解决代码冗余。

## 数组 

内存的划分

1. 寄存器

2. 本地方法区

3. 方法区

4. 栈内存

   存储的都是局部变量，局部变量：定义在方法中的变量。

   而且变量所属的作用域一旦结束，该变量就自动从内存中释放。

   - 局部代码块 {  }

     限定局部生命周期：局部变量在局部代码块执行结束后，即释放。

5. 堆内存

   存储数组和对象，凡是用new建立都在堆中。

   特点：

   - 每一个实体都有首地址

   - 堆内存中每一个变量都有默认初始化值

     根据类型不同可以分为：

     ​	int			  0

     ​	double 	  0.0

     ​	float 		  0.0f

     ​	boolean	 FLASE

     ​	char		  ‘\u0000’

   - 垃圾回收机制：内存管理

     

   引用数据类型：

   ​	`int[] arr = new int[3]`，该new过程在堆中创建实体后，将该实体的==地址==赋给arr变量。==引用数据类型不指向任何内容时，将其赋值为空`arr = null`。==

   ​	当堆内存中的实体不被任何引用数据类型指向时，该实体被认定为“垃圾”，而不是像栈内存中立刻被释放。Java存在不定时的自动垃圾回收机制，类似于C++的析构函数(手动回收垃圾)。

## 求最值

![1581417322304](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\1581417322304.png)

```java
/*
	1.选定最大值区域，填装首值或任意值
	2.遍历数组，若当前选定值 大于 当前最大值，最大值区域填装当前值
	3.遍历数组结束，最大值即被选出
*/
int max = arr[0];
for(int i = 0;i < arr.length;i++)
{
    if(arr[i] > max)
        max = arr[i];
}
/* 最终max为遍历后的最大值 */
```

## 选择排序



![1581417631813](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\1581417631813.png)

```java
/*
	SelectSort：
	- 外层循环遍历选定待比较元素
	- 内层循环遍历选定除待比较元素外的参考元素群
*/
for(int i = 0;i < arr.length - 1;i++)
{
    for(int j = i+1;j < arr.length - 1;j++)
    {
        if(arr[i] > arr[j])
        {
            /* swap values */
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
}

```

## 选择排序 [改进]

![1581419366521](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\1581419366521.png)

```java
/*
	SelectSort[Extra]：
	1.创建区域存储参考范围内的最小值及其角标
	2.与最小值进行内容和角标的交换
*/

for(int i = 0;i < arr.length - 1;i++)
{
    //创建区域存储参考范围内的最小值及其角标
    int miniTemp = arr[i];
    int index = i;
    
    /* 遍历参考范围 */
    for(int j = i+1;j < arr.length - 1;j++)
    {
        //求参考范围内的最小值
        if(miniTemp > arr[j])
        {
            miniTemp = arr[j];
            index = j;
        }
    }
    
    //只与最小值进行内容和角标的交换
    swap(arr,i,index);
}

public static void swap(int[] arr,int i,int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```



## 冒泡排序

![1581418609220](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\1581418609220.png)

```java
/*
	Bubble Sort:
	1.外层循环代表被比较轮数 (单次遍历为1轮)
	2.内层循环代表被比较次数 (两值比较为1次)
*/
for(int i = arr.length - 1;i > 0;i--)
{
    for(int j = 0;j < i;j++)
    {
        if(arr[j] > arr[j+1])
        {
            /*swap values*/
            int temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }
    }
}

/* Second Method */
for(int i = 0;i < length - 1;i++)
{
    for(int j = 0;j < length - 1 - i;j++) //第i个值要冒泡(length-1-i)次
    {
        if(arr[j] > arr[j+1])
        {
            /*swap values*/
            int temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }
    }
}
```

==P126==

## 静态代码块：static { }

随着类的加载而执行，在类加载时只执行一次。
用于给类初始化，通常此类中都是静态成员。

==P127==

## 构造代码块：{ }

对象创建几个，构造代码块调用几次。

构造函数是给调用它的对象进行针对性的初始化。
构造代码块是对所有对象进行通用初始化。

### 局部代码块：

限定局部变量的生命周期。

类中的方法都是静态的，因此该类是不需要创建对象的。为了保证其他程序不创建该类对象，可以将该类的构造函数私有化`private`

==P131==

## 单例设计模式：

一个类在内存中只需要一个对象

```
为保证对象的唯一性：
- 不允许外部程序new对象
- 在该类中创建一个本类的实例
- 对外提供访问该唯一对象的方法
```

==P139==

## 覆盖父类方法

重载：同一个类中的同名函数，参数列表不同，与返回值类型无关。

覆盖/重写：子父类中的同名函数，返回值类型和参数列表完全相同。

**子类方法覆盖父类方法时：**

1. **子类权限必须 >= 父类权限(public > 无)，不包含private**
2. **静态内容只能覆盖静态内容，静态内容只能被静态覆盖**

什么时候使用覆写操作？

​    对程序进行升级时，采用继承的方式，添加新功能。

==P141==

## super语句

在子类的构造函数中，第一行有一个默认的隐式语句`super();`，等价于父类的**空参**构造函数。

 子类中所有的构造函数，默认都会访问父类中的**空参**构造函数。

为什么子类初始化要访问父类的构造函数？

​	子类继承父类获取到了父类中的内容，所以在使用父类内容之前，要参考父类是如何对自己的内容进行初始化的。

**如果父类中没有定义空参构造函数，那么子类的构造函数必须用super明确要调用父类哪个构造函数。同时子类构造函数中，如果使用了this()调用了本类构造函数时，super()就没有了，因为super和this都必须定义在第一行。但是可以保证的是，子类中肯定会有其他的构造函数访问到父类构造函数。**

**注意：super语句必须放在子类构造函数的第一行，因为父类初始化要先完成。**

==P143==

## 实例化

```java
class Son Extends Father
{
	int num = 8;
	Son()
	{
		super();
		//父类初始化super();先于子类成员变量的显式初始化
		//此时 num = 0;
        
        //子类构造函数的特定初始化部分
		return;
	}
}
```

### 一个对象的实例化过程：

`Person p = new Person();`

1. JVM读取ClassPath下的Person.class文件，加载进内存，并会先加载Person的父类。
2. 在堆内存中开辟内存空间，分配地址。
3. 在new Person()对象空间中，对对象的属性进行默认初始化。
4. 调用Person()构造函数进行初始化。
5. 在Person()构造函数第一行，先调用父类中的构造函数进行初始化。
6. 父类初始化完毕后，再对子类的属性进行显式初始化。
7. 再继续完成子类构造函数中的特定初始化。
8. 初始化完毕后，将地址值赋值给引用变量p。

==P144==

## 继承

继承弊端：通过覆写方法的方式，可以打破封装性。

### final关键字：

1. final可以修饰类、方法、变量。
2. final修饰的类不可以被继承。
3. final修饰的方法不可以被覆写。
4. final修饰的变量不能被改变，为常量，**final修饰的变量必须显式初始化，final通常与static连用，避免创建对象浪费资源。**

==P146==

## 抽象类的特点：

1. 抽象方法必须定义在抽象类中，该类也必须被`abstract`修饰。
2. 抽象类不可以被实例化。
3. 抽象类必须有其子类覆盖了所有抽象方法后，该子类才可以实例化，否则该子类仍是抽象类。

**抽象方法的定义格式：** `abstract void function();`

==P147==

## 抽象类的细节：

1. 抽象类存在构造函数，用于给子类初始化。
2. 抽象类中可以不定义抽象方法，用于防止该类创建对象。
3. 抽象类不能和哪些关键字共存？
   1. `private`抽象方法必须被子类覆盖
   2. `static`抽象方法被类名调用无意义
   3. `final`抽象方法必须被覆盖，final禁止被覆盖
4. 抽象类和一般类的不同点：一般类中不能定义抽象方法，且一般类可以被实例化。
5. 抽象类一定是一个父类，同时抽象类可以是一个子类。

==P149==

## 接口

当一个抽象类中的方法都是抽象时，可以将该抽象类定义成**接口**。

### 接口中常见的成员：

1. 全局常量：`public static final`
2. 抽象方法：`public abstract`

这些成员都有固定的修饰符，接口中的成员都是公共的权限。

固定修饰符可以被省略，编译时会被自动补充，`int x`在接口`interface`中定义后是个常量。

==P151==

## 多实现：

解决多继承成员函数调用与覆盖的不确定性

```java
interface A
{
    public abstract void function();
}
interface B
{
    public abstract void function();
}
class Test implements A,B
{
	public void function()
	{
	//同时覆盖了A,B中的function
	//抽象方法被实现后，去掉关键字abstract
	}
}

```

1. 函数名相同，参数列表相同，**返回值相同**的两方法不能同时定义，会产生调用的不确定性。
2. 函数名相同，**参数列表不同**，返回值相同的两方法同时定义，被称为重载。
3. 两方法并存的原则是：参数列表不同 or 方法名不同，**返回值**视为方法体内的封装内容，不作为方法辨别的要素。

==P152==

## 多继承

一个类在继承另一个类的同时，还可以实现多个接口。

```java
class Test extends Q implements A,B {}
```

接口与接口之间是**继承**关系，而且可以**多继承**

```java
interface A {}
interface B {}

interface C extends A,B {}
```

==P154==

## 接口和抽象类的区别：

1. 抽象类中可以定义抽象方法和非抽象方法，子类继承后，抽象方法也必须被实现，非抽象方法可以直接使用。
2. 接口中只能定义抽象方法，必须由子类去实现。
3. 抽象类的继承，通常定义体系的基本**共性内容**。
4. 接口的实现，通常定义体系外的**附加功能**。

==P155==

接口类型的引用指向的都是子类对象

==P156==

## 多态：

父类创建的变量指向子类对象`Father x = new Son();`

==P157==

### 多态的使用前提：

1. 父类中包含共性方法，且父类被子类继承。
2. 父类中的共性方法在子类中被覆写。
3. 父类变量指向的子类对象只能调用**共性方法**，限制了特有功能的访问。

==P159==

### 类型转换：

1. **向上转型**的目的是为了限制特有功能的访问。

   `Father x = new Son();`

2. **向下转型**的目的是为了使用子类的特有方法。

   `Son y = (Son)x;`

3. **转型条件：**必须具备继承关系，只对子类对象进行类型变化。

   

当 x 调用父子类中**同名方法**时，运行的是子类方法，因为方法已经被子类覆写。

```java
class Father
{
    Method()
    {
        //Father Method
    }
}
class Son extends Father
{
	Method()
	{
		//Son Method
	}
	Function(){}
}

Class Main
{
 	public static void main(String args[])
 	{
 		Father x = new Son();
		x.Method();
		//此时调用的是Son Method
		//x不能调用Function()
 	}
}
```

==P161==

## 类型判断：instanceof

​	用于判断对象所属类的**关键字**，只能用于引用数据类型判断。
​	通常在向下转型前，加入`if(x instanceof Father)`做判断。

==P162==

## 多态时成员的特点：

1. 成员变量：父类引用变量指向子类对象，引用的属性保持父类属性。

2. 成员函数：父类引用变量指向子类对象，引用的函数保持子类函数。

3. 静态函数：父类引用变量指向子类对象，引用的静态函数保持父类静态函数。

   **成因：**继承时，成员函数会被覆写，但是**成员变量不存在覆写**的说法，父类引用先寻找父类属性。成员函数需要对象调用，但静态函数**被类绑定**，不需要对象调用，因此跟随父类。

   

   静态函数和属性都是跟随类的，因此保持和父类一致。

   成员函数可以被子类覆写，因此保持和子类一致。

==P165==

## 内部类：

​	内部类定义在外部类中，编译后会生成`Outer$Inner.class`文件。

内部类的访问特点：

1. 内部类可以直接访问外部类的成员。
2. 外部类要访问内部类，必须建立内部类的对象。

==P166==

直接访问外部类中的内部类成员：
`Outer.Inner in = new Outer().new Inner();`

如果内部类是静态的，相当于一个内部类。
`Outer.Inner in = new Outer.Inner();`
`class Outer{ static class Inner{} }`

直接调用静态内部类中的静态函数：
`Outer.Inner.function();`

如果内部类中定义了静态成员，该内部类必须被`static`修饰。

内部类可以定义在局部位置上，如果此时内部类调用了局部变量，该变量必须被`final`修饰。

==P169==

## 匿名内部类：

​	内部类的简写格式，前提是该匿名类必须**继承外部类**或**实现外部接口**。

```JAVA
abstract class Untitle
{
    public abstract void function();
}

class Outer
{
    //全称
    class Inner extends Untitle
    {
        public void function()
        {
            //实现内容
        }
    }
    
    public void method()
    {
		//new Inner().function();
        
        //简写
        new Untitle()
        {
            public void function()
            {
                //实现内容
            }
        }.function();       
    }
}

```

==P170==

## 匿名内部类的引用变量：

```java
abstract class Untitle
{
    public abstract void function1();
    public abstract void function2();
}

class Outer
{
    //全称
    class Inner extends Untitle
    {
        public void function1()
        {
            //实现内容
        }
        public void function2()
        {
            //实现内容
        }
    }
    
    public void method()
    {
		//new Inner().function();
        
        //简写
        //匿名内部类指向给引用变量u
        Untitle u = new Untitle()
        {
            public void function1()
            {
                //实现内容
            }
            public void function2()
            {
                //实现内容
            }
            public void function3()
            {
                //实现内容
            }
        }
        
        //同一个匿名内部类对象，调用两个不同的方法
        u.function1();
        u.function2();
        //不能调用function3()
        //因为u为多态向上转型，父类中无function3()
    }
}
```

### 使用场景：

​	当函数**参数是接口类型**时，且接口中的方法不过多，可以用匿名内部类作为实际参数传递。 

```java
abstract class Untitle
{
    public abstract void function1();
    public abstract void function2();
}

class Main
{
    public static void main(String args[])
    {
        //参数传递
        Method(new Untitle()
        {
         public void function1(){}
         public void function2(){}
        });
    }

    //参数是接口类型
    public static void Method(Untitle u){}
}
```

==P172复习==

## 创建对象的顺序：

1. 父类构造器初始化
2. 显式初始化
3. 构造代码块初始化
4. 子类构造函数特有初始化

==P176==

## 自定义异常

```java
class NameException extends Exception
{
	NameException(){}					   // 构造函数
}

class Main
{
    void Method() throws NameException {}	// 定义处
    
    public static void main(String[] args) throws NameException
    {
        Method();						 // 调用处
    }
}

```



==P177==

## 异常的分类

1. **编译时被检测异常**：Exception及其子类，除RuntimeException外。

   ​								只要异常没处理，会导致编译失败。

   ​								这种异常都可以在编译前针对性处理。

   ​								

   ​								需要被抛出`void Method() throws RuntimeException {}`

   ​								抛出是为了进行捕捉**集中处理**

2. **编译时不检测异常(运行时异常)**：Exception中RuntimeException和其子类。

   ​													可以通过编译，异常在运行时抛出。

   ​													这种问题一般不处理，在运行时强制终止。

   

   ​													不需要被`throws`抛出，需要手动修正程序。

   

   `RuntimeException `是在Java虚拟机**正常运行**期间抛出的异常超类。

   `Error` 				  是在虚拟机不正常运行时，产生的错误。

   

- 自定义异常时，要么继承`Exception`，要么继承`RuntimeException`。



### throw 和 throws 区别

1. throws 使用在函数名称定义处。

   throw   使用在函数内部。

2. throws 抛出的时异常**类**，可以抛出多个，用逗号隔开。

   throw   抛出的是异常**对象**。



- 一个函数只能**引发**一个异常，异常引发后，函数即出栈，可能会导致`return`语句不执行。

  

==P178==

## 异常捕捉：try & catch

​				   对异常进行针对性处理的方式

```java
//以下三个是一个整体
try
{
    /* 需要被检测异常的代码 */
}
catch(异常类 变量)// 该变量用于接收发生的异常对象
{
    /* 处理异常的代码      */
}
finally
{
    /* 一定会被执行的代码  */
}
```

### 什么时候`try`，什么时候`throws` ？

发生的异常可以处理时，用`try{}`
发生的异常无法处理时，在外部`throws`

- `catch(NameException e)`中的对象e，是通过`try`语句传入的。
- JVM的默认异常处理机制`e.printStackTrace()`：用于追踪异常信息。



==P179==

## 多 catch 的情况：

当一个函数外部`throws`多个异常时，需要多个`catch(Exception e)`来接收对象。

- 多个`catch()`在排序时，要把父类`catch`排在后面

==P180总结==

## 异常处理的基本原则：

1. 函数**内部**如果**抛出**需要检测的异常，那么函数名称定义处必须要`throws`，或者在函数内部`try&catch`捕捉，否则编译失败。
2. 如果**调用**到了**声明异常**的函数，那么**调用处**函数名称定义处必须要`throws`，或者在函数内部`try&catch`捕捉，否则编译失败。

==P181==

## finally：

​	`finally { }`是一定会被执行的代码，用于填装无论是否发生异常都一定要执行的内容，通常用于关闭(释放)资源，如断开数据库连接。

```java
/*
 try & finally 组合
 	
 	- 适用情形：
 		发生的异常不准备在本函数内处理
 		但必须在本函数内释放资源时其中try & finally组合。
 	- 注意：
 		无 catch(Exception e) { } 语句即视为异常未处理
 		必须在函数名定义处用 throws 抛出	
*/
void Method() throws Exception
{
	try
	{
		//开启资源
		throw new Exception();
	}
	finally
	{
		//关闭资源
	}
}
```

==P182==

## 异常转换：

```java
/*
	在处理A异常后，抛出B异常。
*/
catch(AException e)
{
    //处理A异常
    throw new BException();
}
```

==P183==

## 异常注意事项：

1. 子类覆写父类方法时，父类方法如果抛出了异常。
   那么子类覆写方法只能抛出父类的异常，或者抛出该异常的子类异常。
2. 如果父类方法抛出多个异常，那么子类异常只能抛出父类异常的子集。
3. 如果父类方法没有抛出异常，那么子类方法覆写时，绝对不能抛出异常。

==P184==

## Object 类的 `boolean equals(Object obj)` 方法：

- 作用：        当且仅当 p1 和 p2 指向同一个对象时，该方法返回 TRUE
- 调用格式：`p1.equals(p2);`

==P185==

通常为了判断对象的特有内容，会覆写`equals(Object obj)`方法

```java
public boolean equals(Object obj)
{
    if(!(obj instanceof Person))
    {
        throw new CastClassException("传入类型不可判断");
    }
    
    /* 类型强制转换，使用私有内容 */
    Person p = (Person)obj;
    return this.age == p.age;
}
```



## 分析堆栈轨迹

```java
// 1，创建一个 Throwable 实例 t
Throwable t = new Throwable();

// 2，getStackTrace() 属于 t 的一个成员函数
// 3，数组用于接收堆栈轨迹查询结果
StackTraceElement[] frames = t.getStackTrace();

// 4，遍历数组：f为本次分析的对象，frames为整个List的区间
for(StackTraceElement f : frames)
{
    /* analyze f */
    // System.out.println(f);
}
```

==P186==

## hashCode() 方法覆写

当`equals()`方法被重写时，通常有必要重写`hashCode()`方法，以维护`hashCode()`方法的常规协定，该协定声明**相等的对象必须具有相等的哈希码**。

==P187==

## getClass() 方法

 获得`.class`文件类型

==P195==

## 包 Package

包在文件系统中的体现就是 **文件夹**。

1. 类名的全程是 ：`包名.类名`
2. 包**创建**必须写在代码第一行 `line 1: package FolderName;`
3. 编译时自动创建包路径：`javac -d <path> test.java`

==P190==

## 包与包之间的访问 ：protected

**注意：**

1. 新建对象时   `packName.className obj = new packName.className();`

2. 定义在包内的**类**想要被访问时，类名必须被`public`修饰

3. 定义在类中的**方法**想要被访问时，方法名必须被`public`修饰

   **默认权限视为被封装 !**

**总结：包与包之间的类进行访问，被访问的包中的类必须是 public ，被访问的包中的类的方法也必须是 public 。**



==不同包之间的类进行继承：==

`protected`：给不同包中的子类使用。

​					1，被此关键字修饰的方法，在被外包访问时，不可直接调用。
​					2，必须通过**继承**才能访问。

​													<访问权限表>

|          | public | protected | default | private |
| -------- | ------ | --------- | ------- | ------- |
| 同一类中 | ok     | ok        | ok      | ok      |
| 同一包中 | ok     | ok        | ok      |         |
| 子类中   | ok     | ok        | -       | -       |
| 不同包中 | ok     | -         | -       | -       |



==P191==

## 包的导入 import

**注意：**`import`导入的是包中的类，不是包中的包。
		   `import`的主要作用是 **简化类名的书写** 。

```java
package FolderName;		// 必须放在第 1 行
import FolderA.classA;	// 导入 FolderA 包中的 classA 类
import FolderA.*	    // 导入 FolderA 包中的全部类

// 1，以往的对象创建方式
FolderA.classA obj = new FolderA.classA();
// 2，导入包后，可以简化成
classA obj = new classA();

```

**包的导入原则：**用到哪个类就导入哪个类，不建议使用 " .* "。



==P192==

## Jar 包

Jar：java的压缩包。

注意：Jar 包可以直接访问，等同于上一级目录。



==P189==

## 多线程

**进程：**正在进行中的程序。

**线程：**进程中一个负责程序执行的执行路径。

**多线程：**一个进程中可以有多条执行路径，称为多线程。

==P199==

## 多线程创建的方式

1. 定义继承`Thread`的类`class ThreadTest`，并在类中覆写`run()`方法。
2. 线程中要运行的任务，定义在覆写的`run()`方法中。
3. 在主函数中创建`ThreadTest`对象`t0`，并用其调用`t0.start()`方法，开启线程。

==P203==

## 多线程的第二种创建方式

引出：当某类存在父类时，不能再`extends Thread`。

1. 实现`Runnable`接口，覆盖`run()`方法：`class Test implements Runnable`

2. 创建`Test`类对象：`Test obj = new Test();`

3. 创建`Thread`类对象，并将`obj`作为参数传入构造函数：

   `Thread t0 = new Thread(obj);`

4. 开启线程：`t0.start();`

==P208==

## 多线程安全问题产生的原因

1. 多个线程在操作共享数据
2. 操作共享数据的线程代码有多条

当一个线程在执行操作共享数据的多条代码过程中，其他线程参与了运算，就会导致线程安全问题的产生。

==P209==

## 解决安全问题：同步代码块

解决思路：
1，将多条操作共享数据的线程代码封装起来，当有线程在执行这些代码的时候，其他线程不可以参与运算。
2，必须要当前线程将这些代码执行完毕后，其他线程才可以参与运算。

**应用同步代码块，封装多行代码。**

```java
synchronized(obj)
{
    // line-0
    // line-1
}
```

 **同步的前提：**

- 同步中必须有多个线程并使用同一个锁
- 即`synchronized(obj)`要使用同一个对象。

==P210==

## 同步函数

格式：`public synchronized void functhion(void){}`

**同步函数的锁：**

同步函数和同步代码块的区别：
1，同步函数的锁是固定的`this`
2，同步代码块的锁是任意的对象

建议使用同步代码块

==P214==

## 静态同步函数的锁

`public static synchronized void function(void){}`

静态函数的锁是 **调用该静态同步函数的类** 的字节码文件对象

获取字节码文件对象的方式：
1，`obj.getClass()`返回值
2，`Object.class`的值

==P216==

## 死锁

- 死锁的体现形式之一是**同步的嵌套**

```java
 if(flag)
 {
     synchronized(MyLock.lockA)
     {
         System.out.println(" if...lockA...");
         synchronized(MyLock.lockB)
         {
             System.out.println(" if...lockB...");
         }
     }
 }
else
{
    synchronized(MyLock.lockB)
    {
        System.out.println(" else...lockB...");
        synchronized(MyLock.lockA)
        {
            System.out.println(" else...lockA...");
        }
    }

}
```

- 线程-1 外部拿到 lockA ，内部拿不到 lockB 。

- 线程-2 外部拿到 lockB ，内部拿不到 lockA 。

- 两线程在争夺过程中产生了 **死锁**

  

## 线程间的通信

多个线程在处理同一资源，但是任务不同

```java
class Input implements Runnable
{
    Resource r;    
    Input(Resource r)
    {
    	this.r = r;
    }
    public void run()
    {
      synchronized(r)
      {
        r.name = "";
        r.sex = "";
      }
    }
}

class Output implements Runnable
{
    Resource r;   
    Output(Resource r)
    {
    	this.r = r;
    }
    public void run()
    {
        while(true)
        {
        	synchronized(r)
            {
            	System.out.println(r.name + "..." + r.sex);
            }
        }
    }
}
```

- Input 和 Output 线程应该通过**线程间的通信**共用一个 Resource 对象

- Input 和 Output 线程同步代码块应该用相同且唯一的锁：Resource r

  

## 等待唤醒机制

涉及的方法：

1. `wait()`：让线程处于冻结状态，被 wait 的线程被存储在**线程池**中
2. `notify()`：唤醒线程池中的一个线程(无序任意)
3. `notifyAll()`：唤醒线程池中的所有线程

- 这些方法必须都定义在**同步**中

  因为这些方法是用于操作线程状态的方法

  必须要明确到底操作的是**哪个锁**上的线程

```java
synchronized(obj)
{
	obj.wait();
	obj.notify();
	obj.notifyAll();
}
```

- 以上方法只应由作为此对象监视器的所有者的线程来调用

  监视器：同步函数的锁 obj

  `wait()`被 obj 调用，该线程就被存储在 obj 的**线程池**当中

为什么操作线程的方法`wait()、notify()、notifyAll()`都被定义在 Object 类中？
      因为这些方法都是**监视器**的方法，监视器就是锁。
      锁可以是**任意的对象**，任意对象调用的方法一定定义在 Object 类中。



## 多线程-多生产多消费问题

`if(falg)`：线程唤醒后只能单次判断该锁，会造成数据错误

`while(falg)`：线程唤醒后会**重复**判断该锁

`notify`：容易唤醒同向线程，造成死锁

`notifyAll`：通过唤醒所有线程的方式，强制唤醒对向线程

```JAVA
public synchronized void set(String name)
{
    while(flag)
        try{this.wait();}catch(InterruptedException e){}

    this.name = name + count;
    count++;
    System.out.println("...Producer......."+this.name);
    flag = true;
    notifyAll();
}

public synchronized void out()
{
    while(!flag)
        try{this.wait();}catch(InterruptedException e){}
    System.out.println("...Consumer..."+this.name);       
    flag = false;
    notifyAll();   
}
```



## Lock对象-锁的操作

- 同步代码块`synchronized(obj){}`对于锁的操作是隐式的

- Lock 是接口，可以通过多态的方式建立Lock对象

- 获取锁：`lock.lock();`

- 释放锁：`lock.unlock();`

- 为防止代码中抛出异常，释放锁动作`lock.unlock();`应放在`finally{}`代码块中。

  

每个 Lock 可以定义多组 Condition 对象

- `Condition c1/c2 = lock.newCondition();`

- 可以通过`c1.await() / c2.signal()`和`c2.await() / c1.signal()`的方式实现仅唤醒对向线程，代替`notifyAll()`

  

## wait 和 sleep 的区别

1. wait 可以指定时间，也可以不指定，可以保持一直等待。
   sleep 必须指定睡眠时间，时间到以后必须被唤醒。

2. 在同步中，对 CPU 的执行权和锁的处理不同。

   wait ：释放执行权，释放锁。

   sleep：释放执行权，不释放锁。

- `synchronized`同步中可以同时**激活**多个线程，但是只能**运行持有锁**的那一个线程

  

## 停止线程

1. `stop()`方法，[有隐患]。
2. `run()`方法结束。
   在`run()`方法内的**控制循环**上添加`flag`，促使循环结束。

- `t0.interrupt()`方法强制将线程从冻结状态恢复到运行状态，让线程具备CPU的执行资格，同时抛出 InterruptedException 异常。

  ```java
  /*
  #隐患：
  	t0 t1 同时被 wait() 函数冻结后，无法通过更改 flag 停止线程。
  
  #解决方案：
  	通过 interrupt() 函数唤醒 t0 t1 线程，并在捕捉抛出异常的同时，再次通过更改 flag 的方式终止线程。
  */
  
  public synchronized void run()
  {
    while(flag)
    {
          try
          {
              wait();//t0 t1
          }
          catch(InterruptedException e)
          {
              flag = false;
          }
    }  
  }
  
  t0.interrupt();
  t1.interrupt();
  ```



## 守护线程

`t0.setDaemon()`：t0 被设置为守护线程(后台线程)。

- 普通线程需要手动结束。
- 守护线程在前台线程均结束后，自动结束。



## 多线程 join() 方法

`t1.join()`

- 临时加入一个线程运算时可以使用 join 方法。
- 哪一个线程执行到`t1.join()`，哪个线程就释放，并立即执行 t1 线程至完毕。

`Thread.yield()`
    **暂停**当前正在执行的线程对象，并执行其他线程。

**线程组**
	将多个线程封装成同一组后，可以对同组线程进行`interrupt()`等操作。

==P232==

## 匿名内部类创建线程

```JAVA
class test
{
    public static void main(String[] args) 
    {
        /* Thread 线程 */
        new Thread()
        {
            public void run()
            {
                for(int x=0; x<50; x++)
                {
                    System.out.println("Thread" + x);
                }
            }
        }.start(); 
        
		/* 主线程 */
        for(int x=0; x<50; x++)
        {
            System.out.println("main" + x);
        }

        /* Runnable 线程 */
        Runnable r = new Runnable()
        {
            public void run()
            {
                for(int x=0; x <50; x++)
                {
                    System.out.println("Runnable" + x);
                }
            }
        };

        new Thread(r).start();

    }
}
```

**复合匿名内部类**

```JAVA
class test
{
    public static void main(String[] args)
    {
        /* 父类：优先级最低 */
        new Thread(new Runnable()
        {
            public void run()
            {
                /* 任务：优先级其次 */
                System.out.println("runnable run");
            }
        })
        {
            public void run()
            {
                /* 子类：优先级最高 */
                System.out.println("subThread run");
            }
        }.start();
    }
}
```



==P233==

## 常用对象API：String类

- 字符串对象一旦被初始化后就不会被改变
- 相同字符串被存储在字符串常量池中，可重复利用
  `String s1 = “test”`
  `String s2 = “test”`
  `s1 == s2`为 `true`
- String类中覆写了`equals()`方法，作用为比较字符串内容
  `String s1 = “test”`
  创建一个字符串对象在常量池中
  `String s2 = new String(“test”)`
  创建两个对象，1个new、1个字符串对象均在对内存中
  `s1 == s2`为 `false`
  `s1.equals(s2)`为`true`

==P234==

## String类构造方法

 
