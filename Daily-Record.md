# 2018/9/11

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

# 2018/09/12
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
