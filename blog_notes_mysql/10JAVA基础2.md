# JAVA基础

## 1.next()与nextLine()之间的区别

- `next()`: 读取输入中的下一个以空格分隔的单词（仅读取到空格之前的内容）。
- `nextLine()`: 读取输入中的整行内容（包括空格）。

next()-->输入了空格,因此在"si"输出后结束

![image-20230801171738855](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011717886.png)

nextLine()

![image-20230801173142471](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011731507.png)

## 2.byte在运算时强制转换

如图如果

byte a = 2;
byte b = 3;
byte c = a+ b;

直接相加会报错,因为当两个byte相加时,自动会转换为int类型,再次byte定义会导致int -->byte

![image-20230801141321612](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011413655.png)

解决这种情况,可以使用强制转换

![image-20230801142132549](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011421582.png)

或者使用int定义c,这样数据类型相符也能直接输出

![image-20230801142457779](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011424824.png)

 另一种情况中a+=b算出等于-125,原因是不超过范围的情况下,系统会自动将其强制转换为byte

![image-20230801143532016](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011435047.png)

## 3.异或运算中两个数的互换(不使用其他变量)

其中

已经知道a = a^b;b = a^b;并且两个相同异或运算再与另一个变量异或运算等于另一个变量本身,(如:a^b^a=b)

因此:b = a^b;此处可以理解为:b=(a^b)^b=a;同理:a=a^(a^b)=b;因此两数成功位置进行了互换并且不需要借助其他变量暂存.

![image-20230801193024534](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308011930604.png)

## 4.printf与println的区别

  **`printf`：**

- `printf` 是一个格式化输出方法，它可以根据指定的格式输出文本。它类似于C语言的 `printf` 函数。



**`println`：**

`println` 是一个用于输出文本并换行的方法。它将文本输出到控制台，并在输出完成后自动换行。

### 常用的格式化输出字符

1. **整数类型：**
   - `%d`: 十进制整数。
   - `%o`: 八进制整数。
   - `%x` 或 `%X`: 十六进制整数，小写或大写。
   - `%f`: 十进制浮点数。
2. **字符和字符串：**
   - `%c`: 字符。
   - `%s`: 字符串。
3. **布尔类型：**
   - `%b`: 布尔值（true 或 false）。
4. **其他类型：**
   - `%e` 或 `%E`: 科学计数法浮点数，小写或大写。
   - `%g` 或 `%G`: 根据数值不同，自动选择 `%f` 或 `%e` 格式，小写或大写。
5. **宽度和精度：**
   - `%n`: 换行符。
   - `%t`: 日期/时间格式化。

## 5.关于JDK17在javac编译后乱码的问题

JDK17中需要输入

```cmd
-Dfile.encoding=utf8 CLASS_NAME.java
```

JDK8 中用

```cmd
encoding=utf8 CLASS_NAME.java
```

