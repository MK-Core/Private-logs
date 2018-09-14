## Java输入输出流

```
  import java.util.*;
  public class Untitled
  {
      public static void main(String[] args)
      {
          System.out.println("please input something");
          Scanner x = new Scanner(System.in);
          String s = x.nextLine();
          System.out.println("normal running" + s);
      }
  }
```

## 数组定义与赋初值的方法

1. for循环

2. `int [] nums = {0,1,2,3,4,5,6,7,8,9};`

3. `int [] nums = new int[]{0,1,2,3,4,5,6,7,8,9};`

## 二分查找

```
// BinarySearch Practice
class BinarySearch
{
    public static int search(int[] num,int target)
    {
        int head = 0;
        int tail = num.length;
        while(head < tail)
        {
            int m = (tail - 1)/2 + 1;// find the middle point
            if(target == num[m])
            {
                return m;
            }
            else if(target > num[m])
            {
                head = m + 1;
            }
            else
            {
                tail = m - 1;
            }
        }
        return -1;
    }
}
```
3. windows终端清屏方法：cls



## 二分查找



```

// BinarySearch Practice

class BinarySearch

{

    public static int search(int[] num,int target)

    {

        int head = 0;

        int tail = num.length;

        while(head < tail)

        {

            int m = (tail - 1)/2 + 1;// find the middle point

            if(target == num[m])

            {

                return m;

            }

            else if(target > num[m])

            {

                head = m + 1;

            }

            else

            {

                tail = m - 1;

            }

        }

        return -1;

    }

}

```

3. windows终端清屏方法：cls

## 异常
1. try-throw-catch 模板
```
    import java.util.*;
    public class test
    {
        public static int quotient(int number1,int number2)
        {
            if(number2 == 0)
                throw new ArithmeticException("Divisor cannot be zero");// 此条 抛出异常
                /*
                    抛出异常
                    就是在异常类中创建一个对象
                    期中ArithmeticException()是该对象的构造方法
                    
                    当异常被抛出，正常的执行流程被中断
                        
                    异常的抛出方式
                        异常可以通过try中的throw语句抛出
                        异常也可以通过try中调用的方法简介抛出异常
                */
                return number1 / number2;
        }
        public static void main(String[] args)
        {
            Scanner in = new Scanner(System.in);
            System.out.println("Enter two integers");
            int number1 = in.nextInt();
            int number2 = in.nextInt();
            /*
                异常的的调用语句包含了try和catch两块

                try块下：包含了正常执行的代码
                catch块下：异常被catch所捕获，catch块中的代码用以处理异常

                * catch块执行结束后，执行catch块后的语句

                throw语句的调用方法类似于方法的调用
                过程为：
                    1. 先执行try块下正常执行的代码
                    2. 触发异常，调用throw语句，通过构造函数创建异常对象
                    3. 调用catch块，块内异常处理语句运行
                    4. catch块结束后不返回至throw语句，而是执行catch块后的语句

                catch块的参数-"异常类型名称 ex"
                    其中：ex之前的类型指定了catch块可以捕捉的异常类型
            */
            try
            {
                int result = quotient(number1,number2);
                System.out.println(number1 + "/" + number2 + " is " + result);
            }
            catch (ArithmeticException ex)
            {
                System.out.println("Exception: an integer " + "cannot be divide by zero");
                //System.out.println(ex.getMessage());
            }

            System.out.println("Excution continues ...");
        }
    }
```

3. 异常处理最根本的优势就是：将检测错误从处理错误中分离出来
4. 技巧： `input.nextLine();`单独放在一行用以丢弃当前输入行，便于键入回车键更换新行

5. 思考 ?
    1. `System.out.println("changed" + 1/0);`抛出异常
    2. `System.out.println("changed" + 1.5/0);`不会抛出异常,得到Infinity

6. `ex.getMessage()`放在`System.out.println("...")`内，用以重复异常构造函数内的字符串内容

## 异常类型
1. 系统错误：用Error类表示，由Java虚拟机抛出
2. 异常 Exception：可以被程序捕获和处理
3. 运行时异常：用RuntimeException类表示，通常由Java虚拟机抛出，是Exception类的子类
    1. 免检异常：Error类和RuntimeException类异常都是免检异常
    2. 必检异常：意味着编译器会强制程序员检查，并通过try-catch块处理它们
4. 注意：父类不能强制转换成子类，子类可以强制转换成父类

## 异常处理模型
```
    method1()
    {
        // 2.捕获异常
        try
        {
            //调用 method2;
        }
        catch (Exception ex)
        {
            Process exception;
        }
    }

    method2() throws Exception// 1.声明异常
    {
        if (//故障条件)
        {
            throw new Exception();// 3.抛出异常
        }
    }
```
1. 声明一个异常
    1. 每个方法都必须声明它可能抛出的必检异常类型，这称为声明异常
    2. 任何代码都可能发生“系统错误和运行时错误”，因此Error和RuntimeException异常不必显式声明
    3. 声明格式：`public void method() throws Exception1,Exception2,..`
2. 抛出一个异常
    1. 检测到错误的程序可以创建一个合适的异常类型的对象并且抛出它，这称为抛出异常
    2. 抛出格式`throw new Exception("some message");`
    3. Java的每个异常类至少有两个构造方法
        1. 一个无参数构造方法
        2. 一个参数为`String`类型的构造方法
3. 捕获一个异常
    1. 如果在执行try块的过程中没有出现过异常，则会跳过catch子句
    2. 如果try块中的某条语句抛出一个异常，Java就会跳过try中的剩余语句，去处理异常
        * 内部嵌套函数触发的异常如果不能被内部catch抓取，可以被调用者-外部函数的catch抓取，从而解决。如果在调用链下，异常适中不能被抓取，会报错。

    * 注意事项： 
        1. 如果一个catch块可以捕捉父类异常，那么该catch也可以捕捉其所有子类异常
        2. catch块中设置异常的抓取顺序很重要，如果父类异常catch块出现在子类异常catch块之前，就会发生错误
        3. Java强迫程序员处理必检异常(1.Error 2.Runtime Exception)
            1. 如果在try内触发了必检异常
            2. 那么必须在catch中捕捉该必检异常
            3. 或者必须在try外函数名后声明`throws`该异常
        ```
        // 方案1 catch中捕捉必检异常
        void p1()
        {
            try
            {
                p2();// 触发必检异常
            }
            catch(必检异常 ex)
            {
                //...
            }
        }

        // 方案2 函数名后声明必检异常
        void p1() throws 必检异常
        {
            try
            {
                p2();//触发必检异常
            }
            catch(必检异常 ex)
            {
                //...
            }
        }
        ```

    3. catch块处理多个异常参数时：
    ```
        catch(Exception1|Exception2|...|Exceptionk ex)
        {
            //Same code for handling these exceptions
        }
    ```

## 从异常中获取信息
* 可以通过调用一些异常类的成员函数，使异常信息显示的更完整

## 异常运行顺序
```
    try
    {
        statement1;
        statement2;// 此条触发异常
        statement3;// 此条不再运行
    }
    catch(Exception)
    {
        //dealing with Exception
    }

    statement4;// 如果异常未被捕获，则不执行此条
```

## finally子句
1. 在任何情况下`finally`块中的代码都会执行
2. `finally`块不会被try块中的异常触发屏蔽
3. `finally`块不会因为异常没有被捕捉到而被屏蔽
4. 即使在`finally`块前有一个`return`语句，`finally`块仍然执行
5. 格式：
```
    finally
    {
        finalStatements;
    }
```

## 何时使用异常
1. 一个项目中多个类都会发生的共同异常应该考虑作为一个异常类
2. 对于发生在个别方法中的简单错误最好进行局部处理，无需抛出异常
3. 当必须处理不可预料的错误情况时使用`try-catch`块，不要用它处理简单的、可预料的情况

## 重新抛出异常
* 如果异常处理器并不能处理一个异常，或者只是简单的希望它的调用者注意到该异常，Java允许该异常处理器重新抛出异常
```
try
{
    statements;
}
catch (TheException ex)
{
    perform operations before exits;

    throw ex;// 此处重新抛出异常
}
```

## 链式异常
```
import java.util.*;

public class ExceptionChains
{
  public static void main(String[] args)
  {
    try
    {
      method1();
    }
    catch (Exception ex)
    {
      ex.printStackTrace();
    }
  }

  public static void method1() throws Exception
  {
    try
    {
      method2();
    }
    catch (Exception ex)
    {
      throw new Exception("New info from method1", ex);
      // 注意：新异常在此处被打包
    }
  }

  public static void method2() throws Exception
  {
    throw new Exception("New info from method2");
  }
}
```

1. method2 抛出一个异常，该异常被method1的catch捕获，并被包装成一个新异常
2. 新异常被抛出，并在main方法中catch块中被捕获
3. `printStackTrace()`显示从method1中抛出的新异常，然后显示从method2中抛出的原始异常

## 创建自定义异常类
1. Java定义了相当多的异常类，尽量使用它们而不要自定义新异常类
2. 自定义异常类往往继承已有的Java原生异常类

## File 类
1. 绝对文件名：由文件名和它的完整路径以及驱动器字母组成
2. 相对文件名：完整目录被忽略，只包括文件名及其后缀

* 注意：
    1. 在Windows中目录的分隔符是反斜线`\`，但是在Java中，反斜线是一个特殊的字符，应该写成`\\`的格式
    2. 创建一个File对象并不会在机器上创建一个文件，不管文件是否存在都可以创建任意文件名的File实例，可以通过`exists()`方法来判断这个文件是否存在
    3. `/`是Java的目录分隔符，这点和UNIX系统是一样的
    4. 在程序中，不要直接使用Windows系统的`绝对文件名`，因为它会造成只能在Windows系统上工作，而不能再其他系统上工作
    5. 通常使用`相对文件名`，为`当前目录下`的文件创建对象

## 文件的输入和输出
* 注意：File对象封装了文件或路径的属性，并不包括创建文件的方法，也不包括从文件中读写数据的方法

1. 使用PrintWritter类向文本文件写入数据
    1. 首先为文本文件创建一个PrintWriter对象`PrintWriter output = new PrintWriter(filename);`
    2. 示例：
    ```
    import java.io.IOException;// 头部声明IO异常
    import java.util.*;

    public class test
    {
        public static void main(String[] args) throws IOException // 抛出IO异常
        {
            java.io.File file = new java.io.File("score.txt");// 创建要新建的文件对象

            if (file.exists())// 判断该同名文件是否已经存在
            {
            System.out.println("File already exists");
            System.exit(1);
            }

            java.io.PrintWriter output = new java.io.PrintWriter(file);// 创建文件输入流对象

            output.print("John T Smith ");
            output.println(90);
            output.print("Eric K Jones ");
            output.println(85);

            output.close();
            /*
            必须使用close()方法关闭文件，
            如果没有使用该方法
            数据就不能正确的保存在文件中
            */
        }
    }
    ```

    3. 使用try-with-resources自动关闭资源
        1. 程序员会经常忘记关闭文件，Java提供了`try-with-resources`机制自动关闭文件
        2. 格式：
        ```
            try (创建PrintWriter对象)
            {
                向File对象内写入信息
            }
        ```

        3. 注意：
            1. try后创建的资源必须是`AutoCloseable`子类型，比如：PrintWriter，具有一个close()方法
            2. 资源的声明和创建必须在同一行语句
            3. 资源的`close()`方法自动调用以关闭资源
2. 使用Scanner类从文件中读取文本数据

