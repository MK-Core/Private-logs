#Java笔记
##Java的第一个程序
1. <pre><code>
	/* 第一个Java程序 */
    public class FirstSample	//class类型
    {
			 public static void main(String[] args)	//静态，空类型，大写，方括号 
			{    
				System.out.println("Welcome to Java !");
			}     
	}
2. 没有「return 0];，想结束程序调用「System.exit(0)」//  0表示程序正常结束 

##注释
1. 以 /* 开始 **/ 结束的可以自动生成文档
2. 注释规则同C++

##数据类型
1. Java「没有」无符号数(unsigned)
2. NaN(Not a number)表示计算的结果不是数字
	1. if(Double.isNaN(var))	// 判断var是否为NaN，NaN的类型为double 
	2. 「不可以」if(var == Double.NaN) // 所有的非数值都不相等 
3. boolean和int之间「不能转换」，boolean只有true和false
4. 0b1001，0b开头可以写二进制数
5. 1_000 数字中可以加“下划线”便于越多，编译器会自动去掉
6. \u00A0 在「注释」中会报错，是“换行”的转义字符
7. c:\users 在「注释」中会报错，因为“\u”后面跟的不是4位16进制数
8. 一定要当心“\u”它会在程序运行到该点之前转化成转义内容，发挥作用

##Unicode
1. 第 1 个代码级别：码点从 U+0000 到 U+FFFF，「基本语言」
2. 其余 16 个代码级别：码点从 U+10000 到 U+10FFFF，「辅助字符，特殊字符」

##变量
1. Java中不区分变量的「声明」和「定义」

##常量
1. final double CM = 2.54; // 常量标志，常量类型，一般大写 
2. <pre><code>
	/* 将常量定义在方法外，供多个方法调用 */
	public class Constants2
	{
		public static final double CM = 2.54; // 注意：前部和方法前部对应 
		public static void main(String[] args)
		{
			System.out.println("The cons is : " + CM);
		}
	}

##运算符
1. public static strictfp void main (String[] args)
	// 标记「strictfp」后该函数按严格计算->有效位缩短->容易移植 
2. x 的 a 次幂：Math.pow(x,a)，根号 x ：Math.sqrt(x,a)
3. 「StrictMath」容易移植->所有平台结果相同，「无Strict」->精度高，计算速度快
4. 在顶部加 import java.lang.Math.*; // 可以省略Math，注意结尾「;」 

##floorMod方法
1. <pre><code>
	/* 这是一个时钟校准程序 */
	public static void main (String[] args)
	{
		int p = 0;
		int ad = 0;
		int y = Math.floorMod(p + ad , 12); // 除数，被除数 
		System.out.println("The result is: " + y);
	}
2. 通常 "%" 取余，被除数若为负数，那么余数也为负数->不符合要求
3. Math.floorMod(被除数,除数) 无论被除数如何，结果为正
4. 若「除数」为负数，那么结果也为负

##数值转换
1. 		   int   (4)  long
	float  double(4)		// 整形转化为浮点型，int转化为double恰好不损失精度 
2. 同为整形，不能逆向转换
3. 给「浮点类型」直接赋「整数」也是没关系的，如：double i = 5;
4.<pre><code>
	/*  「字符」可以直接赋给「整型」和「浮点型」  
	 长度适合可以直接转换，长度不适合只能强制转换 */
	public class FirstSample
	{
		public static void main(String[] args)
		{
			int i = 'A';
			System.out.println((char)(i + 1));		 
		}
	}
	
	/*  「整数」和「浮点数(去小数)也可以直接转化为「字符」 */
	public class FirstSample
	{
		public static void main(String[] args)
		{
			double i = 'A';
			System.out.println((char)(i + 1.25));		 
		}
	}
5. 'a'的unicode比'A'大
6. <pre><code>
	/* 转换「小写字母」为「大写字母」
	public class FirstSample
	{
		public static void main(String[] args)
		{
			char ch = 'c';
			// char m = (char)(ch + ('A'  - 'a')); 
			System.out.println(m);		 
		}
	}
	另一方面说明 char是可以进行运算的 */
	
	
##强制转换
1. 浮点数「强制转化」整型 <pre><code>
	double a = 5.5;
	int b = (int)a; // 去掉小数部分 
2. 四舍五入效果：int b = (int)Math.round(a);

##自增自减
1. int a = 2 * (++m) // 先发生(m+1)，再进行 2*(m+1) 
2. int a = 2 * (m++) // 先发生 2*m，再进行 m = m+1 

##与或逻辑 && ||
---|与|---
---|---|---
0|0|0
1|0|0
0|1|0
1|1|1
		
---|或|---
---|---|---
0|0|0	 
1|0|1	
0|1|1	
1|1|1
1. 短路：(x != 0) && (1/x > x + y) // 在x不为0时，执行后面式子「前面条件不通过，不执行后面」 
2. 成立->执行：if(m != A && m != B) //m既不等于A，也不等于B时「执行if」

---|与|或
---|---|---
短路|有0为0|有1为1	 
成立|全1为1|有1为1
	
##短路
1. 当计算p1 && p2时，先计算p1，如果p1为true再计算p2。如果p1为false，则不计算p2。
2. 当计算p1 || p2时，先计算p1，如果p1为false再计算p2。如果p1为true，则不计算p2

##三元操作符
1. x<y ? x:y; // true返回x,false返回y 

##按位与
1. (0b0001 & 0b0001) / 0b0001 // 「分母」返回"1"所在的位 
2. 1 << 3是指 1000 效果

##枚举类型
1. enum Size{SMALL,MEDIUM,LARGE,EXTRA_LARGE};
2. Size s = Size.MEDIUM;

##字符串类型String
1. <pre><code>
	/* 从字符串中提取一部分 */
	String greeting = "Hello";
	String s = greeting.substring(0,3); // 不想取的第一位，便于计算长度 
	//  结果为 “Hel” 
2. 字符串之间用“+”拼接
3. 分隔：String all = String.join("/","S","M","L","XL"); // all is"S/M/L/XL" 
4. 检测相等：“Hello”.equals("hello"); // false 
5. 忽略大小写： "Hello".equalsIgnoreCase("hello"); // true 
6. 上面两种均为 boolean类型 

##显示当前时间
1. <pre><code>
	/* 主要体会「商」和「余数」的应用 */
	import java.util.*;
	public class FirstSample
	{
		public static void main(String[] args)
		{
			long totalMilliseconds = System.currentTimeMillis();
			
			long totalSeconds = totalMilliseconds / 1000; // 总秒数 
			
			long currentSecond = totalSeconds % 60; // 当前秒数，取余数 
			
			long totalMinutes = totalSeconds / 60; // 总分钟，取商 
			
			long currentMinute = totalMinutes % 60; // 当前分钟，取余数 
			
			long totalHours = totalMinutes / 60; // 总小时，取商 
			
			long currentHour = totalHours % 24; // 当前小时，取余数「24」 
			
			System.out.println("Current time is " + currentHour + ":" + currentMinute + ":" + currentSecond + " GMT");
		}
	}
	/* 思路主要是对上一级 "/" 取商得到当前总量，对总 "%" 取余得到当前分量 */
	/* currentTimeMillis() 返回的是GMT与1970年1月1日0点之间的毫秒差值 */


##保留两位小数
1. <pre><code>
	/* 计算营业税 6% */
	import java.util.*;
	public class FirstSample
	{
		public static void main(String[] args)
		{
			Scanner in = new Scanner(System.in);
			System.out.println("Enter purchase amount :");
			double purchaseAmount = in.nextDouble();
			
			double tax = purchaseAmount * 0.06;
			System.out.println(tax);
			System.out.println("Sales tax is " + (int)(tax * 100) / 100.012); 
		}
	}
	/*  通过移位的形式，保留了两位小数  */
	/* 将tax向前移动两位，取整，又转化回浮点数 */



##零钱化整
1. <pre><code>
 	/*  先全部化为penny，通过移位保留小数的方式 
	 * 从大到小开始凑，然后取余 
	 * 凑100，得到dollar 
	 * 凑25，得到quarter 
	 * 凑10，得到dime 
	 * 凑5，得到nickel 
	 */
	import java.util.*;
	public class FirstSample
	{
		public static void main(String[] args)
		{
			Scanner in = new Scanner(System.in);
			
			System.out.println("Enter an amount in double,for example 11.56 : ");
			double amount = in.nextDouble();
			
			int remainingAmount = (int)(amount * 100); //全部转化为penny
			
			int numberOfOneDollars = remainingAmount / 100; //凑100，得到dollar
			remainingAmount = remainingAmount % 100; 
			int numberOfQuarters = remainingAmount / 25; //凑25，得到quarter
			remainingAmount = remainingAmount % 25;
			int numberOfDimes = remainingAmount / 10; //凑10，得到dime
			remainingAmount = remainingAmount % 10;
			int numberOfNickels = remainingAmount / 5; //凑5，得到nickel
			remainingAmount = remainingAmount % 5;
			int numberOfPennys = remainingAmount;
			
			System.out.println("Your amount " + amount + "consists of \n" + 
								"\t" + numberOfOneDollars + " dollars\n" +
								"\t" + numberOfQuarters + "quarters\n" + 
								"\t" + numberOfDimes + "dimes\n" + 
								"\t" + numberOfNickels + "nickels\n" + 
								"\t" + numberOfPennys + "pennys");


##String类型
1. <pre><code> 
	/*  “+=”可以用在字符串的连接中  */
	String message = "Welcome to Java";
	message += " and Java is fun";
	/*  message is "Welcome to Java and Java is fun"  */
2. <pre><code>
	/* next()与nextLine()的区别 */
	import java.util.*;
	public class FirstSample
	{
		public static void main(String[] args)
		{
			Scanner in = new Scanner(System.in);
			System.out.println("Enter three strings : ");
			String s1 = in.next();
			String s2 = in.next();
			String s3 = in.next(); // next()以‘ ’、‘\t’、‘\f’、‘\r’或'\n'作为分词符号，以回车结束 
			
			System.out.println( "s1 is " + s1 +
								"\ns2 is " + s2 +
								"\ns3 is " + s3 );
			/*
			 * Enter three strings : 
			 * Welcome	to Java	
			 * s1 is Welcome
			 * s2 is to
			 * s3 is Java
			 */
			System.out.println("Enter a string :");
			String s = in.nextLine(); // nextLine()读取一整行文本，以回车结束 
			System.out.println("s is " + s);
			/*
			 * Enter a string :
			 * Welcome to Java
			 * s is Welcome to Java 
			 */
		}
	}
	
##从对话框获取输入(GUI)
1. <pre><code>
	import javax.swing.JOptionPane; // 关注这个头文件 
	public class FirstSample
	{
		public static void main(String[] args)
		{
			/*  在窗口中键入值  */
			String num = JOptionPane.showInputDialog("Input a int number");

			String out = "The String number is " + num; //  此时输入的num为String类型，不能运算 
			JOptionPane.showMessageDialog(null,out); //_「以窗口的形式输出」_
			
			int numInt = Integer.parseInt(num);	//	 将String类型的num转化为int类型的num，可以运算 
			System.out.println("( Real number + 1 ) is " + (numInt + 1));
		}
	}
		/*
		 * The String number is 123
		 * ( Real number + 1 ) is 124
		 */

##三种错误
1. 语法错误(syntex error)或编译错误(compile error)
2. 运行错误(runtime error)是引起程序非正常中断的错误
	- 运行程序时，当环境检测到一个不可能执行的操作时，就会出现运行错误
3. 逻辑错误(logic error)，通常上说的bug
	- 该程序既没有语法错误，也没有运行错误，但是不能得到正确的结果

##检验奇偶
1. <pre><code>
	if (number % 2 == 0) //  if（）中的内容必须是boolean类型(表达式)，不可以是int类型(表达式) 
	System.out.println(number + "is even.");
	
	else (number % 2 == 1)
	System.out.println(number + "is odd.");
	
	/* 简化代码 */
	
	boolean even = number % 2 == 0;
	System.out.println(even);
	
##德摩根定理
1. !(condition1 && condition2) = !condition1 || !condition2
2. !(condition1 || condition2) = !condition1 && !condition2

##swith
1. 一旦匹配其中一个case，就从匹配的case处开始执行，直到遇到break语句或达到switch语句的末端。
	1. 没有break的时候，选中 case x:，执行该语句后的条件，再执行下一条语句的条件，直到遇到break，跳出switch，或执行到switch结束。
	2. 有break的时候，选中 case x:，执行该语句后的条件，跳出switch。


##条件表达式
1. 布尔表达式 ? 表达式1 : 表达式2
2. 布尔表达式为true，返回表达式1。布尔表达式为false，返回表达式2。
3. max = (num1 > num2) ? num1 : num2; // 返回最大值
4. System.out.println((num % 2 == 0) ? "num is even" : "num is odd");
5. /* 三目运算符中的表达式可以是「字符串」 */

##格式化控制台输出
1. System.out.printf("%format1%format2" , item1 , item2);
	1.	 /* 注意「printf」，百分号"%"的位置，负号"-"的位置 */
	2. 条目和标识符必须在次序，数量，「类型」上相匹配。
	3. 默认情况下，浮点值显示小数点后六位
	4. %5d //输出的整数宽度为5。不足5，在前面加空格。超出5，自动增加宽度。
	5. %10.2 //输出浮点数宽度「数字位数＋小数点占一位」为10，缺空溢补。
	6. %10.2 //保留两位小数， 会产生「四舍五入」 
	7. %8d，默认是右对齐的，空格放在左边。
	8. ％-8d，左对齐，空格放在右边。

##GUI确认对话框
1. 选择窗口

```
	int option = JOptionPane.showConfirmDialog(null,"Continue ?");
	/*
	 * 选择「yes」option变量返回值「JOptionPane.YES_OPTION(0)」
	 * 选择「no」 option变量返回值「JOptionPane.NO_OPTION(1)」
	 * 选择「cancel」option变量返回值「JOptionPane.CANCEL_OPTION(3)」
	 */
```

2. 猜生日算法

```
	/*应用举例*/
	int answer = JOptionPane.showConfirmDialog(null,"Is your birthday 	in these numbers\n" + set1);
	if (answer == JOptionPane.YES_OPTION)
		day += 1;
	/*猜生日算法*/
```

##循环
1. Java有三种循环
	1. for循环
	2. while循环
	3. do-while循环
2. 要保证循环继续条件最终可以变为false
3. 常犯错误：使循环「多执行一次」或「少执行一次」
4. 循环设计策略
	
	```
		/*「循环设计策略」
		 * 可以编写循环只执行一次的代码，然后规划如何在循环中重复执行这些代码 
		 */
		
		// 1. 确定需要重复的语句
		
		// 2. 将这些语句放入一个循环中
		while (true)
		{
			语句组;
		} 
		
		// 3. 为循环继续条件编码，并为控制循环添加适合的语句。
		while (循环继续条件)
		{
			语句组;
			// 用于控制循环的附件语句; 
		}
	```
	
5. Math.random()产生的是0.0到0.1的double类型 *包含0不包含1*
6. 计时器

	```
		/* 计时器 */
		long startTime = System.currentTimeMillis();
		long endTime = System.currentTimeMillis();
		long testTime = startTime - endTime;
	System.out.println("Test time is : " + testTime / 1000 + " Seconds ");
	```
	
7. 自增字符串
	
	```
		/* 自增字符串 */
		String output = ""; // 此处定义了一个空字符串 
		output += "\n" + number1 + "-" + number2 + "=" + answer +
		((number1 - number2 == answer)?"correct":"wrong");
		/*
		 * 假设上述在循环体中
		 * 随着次数的增加
		 * output中的字符会不断累加、换行
		 * 最后系统会统一输出「每一次」的纪录
		 */
	 ```
	 
8.  采用哪一种循环 
	1. 已知重复次数，就采用for循环。
	2. 无法确定重复次数，就采用while循环。
	3. 在检验继续条件前，需要执行循环体，就采用do-while循环。
9. 最小化数值误差

	```
		/*  最小化数值误差 
		 * 在浮点数求和过程中
		 * 由于计算机使用固定位数表示浮点数
		 * 不能精确表示某些浮点数
		 * 因此，得到的sum会比精确结果差一点
		 *  使用整数计数器以确保所有数字都被加到sum中 
		 */
		
		//	常规思路
		double sum = 0;
		for(double i = 0.01; i <= 1.0 ;i = i + 0.01) // 已知首项、公差和最大值
			sum += i;
		// 实际结果是49.050000000000003(50.5)
		
		//  整数计数器 
		
		double firstValue = 0.01;// 首项
		for (int count = 0;count < 100;count++) // 已知要累加100次
			{
				sum += firstValue;
				currentValue += 0.01;//  从小到大顺序累加 
			}
		// 实际结果是50.050000000000003(50.05)
		
		/* 从大到小添加数字没有 从小到大 添加数字精确
		 *  在大数之前添加小数是减小误差的一种方法
		 */
	```

##蒙特卡罗模拟
1. <pre><code>
	/*
	 * 该模拟使用「随机数」和「概率」来预测值
	 * 程序段为向圆外切的正方向内投随机点
	 * 进而预测pi值
	 */
	public class FirstSample
	{
		public static void main(String[] args)
		{
			final int NUMBER_OF_TRIAL = 1000_0000;
			int numberOfHits = 0;
			for (int i = 1;i <= 1000_0000; i++)//  已知循环次数 
			{
				double x = Math.random() * 2 - 1;
				double y = Math.random() * 2 - 1;//  产生定义域内的随机数 
				
				if(x*x + y*y <= 1)//  点在圆内条件 
					numberOfHits++;
			}
			System.out.println(numberOfHits);
			System.out.println("The result of pi is : " + (4.0 * numberOfHits)/10000000);
				
		}
	}

##break & contiune 
1.  if是条件语句，不是循环语句。 
2. <pre><code>
	// break是结束整个循环体，continue是结束单次循环
		while(x++ < 10)
	{
		if(x == 3)
		{
			break;
		}
		printf("%d\r\n", x);
	}
	// 结果是输出 1 2 就退出了整个while循环
	
	// 但是如果使用continue
		while(x++ < 10)
	{
		if(x == 3)
		{
			continue;
		}
		printf("%d\r\n", x);
	}
	// 结果是：1 2 4 5 6 7 8 9 10 仅仅是不输出3，只结束了当次循环
3. 在while do-while循环中，continue语句后，立即计算「循环继续条件」。
4. 在for循环中，continue语句后，先执行每次迭代后的动作「即for中的语句3」，再转去计算「循环继续条件」。
5. break和contiue少用为好。

##检验素数
1. 为了测试number是否为素数，就要检测它是否能被2、3、4，一直到number/2的整数整除。
2. <pre><code>
	/* 检测素数的模块 */
	for(i = 2;i <= number/2;i++)
	{
		if (number % i == 0)
			{
				isPrime = false;
				break;//  如果不是素数，跳出检测循环，不再检测下去 
				// 如果暂时是素数，继续检测直至完全是素数，循环结束 
			}
	}
3. <pre><code>
	/*
	 * 从小到大打印 50 个素数
	 * 每行打印 10 个
	 * 完整程序
	 */

	public class FirstSample
	{
		public static void main(String[] args)
		{
			final int TOTAL = 50;// 总共需要打印50个素数
			final int TOTAL_PER = 10;// 每行打印10个
			int count = 0;// 记录素数的个数
			int number = 2;// 初始待测数字
		
			
			while(count < TOTAL)
			{
				
				boolean judge = true;//_问题在于 judge要在循环完成后「重置」_
				for(int i = 2;i <= number/2;i++)// 检测一个数是否为素数
				{
					if(number % i == 0)
					{
						judge = false;// 说明number此时不是素数
						break;// 如果不是素数，跳出检测
						// 如果暂时是素数，继续检测至完全是素数
					}
					
				}
				
				if(judge)
				{
					count++;
					// number是素数
					if(count % TOTAL_PER == 0)
					{
						// number是边界值，需要换行
						System.out.println(number);
					}
					else
					{
						// number是非边界值，顺序打印
						System.out.print(number + " ");
					}
				}
				//不是素数，不打印，检测下一个
				number++;
			}
						
		}
	}

##方法
1. 「方法」是为了完成一个操作而组合在一起的语句组。
2. 定义方法时，括号内的参数是 形式参数 。
3. 调用方法时，括号内的参数是 实际参数 。
4. 没有返回值的方法类型为void。
5. <pre><code>
	/*
	 * 对于有「返回值」的「方法」而言
	 * return语句是必须有的
	 * 而且是无论如何，一定可以执行到的 
	 */
	public static int sign(int n)
	{
		if(n > 0)
			return 1;
		else if(n == 0)
			return 0;
		else if(n < 0)
			return -1;
		// 此处的if(n < 0)应该去掉，只剩下else
		// 这样，无论if的条件如何，程序都一定会执行return
		// 如果不去掉，会产生「编译错误」
	}
6. 如果方法定义在不同的类中，可以采用「类名.方法名」来调用该方法。
7. 活动记录：用于保存方法中的参数和变量 -> 活动记录置于一个内存区域中 -> 称为[堆栈]
8. 当一个方法1调用另一个方法2时，调用者(方法1)的活动记录保持不动，一个新的活动记录被创建用于被调用的新方法(方法2) -> 「堆栈过程」
9. 一个方法(方法2)结束返回到调用者(方法1)，其相应的活动记录也被释放 -> [释放栈过程]
10. void方法可以用 return; 语句终止方法，并返回到方法的调用者。
11. <pre><code>
	/*
	 * 当score是一个无效值，就可以用 return; 退出
	 */
	public static void printGrade(double score)
	{
		if (score < 0 || score > 100)
			return;
		// ......
	}



##按值传递
1. 实参必须与方法签名中定义的参数在「次序」和「数量」上匹配，在「类型」上兼容。
2. 上文中的「兼容」是指，不需要经过显示的类型转换，实参就可以传递给形参。
3. 如 int型 实参 传递给 double型 形参。
4. <pre><code>
	/*
	 * 如果实参是变量，则将该变量的「值」传递给形参
	 * 这意味着：无论形参在方法中是否改变，该变量都不受影响
	 */
	
	public class Increment
	{
		public static void main(String[] args)
		{
			int x = 1;
			System.out.println("Before the call,x is " + x);
			increment(x);
			System.out.println("After the call,x is " + x);
		}
		
		public static void increment(int n)
		{
			n++;
			System.out.println("n inside the method is " + n);
		}
		
	}
	
	/*
	 * Before the call, x is 1
	 * n inside the method is 2
	 * After the call, x is 1
	 */
5. <pre><code>
	// 著名的「交换变量」代码段
	public class TestPassByValue
	{
		public static void main(String[] args)
		{
			int num1 = 1;
			int num2 = 2;
			
			System.out.println("Before invoking the swap method,num1 is " + num1 + " and num2 is " + num2);
			
			swap(num1,num2);
			
			System.out.println("After invoking the swap method,num1 is " + num1 + " and the num2 is " + num2);
		}
		
		public static void swap(int n1,int n2)
		{
			System.out.println();
			
			System.out.println("\tInside the swap method");
			System.out.println("\t\tBefore swapping ,n1 is " + n1 + "and n2 is " + n2);
			
			int temp = n1;
			n1 = n2;
			n2 = temp;
			System.out.println("\t\tAfter swapping,n1 is " + n1 + " and n2 is " + n2);
			
			System.out.println();
		}
	}
	
	/*
	 *	Before invoking the swap method,num1 is 1 and num2 is 2
	 *
	 *		Inside the swap method
	 *			Before swapping ,n1 is 1and n2 is 2
	 *			After swapping,n1 is 2 and n2 is 1
	 *
	 *	After invoking the swap method,num1 is 1 and the num2 is 2
	 */
	
	// 也可以利用「堆栈」过程来解释这个原因

##方法
```
/* **将hex转化为10进制数字的代码段** */
	public static void main(String[] args)
	{
		Scanner in = new Scanner(System.in);
		
		System.out.print("Enter a hex number: ");
		String hex = in.nextLine();// 此时输入的是string
		
		System.out.println("The decimal value for hex number " + hex + " is " + hexToDecimal(hex.toUpperCase()));
	}
	
	public static int hexToDecimal(String hex)
	{
		int decimalValue = 0;// 给十进制结果赋初值
		for (int i = 0;i < hex.length();i++)
		{
			char hexChar = hex.charAt(i);// 遍历hex字符串，从最高位到最低位
			decimalValue = decimalValue * 16 + hexCharToDecimal(hexChar);
			/* 由于是从最高位开始累乘，因此上式为这种形式 */
		}
		
		return decimalValue;
	}
	/* 此函数将字母对应转换成数字，将数字字符转换成值 */
	public static int hexCharToDecimal(char ch)
	{
		if (ch >= 'A' && ch <= 'F')
			return 10 + ch - 'A';
		else
			return ch - '0';
	}
```

##重载方法
1. 重载方法是指使用[同样的名字]定义[不同的方法],
	[只要它们的签名是不同的]

```
	/* 求三个double中的最大值 *//
	/* 求两个double中的最大值 *//
	public static double max(double num1,double num2)
	{
		if(num1 > num2)
			return num1;
		else
			return num2;
	}
	public static double max(double num1,double num2,double num3)
	{
		return max(max(num1,num2),num3);
	}
```

2. 执行「同样的功能」但是具有「不同的参数类型」的方法应该使用「同样的名字」
3. 被重载的方法必须具有不同的「参数列表」，不能基于不同修饰符(public static)或返回类型(int or void)来重载方法
	 **重点在于「参数列表」不同**
4. 调用重载方法时，Java编译器会寻找最精确的匹配方法
	 如果编译器无法判断哪个是最精确的匹配方法，就会产生「编译错误」

```
public static void main(String[] args)
{
	double call = max(1,2);
}
public static double max(int num1,double num2)
public static double max(double num1,int num2)
```

##变量的作用域
1. 「局部变量」在方法中定义的变量，作用域从「声明变量处」到 「包含变量的块」结束
2. 包含变量的块是指{	}
3. 方法的「参数」作用域涵盖「整个方法」
4. 在for循环头声明的变量，其作用域是「整个for循环」
5. 可以在方法中「不同块」里声明「同名变量」
6. 不能在「嵌套块」中两次声明同一个变量

```
/* 嵌套块 */
public static void method2()
{
	int i = 1;// 此处i重名
	int sum = 0;
	
	for(int i = 1;i < 10;i++)// 此处i重名
	{
		sum += i;
	}
}
```


```
/* 
 * 生成随机字符 
 * 0 < Math.random() < 1
 * 因此和 Math.random 右边界相乘的数值要+1
 * 
 * 如果 char 周围有数字操作符(+、-)
 * char 类型 就会自动转换成 数字
 * 
 * 获取 任意两个字符 ch1 ch2 之间的字符
 * (char)(ch1 + random()*(ch2 - ch1 + 1))
 * 
 * 「以下代码段为随机获取某种特定类型字符」
 * 
 */
 public class RandomCharacter
 {
 	public static char getRandomCharacter(char ch1,char ch2)
 	{
 		return (char)(ch1 + Math.random()*(ch2 - ch1 + 1));
 	}
 	
 	public static char getRandomLowerCaseLetter()
 	{
 		return getRandomCharacter('a','z');
 	}
 	
 	public static char getRandomUpperCaseLetter()
 	{
 		return getRandomCharacter('A','Z');
 	}
 	
 	public static char getRandomDigitCharacter()
 	{
 		return getRandomCharacter('0','9');
 	}
 	
 	public static char getRandomCharacter()
 	{
 		return getRandomCharacter('\u0000','\uFFFF');
 	}
 }
```

##程序设计思想
1. 将要解决的问题逐步分解为小问题
2. 自顶向下设计框架，自底向上完善内容
3. 逐步求精

##数组
1. 声明数组 + 创建数组 + 将数组引用赋值给变量
2. 数组类型[]数组引用变量 = new 数组类型 [数组大小];
	1. 声明数组: 数组类型[] 数组引用变量;
	2. 创建数组: 数组引用变量 = new 数组类型[数组大小];
3. 获取数组大小: 数组名.length
4. 创建数组后，元素会被赋默认值
	1. 数值型 默认0
	2. char型 默认'\u0000'
	3. boolean型 默认false
5. **数组初始化语法**
	1. 声明数组 + 创建数组 + 初始化数组
	2. double[] myList = {1.9,2.9,3.4,3.5};
	3. 			「等价于」
	4. double[] myList = new double[4];
	5. myList[0] = 1.9;
	6. myList[1] = 2.9;
	7. myList[2] = 3.4;
	8. myList[3] = 3.5;
6. 使用数组初始化语法时，必须将声明、创建和初始化数组都放在一条语句中，将它们分开会产生编译错误 。
7. **处理数组元素时，经常用 for 循环**
	1. 数组中所有元素都是同一类型
	2. 数组的大小已知
8. 下面循环使用 System.in 初始化数组

	```
		Scanner in = new Scanner(System.in);
		System.out.print("Enter " + myList.length + "values");
		for (int i = 0;i < myList.length; i++)
			myList[i] = input.nextDouble();
	```

9. 使用循环打印数组中的每一个元素
	
	```
		for (int i = 0; i < myList.length; i++)
		{
			System.out.print(myList[i] + " ");
		}
	```

10. 对于char[]类型的数组，可以使用一条语句直接打印，而不循环

	```
		char[] city = {'D','a','l','l','a','s'};
		System.out.println(city);
	```

11. 对数组所有元素求和
	
	```
		for (int i = 0;i < myList.length;i++)
		{
			total += myList[i];
		}
	```
	
12. 求数组中的最大元素
	
	```
		double max = myList[0];// 事先将最大值假设为首元素
		//int indexOfMax = 0;
		for (int i = 1;i < myList.length;i++)
		{
			if (myList[i] > max)
				{
					max = myList[i];
				//indexOfMax = i;// 返回最大值的下标
				}
		}
	```

13. 随机打乱数组元素(shuffling)

	```
		/* 倒序洗牌 */
		for (int i = myList.length - 1; i > 0; i--)// 从尾到头
		{
			// 在 0 到 i 之间(包含端点)产生随机值赋给 j
			int index = (int)(Math.random() * (i + 1));
			//「值得注意」i 以后的元素都被打乱过顺序了
			
			// Swap myList[i] with myList[j]
			double temp = myList[i];// 腾出空瓶子
			myList[i] = myList[index];
			myList[index] = temp;
			// 要完成交换，保证原数组的元素仍留在数组里面
		}
		
		/* 顺序洗牌 */
		for (int i = 0; i < myList.length; i++)
		{
			// 在 0 到 myList.length 之间产生随机数(包含端点)
			int index = (int)(Math.random() * myList.length);
			
			double temp = myList[i];
			myList[i] = myList[index];
			myList[index] = temp;
		}
	```

14. 移动元素

	```
		double temp = myList[0];// 保留 首元素
		
		//从次元素开始，所有元素右移一位
		for(int i = 1;i < myList.length; i++)
		{
			myList[i - 1] = myList[i];
		}
		
		myList[myList.length - 1] = temp;
	```
	
15. 简化编码
	
	```
		/* 给定数字，显示对应月份英文 */
		String months = {"January","February",...,"December"};
		
		System.out.print("Enter a month number (1 to 12):");
		int monthNumber = input.nextInt();
		System.out.println("The month is " + months[monthNumber - 1]);
	```

16. foreach循环：Java支持一个「不使用下标变量就可以“顺序”遍历整个数组」的循环

	```
		for (double e: myList)
		{
			System.out.println(e);
		}
		// 效果为 myList 中的每一个元素都会依次赋给 e ,然后对 e 进行操作
	```
	
##复制数组
1. 复制数组有三种方法
	1. 使用「循环语句」逐个的复制数组中的元素
	2. 使用 System 类中的静态方法arraycopy **重点掌握**
	3. 使用 clone 方法复制数组(教材第13章)
2. arraycopy(源数组，源数组起始处，目标数组，目标数组起始处);
	1. 从 源数组 复制到 目标数组中的 元素个数 由参数 length 制定
	2. 复制前，必须创建目标数组，以对其分配内存
	3. 复制完成后，两数组具有相同的内容，但占有独立的内存空间
3. 数组一旦创立就不能改变大小，即不能改变[size]

	``` 
		/*
		 * 首先 这个程序可以通过编译
		 * 其次 可以通过这样的方式重设 myList 的大小
		 */
		public class FirstSample
		{
			public static void main(String[] args)
			{
				int[] myList;
				myList = new int[10];
				
				myList = new int[20];		
			}
		}
	```

4. 数组可以作为 **方法的传递参数**

	```
		public static void printArray(int[] array)
		{
			for(int i = 0; i < array.length; i++)
			{
				System.out.print(array[i] + " ");
			}
		}
	
		printArray(new int[]{3,1,2,6,4,2});// 调用
		printArray(myList)// 调用
		
		// new elementType[]{value0,value1,...,valuek}; 
		// 该数组没有显示的引用变量，成为「匿名数组」
	```

5. Java 使用「按值传递」的方式将实参传递给方法
	1. 对于基本数据类型参数，传递的是实参的值
	2. 对于数组类型的参数，参数的值是数组的引用
		1. 即 方法中的数组 和 传递的数组 是一样的
		2. 如果改变方法中的数组，将会看到方法外的数组也变化了
	
	```
		public class Test
		{
			public static void main(String[] args)
			{
				int x = 1;
				int[] y = new int[10];
				
				m(x,y);
				
				System.out.println("x is " + x);
				System.out.println("y[0] is " + y[0]);
			}
			
			public static void m(int number,int[] numbers)
			{
				number = 1001;
				numbers[0] = 5555;
			}
		}
		// x is 1
		// y[0] is 5555
	```
	
	6. 数组存储在「堆」中，数组引用存储在「栈」中
	7. **从方法中返回数组**
	
	```
	// 该程序段 输入数组，返回逆序数组
	// 此处注意方法的返回类型是 数组类型
	
		public static int[] reverse(int[] list)
		{
			int[] result = new int[list.length];
			
			for (int i = 0, j = result.length - 1; i < list.length; i++, j--)
			{
				result[j] = list[i];
			}
	
	// j 从大到小，i 从小到大
			
			return result;
		}
		
	/*
	 * 值得注意的是
	 * 在倒序交换数组的值时
	 * 一定要新定义一个数组
	 * 不可以用下面的方式
	 * int temp = list[i];
	 * list[i] = list[j];
	 * list[j] = temp;
	 * 因为它随着循环进行的过程中
	 * 把数组倒序交换至 i = j 处后
	 * 又重新交换成顺序
	 * 因此输出的结果和原数组一致
	 * 并没有被倒序输出
	 */
	```
	
##统计每个字母出现的次数
```
		public static void main(String[] args)
		{
			char[] chars = createArray();// 产生随机小写字母赋给 chars数组
			
			System.out.println("The lowercase letters are:");
			displayArray(chars);// 每20打印数组
			
			int[] counts = countLetters(chars);// 统计每字符重复次数
			System.out.println();
			System.out.println("The occurrences of each letter are : ");
			displayCounts(counts);// 每20打印统计结果
		}
		
		// 产生单个随机字符	
		public static char getRandomLowerCaseLetter()
		{
			char result = (char)('a' + Math.random() * ('z' - 'a' + 1));
			return result;
		}
		
		// 每单个随机字符存储在数组中 「返回」
		public static char[] createArray()
		{
			char[] chars = new char[100];//此处创建了一个新数组
			
			for (int i = 0; i < chars.length; i++)
				chars[i] = getRandomLowerCaseLetter();
			
			return chars;
		}
		
		// 每20打印数组内容
		public static void displayArray(char[] chars)
		{
			for (int i = 0; i < chars.length; i++)
			{
				if((i + 1) % 20 == 0)
					System.out.println(chars[i]);
				else
					System.out.print(chars[i] + " ");
			}
		}
		
		// 创建具有26个值的数组，每单个元素记录字符重复次数
		// count[char[i] - 'a']，产生的字母总在26个字母范围内
		public static int[] countLetters(char[] chars)
		{
			int[] counts = new int[26];
			
			for(int i = 0; i < chars.length; i++)
				counts[chars[i] - 'a']++;
			
			return counts;
		}
		
		// i + 'a' 字符对应 counts[i] 次数
		public static void displayCounts(int[] counts)
		{
			for (int i = 0; i < counts.length; i++)
			{
				if((i + 1) % 10 == 0)
					System.out.println(counts[i] + " " + (char)(i + 'a'));
				else
					System.out.print(counts[i] + " " + (char)(i + 'a') + " ");
			}
		}
```

1. 产生随机小写字母
	1. (char)('a' + Math.random() * ('z' - 'a' + 1));
	2. 通过for循环遍历，把产生的每一个随机字符装进数组
	3. 最终的随机字符数组为int[] chars
2. 按每行20显示
	1. 用for循环便利chars数组
	2. 计算 i % 20
		1. 余数为0 => 换行
		2. 余数不为0 => 平铺
3. 计算字符重复次数
	1. 创建具有26个元素的数组int[] counts
	2. 由于产生的字母一定在26个字母的范围内
	3. for循环，遍历chars[]
	4. count[chars[i] - 'a']++
4. 打印统计结果
	1. for循环遍历counts[]
	2. 字符 (char)('a' + i) <=> 次数counts[i]
	3. 每10个换行一次
5. 有这样一个问题 ?
	1. 如果将第3行: char[] chars = new char[100];
	2. 改为
	
	```
		char[] chars = new char[100];
		chars = createArray();
	```
	
	3. 会出现什么错误 ?
	4. 这样会创建两个数组
		1. 第1行是用new char[100]创建一个数组
		2. 第2行通过调用createArray()创建一个数组，并将这个数组的引用赋值给chars
		3. 第1行生成的数组就变成了“垃圾”
		4. Java在后台自动回收“垃圾”
		5. 程序会正常编译通过，但它会产生一个不必要的数组

##可变长参数列表
1. 定义：类型...参数名称
2. 只能给方法中指定一个可变长参数，同时该参数必须是最后一个参数，任何常规参数必须在它之前
3. Java将可变长参数当成数组对待
4. 当用数目可变的参数「调用方法」时，Java会创建一个数组并把参数传给它
5. 可以将「数组」或「数目可变的参数」传递给可变长参数
6. 传递过程中，「类型」必须相同

```
	/*
	 * 打印个数不定的列表中最大值的方法
	 */
	public class VarArgsDemo
	{
		public static void main(String[] args)
		{
			printMax(34,3,3,2,56.5);// 「数目可变的参数」
			printMax(new double[]{1,2,3});// 参数为直观数组
		}
		
		public static void printMax(double...numbers)
		{
			if(numbers.length == 0)
			{
				System.out.println("No argument passed");
				return;
			}
			
			double result = numbers[0];
			
			for (int i = 1; i < numbers.length; i++)
				if(numbers[i] > result)
					result = numbers[i];
			
			System.out.println("The max value is " + result);
		}
	}
```

##数组的查找
1. 常用的「查找」算法和数据结构
	1. 线性查找(linear searching)
	2. 二分查找(binary searching)
2. **线性查找法**：将要查找的关键字与数组中的元素逐个比较，持续到找到匹配元素，或者查找列表结束无果
	1. 如果匹配成功，返回匹配元素的数组下标
	2. 如果没有匹配，返回-1

```
	public static int linearSearch(int[] list,int key)
	{
		for(int i = 0; i < list.length; i++)
		{
			if(key == list[i])
				return i;
		}
		
		return -1;
	}
```
3. 线性查找法执行时间随着数组元素个数的增长而增长，对于大数组而言，效率不高
4. **二分查找法**：前提条件是数组中的元素必须已经按「升降序」排好
	1. 首先将关键字与数组中间元素进行比较
	2. 如果关键字小于中间元素，只需在数组前一半继续查找
	3. 如果关键字和中间元素相等，则匹配成功
	4. 如果关键字大于中间元素，只需在数组后一半继续查找
5. 对于数组而言
	1. low 为 0
	2. high 为 list.length - 1
	3. mid = (low + high) / 2
	4. 	 「实现过程」
	5. if key < list[mid]
	6. high = mid - 1
	7. if key == list[mid]
	8. return mid
	9. if key > list[mid]
	10. low = mid + 1
	11. **当「匹配关键字」后结束查找**
	12. **当 low > high 结束查找** //循环的结束条件

```
	public static int binarySearch(int[] list, int key)
	{
		int low = 0;
		int high = list.length - 1;
		
		while(high >= low)
		{
			int mid = (low + high) / 2;
			if(key < list[mid])
				high = mid - 1;
			else if(key == mid)
				return mid;
			else
				low = mid + 1;
		}
		
		return -1//Not found
	}
```

##数组的排序
1. **选择排序**
	1. 先在数列中找到「最小数」，将它和「第一个元素」互换
	2. 在剩下的数中找到「最小数」，将它和「第二个元素」互换
	3. 依此类推，直到数列中仅剩一数为止
```
	public class SelectionSort
	{
		public static void selectSort(double[] list)
		{
			for (int i = 0; i < list.length - 1; i++)
			{
				double Min = list[i];
				int MinIndex = i;
				
				/* 找到最小值 */		
				for (int j = i + 1; j < list.length; j++)
				{
					if(Min > list[j])
					{
						Min = list[j];
						MinIndex = j;
					}
				}
				/***********/	
				
				// 将 Min	 与第 i 个值交换，直至遍历 i 结束
				if (MinIndex != i)
				{
					list[MinIndex] = list[i];
					list[i] = Min;// 交换
				}
			}
		}
	}
```

##Arrays类
1. java.util.Arrays类包含一些实用的方法用于常见的数组操作
	1. 排序操作 sort()、parallelSort()
	2. 查找操作 binarySearch()
	3. 数组比较 equals()
	4. 填充数组 fill()
	5. 返回数组的字符串 toString()
2. 排序操作
```
	double numbers = {6.0,4.4,1.9,2.9,3.4,3.5};
	
	java.util.Array.sort(numbers);
	// 结果 numbers 数组现在已经为{1.9 2.9 3.4 3.5 4.4 6.0}
	
	java.util.Arrays.parallelsort(numbers);
	// 效果和上面相同
	
	java.util.Arrays.sort(numbers,0,3);
	// 结果 numbers 数组现在已经为{1.9 4.4 6.0 2.9 3.4 3.5}
	// 从 0 位置开始排序 到 3 位置结束
```
3. 二分查找 binarySearch()
	1. 数组必须按照「升序」排好
	2. 无匹配会返回-「插入位置」

```
	public static void main(String[] args)
	{
		int[] list = {2,4,7,10,11,45,50,59,60,66,69,70,79};
		System.out.println(java.util.Arrays.binarySearch(list,11));
		System.out.println(java.util.Arrays.binarySearch(list,12));

	}
	// 结果为： 4 －6
```

4. 检测两数组是否相等
```
		public static void main(String[] args)
	{
		int[] list1 = {2,4,7,10};
		int[] list2 = {2,4,7,10};
		int[] list3 = {4,2,7,10};
		
		System.out.println(java.util.Arrays.equals(list1,list2));
		System.out.println(java.util.Arrays.equals(list2,list3));
	}
// boolean类型结果 true false
```

5. 将数组作为字符串返回
```
		public static void main(String[] args)
	{
		int[] list = {2,4,7,10};
		
		System.out.println(java.util.Arrays.toString(list));
	}
// 结果为： [2, 4, 7, 10]
```

##args命令行参数
1. 从命令行调用 main 函数时，可以用 args 传递字符串
2. 例如：java 类名 "First num" alpha 53
	1. 传递的字符串不必用""分隔，用「空格」分隔即可
	2. 当传递的字符串内有「空格」，需要用""分隔
	
```
	public class Calculator 
{
  /** Main method */
  public static void main(String[] args) 
  {
    // Check number of strings passed
    if (args.length != 1) 
    {
      System.out.println(
        "Usage: java Calculator \"operand1 operator operand2\"");
      System.exit(0);
    }

    // The result of the operation
    int result = 0;

    // Split items from a string 
    String[] tokens = args[0].split(" ");

    // Determine the operator
    
    // 这里的 switch() 内的用法 值得关注
    switch (tokens[1].charAt(0)) 
    {
      case '+': result = Integer.parseInt(tokens[0]) +
                         Integer.parseInt(tokens[2]);
                break;
      case '-': result = Integer.parseInt(tokens[0]) -
                         Integer.parseInt(tokens[2]);
                break;
      case '*': result = Integer.parseInt(tokens[0]) *
                         Integer.parseInt(tokens[2]);
                break;
      case '/': result = Integer.parseInt(tokens[0]) /
                         Integer.parseInt(tokens[2]);
    }

    // Display result
    System.out.println(tokens[0] + ' ' + tokens[1] + ' ' 
      + tokens[2] + " = " + result);
  }
}
```

##二维数组
1. 二维数组 用以存储「矩阵」和「表格」
2. 声明：数据类型[][] 数组名;
3. 创建：数组名 = new int[行][列];

```
	int[][] array = {
							{1,2,3},
							{4,5,6},
							{7,8,9},
							{10,11,12}
						  };
	// 第一行 等价为
	int[][] array = new int[4][3];
	array[0][0] = 1; array[0][1] = 2; array[0][2] = 3;
	
```
4. [二维数组长度]假设 array = new int[3][4]
	1. x.length = 3 // 为外层数组长度
	2. x[0].length = 4 // 为内层数组长度
5. 锯齿数组：二维数组中「每一行」本身就是一个数组，因此，各行的长度可以不同
```
	int[][] triangleArray = {
									 {1,2,3,4,5},
									 {2,3,4,5},
									 {3,4,5},
									 {4,5},
									 {5}
									 };
	// 「数组」与「数组」之间「逗号」分隔
	// 「数组」最末尾由「分号」结尾
```

6. 事先不知道锯齿数组的值，但是知道长度，可采用如下方法创建「锯齿数组」
```
	int[][] array = new int[5][]; // 此处必须指定第一个下标
	array[0] = new int[5];
	array[1] = new int[4];
	array[2] = new int[3];
	array[3] = new int[2];
	array[4] = new int[1];
	
	// 现在可以给数组赋值 如
	array[0][3] = 50;
	array[4][0] = 45;
```

7. 可以将「一维数组名」赋值给「二维数组第一层」
```
	int[][] array = new int[5][6];
	int[]	x = {1,2};
	array[0] = x;
```

8. 初始化二维数组
```
	for(int row = 0; row < matrix.length; row++)
	{
		for(int column = 0; column < matrix[row].length; column++)
		{
			matrix[row][column] = input.nextInt();
		}
	}
```

9. 打印二维数组
```
	for(int row = 0; row < matrix.length; row++)
	{
		for(int column = 0; column < matrix[row].length; column++)
		{
			System.out.print(matrix[row][column] + " ");
		}
		System.out.println();// 每行打印结束后 换行
	}
```

10. 求所有元素的和
```
	int total = 0;
	for(int row = 0; row < matrix.length; row++)
	{
		for(int column = 0; column < matrix[row].length; column++)
			total += matrix[row][column];
	}
```

11. 按列求和
```
	for (int column = 0; column < matrix[0].length; column++)
	{
		int total = 0; // 与 10 的区别
		for (int row = 0; row < matrix.lenth; row++)
			total += matrix[row][column];
		System.out.println("Sum for column " + column + " is " + total);
	}
```

12. 哪一行的和最大？
```
	int maxRow = 0;
	int indexOfMaxRow = 0;
	
	// Get sum of the first row in maxRow
	for(int column = 0; column < matrix[0].length; column)
	{
		maxRow += matrix[0][column];
	}
	
	for(int row = 1; row < matrix.length; row++)
	{
		int totalOfThisRow = 0;
		for (int column = 0; column < matrix[row].length; column++)
			totalOfThisRow += matrix[row][column];
		
		if (totalOfThisRow > maxRow)
		{
			maxRow = totalOfThisRow;
			indexOfMaxRow = row;
		}
	}
	
	System.out.println("Row " + indexOfMaxRow + " has the max sum of " + maxRow);
	
	/* 
	 * 思路为
	 * 先将第一组的和 给最大值
	 * 然后逐组求和 都与 最大和 比较
	 * 返回 最终结果
	 */
```
13. 随意打乱
```
	for(int i = 0; i < matrix.length; i++)
	{
		for(int j = 0; j < matrix[i].length; j++)
		{
			int i1 = (int)(Math.random() * matrix.length);
			int j1 = (int)(Math.random() * matrix[i].length);
			
			int temp = matrix[i][j];
			matrix[i][j] = matrix[i1][j1];
			matrix[j1][i1] = temp;
		}
	}
// 随机产生下标 i1 和 j1
// 互换 matrix[i][j] 和 matrix[i1][j1]
```

##将「二维数组」传递给「方法」
1. 二维数组可以作为「方法」的「传递参数」
	```
		public static int method(int[][] m)
	```
	
2. 二维数组可以作为方法的「返回值」
	```
		public static int[][] method()
	```
	
###多选题测验评分
```
	public class GradeExam {
  /** Main method */
  public static void main(String args[]) 
  {
    // Students' answers to the questions
    char[][] answers = {
      {'A', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'},
      {'D', 'B', 'A', 'B', 'C', 'A', 'E', 'E', 'A', 'D'},
      {'E', 'D', 'D', 'A', 'C', 'B', 'E', 'E', 'A', 'D'},
      {'C', 'B', 'A', 'E', 'D', 'C', 'E', 'E', 'A', 'D'},
      {'A', 'B', 'D', 'C', 'C', 'D', 'E', 'E', 'A', 'D'},
      {'B', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'},
      {'B', 'B', 'A', 'C', 'C', 'D', 'E', 'E', 'A', 'D'},
      {'E', 'B', 'E', 'C', 'C', 'D', 'E', 'E', 'A', 'D'}};
      
      // 每个学生是一个子一维数组

    // Key to the questions
    char[] keys = {'D', 'B', 'D', 'C', 'C', 'D', 'A', 'E', 'A', 'D'};

    // Grade all answers
    for (int i = 0; i < answers.length; i++) 
    {
      // Grade one student
      int correctCount = 0;
      
      for (int j = 0; j < answers[i].length; j++) 
      {
        if (answers[i][j] == keys[j])
          correctCount++;
      }

      System.out.println("Student " + i + "'s correct count is " +
        correctCount);
    }
  }
}
```

###找出距离最近的点
```
int p1 = 0, p2 = 1; // Initial two points
double shortestDistance = distance(points[p1][0], points[p1][1], points[p2][0], points[p2][1]); // Initialize shortestDistance

for (int i = 0; i < points.length; i++) 
{
	for (int j = i + 1; j < points.length; j++) 
	{
		double distance = distance(points[i][0], points[i][1], points[j][0], points[j][1]); // Find distance

		if (shortestDistance > distance) 
		{
			p1 = i; // Update p1
			p2 = j; // Update p2
			shortestDistance = distance; // Update shortestDistance 
		}
	}
}

```

###数独
1. 验证数独正确的方案
	1. 检查每行、每列、每个小方块都有1-9的数字
	2. 检查单元格：每个单元格内的数字在每行、每列、每个小方格唯一
2. 程序采用「第二种方法」验证数独正确
```
	  public static boolean isValid(int i, int j, int[][] grid) {
    // Check whether grid[i][j] is valid at the i's row
    for (int column = 0; column < 9; column++)
      if (column != j && grid[i][column] == grid[i][j])
        return false;

    // Check whether grid[i][j] is valid at the j's column
    for (int row = 0; row < 9; row++)
      if (row != i && grid[row][j] == grid[i][j])
        return false;

    // Check whether grid[i][j] is valid in the 3 by 3 box
    for (int row = (i / 3) * 3; row < (i / 3) * 3 + 3; row++)
      for (int col = (j / 3) * 3; col < (j / 3) * 3 + 3; col++)
        if (row != i && col != j && grid[row][col] == grid[i][j])
          return false;

    return true; // The current value at grid[i][j] is valid
  }

	/*
	 * 检验每个单元格内的数字在每行是否唯一
	 * 检验每个单元格内的数字在每列是否唯一
	 * 检验每个单元格内的数字在每个小方格是否唯一
	 * 
	 * 任意的 grid[i][j] ,它的起始单元格为 grid[3*(i/3)][3*(j/3)]
	 * 如果grid[r][c]是3x3的起始方格，用如下方法遍历
	 * 	for(int row = r; row < r + 3; row++)
	 * 		for(int col = c; col < c + 3; col++)
	 * 	 		// 遍历整个方块
	 */
```

##多维数组


##Java库中的类
1. java.util.Date 类
```
	java.util.Date date1 = new java.util.Date();
	
	date1.Date(timeLength); 
	// 在格林尼治19700101 00:00上增加 timeLength 毫秒
	// 该方法 为void 没有返回值
	date1.setTime(timeLength);
	// 为对象 date1 设定一个新的流逝时间
	
	date1.toString();// 返回当前日期和时间的字符串表示
	date1.getTime();// 返回从 格林威治19700101 至今流逝的毫秒
```

2. 回忆 System.currentTimeMillis();
3. java.util.Random 类
	1. Random() // 以当前时间为种子 创建Random对象
	2. Random(seed: long)// 以一个特定值为种子 创建Random对象
	3. nextInt()// 返回一个随机int值
	4. nextInt(n:int)// 返回一个从 0 到 n(不包含n)的随机值
	5. nextLong()// 返回一个随机long值
	6. nextDouble()// 返回一个从0.0到1.0(不包含1.0)的double
	7. nextFloat()// 从0.0 到 1.0F
	8. nextBoolean()// 返回一个随机boolean
4. 如果两个Random对象有相同的种子，那么会产生相同的随机数列
```
public class FirstSample
{
	public static void main(String[] args)
	{
		java.util.Random random1 = new java.util.Random(3);
		System.out.print("From random1: ");
		for(int i = 0; i < 10; i++)
			System.out.print(random1.nextInt(1000) + " ");
			// 从 0 到 1000
		java.util.Random random2 = new java.util.Random(3);
		System.out.print("\nFrom random2: ");
		for(int i = 0;i < 10; i++)
			System.out.print(random2.nextInt(1000) + " ");
			// 从 0 到 1000
	}	
}
// From random1: 734 660 210 581 128 202 549 564 459 961 
// From random2: 734 660 210 581 128 202 549 564 459 961 
```

5. Point2D类
	1. Point2D(x:double,y:double) //用给定的x和y坐标创建对象
	2. distance(x1:double,y1:double) //上(x,y)到(x1,y1)距离
	3. distance(p:Point2D)// 返回该点到定点p的距离
	4. getX()// 返回该点的x坐标
	5. getY()// 返回该点的y坐标
	6. toString()// 返回该点的字符串表示
	7. import javafx.geometry.Point2D;//头部声明
```
	import java.util.Scanner;
	import javafx.geometry.Point2D;
	public class FirstSample
	{
		public static void main(String[] args)
		{
			Scanner input = new Scanner(System.in);
			
			System.out.print("Enter point1 x,y:");
			double x1 = input.nextDouble();
			double y1 = input.nextDouble();
			System.out.print("Enter point2 x,y:");
			double x2 = input.nextDouble();
			double y2 = input.nextDouble();
			
			Point2D p1 = new Point2D(x1,y1);
			Point2D p2 = new Point2D(x2,y2);
			System.out.println("p1 is " + p1.toString());
			System.out.println("p2 is " + p2.toString());
			
			System.out.println("Distance is :" + p1.distance(p2));
		}	
	}
	/*
		Enter point1 x,y:1 2
		Enter point2 x,y:3 4
		p1 is Point2D [x = 1.0, y = 2.0]
		p2 is Point2D [x = 3.0, y = 4.0]
		Distance is :2.8284271247461903
	*/
```

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
1. 实例变量-对象变量
	1. 指在数据域中没有被注明 static 的变量
	2. 实例变量不能被同一个类下的不同对象所共享
	3. 同类下的不同对象针对同一个实例变量做出的改变不互相影响
		* object1 中的 data 不会影响 object2 中的 data
	4. 如果想要同类下的所有对象共享数据域，就要使用static变量
	
	
2. 静态变量-类变量
	1. 静态变量可以被类下的所有对象共享
		* 共享意味着：改变值后相互影响
	2.	静态方法使用注意事项 
		1. 静态方法不能访问类下的任何对象
		2. 静态方法只能访问静态成员(成员函数+成员变量)
		3. 非静态方法既可访问静态又可访问非静态
		4. 静态方法中不可以使用 this 和 super 关键字
		5. 主函数是静态的
			* 主函数只能调用 static 方法
			* 可以采用用“对象.方法”的形式来调用非静态方法
	3. 静态变量可以用来统计创建对象的个数
	
	
3. 实例变量和静态变量的区别：
	1. 变量声明周期不同
		1. 实例变量随着对象的创建而存在，随着对象的回收而释放
		2. 静态变量随着类的加载而存在，随着类的消失而消失
	2. 调用方式不同
		1. 实例变量只能被对象调用
		2. 静态变量即可以被对象调用，又可以被类名调用
			* 不建议用对象调用static变量
	3. 数据存储位置不同
		1. 成员变量存储在堆内存的对象中，也称对象的特有变量
		2. 静态变量存储在「方法区的静态区」下，也称对象的共享数据
	4. 静态变量前省略的是“类名.”
	5. 非静态变量前省略的是“this.”
		

4. 主函数`public static void main(String[] args)`
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
	
5. 成员变量和局部变量的区别：
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

6. 当局部变量与成员变量同名时
	1. 局部变量的值会覆盖成员变量的值
	2. 当方法在栈内运行时，由于局部变量也存储在栈内，所以优先取得局部变量的值
	3. 当栈中不存在该变量名时，才选择去堆内存中对象下查找是否有该名字的变量

7. 类类型参数
	* 指方法的参数为类的对象
	* 该方法的功能：用于改变对象的属性
	* 类类型变量一定指向对象，或者为null，不能赋值为其他

8. 匿名对象
	* 形式：new className();
	* 定义对象的简写格式
	1. 使用方式
		1. 当对象对方法「只进行一次调用时」就可以简化成匿名对象
		2. 匿名对象可以作为「方法参数」传递

9. 基本数据类型参数传递
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
10. 引用数据类型参数传递
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
	
11. 封装
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

12. 权限修饰符
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
 	
 
## Java 数据库程序设计

 1. 关系型数据库系统
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
 		
 
 2. SQL
 
