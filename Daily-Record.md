# 2018/9/11

## java输入输出流

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
