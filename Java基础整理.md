# Java学习笔记

## 第一章：基础语法整理

### String拼接

```java
/*
 ... 
*/
int a=10,b=20;
//以下两条代码输出结果均为String类型
System.out.println(""+a+b);
//输出1020
System.out.println(a+b+"");
//输出30
```

### Scanner用法

1. 获取系统输入流：new scanner(System.in)

2. 判断输入截止：hasNext()/hasNextLine

3. 获取用户输入信息：scanner.next()/scanner.nextLine()

4. 关闭scanner方法：scanner.close()

   完整代码如下所示：

   ```java
   import java.util.Scanner;
   
   public class InputScnner {
       public static void main(String[] args) {
           System.out.println("please input a string:");
   
           //Java-Scnner输入流
           Scanner scanner = new Scanner(System.in);
   				/*
   				next方法：
   				1.只有在遇到有效字符才正式生效，即开始输入的若干空格字符不被正常识别记录
   				2.有效字符之后遇到空格的元素被剔除
   				3.以Enter作为截止输入符
           */
           //next() 
           if(scanner.hasNext()){
               String str = scanner.next();
               System.out.println("output is "+str);
           }
   				/*
   				nextLine方法：
   				1.以Enter作为截止输入符
   				2.即Enter之前的所有的符号均可被正常识别记录
           */
           //nextLine() 
           if(scanner.hasNextLine()){
               String str = scanner.nextLine();
               System.out.println("output is "+str);
           }
           //close scnner
           scanner.close();
       }
   }
   ```

### switch case穿透

switch-case匹配结构中，若case分支不存在break语句且当前条件匹配该case，则直接执行此case及之后所有case分支语句，直到遇到下一个break停止执行,代码示例如下：

```java
/*
 如果当前I1值为B，则匹配第二个case语句，程序整体输出B所在case语句之后所有sout语句，
 直至遇到break为止，若D所在case语句也不存在break，则default语句依旧被输出。
 输出结果为：
 Nice!
 ohyeah!
 shit!
*/
switch (I1){
            case "A":
                System.out.println("Good!");
                break;
            case "B":
                System.out.println("Nice!");

            case "C":
                System.out.println("ohyeah!");
                
            case "D":
                System.out.println("shit!");
                break;
            default:
                System.out.println("Wrong!");
        }
```

### 值传递和引用传递

```java
//值传递
public class Test {    
    public static void main(String[] args) {
        int a = 1;
        System.out.println(a);//输出 a = 1
        Test.change(a);
        System.out.println(a);//输出 a = 1
    }
    public static void change(int a){
        a = 10;
    }
}
//引用传递
public class Test {
    public static void main(String[] args) {
        Person person = new Person();
        person.name = "lisi";
        System.out.println(person.name);//输出 lisi
        Test.change(person);
        System.out.println(person.name);//输出 zhangsan
    }
    public static void change(Person person){
        person.name = "zhangsan";
    }
}
class Person{
    String name;
}
```

### 可变参数

1. JDK 1.5新增功能
2. 在方法声明中，在指定参数类型后添加省略号(...)
3. 一个方法中只能声明一个可变参数，<font color ="ff0000">它必须是方法的最后一个参数</font>，任何其他普通参数均需在其之前声明。

```java
public class Exchange {
    public static void main(String[] args) {
        printMaxmum(1.2,323,12,44,4.5);
        printMaxmum(new double[]{1,3,7.7,6});
    }
  	//可变参数
    public static void printMaxmum(double... number){
        if(number.length==0)
        {
            System.out.println("no number");
            return;
        }
        double max = number[0];

        for (int i = 0; i < number.length; i++)
        {
            if (number[i]>max)
                max=number[i];
        }
        System.out.println("the max value is :"+max);
    }
}
```

### 增强for循环

```java
int[] arrays_one = {1,2,3,4,5};
int[][] arrays_two = {{1,2},{2,3},{3,4},{4,5}};
//JDK1.5新增功能
//一维数组
for (int array:arrays_one)
{
  System.out.println(array);
}
//二维数组
for(int[] ints:arrays_two)
{
  for(int anInt:ints)
    System.out.println(anInt);
}
```

### 稀疏数组

```java
import java.util.Scanner;

public class Test {

    public static void main(String[] args) {
        //二维数组创建
        System.out.println("please input matrix's nums,lins and cows:");
        Scanner scanner = new Scanner(System.in);
        int sum = scanner.nextInt();//有效值总数
        int lin = scanner.nextInt();//行数
        int cow = scanner.nextInt();//列数
				//初始化二维数组
        int[][] arrays_two = new int[lin][cow];
        for (int i = 0; i < sum; i++) {
            System.out.println("please input the value and its position: ");
            int num_v = scanner.nextInt();//元素值
            int lin_l = scanner.nextInt();//对应的行数
            int cow_c = scanner.nextInt();//对应的列数

            arrays_two[lin_l-1][cow_c-1] = num_v;
        }
				//输出二维数组
        for (int[] ints : arrays_two) {
            for (int anInt : ints) {
                System.out.print(anInt+"\t");
            }
            System.out.println();
        }
        /*
        初始化稀疏数组，其中行数为有效数字个数+1，列数固定3列
        其中第一行存放稀疏数组的有效值个数，行数，列数
        其余行存放对应的有效值以及其行列数
        */
        int[][] arrays_xishu = new int[sum+1][3];
        arrays_xishu[0][0] = sum;
        arrays_xishu[0][1] = arrays_two.length;
        arrays_xishu[0][2] = arrays_two[0].length;
        //遍历原数组，将有效值存放于稀疏数组中
        int count = 0;
        for (int i = 0; i < arrays_two.length; i++) {
            for (int j = 0; j < arrays_two[i].length; j++) {
                if(arrays_two[i][j]!=0)
                {
                    count += 1;
                    arrays_xishu[count][0] = arrays_two[i][j];
                    arrays_xishu[count][1] = i+1;
                    arrays_xishu[count][2] = j+1;
                }
            }
        }
        //
        System.out.println("稀疏数组如下所示：");
        for (int[] ints : arrays_xishu) {
            for (int anInt : ints) {
                System.out.print(anInt+"\t");
            }
            System.out.println();

        }
        scanner.close();
    }
}
```

## 第二章：面向对象思想

### 面向对象和类

- 构造函数
  - 必须和类名一样，且没有返回值。
  - <font color ="ff0000">new 本质是在调用构造方法，初始化对象的值。</font>
  - 定义有参构造之后，若想使用无参构造，需显示定义一个无参构造。

- 析构函数

  Java不存在析构函数,Java具有内存回收机制，当变量退出其生命周期时，JVM会自动识别并调用垃圾回收器GC。

### 封装

**遵循原则：高内聚，低耦合**

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

### 继承

- 继承是类与类之间的一种关系，除此之外，类与类之间还可以存在依赖、组合、聚合等关系。

- 继承关系的两个类，一个为子类（派生类），一个为父类（基类）。子类继承父类，使用关键字extendes。

- <div><font color = "ff0000">Java中类只有单继承，没有多继承,其中object类是所有类的父类。</font></div>

**super关键字**

```java
//父类
public class Person{
    public Person() {
        System.out.println("Person无参构造");
    }
    protected String name = "zhangsan";
}
//子类
public class Student extends Person {
   	public Student() {
      	//！！默认隐藏调用父类的！无参！构造函数！！
      	//如果调用有参构造函数，需显示声明super()方法
      	//super();
        System.out.println("Student无参构造");
    }
    private String name = "bushizhangsan";
    public void test(String name){
        System.out.println(name);//输出当前name
        System.out.println(this.name);//输出当前类对应的name
        System.out.println(super.name);//输出父类对应的name
    }
}
//主方法
public class Main {
    public static void main(String[] args) {
        Student student = new Student();
        student.test("张三");
    }
}
//程序输出
Person无参构造
Student无参构造
张三
bushizhangsan
zhangsan
```

**方法重写**

1. 方法名必须相同，参数列表必须相同。
2. 修饰符：继承子类属性的范围相较父类属性可以扩大，但不可以缩小：public>protected>default>private
3. 抛出异常范围：可以被缩小，但不可以被扩大：ClassNotFoundException --> Exception(大)
4. 重写前后子类方法名必须和父类一致，但是方法体可以不同。

- 静态方法重写

  ```java
  //父类
  public class Person{
      public static void test(){
          System.out.println("Person=>test");
      }
  }
  //子类
  public class Student extends Person {
      public static void test(){
          System.out.println("Student=>test");
      }
  }
  //主方法
  public class Main {
      public static void main(String[] args) {
          Student student = new Student();
          student.test();
          Person person = new Student();//延伸创建父类对象
          person.test();
      }
  }
  //输出结果
  Student=>test
  Person=>test
  ```

- 非静态方法重写

  ```java
  //父类
  public class Person{
      public void test(){
          System.out.println("Person=>test");
      }
  }
  //子类
  public class Student extends Person {
    	@Override//注解：有功能的注释
      public void test(){
          System.out.println("Student=>test");
      }
  }
  //主方法
  public class Main {
      public static void main(String[] args) {
          Student student = new Student();
          student.test();
          Person person = new Student();//重写父类方法
          person.test();
      }
  }
  //输出结果
  Student=>test
  Student=>test
  ```

  