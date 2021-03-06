# Js转型函数

JavaScript中有六种数据类型，分别是：Undefined类型、Null类型、Boolean类型、Number类型、String类型、Object类型

JavaScript中用typeof操作符检测数据类型

六种数据类型有三种转型函数，分别是：Boolean（）用于将一个值转换为其对应的布尔值、Number（）用于将一个值转换为其对应的数值、String（）用于将一个值转换为其对应的字符串形式

转型函数的转换规则：

​    首先，三种转型函数作用于null和undefined的规则如下

|           | Boolean（） | Number（） | String（）  |
| --------- | ----------- | ---------- | ----------- |
| null      | false       | 0          | "null"      |
| undefined | false       | NaN        | "undefined" |

 

三种转型函数的转换规则：

1、Boolean（）

| 数据类型  | 转换为true的值               | 转换为false的值 |
| --------- | ---------------------------- | --------------- |
| Boolean   | true                         | false           |
| String    | 任何非空字符串               | ""（空字符串）  |
| Number    | 任何非零数字值（包括无穷大） | 0和NaN          |
| Object    | 任何对象                     | null            |
| Undefined | n/a                          | undefined       |

 

2、Number（）

如果是Boolean 值，true 和false 将分别被转换为1 和0。

如果是数字值，只是简单的传入和返回。

如果是null 值，返回0。

如果是undefined，返回NaN。

如果是字符串，遵循下列规则：

如果字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即"1"会变成1，"123"会变成123，而"011"会变成11（注意：前导的零被忽略了）；

如果字符串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值（同样，也会忽略前导零）；

如果字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整数值；

如果字符串是空的（不包含任何字符），则将其转换为0；

如果字符串中包含除上述格式之外的字符，则将其转换为NaN。

如果是对象，则调用对象的valueOf()方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的toString()方法，然后再次依照前面的规则转换返回的字符串值

3、String()

在不知道要转换的值是不是null或undefined的情况下，就用String()，这个函数可以将任何类型的值转换为字符串，其遵循以下规则：

如果值有toString()方法，则调用该方法（没有参数）并返回相应的结果；

如果值是null（其没有toString()方法），则返回"null"；

如果值是undefined（其没有toString()方法），则返回"undefined"。