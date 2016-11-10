# DOL实例分析&编程

本次实验包括，包含以下内容：

- **Result** ：修改完实例以后得到的运行结果；
- **Progress ** ：修改实例的过程；
- **Experimental experience ** ：实验感想、实验心得。

------

[TOC]

## Result(运行结果截图)

* example1 :

![example1](http://ww2.sinaimg.cn/large/e3bf9b05gw1f9mx5b2n1vj20c30b4djj.jpg)



* example2 : 

![example1](http://ww1.sinaimg.cn/large/e3bf9b05gw1f9mx7aol55j20bp0b4q6p.jpg)

## Progress(修改实例的过程)

### Example1: 

​	example1修改的要求是通过修改` square.c` 中的部分代码，使其最终输出3次方数。我们先来看一看未修改之前` square.c` 文件的关键代码：

```c
if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
```

这其中，第三行代码 ` i = i * i` 表示当前代码最终输出的是2次方数。因此，为了达到本次实验的要求，即输出3次方数，只需要将` i = i * i` 改成 ` i = i * i * i` 即可。修改后的代码如下：

```c
if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
```

运行修改后的样例，即可输出3次方数。



### Example2:

​	example1修改的要求是通过修改` example2.xml` 中的部分代码，使其中的square模块由` 3` 个变成` 2` 个，最终输出4次方数（2个square模块即做2次平方）。我们先来看一看未修改之前` example2.xml` 文件的关键代码：

```xml
<variable value="3" name="N"/>
```

```xml
 <!-- instantiate resources -->
  <process name="generator">
    <port type="output" name="10"/>
    <source type="c" location="generator.c"/>
  </process>

  <iterator variable="i" range="N">
    <process name="square">
      <append function="i"/>
      <port type="input" name="0"/>
      <port type="output" name="1"/>
      <source type="c" location="square.c"/>
    </process>
  </iterator>

  <process name="consumer">
    <port type="input" name="100"/>
    <source type="c" location="consumer.c"/>
  </process>

  <iterator variable="i" range="N + 1">
    <sw_channel type="fifo" size="10" name="C2">
      <append function="i"/>
      <port type="input" name="0"/>
      <port type="output" name="1"/>
    </sw_channel>
  </iterator>

```

在未修改的代码中，通过迭代定义了` 3 ` 个`  square` 模块，其中

```xml
<variable value="3" name="N"/>
```

这行代码中` value` 的值即表示迭代的次数，也表示最终生成的` square` 模块的数目，可以看到，当前` square` 模块的数目为` 3 ` ，为了达到本次实验的要求，我们只需要将这里` value` 的值设为` 2` 。修改后的代码如下：

```xml
<variable value="2" name="N"/>
```

运行修改后的样例，即可输出4次方数，也就说明，修改代码以后， ` square` 的数目变成了` 2` 。

## Experimental experience(实验心得)

这次实验很简单，只需要修改两句代码即可。如果要说学到了什么东西的话，那大概就是` 复习了生产者消费者问题的基本思想` ，其次就是` 对dol中各模块之间的连接方式有了一定的理解` 。



