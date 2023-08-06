# JAVA关于强制转换

定义一个char a ='A';

直接输出会直接输出字符a也就是A

那么将a+1后的结果会是什么样呢?

首先是

```
char = a+1;
```

![image-20230806160820427](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308061608475.png)

很明显,因为char+1自动转换为int ,int--->byte会造成数据缺失导致报错

因此我们使用强制转换

![image-20230806160522435](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308061605613.png)

得到结果:      B

我们可以发现,使用char强制转换时,会将0-65536范围内的unicode编码输出,比如85对应A

但是当我们使用++时,数值类型并不会改变

因为JAVA中:

> 递增运算符只是对变量的值进行增加操作，但不会影响变量的数据类型

![image-20230806162937012](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308061629368.png)

 

但是相反 复合赋值运算包含隐性强制转换类型,

![image-20230806163532310](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308061635528.png)

因此与运算后复制不同的是,它自带强制类型转换,而传统赋值会因为类型不匹配导致报错

![image-20230806163923296](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202308061639397.png)



因此我们可以总结出,递增运算符只是对变量的值进行增加操作，但不会影响变量的数据类型

而复合赋值运算符会隐含强制转换