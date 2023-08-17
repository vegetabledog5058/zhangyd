# 面向对象3(继承及object类)

## 1.继承中的实例化过程(面试题)

### 1.静态变量的隐藏

> 父类

```  java
public class Sup {


    static int a = 1;

    static {
        b = 3;
    }

    static int b = 2;

    public Sup(int a, int b) {
        print();
        this.a = a;
        this.b = b;
        print();
    }

    public void print() {
        System.out.println(a);
        System.out.println(b);
    }
}
```

> 子类

```java
public class Sub extends Sup {

    static int a = 11;
    static int b = 22;


    public Sub(int a, int b) {
        super(a, b);
        print();
    }

    @Override
    public void print() {
        System.out.println("Sub: " + this.a);
        System.out.println("Sub: " + this.b);
        System.out.println("Sup: " + super.a);
        System.out.println("Sup: " + super.b);
    }

}
```

> 测试类

```java
 public static void main(String[] args) {
        Sub sub = new Sub(6, 9);
        // 调用 static 方法时，看 sub 对象的类型是谁
    }
```

> 过程:
>
> 1.**Main 方法执行：** 在 `main` 方法中，首先创建了一个 `Sub` 类的对象 `sub`，通过调用 `Sub` 类的构造函数，传递参数 `6` 和 `9`。接着，程序将执行构造函数中的代码
>
> 2.之后是父类Sup的静态初始化,a和b默认值为0,之后赋值为a=1;b=3;之后b再次赋值为2,这一步时a=1,b=2;
>
> <img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171845440.png" style="zoom:33%;" />
>
> 3.调用print方法,这里Sub重写了print方法,因此执行子类Sub的print方法,打印当前ab的值,此时ab的值被子类隐藏,因此this结果是11和22,而super打印Sup的ab值,1和2
>
> <img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171855173.png" style="zoom:30%;" />
>
> > 在 `Sub` 类的构造函数中，首先调用了父类 `Sup` 的构造函数，通过 `super(a, b)`，并传递参数 `6` 和 `9`。这里要注意，
>
> 之后在Sup方法内对静态成员变量进行赋值,将6和9的值传递,随后再次执行print方法,结果如下
>
> <img src="https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171904132.png" alt="image-20230817190350412" style="zoom:50%;" />
>
> 最后再次到sub子类,执行print方法,再次打印结果,共三次结果![image-20230817190702069](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171907299.png)

### 2.static静态方法子类对父类的隐藏

> 源代码不变,将print方法的属性改为static,以及修改方法

> ![image-20230817191355147](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171913300.png)
>
> 过程不变依旧是先进行父类的静态初始化,再到子类,然后再次执行print方法,可是这时候究竟执行的是父类的print方法还是子类的呢?
>
> 答:子类会对父类进行隐藏,这点没错,但是此时依然在父类中,隐藏只会影响子类中的方法,不会影响父类中的方法,因此此时依然会执行父类的方法,打印:Sub1 Sub2
>
> ![image-20230817193554257](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171935647.png)
>
> > 之后a和b进行赋值,打印a和b的值(a和b的值是主函数传递的参数)得到结果:
> >
> > Sub6
> > Sub9
>
> 最后执行子类的print方法,打印11,和22
>
> ![image-20230817193908863](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308171939444.png)

### 3.构造方法以及子类变量对父类的隐藏

父类

```java
public class Sup {

   int a = 1;

    static {
        b = 3;
    }

    static int b = 2;

    public Sup(int a, int b) {
        print();
        this.a = a;
        this.b = b;
        print();
    }

    public  void print() {
        System.out.println("Sub"+a);
        System.out.println("Sub"+b);
    }
}

```

子类

```java
public class Sub extends Sup {

    static int a = 11;
     int b = 22;


    public  Sub(int a, int b) {
        super(a, b);
        print();
    }

@Override
    public  void print() {

        System.out.println("Sup: " + a);
        System.out.println("Sup: " + b);
    }

}
```

> 整个的顺序是从父类加载后的的静态初始化开始,再到子类的静态初始化
>
> 因此父类中b的值是:3然后改为2,子类a的值为11
>
> 随后进行构造方法指向父类,随后开始进行实例初始化,a初始值为0;但是因为子类对父类隐藏的原因,a为11,b为子类静态初始化时默认值为0因此打印的始终是子类的变量
>
> > 注:
> >
> > 1.子类对父类的变量隐藏可以是静态和实例任意一个,只要变量名相同就可以发生隐藏
> >
> > 2.方法中只有子类的静态方法可以隐藏父类静态方法
>
> ![image-20230817204309835](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308172043356.png)
>
> 两次得到相同的结果
>
> 之后再进行子类的实例初始化,将b的值赋值为22,再次调用print方法输出此时的11和22,得到结果
>
> ![image-20230817204525031](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308172045619.png)

## 2.object类

### 1.什么是object类

> `Object` 类是所有类的根类（也称为基类或超类）。
>
> 每个类都直接或间接地继承自 `Object` 类。也就是说所有 Java 类都具有 `Object` 类所定义的方法和属性。

### 2.常见object类方法

一些 `Object` 类中常见的方法和概念：

1. **`toString()` 方法：** `Object` 类中有一个 `toString()` 方法，用于返回对象的字符串表示。在实际编程中，可以覆写方法，以便根据实际需求返回更有意义的字符串。
2. **`equals()` 方法：** `Object` 类中的 `equals()` 方法用于比较两个对象是否相等。默认情况下，它比较的是对象的引用是否相等，可以在自定义类中覆写这个方法，以便根据定义来判断两个对象是否相等。
3. **`hashCode()` 方法：** `Object` 类中的 `hashCode()` 方法返回对象的哈希码。哈希码通常用于数据结构中的查找和存储操作，例如哈希表。
4. **`getClass()` 方法：** `Object` 类中的 `getClass()` 方法返回对象所属的类的 `Class` 对象，可以用来获取对象的运行时类信息。
5. **`wait()`, `notify()`, `notifyAll()` 方法：** 用于实现多线程间的协作。`wait()` 使线程等待，`notify()` 唤醒一个等待的线程，`notifyAll()` 唤醒所有等待的线程。
6. **`finalize()` 方法：** `Object` 类中的 `finalize()` 方法是一个被垃圾回收器调用的方法，在对象被回收前执行一些清理操作。

### 3.equals方法重写的准则

1. **对称性（Symmetry）：** 如果 `a.equals(b)` 返回 `true`，那么 `b.equals(a)` 也应该返回 `true`。
2. **反射性（Reflexivity）：** 对于非空对象 `a`，`a.equals(a)` 应该始终返回 `true`。
3. **传递性（Transitivity）：** 如果 `a.equals(b)` 返回 `true`，`b.equals(c)` 返回 `true`，那么 `a.equals(c)` 也应该返回 `true`。
4. **一致性（Consistency）：** 对于任何非空对象 `a` 和 `b`，多次调用 `a.equals(b)` 应该始终返回相同的结果，前提是对象的状态没有改变。
5. **非空性（Non-nullity）：** 对于任何非空对象 `a`，`a.equals(null)` 应该返回 `false`。

### 4.tostring方法重写准则

1. **提供有意义的信息：** `toString()` 方法的返回值应该提供有关对象状态的信息，以便开发人员能够理解对象的内容。避免返回无用的信息。
2. **易于阅读：** 返回的字符串应该易于阅读和理解，而不仅仅是内存地址或者未格式化的数据。
3. **包含属性：** 如果对象有属性，通常会将这些属性包含在返回的字符串中。
4. **格式化：** 格式化返回的字符串，使其看起来整洁，可以使用换行符或空格进行分隔。
5. **考虑 null：** 考虑对象属性为 `null` 的情况，以防止 `NullPointerException`。
6. **可用性：** 重写 `toString()` 方法是为了方便开发人员，所以确保方法是公开（`public`）的。

默认方法:

>默认的 `toString()` 方法会返回一个包含类名和对象的哈希码的字符串。

```java
public class Main {
    public static void main(String[] args) {
        Object obj = new Object();
        System.out.println(obj.toString()); // 输出：java.lang.Object@hashcode
    }
}
```

> 常见重写返回打印属性

```java
public class Student {
    private String name;
    private int age;
// Constructor

// Getters and setters

@Override
public String toString() {
    return "Student{name='" + name + "', age=" + age + "}";
}
}
```

输出

```java
Student student = new Student("Alice", 20);
System.out.println(student); // 输出：Student{name='Alice', age=20}
```

## 5.getClass方法

```java
// getClass 获取对象的 Class 对象
        Class cla = stu.getClass();

        System.out.println(cla);
        // 类的全限定名
        System.out.println(cla.getName());
        // 类名
        System.out.println(cla.getSimpleName());
        // 包名
        System.out.println(cla.getPackageName());
        // 获取父类
        System.out.println(cla.getGenericSuperclass());
```

## hashCode方法

1.用法

> 用于返回对象的哈希码（散列码）。哈希码是一个整数，通常用于数据结构如哈希表中的查找和存储操作。

> 如果两个对象通过 `equals()` 方法比较是相等的，那么它们的 `hashCode()` 方法应该返回相同的哈希码值。相反如果哈希码值相同,两者不一定不一定相同

## 3.super关键字

### 1.用法

> 用于引用父类中的成员（方法、属性、构造方法）。它可以在子类中使用，以便访问继承自父类的内容。

#### **调用父类的方法或属性**

```java
class Parent {
    void method() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    void method() {
        super.method(); // 调用父类的方法
        System.out.println("Child method");
    }
}
```

#### **访问父类的成员**

```java
class Parent {
    String name = "Parent";
}

class Child extends Parent {
    String name = "Child";
    

void printNames() {
    System.out.println(super.name); // 访问父类的成员
    System.out.println(name); // 访问子类的成员
}

}
```

>在 Java 中，调用父类的构造方法需要使用 `super()` 关键字。在子类的构造方法中使用 `super()` 可以显式地调用父类的构造方法，确保父类的初始化也会发生。

#### **调用父类的默认构造方法：

 如果父类有一个默认的无参构造方法，子类的构造方法可以使用 `super()` 来调用父类的默认构造方法。

```java
class Parent {
    Parent() {
        System.out.println("Parent constructor");
    }
}

class Child extends Parent {
    Child() {
        super(); // 调用父类的构造方法
        System.out.println("Child constructor");
    }
}
```

#### **调用带参数的父类构造方法：** 

如果父类没有默认的无参构造方法，而是带有参数的构造方法，子类的构造方法可以使用 `super(参数列表)` 来调用带参数的父类构造方法。

```java
class Parent {
    Parent(String message) {
        System.out.println("Parent constructor: " + message);
    }
}

class Child extends Parent {
    Child() {
        super("Hello from Parent"); // 调用父类的构造方法，传递参数
        System.out.println("Child constructor");
    }
}
```

#### **隐式调用父类的构造方法：**

 如果子类的构造方法中没有显式调用 `super()` 或者 `this()`，则会隐式地调用父类的无参构造方法。但是，如果父类没有无参构造方法，则会编译错误。

> 注:此时要么给父类添加一个无参的构造方法或者子类中通过super关键字调用父类构造方法

```java
class Parent {
    Parent(String message) {
        System.out.println("Parent constructor: " + message);
    }
}

class Child extends Parent {
    Child() {
        // 隐式调用父类的无参构造方法，编译错误因为父类没有无参构造方法
        // super();
        System.out.println("Child constructor");
    }
}
```



