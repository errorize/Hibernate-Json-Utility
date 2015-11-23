# Hibernate-Json-Utility
直接跳过VO，把实体类当作VO使用，根据指定的类属性，将类序列化成为字符串

【1】项目：《根据指定的类属性，将类序列化成为字符串》

【2】最适合的使用场景：使用SpringMVC / Struts 2 + Hibernate的Web项目。

【3】实现该项目的意图：一般使用Hibernate的Web项目都是通过手动编写VO（value object），也就是
使用Hibernate读取数据库的数据之后，然后把一个一个Hibernate实体（Entity）的数据set进另外一个
VO类，然后交由Jackson去转化，但是这个过程中，反复编写大量代码，而且不断让JVM开辟堆内存，循环
遍历，很明显是浪费人力和浪费计算机的计算资源。因此，开发一个根据指定的类属性，将类序列化成为
字符串很有必要。

【4】实现思路：
a、输入的类属性，形式是{"person.children", "person.father"}。
b、将输入的类属性转化为如下数据结构（这里使用树的结构）：
      person
       /  \
children  father
c、然后使用层序遍历，逐步递归到路径指定的深度，在递归过程中将属性归类，按类型去把通过getter
方法获取的值转化字符串。

【5】该项目的利与弊：
a、5个“有利于”：有利于直接把Entity直接当作VO使用，有利于有针对性控制触发Hibernate的延迟加
载，有利于减少重复编写代码，有利于减少计算资源的浪费，有利于减轻GC回收垃圾对象的压力。
b、弊端是该项目采用面向过程与面向对象的混合思想编写，采用面向过程编写是为了效率，C语言就是面
向过程的语言，同时导致代码混乱。对类型转化成字符串的支持不够多，希望通过Githup吸引更多的开发
者来完善，直至这个项目和阿里巴巴fastJson一样完善。
