---
title: java学习笔记（一）
date: 2020-03-27 19:11:17
tags:
---
## 命名常量
- 变量名为**大写字母**
- 声明常量的语法
```
final datatype CONSTANTNAME = value;
// 定义Π
final double PI = 3.141592653;
```
- 使用常量的**好处**：
  1. 不必重复输入同一值
  2. 方便修改常量值
  3. 提高程序易读性


## 幂运算
- 使用方法：Math.pow(a,b),计算 **a** 的 **b** 次方。
- pow 定义在 java API 的 Math 类
- e.g.：
```
System.out.println(Math.pow(2,3));
```

## 整型直接量
- 默认情况下，整型直接量是一个十进制整数。
- 表示一个**二进制**整数直接量，用 **0b 或 0B** 开头
- 表示一个**八进制**整数直接量，用 **0** 开头
- 表示一个**十六进制**整数直接量，用 **0x 或 0X** 开头
- e.g.
    ``` 
    System.out.printl(0B1111);  //15
    System.out.printl(07777);   //4095
    System.out.printl(0XFFFF);  //65535
    ```

## 科学计数法
-  123.456 可以写成 1.23456E2 或 1.23456E+2
-  0.0123456 可以写成 1.23456E-2
-  为了提高可读性，2345678 课写成 23_456_78
   -  下划线必须置于两个数字之间

## 显示当前时间
```
class CurrentTime {
    public static void main(String[] args){
        // System.currentTimeMillis() 方法是获取1970年1月1日午夜到现在的的毫秒数
        long totalMilliseconds = System.currentTimeMillis();
        // totalSeconds 是总秒数
        long totalSeconds = totalMilliseconds/1000;
        // currentSecond 是现在的秒数
        long currentSecond = totalSeconds % 60;
        // totalMinutes 是总分钟数
        long totalMinutes = totalSeconds / 60;
        // currentMinutes 是现在的分钟数
        long currentMinutes = totalMinutes % 60;
        // totalHours是总小时数
        long totalHours = totalMinutes / 60 ;
        // currentHours 是标准时间加上时差，也就是现在的北京时间
        long currentHours = (totalHours + 8) % 24 ;
        System.out.println("现在的时间是："+currentHours +":" + currentMinutes + ":" + currentSecond);
    }
}
```
## 使用蒙特卡罗模拟计算Π
- 蒙特卡罗模拟是以概率统计理论为指导的统计模拟原理
  ```
public class ComputePi {
        //使用蒙特卡罗模拟计算Π
        /*蒙特卡罗模拟是以概率统计理论为指导的统计模拟原理*/
        public static void main(String[] args){
            getPi();
        }
        public static void getPi(){
            //产生随机点,点的个数决定误差大小
            final int HIT_NUMBER_OF_SQUARE = 10000000;
            //定义落在圆上的变量
            int hitNumberOfCircle = 0;
            for (int i = 0 ; i < HIT_NUMBER_OF_SQUARE ; i++ ){
                // 坐标为-1到1
                double x = Math.random() * 2 - 1;
                double y = Math.random() * 2 - 1;
                if( x * x + y * y <= 1 ) hitNumberOfCircle++;
            }
            double pi = 4.0 * hitNumberOfCircle / HIT_NUMBER_OF_SQUARE;
            System.out.println("Pi is "+pi);
        }
    }
  ```




