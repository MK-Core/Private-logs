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
