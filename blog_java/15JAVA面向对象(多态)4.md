# JAVA面向对象4(多态)

## 一.静态成员和实例成员的区别

### 1.为什么使用静态变量

> 静态变量可以被类的所有实例共享，无论一个类创建了多少个对象，它们都共
> 享同一份静态变量。
> 也就是说，静态变量只会被分配一次内存，即使创建多个对象，这样可以节省
> 内存。

### 2.静态方法为什么不能调用非静态成员?

> 静态方法是属于类的，在类加载的时候就会分配内存，可以通过类名直接访
> 问。
> 非静态成员属于实例对象，只有在对象实例化之后才存在，需要通过类的实例
> 对象去访问。
> 在类的非静态成员不存在的时候静态方法就已经存在了，此时调用在内存中还
> 不存在的非静态成员，属于非法操作。

### 3.静态方法和实例方法有何不同？

> 调用方式不同
> 在外部调用静态方法时，可以使用 类名.方法名 的方式，也可以使用 对象.
> 方法名 的方式，而实例方法只有后面这种方式。也就是说，调用静态方法
> 可以无需创建对象 。
> 不过，需要注意的是一般不建议使用 对象.方法名 的方式来调用静态方法。
> 这种方式非常容易造成混淆，静态方法不属于类的某个对象而是属于这个
> 类。因此，一般建议使用 类名.方法名 的方式来调用静态方法。
> 访问类成员是否存在限制
> 静态方法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静
> 态方法），不允许访问实例成员（即实例成员变量和实例方法），而实例方
>
> 法不存在这个限制

### 4.静态成员的特点

- 只有一份
- 类加载时初始化
- 在所有实例间共享

静态成员包括哪些

- 静态变量
- 静态方法
- 静态块

### 5.内存分配

```java
public class Person {
String name; // 实例属性
String gender; // 实例属性
static int live = 1; // 静态属性
public Person(String name, String gender) {
this.name = name;
this.gender = gender;
}
public void sayHello(){
System.out.printf("我是%s,%s生,我们都知道人的生命只有%d次
\n",this.name,this.gender,Person.live);
}

                  
public static void main(String[] args) {
Person p1 = new Person("美少女","女");
Person p2 = new Person("浩哥","男");
p1.sayHello();
p2.sayHello();
}
}
```

第一步：加载类
运行该程序，JVM会执行Person.main()来启动程序（第15行代码），此时
第一次出现了类Person
程序运行期间，第一次出现类名Person时，开始加载类Person，将Person
的字节码文件Person.class从硬盘加载到内存的元空间，如图中的红色部分
所示。
第二步：初始化静态成员
类Person加载后立即为类的静态成员分配内存（静态变量，静态方法都分
配内存），静态成员分配在元空间中，如图中蓝色部分
第4行的静态变量live被分配了内存
提示：不现在没有创建Person类的对象，此时静态成员已经分配了内存
第三步：实例化对象
静态成员分配完内存后，开始执行main方法中的代码
创建p1对象：第16行代码，图中绿色部分
第一步：在堆中为p1分配name和gender的内存
第二步：在栈中为p1分配内存
第三步：p1指向堆中分配的内存
创建p2对象：第17行代码，图中紫色部分
第一步：在堆中为p2分配name和gender的内存
第二步：在栈中为p2分配内存
第三步：p2指向堆中分配的内存
public static void main(String[] args) {
Person p1 = new Person("美少女","女");
Person p2 = new Person("浩哥","男");
p1.sayHello();
p2.sayHello();
}
}
![image-20230818194002191](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308181940273.png)

### 小结：

- 对象的实例new几次就分配几次内存，不new就没有分配内存
- 静态变量在类加载时初始化，分配内存，不new对象，静态变量也分配了内存
- 静态变量只有一份，所有实例共享一份静态变量
- 实例方法可以访问静态成员，因为内存中一定存在静态成员
- 静态方法不允许访问实例成员，因为实例成员不new，内存中就不存在实例成员
- 静态方法中如果要访问实例成员，必须先new出实例，然后由对象的引用调用

## 二.多态

> 多态是面向对象的三大特征之一。
> 多态一词的通常含义是指能够呈现出多种不同的形式或形态。而在程序设计术语中，
> 它意味着一个特定类型的变量，可以引用不同类型的对象，并且能自动地调用引用的
> 对象的方法。
> 也就是根据用到的不同对象类型，响应不同的操作。方法重写是实现多态的基础。通
> 过下面的例子可以简单认识什么是多态

### 例子

```java
public class Pet {
public void toHospital() {
System.out.println("宠物去医院");
}
}
class Dog extends Pet {
@Override
public void toHospital() {
System.out.println("狗去医院");
}
}
class Bird extends Pet {
@Override
public void toHospital() {
System.out.println("鸟去医院");
}
    
    
}
class Test {
public static void main(String[] args) {
Dog dog = new Dog();
dog.toHospital();
Bird bird = new Bird();
bird.toHospital();
Pet pet; //声明一个pet类
pet = new Dog(); //创建一个dog对象赋值给dog变量
pet.toHospital();
pet = new Bird();
pet.toHospital();
}
}
```

> 注意:多态意味着在一次方法调用中根据包含的对象的实际类型（即实际子类的对
> 象）来决定应该调用哪个子类的方法，而不是由用来存储对象引用的变量的
> 类型决定的。当调用一个方法时，为了实现多态操作，这个方法即是在父类
> 中声明过的，也必须是在子类中重写过的方法。

### 使用

1. **编译时多态：**
   - 也称为静态多态性。
   - 发生在编译阶段，即在代码编译为机器代码之前。
   - 主要涉及方法的重载（方法名相同，参数列表不同）。
   - 在编译时，编译器根据方法的参数列表确定要调用的方法，编译器能够在编译时静态地决定使用哪个方法。
2. **运行时多态：**
   - 也称为动态多态性。
   - 发生在程序运行时，即在代码实际执行时。
   - 主要涉及方法的重写（子类重写父类的方法）和接口的实现。
   - 在运行时，实际调用的方法会根据对象的实际类型（而不是变量的声明类型）来确定，这使得不同类型的对象可以表现出不同的行为。

### 实现多态的三个条件

1. **继承（Inheritance）：** 存在继承关系，其中一个类是另一个类的子类。子类继承了父类的属性和方法。
2. **方法重写（Method Overriding）：** 子类必须重写（覆盖）父类的方法，以便在子类中实现特定的行为。子类中重写的方法的方法签名必须与父类中的方法相同。
3. **父类引用指向子类对象（Upcasting）：** 父类可以引用其子类的对象。这意味着可以将子类对象赋值给父类引用变量，从而使用父类引用来调用子类中重写的方法。

## 三.类型转换

### 1.向上转型

子类向父类转换称为向上转型。
向上转型的语法格式如下：

```java
父类类型 引用变量名 = new 子类类型();
```

例如： 

```java
Pet pet = new Dog();
```

> 之前介绍了基本数据类型之间的类型转换，

> 1 把int类型常量或变量赋值给double类型的变量，可以自动进行类型转换。
> 2 把double类型的常量或变量赋值给int类型的变量，必须进行强制转换。
> 实际上在引用数据类型的子类和父类之间也存在着类型转换问题

```java
pet pet = new Dog(); // 子类转换成父类，也称为父类引用指向子类对象
pet.toHospital(); // pet 对象调用的是Dog类的toHospital() 方法，体
现了多态。
```

> 多态就是说一个父类可能有多个子类，每个子类都重写了父类的方法（每个子类都有
> 不同的方法实现），当父类引用调用方法时，父类引用指向哪个子类，就调用哪个子
> 类的方法，形成了父类引用调用相同的方法名称时，有不同的输出形态。

### 2.向下转型

 前面已经提到，当向上转型发生后，将无法调用子类新增的方法。但是如果需要调用
子类新增的方法，可以通过把父类转换为子类实现。
将一个指向子类对象的父类引用赋值给一个子类的引用，即将父类类型转换为子类类
型，称为向下转型，此时必须进行强制类型转换。
向下转型的语法规则如下。

> 子类类型 引用变量名 = (子类类型) 父类类型的引用变量;
> 例如：

```java
 Dog dog = (Dog)pet;
```

> 注意转型时的继承关系

> 常见的错误转型格式
>
> ```java
> Cat cat = (Cat) new Dog(); // 编译错误，Cat 和 Dog 没有继承关系
> 
> Animal animal = new Animal();
> Dog dog = (Dog) animal; // 编译错误，Animal 不是 Dog 的父类
> 
> Animal animal = null;
> Dog dog = (Dog) animal; // 运行时 NullPointerException 异常
> 
> Animal animal = new Dog();
> Mammal mammal = (Mammal) (Animal) animal; // 转型过多，但是可能不必要
> ```

### 通常使用instance of 来检查转型的安全性

```java
Animal animal = new Dog(); // 假设有继承关系
if (animal instanceof Dog) {
    Dog dog = (Dog) animal; // 向下转型
    dog.fetch(); // 可以安全地调用 Dog 类的方法
} else {
    System.out.println("animal is not a Dog");
}
```

### instanceof 运算符

在向下转型过程中，如果不是转换为真实的子类类型，会出现类型转换异常。所以在
Java中提供了instanceof运算符来进行类型转换的判断。
使用instanceof时，对象的类型必须和instanceof后面的参数所指定的类有继承关
系，否则会出现编译错误。
在使用instanceof时，先判断获取的对象是否是某一类型，再做强制类型转换，
然 后 再 对 对 象 进 行 操 作 。 这 是 传 统 的 写 法 ， 在 Java 16 的 增 强 之 后 ， 对 于
instanceof的判断以及类型转换可以合二为一了;使得代码可以更加简洁和易读，特别是在处理类型转换时。这个新用法被称为"模式匹配"（Pattern Matching），它可以结合 `instanceof` 和类型转换操作，使代码更加紧凑和类型安全。

例如:

```java
class Animal {
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();

    // 使用 instanceof 模式匹配
    if (animal instanceof Dog dog) {
        dog.bark(); // 可以直接在条件块内使用 dog 变量，不需要再进行强制类型转换
    } else {
        System.out.println("animal is not a Dog");
   }
}
}
```

此外，在Java中，可以使用getClass()方法来进行类型转换的判断。getClass()方
法是Object类的一个方法，所有Java类都继承自Object类，因此它可以在任何对
象上调用。

例如:

```java
class Animal {
}

class Dog extends Animal {
}

class Cat extends Animal {
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); //实例化dog

    if (animal.getClass() == Dog.class) {
       System.out.println("The animal is a Dog");
    } else if (animal.getClass() == Cat.class) {
        System.out.println("The animal is a Cat");
    } else {
        System.out.println("The animal is not a Dog or a Cat");
    }
}

}
```

> 注意:getClass()返回的是运行时类的Class对象，所以比较时要使用==运算符，而
> 不是使用equals()方法。
>
> 另外，使用getClass()方法进行类型转换的判断通常
> 用于处理特定类型的对象，而不是用于处理继承层次结构的类型判断。在处
> 理继承层次结构时，通常会使用instanceof运算符来进行更灵活和安全的类
> 型检查

### 多态的应用

从上面的例子不难发现，多态的优势非常突出。
可替换性：多态对已存在的代码具有可替换性。
可扩充性：多态对代码具有可扩充性。增加新的子类不影响已存在类的多态性、继承
性，以及其他特性的运行和操作。实际上新加子类更容易获得多态。
接口性：多态是父类向子类提供了一个共同接口，由子类来具体实现。
灵活性：多态在应用中体现了灵活多样的操作，提高了使用效率。
简化性：多态简化了应用软件的代码编写和修改过程，尤其在处理大量对象的运算和
操作时，这个特点尤为突出和重要。
在多态的程序设计中，一般有以下两种主要的应用形式。

