---
title: java学习笔记
date: 2020-05-13 14:32:05
tags:
---
# 正则表达式
## split
### 根据 "."切割 IP 地址
#### 错误代码
```
public class Spilt {
    public static void main(String[] args){
        String s = "192.168.0.111";
        String[] list = s.split(".");
        for (String result : list){
            System.out.println(result);
        }
    }
}
/*

*/
```
#### 正确代码
```
public class Spilt {
    public static void main(String[] args){
        String s = "192.168.0.111";
        String[] list = s.split("\\.");
        //String[] list = s.split("[.]");
        for (String result : list){
            System.out.println(result);
        }
    }
}
/*
192
168
0
111
*/
```
### 按照数字分割

```
 public class Spilt {
    public static void main(String[] args){
        String s = "1Java2C3C++4python";
        String[] list = s.split("[\\d]");
        for (String result : list){
            System.out.println(result);
        }
    }
}
/*

Java
C
C++
python
*/
```
## matches
是就返回true，否则返回false
### 匹配字符串
```
public class Spilt {
    public static void main(String[] args){
        String s = "java is fun";

        //匹配字符串是否为java
        System.out.println(s.matches("java"));

        //匹配字符串是否是java+一个字符
        System.out.println(s.matches("java."));

        //匹配字符串是否是java+任意多个字符（也可没有）
        System.out.println(s.matches("java.*"));

        //匹配字符串是否是java+至少一个字符
        System.out.println(s.matches("java.+"));

        //匹配字符串是都包含is
        System.out.println(s.matches(".*is.*"));

    }
}
/*
false
false
true
true
true
 */
```
# 字符串类型转换及命令行参数
## 基本数据类型对应的包装累
- Character —— char 类型
- Double —— double 类型
- Integer —— int 类型
- 这些包装类封装了一些静态方法

## 字符串与数值类型间的互相转换
- 将字符串转换为 int 型
> **int intValue = Integer.parseInt(intString);**
- 将字符串转换为 double 型
> **double doubleValue = Double.parseDouble(doubleString);**

- 将数值转换为字符串类型

> 1. **String s = doubleValue + "";**
> 2. **Integer.ToString(intValue);**
> 3. **String.valueOf(intValue);**

## 完成简单的命令行四则运算计算器
### 代码内容
```
package ooo;

public class Calculator {
    public static void main(String[] args) {

        //输入时的元素与元素之间要用空格隔开
        //判断输入形式是否正确

         if (args.length!=3){
             System.out.println("Usage : java Calculator 2+3");
             System.exit(0);//退出
         }

         int result = 0;

         switch(args[1].charAt(0)){
             case '+':
                 result = Integer.parseInt(args[0])+Integer.parseInt(args[2]);
                 break;

             case '-':
                 result = Integer.parseInt(args[0])-Integer.parseInt(args[2]);
                 break;

             case '*':
                 result = Integer.parseInt(args[0])*Integer.parseInt(args[2]);
                 break;

             case '/':
                 result = Integer.parseInt(args[0])/Integer.parseInt(args[2]);
                 break;
         }
        System.out.println(args[0]+' '+ args[1]+' '+args[2]+" = "+result);
    }
}
```
### 使用命令行输入
> - *C:\Users\80975\IdeaProjects\untitled\src>javac ooo/Calculator.java*

> - *C:\Users\80975\IdeaProjects\untitled\src>java ooo.Calculator 5 "*" 3
5 * 3 = 15*
(注意乘号需要加双引号)

> - *C:\Users\80975\IdeaProjects\untitled\src>java ooo.Calculator 5 + 3
> 5 + 3 = 8*

# 其他
```
public class Demo1 {
    public static void main(String[] args) {
        String s1 = "I Love You.";
        String s2 = new String("I Love You.");
        String s3 = "I Love You.";
        String s4 = new String("I Love You.");
//        System.out.println("s1与s3是否相同："+(s1==s3));
//        System.out.println("s2与s4是否相同："+(s2==s4));
/*
s1与s3是否相同：true
s2与s4是否相同：false
s1 是不可变字符串
 */
//        System.out.println("s1与s2是否相同："+(s1==s2));
//        System.out.println("s1与s2是否相同："+s1.equals(s2));
/*
s1与s2是否相同：false
s1与s2是否相同：true
由此可见
equals是比较两个字符串的值
==是比较地址
*/
//        System.out.println(s1.length());
        /*
        11
        字符个数就是字符串长度。
         */
//        System.out.println(s1.charAt(4));
        /*
        v
        取下标为4的字符，从0开始。
         */
//        System.out.println(s1.substring(2,6));
        /*
        Love
        取子串，2是起始位置的下标(闭区间)，6是结束位置的下标(开区间)，
         */
//        System.out.println(s1.toLowerCase());
        /*
        i love you.
        把字符串转化为小写形式
         */
//        System.out.println(s1.toUpperCase());
        /*
        I LOVE YOU.
        把字符串转化为大写形式
         */
//        System.out.println("    (i love you.)    ".trim());
        /*
         (i love you.)
         删除两端的空格
         */
//        System.out.println("i love you.".replace('o','X'));
//        System.out.println("i love you.".replace("o","X"));
//        System.out.println("i love you.".replace("ou","XX"));
//        System.out.println("i love you.".replaceFirst("o","X"));
//        System.out.println("i love you.".replaceAll("o","X"));
        /*
        i lXve yXu.  把找到的所有都替换
        i lXve yXu.  同上
        i love yX.   可以以字符串换字符串
        i lXve you.  替换找到的第一个
        i lXve yXu.  字符串可以是特殊的字符串
         */
//        System.out.println("I Love You.".indexOf('x'));
//        System.out.println("I Love You.".indexOf('o'));
//        System.out.println("I Love You.".indexOf('o',4));
//        System.out.println("I Love You.".indexOf("Love"));
//        System.out.println("I Love You.".lastIndexOf('o'));
//        System.out.println("I Love You.".lastIndexOf('o',0));
        /*
        -1  找不到返回-1
         3  找得到返回第一个的下标
         8  从下标为4开始查找
         2  查找字符串，返回字符串首字母的下标
         8  反向搜索
         -1 答案永远为-1
         */
//        int k="I Love You.txt".lastIndexOf(".");
//        System.out.println("I Love You.txt".substring(k+1));
        /*
        txt     可用于查找文件类型
         */
//        String[] list = s1.split(" ");
//        System.out.println();
//        for(String result:list){
//            System.out.println(result);
//        }
        /*
        I
        Love
        You.
         */
    }
}
```


 


