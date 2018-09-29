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
1. 
