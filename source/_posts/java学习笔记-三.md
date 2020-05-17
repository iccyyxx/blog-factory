---
title: java学习笔记(三)
date: 2020-05-15 08:33:36
tags:
---
# 继承
- 面向过程的范式是方法的设计
- 面向对象的范式重点在将数据和方法结合在对象中
- 继承是面向对象过程中体现代码重用的一个重要且强大的特征
- 例题：
  >假设要定义一个类来对圆、矩形和三角形建模。这些类有很多共同的特性。设计这些类来避免冗余的最好方式是什么？
  >使用继承
- 继承使得我们可以定义一个通用的类，即父类（超类）
  在这个类中定义通用的特征和行为
  之后扩充该类为一个更加特定的类（子类、派生类）
  在子类中定义个性部分的特征和行为
  而通用的部分不需要被定义而是被继承下来
- 继承的语法关键字是 **extends**
- 静态方法可以被继承不能被重写
- java中的每个类都源于 java.lang.Object类
  ```
  class ClassName extends Superclass{
      class body
  }
       
 ```

- 设计通用类
  ```
  public class GeometricObject {
    //私有的成员变量
    private String color = "white";
    //几何体是否填充
    private boolean filled;

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public boolean isFilled() {
        return filled;
    }

    public void setFilled(boolean filled) {
        this.filled = filled;
    }

    public Date getDataCreated() {
        return dataCreated;
    }

    public void setDataCreated(Date dataCreated) {
        this.dataCreated = dataCreated;
    }

    //几何体创建的时间
    private java.util.Date dataCreated;

    //无参构建方法
    public GeometricObject(){
        dataCreated = new java.util.Date();
    }
    public GeometricObject(String color,boolean filled){
        dataCreated = new java.util.Date();
        this.color = color;
        this.filled = filled;
    }
    public String toString(){
        return "created on"+dataCreated + "\ncolor:" + color + "and filled:" + filled;
    }
}
  ```
- 子类继承以上父类
  ```
public class Circle1 extends GeometricObject{
    public double getRadius() {
        return radius;
    }

    public void setRadius(double radius) {
        this.radius = radius;
    }

    private double radius;

    public Circle1(){
        this.radius = 1;
    }
    public Circle1(double radius){
        this.radius = radius;
    }
    public Circle1(double radius,String color, boolean filled){
        this.radius = radius;
        setColor(color);
        setFilled(filled);
    }
    public double getArea(){
        return radius * radius * Math.PI;
    }
    public double getPerimeter(){
        return 2 * radius * Math.PI;
    }
    public void printCircle(){
        System.out.println("The circle\n creatde:"+getDataCreated()+"radius :"+radius);
    }
}
  ```
- >父类的构造方法能继承吗？
  - 父类的构造方法不能被继承
  - 使用 **super** 关键字显式调用
  - 若无被显示调用将自动隐式调用无参构造方法
  - 一定会被调用


## super
- super一定是子类构造方法的第一条语句
- super调用父类的构造方法
    ```
    public Circle1(double radius,String color, boolean filled){
        /******
        this.radius = radius;
        setColor(color);
        setFilled(filled);
        ******/
        //可换为
        super(color,filled);
        this.radius = radius;
    }
    
    ```
- 使用 super 的方法
  - 子类有可能创建的方法和父类的方法同名，这种情况下就是把父类的同名方法给重写了。

- 构造方法链示例
    ```
    class Faculty extends Employee {
    public static void main(String[] args) {
        new Faculty();
    }

    public Faculty() {
        System.out.println("(4)");
    }
}

class Employee extends Person1 {
    public Employee() {
        this("(2)");
        System.out.println("(3)");
    }

    public Employee(String s) {
        System.out.println(s);
    }
}

class Person1 {
    public Person1() {
        System.out.println("(1)");
    }
}
```
以上的输出为：
```
(1)
(2)
(3)
(4)
```

## 实现方法重写的条件：两同两小一大的原则
- 两同：指子类和父类的方法名和参数完全相同
- 两小：
    - 指子类方法的返回类型比父类的同名方法返回类型相同或更小
    - 指子类同名方法抛出的异常比父类抛出的异常更小或相同
- 一大：指子类方法的可见性（访问权限）修饰符比父类同名方法范围大或相同



# 对象转换
- 对象转换：把一种类类型的对象转换为继承体结构中的另一种类类型的对象，有隐式转换和强制转换（显示转换）


## 隐式转换(向上转型)
1. 子类可以被隐式的自动的转换为其父类的类型
2. **Object o = new Student()**
3. 若**Syudent b = o;**则编译错误
   因为Student对象总是Object的实例，但是Object对象不一定是Student的实例


## 显示转换
1. **Student b = (Student)o**
2. **Instanceof运算符**
    使用 instanceof 运算符来检测一个对象是否是一个类型的实例：
   ```
   Fruit f = new Apple();
   f instanceof Apple 将返回 true
   f instanceof Orange 将返回 false
   ```
3. 示例：
   ```
   public class Demo1 {
    public static void main(String[] args) {
        Object o1 = new Circle1();
        Object o2 = new Rectangle();
        if (o1 instanceof Circle)
            System.out.println(((Circle1)o1).getArea());
        if (o2 instanceof Rectangle)
            System.out.println(((Rectangle)o2).getArea());
    }
    }
```
4. 用数组保存以上对象实例
```
public class Demo1 {
    public static void main(String[] args) {
        Object[] objects = new Object[2];
        objects[0] = new Circle1();
        objects[1] = new Rectangle();
        for (Object o : objects){
            if (o instanceof Circle)
                System.out.println(((Circle1)o).getArea());
            if (o instanceof Rectangle)
                System.out.println(((Rectangle)o).getArea());
        }
    }
}
```

# 多态
- 多态意味着父类的变量可以指向子类的对象，当调用该父类变量的一些成员方法，其行为可以表现为子类同名方法的行为特征，而不是父类同名方法的特征
- 相同类型的变量，调用一个方法时呈现出不同的行为特征，所以称为多态。
- 实例
```
public class Demo1 {
    public static void main(String[] args) {
        myPrint(new Object());
        myPrint(new Person());
        myPrint(new Student());
        myPrint(new GraduateStudent());
        }
/*******打印任意对象的信息*********/
//参数：用子类的共同父类
public static void myPrint(Object o){
        //子类必须重写父类的同名方法
        System.out.println(o.toString());

        }
        }
class Person{
    public String toString(){
        return "Person !";
    }
}

class Student extends Person{
    public String toString(){
        return "Student !";
    }
}

class GraduateStudent extends Student{
    public String toString(){
        return "GraduateStudent !";
    }
}
```