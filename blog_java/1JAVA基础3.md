# JAVA基础3

## 1.switch 和 if 的区别

### switch后只能跟等值判断

比如:

```java
int num = 2;
switch (num) {
    case 1:
        // 当num的值等于1时，执行这里的代码
        break;
    case 2:
        // 当num的值等于2时，执行这里的代码
        break;
    case 3:
        // 当num的值等于3时，执行这里的代码
        break;
    default:
        // 如果没有匹配的值，则执行这里的代码
}


```

因此switch中可以使用字符串类型的判断

```java
 Scanner sc = new Scanner(System.in);
 double a = sc.nextInt();
 double b = sc.nextInt();
 String c = sc.next();

 switch (c){
    case "+"-> System.out.println(a+b);
    case "-"-> System.out.println(a-b);
    case "*"-> System.out.println(a*b);
    case "/"-> System.out.println(a/b);
     default -> System.out.println("无效");
};
```

这里的运算符可以通过switch来进行等值判断

### if更适合连续区间的判断

没有switch选择结构的限制，适合某个变量处于某个连续区间时的情况。

比如:

if

```java
int num = 5;
if (num >= 1 && num <= 5) {
    // num在范围[1, 5]内，执行这里的代码
} else if (num >= 6 && num <= 10) {
    // num在范围[6, 10]内，执行这里的代码
} else {
    // 不在以上范围内，执行这里的代码
}
```

switch

```sql
int num = 5;
switch (num) {
    case 1 to 5: // 错误，不能直接使用范围
        // 执行这里的代码
        break;
    case 6 to 10: // 错误，同样不能使用范围
        // 执行这里的代码
        break;
    default:
        // 执行这里的代码
}


```



## 2.yield

大多数时候,switch表达式内部,外面会返回简单的值,但是如果需要复杂的语句,我们也可以写很多语句放在{}内,然后此时需要用yield返回一个值作为switch语句的返回值

### 3.题目练习

//输入年月,输出天数

```java
         Scanner sc = new Scanner(System.in);
        System.out.println("输入年份");
        int year = sc.nextInt();
        System.out.println("输入月份");
        int month = sc.nextInt();

        switch (month){
            case 1,3,5,7,8,10,12 -> System.out.println("31");
            case 2 -> {
                if (year % 4 != 0 || year % 400 != 0) {
                    System.out.println("28");
                } else {
                    System.out.println("29");
                }
            }
            case 4,6,9,11 -> System.out.println("30");

        }

```

> 计算器

* 编写一个简单的计算器程序，要求用户输入两个数和操作符（+、-、*、/），然后根据操作符进行相应的运算，并输出结果。如果输入的运算符不是有效的运算符，则输出"无效的运算符"。

```java
import javax.xml.transform.Result;
import java.util.Scanner;

/**
 * @Author:Yinan
 * @DATE:
 */

/*
    编写一个简单的计算器程序，要求用户输入两个数和操作符（+、-、*、/），然后根据操作符进行相应的运算，并输出结果。
    如果输入的运算符不是有效的运算符，则输出"无效的运算符"。
 */
public class Test02 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入第一个值：");
        double a = sc.nextDouble();
        System.out.println("请输入第二个值：");
        double b = sc.nextDouble();
        System.out.println("请输入需要执行的计算（+、-、*、/）：");
        String c = sc.next();
        switch (c) {
            case "+" -> {
                double result = a+b;
                System.out.printf("计算的结果为：%f F \n", result);
            }
            case "-" -> {
                double result = a-b;
                System.out.printf("计算的结果为：%f F \n", result);
            }
            case "*" -> {
                double result = a*b;
                System.out.printf("计算的结果为：%f \n", result);
            }
            case "/" -> {
                double result = a/b;
                System.out.printf("计算的结果为：%f \n", result);
            }
        }
    }
}
```



> 季节

* 编写一个程序，根据用户输入的月份（1 到 12），输出该月份所属的季节。假设春季是 3到 5 月，夏季是 6 到 8 月，秋季是 9 到 11 月，冬季是 12、1 和 2月。如果输入的月份超出了范围，输出"输入错误"。

```java
import java.util.Scanner;
import java.util.zip.Deflater;

/**
 * @Author:Yinan
 * @DATE:
 */
/*
编写一个程序，根据用户输入的月份（1 到 12），输出该月份所属的季节。假设春季是 3到 5 月，夏季是 6 到 8 月，
秋季是 9 到 11 月，冬季是 12、1 和 2月。如果输入的月份超出了范围，输出"输入错误"。
 */

public class Test04 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个月份：");
        int month = sc.nextInt();
        /*方法一
        switch (month){
            case 3,4,5 -> System.out.println("这个月份是春季！！");
            case 6,7,8 -> System.out.println("这个月份是夏季！！");
            case 9,10,11 -> System.out.println("这个月份是秋季！！");
            case 12,1,2 -> System.out.println("这个月份是冬季！！");
            default -> System.out.println("您输入的月份无效");
        }
         */
        //方法二
        if (month == 3 || month == 4 || month == 5 ){
            System.out.println("这个月份是春季！！");
        }else if (month == 6 || month == 7 || month == 8 ){
            System.out.println("这个月份是夏季！！");
        }else if (month == 9 || month == 10 || month == 11 ){
            System.out.println("这个月份是秋季！！");
        }else if (month == 12 || month == 1 || month == 2 ){
            System.out.println("这个月份是冬季！！");
        }else {
            System.out.println("您输入的月份无效");
        }
    }
}
```

>星座

* 编写一个程序，根据用户输入的月份和日期，输出该日期所在的星座。以下是一个简单的星座日期范围参考：

|  水瓶座（1月20日到2月18日）  |  双鱼座（2月19日到3月20日）  |
| :--------------------------: | :--------------------------: |
|  白羊座（3月21日到4月19日）  |  金牛座（4月20日到5月20日）  |
|  双子座（5月21日到6月20日）  |  巨蟹座（6月21日到7月22日）  |
|  狮子座（7月23日到8月22日）  |  处女座（8月23日到9月22日）  |
| 天秤座（9月23日到10月22日）  | 天蝎座（10月23日到11月21日） |
| 射手座（11月22日到12月21日） | 魔羯座（12月22日到1月19日）  |

```java
import java.util.Scanner;

/**
 * @Author:Yinan
 * @DATE:
 */
/*
编写一个程序，根据用户输入的月份和日期，输出该日期所在的星座。
 */
public class Test05 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入月份：");
        int month = sc.nextInt();
        System.out.println("请输入日期：");
        int day = sc.nextInt();
        switch (month) {
            case 1 -> {
                if (day >= 20 && day < 32) {
                    System.out.println("您的星座为水瓶座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为摩羯座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 2 -> {
                if (day >= 19 && day < 29) {
                    System.out.println("您的星座为双鱼座！");
                } else if (day > 0 && day < 29) {
                    System.out.println("您的星座为水瓶座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 3 -> {
                if (day >= 21 && day < 32) {
                    System.out.println("您的星座为白羊座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为双鱼座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 4 -> {
                if (day >= 20 && day < 31) {
                    System.out.println("您的星座为金牛座！");
                } else if (day > 0 && day < 31) {
                    System.out.println("您的星座为白羊座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 5 -> {
                if (day >= 21 && day < 32) {
                    System.out.println("您的星座为双子座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为金牛座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 6 -> {
                if (day >= 21 && day < 31) {
                    System.out.println("您的星座为巨蟹座！");
                } else if (day > 0 && day < 31) {
                    System.out.println("您的星座为双子座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 7 -> {
                if (day >= 23 && day < 32) {
                    System.out.println("您的星座为狮子座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为巨蟹座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 8 -> {
                if (day >= 23 && day < 32) {
                    System.out.println("您的星座为处女座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为狮子座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 9 -> {
                if (day >= 23 && day < 31) {
                    System.out.println("您的星座为天秤座！");
                } else if (day > 0 && day < 31) {
                    System.out.println("您的星座为处女座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 10 -> {
                if (day >= 23 && day < 32) {
                    System.out.println("您的星座为天蝎座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为天秤座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 11 -> {
                if (day >= 22 && day < 31) {
                    System.out.println("您的星座为射手座！");
                } else if (day > 0 && day < 31) {
                    System.out.println("您的星座为天蝎座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            case 12 -> {
                if (day >= 22 && day < 32) {
                    System.out.println("您的星座为摩羯座！");
                } else if (day > 0 && day < 32) {
                    System.out.println("您的星座为射手座！");
                } else {
                    System.out.println("您输入的日期无效！");
                }
            }
            default -> System.out.println("您输入的月份无效");
        }
    }
}
```

> 奖金

* 编写一个程序，根据员工的工龄来计算年终奖金。奖金计算规则如下：

1. 工龄小于等于5年，奖金为工资的5%
2. 工龄大于5年且小于等于10年，奖金为工资的10%
3. 工龄大于10年，奖金为工资的15%
4. (工资和工龄输入)

```java
import java.util.Scanner;

/**
 * @Author:Yinan
 * @DATE:
 */
/*
    编写一个程序，根据员工的工龄来计算年终奖金。奖金计算规则如下：
     工龄小于等于5年，奖金为工资的5%
     工龄大于5年且小于等于10年，奖金为工资的10%
     工龄大于10年，奖金为工资的15%
 */
public class Test06 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入您的工资：");
        double salary = sc.nextDouble();
        System.out.println("请输入您的工龄：");
        int year = sc.nextInt();
        salary *=12;
        if (year <= 5 & year > 0) {
            salary *=0.05;
        } else if (year>5&year<=10) {
            salary *=0.1;
        }else if (year>10){
            salary *=0.15;
        }
        System.out.printf("您的奖金为：%f 元",salary);
    }
}

```

