## 泛型简介
1. 泛型可以参数化类型,这个能力使我们可以定义泛型类型的类或者方法，随后编译器会用具体的类型代替它。
```
	public class Box<T>
	{
	  private T object;
	  public void set(T object) { this.object = object; }
	  public T get() { return object; }
	}
	
	Box<Integer> integerBox = new Box<Integer>();
	Box<Double> doubleBox = new Box<Double>();
```

2. 泛型方法: 在返回类型前加上要泛型的类型
```
public static <K,V> boolean compare(Pair<K,V> p1, Pair<K,V> p2)
```

## 异常
1. 异常分两种：
    1. 编译时被检测异常
        1. Exception及其子类异常，除RuntimeException及其子类外
        2. 这种问题一旦出现，希望在编译时就得到检测，并得到对应的处理方式
        3. 这样的问题都可以针对的进行处理
    2. 编译时不检测异常-运行时异常
        1. RuntimeException及其子类
        2. 这种问题的发生，无法让功能继续运算，更过是调用者的原因导致的，或者由内部状态该表导致
        3. 这样的问题一般不处理，直接编译通过，在运行时，让调用者调用时的程序强制停止，让调用者对代码进行修正

        * 编译器并不检测RuntimeException，因此触发RuntimeException异常的函数可以不标注throws
2. 如果让一个类成为异常类，必须要继承“异常体系”
    1. 只有成为异常体系的子类才具有可抛性，才可以被两个关键字所操作(throw、throws)
    2. 自定义异常时，要么继承Exception，要么继承RuntimeException
3. Java编译器先检查语法错误，再检查简单的逻辑错误，再检查其他错误(如：异常)
4. throw 和 throws的区别
    1. throws
        1. 作用在函数上
        2. 抛出的是异常类，可以抛出多个，用“，”分隔开
    2. throw
        1. 使用在函数内
        2. 抛出的是异常对象
5. try-catch-finally代码块
```
    try
    {
      // 需要被检测异常的代码段
    }

    catch(异常类 变量)// 该变量用来接收发生异常的对象
    {
      // 处理异常的代码
    }

    finally
    {
      // 一定会被执行的代码
    }
```

* try一定要和catch一同配合使用，不可以省略catch，以确保异常得到处理

6. 什么时候用try-catch，什么时候用throws
    1. 当异常可以内部解决时，采用try-catch
    2. 当异常不能内部解决时，采用throws
7. JVM默认异常处理机制就是调用`ex.printStackTrace();`

8. 多catch情况：一定要把父类catch情况放在最下面
    * 如果catch不能解决当前抛出的异常，可以选择在catch模块中继续抛出异常，此时需要在该try-catch模块的外层函数外继续声明`throws <二次抛出异常名>`

9. 异常处理原则
    1. 函数内容包含了需要检测的异常:(1) 函数上必须要声明 or (2) 在内部用try-catch捕捉，否则编译失败
    2. 如果调用了声明异常的函数，要么try-catch要么throws，否则编译失败
    3. 一个功能如果抛出多个异常，那么调用该功能时候，必须有对应多个catch进行针对性的处理。内部有几个需要检测的异常，就抛出几个异常。抛出几个异常，就catch几个异常。

10. finally模块
    1. finally语句的应用:通常用于释放资源
        1. 连接数据库
        2. 查询，出现Exception
        3. 关闭连接，finally设置关闭数据库
    2. `return;`语句并不能阻止`finally`代码段运行
    3. `System.exit(0);`关闭了JVM，因此可以阻止`finally`代码段运行
    4. try-finally代码组合：异常无法直接catch处理，但是资源需要关闭
    ```
        void method() throws Exception
        {
            try
            {
                throw new Exception();
            }

            finally
            {
                // 关闭资源
            }
        }
    ```

11. 异常的注意事项：
    1. 子类在覆盖父类方法时，如果父类方法抛出了异常。那么子类的方法只能抛出与父类相同的异常，或抛出该异常的子类异常。也可以选择不抛出异常。
    2. 如果父类的方法没有抛出异常，那么子类在覆盖时，绝对不能抛出异常。
        * 如果子类覆盖方法中触发了异常，那么只能采用try-catch不能抛出

## Object类及其方法
1. Object：所有类的根类
    * Object是不断抽取而来的，具备所有对象都具备的共性内容。

### 常用的共性内容：
1. `equals()`方法
  1. 参数为Object类型：`equals(Object o)`
  2. 一般都会覆盖此方法，根据对象的特有内容，建立判断对象是否相同的依据
  3. 比较两对象时和`p1 == p2`相同，比较的的是两变量的地址
2. `hashCode()`方法
    1. 两个对象相同的依据：两个对象的哈希值相同，并且两个对象的内容相同
    2. 重写该方法后，可以返回该对象对应的任意数据域
    ```
     public int hashCode()
    {
        return this.age;
    }

    System.out.println(p1.hashCode());
    // 此处显示p1的age值
    ```

3. `getClass()`方法：返回当前对象所属的字节码文件-类名
4. `toString()`方法：建议重写，建立特有内容

## 包 package 简介
1. 对同名类文件进行分类管理
2. 给类提供多层命名空间
3. 包在代码中的定义方式：`package mypack;`
    * 写在程序文件的第一行
4. 类名的全称是`PackageName.ClassName`
5. 包也是一种封装形式
6. 包以文件夹的形式体现

7. 在终端中编译：
	1. 在当前目录下将`.class`文件放入包中：`javac -d . test.java`
	2. 此时生成的`test.class`就放置在写在`test.java`内的包文件夹中
8. 在终端中运行：
	1. 格式：`java mypack.test`
	2. 多个包叠加格式：`java pack1.pack2.pack3.test`
## 包与包之间的访问
1. 在当前包下根据类名找源文件名
2. 自动生成class文件的条件：
	* 保证要用的源文件不存在的情况下，该源文件有和类名称相同的源文件名 
3. test这个类已经有所属的包，所以必须明确其包名`packName.test`
4. 当两个包不在同一路径下时，事先设定在终端设定`set classpath = C:\myclasspath`
5. 包与包之间进行类访问，被访问的包中的类必须是public，被访问的类中的方法也必须是public
6. 不同包中的类是否可以继承
7. 在主包中创建Bpack对象时，并不能拿到method()方法，只有通过继承才能拿到该方法
```
	package packB;
	public class Bpack
	{
		protected void method()
		{
			System.out.println("只有Bpack类的子类可以调用此方法");
		}
	}
	
	// Untitled extends packB.Bpack
	
	Untitled u = new Untitled();
	packB.Bpack b = new packB.Bpack();
	
	u.method();// 如果是protected，只能通过此方式调用method
	
	b.method();// 如果是protected，此方式调用method无效
```

8. Java中的访问权限介绍

       | public | protected | default | private
------ | ------ | --------- | ------- | -------
同一类中 | ok | ok | ok | ok |
同一包中 | ok | ok | ok | 
子类中 | ok | ok |
不同包中 | ok |

## import 包的导入
1. `import packa.test;` 只导入test类
2. `import packa.*;`应用通配符导packa包中的全部类
	1. 此方案只导入包中的类，不导入包中的包
	2. 导入包的原则，用到哪个类就导入哪个类，不建议全部导入
3. 一个`.java`文件中只能有一个`pacakage`语句放在第一行，可以有多个`import`

## Jar：java的压缩包
1. 终端命令格式
	1. 压缩`jar -cf jarName.jar packName`
	2. 解压缩`jar -xvf jarName.jar`
2. Jar包的直接使用
	1. `set classpath = ./jarName.jar`将classpath设定为当前目录下的jar包
	2. `java mypack.test`就可以用java虚拟机直接调用了
	3. 此方法适用于调用一下封装好API的jar包


## 多线程
1. 进程：正在进行中的程序，
2. 线程：就是进程中的一个负责程序执行的控制单元
    * 一个进程中可以有多个执行路径，称为多线程
3. 一个进程当中至少要有一个线程
4. 开启多线程是为了同时运行多部分代码
5. 每一个线程都有自己要运行的内容，称为该线程的任务


