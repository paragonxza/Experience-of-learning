# Java学习笔记

## 第一章

### 面向对象和类

构造函数：必须和类名一样，且没有返回值。

析构函数：Java不存在析构函数,Java具有内存回收机制，当变量退出其生命周期时，JVM会自动识别并调用垃圾回收器GC。

### 信息隐藏和this

- 保护属性信息：类的成员属性是私有的private
  - 获取类成员属性可以使用getter & setter 方法，对应IDEA工具 mac快捷键：command+return；windows快捷键：alt+inter
- 公开行为信息：类的方法是公有的public
- this关键字
  - this负责指向本类中的成员变量
  - this负责指向本类中的成员方法
  - this可以代替本类的构造函数
- this示例

```java
//OO类声明
public class OOExample {

    public static void main (String[] args)
    {
       gets obj = new gets(5);
       System.out.println(obj.sum());
    }
    
}
//gets类声明
public class gets {
    //设定私有变量
    private int m,n;
    //类的构造函数
    public gets(int m){
        this(m,0);
    }
    public gets(int m,int n){
        this.m=m;
        this.n=n;
    }
    //定义sum方法调用add方法
    public int sum()
    {
        return this.add(m,n);//可省略this因为不会引起歧义
    }
    public int add(int m,int n)
    {
        return m+n;
    }

}
```

## 第二章

### 

