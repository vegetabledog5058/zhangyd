# JAVA基础4(循环)

## 1.循环执行顺序以及关系

### 1.while

使用方法：先判断，在执行；当条件[表达式](https://so.csdn.net/so/search?q=表达式&spm=1001.2101.3001.7020)成立时，则执行循环体，然后在进行判断，如果条件不成立时，有可能不执行。一般用于循环次数不确定的循环

```java
//while（布尔（true/false）表达式）{
//循环内容 
//只要布尔表达式为 true 循环体就会一直执行下去。
	public static void main(String args[]) {
		int x = 10;
		while (x < 20) {
			System.out.print("value of x :" + x);
			x++;
			System.out.print("\n");
	}
}
```

​	public static void main(String args[]) {
​		int x = 10;
​		while (x < 20) {
​			System.out.print("value of x :" + x);
​			x++;
​			System.out.print("\n");
​		
​	}
}

### 2.do while

使用方法：先执行，后判断；一般用于循环次数不确定的循环，与while循环不同的是先执行后判断，至少会执行一次(不常用)

```java
//do{
//	//代码语句
//	}while（布尔值表达式）；

//	注意：布尔表达式在循环体的后面，所以语句块在检测布尔表达式之前已经执行了。如果布尔表达式值为true，则语句块while(true)--死循环
//一直执行，直到布尔表达式的值为false。

//	实例:
public class Test {
	public static void main(Staing args[]) {
		int x = 10;
		do {
			System.out.print("value of x :" + x);
			x++;
			System.out.print("\n");
		} while (x < 20);
	}
}
```

### 3.for

for循环执行的次数是在执行前就确定的。语法格式如下:
	//for (  1初始化;  2布尔表达式; 4更新){
			3//代码语句
	//}

```java
//关于for循环有以下几点说明：
//1，最先执行初始化步骤。可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句。for(;;)--死循环
//2，然后，检测布尔表达式的值。如果是true，循环体被执行，如果是false，循环体终止，开始执行循环后面的语句。
//3，执行一次循环后，更新循环控制变量。
//4，再次检测布尔表达式。循环执行上面的过程。
public class Test{
	public static void main (Staing args[ ]){
	for(int x=10;x<20;x=x+1){
	System.out.print("value of x :"+x);
	System.out.print("\n");
			}
		}
}
```

## 2.循环嵌套的执行顺序

1.先判断最外层循环条件，若满足条件则进入第一层循环体;

2.进入第一层循环体后进行第二层循环条件判断，若满足判断条件，进入第二层循环体;

3.由内而外执行循环体操作；

4.执行完第一次内循环体操作后，进行内循环体变量累加，再次执行内循环体操作，直到不满足进入内循环体条件为止；

5.执行外循环体操作；

6.在第一次外循环体操作完成后，外循环体变量累加，回到步骤1，判断是否满足进入外循环体条件，若满足条件，再次依次执行上述步骤，直到不满足进入外循环体条件为止；

7.彻底退出嵌套循环操作。



简单来说,循环总是会先执行最外层循环,满足条件后开始执行内循环,多条循环嵌套时同理.

例如图中1,为外循环,2,3为外循环

![image-20230803221026816](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308032210189.png)

## 3.for与while区别

### 1、for循环：

适合循环次数是已知的操作。如：

int number = 10;
for(int i = 0;i <= number;i++){
    system.out.print(i + "\t");
}

### 2、while循环：

适合循环次数是未知的操作。如：

```java
int number = 0;
while(number < 10){
    system.out.print(number + "\t");
    number++;
}
```

3、do...while...循环：适合至少执行一次的循环操作（注：while循环需要有“；”结尾）。如：

```java
boolean flag;
    do{
	flag = false;//自我的约定，标识。 false代表没有输入错误，true输入错误了
	System.out.println("------------------欢迎使用XXXATM自助服务------------------");
	System.out.println("1.存款  2.取款  3.转账  4.查询余额  5.修改密码  6.退出");
	int choice = input.nextInt();
	switch(choice){
	    case 1:
	        save();//存款
//	        showMenu();
		flag=true;
		break;
	    case 2:
		take();//取款
//		showMenu();
		flag=true;
		break;
	    case 3:
		transfer();//转账
//		showMenu();
		flag=true;
		break;
	    case 4:
		checkBalance();//查询余额
		flag=true;
		break;
	    case 5:
		updatePwd();//修改密码
		break;
	    case 6:
		return;
	    default:
		System.out.println("输入错误，请重新输入！");
		flag = true;//输入错误了，应该循环了
		break;
        }
    }while(flag);
```



## 4.利用for循环嵌套打印菱形和圣诞树(练习)

### 1.菱形

```java
public static void main(String[] args) {
    for(int i=1;i<=7;i++){
        for(int j=7;j>i;j--){
            System.out.printf(" ");

        }  for (int k = 0; k <2*i-1; k++) {
            System.out.print("*");
        }
        System.out.println();
    }
    for(int i=1;i<7;i++){
        for(int j=0;j<i;j++){
            System.out.printf(" ");

        }  for (int k =2*(7-i)-1; k >0; k--) {
            System.out.print("*");
        }
        System.out.println();
    }

}
```

![image-20230803221206046](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308032212180.png)

### 2.圣诞树

![image-20230803221438715](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308032214812.png)

```java
public static void main(String[] args) {
    int j=0;
    for (int i = 1; i <=4; i++) {
        for (j = 12; j >= i; j--) {
            System.out.print(" ");
        }for (int k = 0; k <2*i-1; k++) {
            System.out.print("*");
        }
        System.out.println();
    }
    for (int i = 1; i <=3; i++) {
        for (j = 10; j >= i; j--) {
            System.out.print(" ");
        }for (int k = 0; k <(2*i-1)+4; k++) {
            System.out.print("*");
        }
        System.out.println();
    }
    for (int i = 1; i <=3; i++) {
        for (j = 9; j >= i; j--) {
            System.out.print(" ");
        }for (int k = 0; k <(2*i-1)+6; k++) {
            System.out.print("*");
        }
        System.out.println();
    }
    for (int i = 1; i < 7; i++) {
        for ( j = 1; j <= 11; j++) {
            System.out.print(" ");
        }for (int k = 0; k <3; k++) {
            System.out.print("*");
        }
        System.out.println();

    }

}
```