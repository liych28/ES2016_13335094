# DOL配置日志
本次实验基于**markdown**，包含以下内容：


- **Description** ：对DOL框架的描述（随着实验进行迭代添加、修改）；
- **How to install ** ：DOL安装笔记；
- **Experimental experience ** ：实验感想、实验心得。


-----------------------------


[TOC]

## Description(DOL框架描述)

> 待添加

## How to install(DOL安装笔记)
1.  安装一些必要的环境：
* `$ sudo apt-get update`
* `$ sudo apt-get install ant`
* `$ sudo apt-get install openjdk-7-jdk`
* `$ sudo apt-get install unzip`

2. 下载DOL框架相关文件：
* `sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz`
* `sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip`

3. 解压文件：
* 新建dol的文件夹：
`$ sudo mkdir dol`
* 将dolethz.zip解压到dol文件夹中：
`$ sudo unzip dol_ethz.zip -d dol`
* 解压systemc：
`$ sudo tar -zxvf systemc-2.3.1.tgz`

4. 编译systemc：
* 解压后进入systemc-2.3.1的目录下：
`$ cd systemc-2.3.1`
* 新建一个临时文件夹objdir：
`$ sudo mkdir objdir`
* 进入该文件夹objdir：
`$ cd objdir`
* 运行configure(能根据系统的环境设置一下参数，用于编译)：
`$ sudo ../configure CXX=g++ --disable-async-updates`
* 编译：
`$ sudo make install`
* 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)：
`$ sudo pwd`

5. 编译dol：
* 进入刚刚dol的文件夹：
`$ cd ../dol`
* 修改build_zip.xml文件：
 找到下面这段话，就是说上面编译的systemc位置在哪里，
`<property name="systemc.inc" value="YYY/include"/>`
`<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>`
把YYY改成上页pwd的结果（ 注意，对于64位 系统的机器， lib-linux要改成lib-linux64）
* 编译：
`$ sudo ant -f build_zip.xml all`
如果成功会显示build successful，如下图所示：
![BUILD SUCCESSFUL](http://ww3.sinaimg.cn/large/0067oVAPgw1f8l8rxcyi7j30k90fnq74.jpg) 
6. 运行例子：
* 进入build/bin/mian路径下：
`$ cd build/bin/main`
* 然后运行第一个例子：
`$ ant -f runexample.xml -Dnumber=1`






## Experimental experience(实验心得)


* 在**配置**DOL的过程中，按照PPT给出的步骤，并**没有**出现什么**问题**；
* 此次实验中，学到最有用的还是关于**Git**的相关知识，以及**Markdown**语法。




