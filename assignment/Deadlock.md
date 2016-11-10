# DeadLock死锁

本次实验包括，包含以下内容：

- **Result** ：修改完实例以后得到的运行结果；
- **Progress ** ：实验过程，对死锁产生的解释；
- **Question** ：产生死锁的4个必要条件。
- **Experimental experience ** ：实验感想、实验心得。

------

[TOC]

## Result(运行结果截图)

![deadlock](http://ww1.sinaimg.cn/large/e3bf9b05gw1f9n0hmtclmj20bf0bejt2.jpg)

## Progress(实验过程)

### 对关键字synchronized的介绍:

* 当用关键字` synchronized`来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。 

* 当一个线程访问` object`的一个` synchronized`同步代码块或同步方法时，其他线程对`object`中所有其它` synchronized`同步代码块或同步方法的访问将被阻塞。 

  也就是说，用关键字` synchronized`修饰` class`中的方法是产生死锁的必要前提。

### Deadlock.java代码:

```java
class A{
	synchronized void methodA(B b){
		b.last();
	}
	
	synchronized void last(){
		System.out.println("Inside A.last()");
	}
}
```

```java
class B{
	synchronized void methodB(A a){
		a.last();
	}
	
	synchronized void last(){
		System.out.println("Inside B.last()");
	}
}
```

```java
  class Deadlock implements Runnable{
	  A a = new A();
	  B b = new B();
	  
	  //构造函数
	  Deadlock(){
		  Thread t = new Thread(this);
		  int count = 20000;
		  
		  t.start();
		  while(count-- >0);
		  a.methodA(b); 		  
	  }

	@Override
	public void run() {
		// TODO Auto-generated method stub
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
}
```



当 ` Deadlock.java` 被运行的时候，` class`  ` A` 和` class` ` B` 的实例` a` 和` b` 被依次声明。紧接着构造函数也被执行，在构造函数中，线程` t`被创建，当` t.start()` 被执行的时候，线程` t` 就被插入到调度队列里面，当调度到它的时候，就跑` run()` 里面的代码，运行` b` 实例的` methodB()`方法，打印相应的文字。此外，线程` t`开始运行以后，经过一段时间的延迟，实例` a`的` methodA()`方法被调用。当这两个线程同时调用同一` class`中的方法时，就会产生死锁，导致程序无法正常执行下去，这也是关键字`synchronized` 的特性所导致的。









## Question(产生死锁的4个必要条件)

  死锁就是两个或者多个进程，互相请求对方占有的资源。 

* 互斥条件：  一个资源每次只能被一个进程使用。
* 请求与保持条件：  一个进程因请求资源而阻塞时，对已获得的资源保持不放。
* 不剥夺条件:  进程已获得的资源，在末使用完之前，不能强行剥夺。
* 循环等待条件:  若干进程之间形成一种头尾相接的循环等待资源关系。



## Experimental experience(实验心得)

这次实验所用到的代码在PPT中都给出了，做起来不存在什么难度。主要就是复习了死锁的相关知识，同时也了解了`java` 中`synchronized`关键字的相关知识。



