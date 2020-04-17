---
title: JMM内存模型
date: 2020-04-17 10:44:40
tags: 编程
---

#### 内容摘要 
- 原子性
- 有序性
- 可见性
- hapen-before
- 线程安全的问题

###### 原子性
原子性就是指一个操作是不可中断的，即使是在多个线程一起执行的时候，一旦操作开始就不受其他线程的干扰



###### 有序性
在并发的时候，程序的执行可能会出现乱序。 



一条指令的执行是可以分为很对步骤的：
- 取指IF
- 译码和取寄存器操作数ID
- 执行或者有效地址计算EX
- 存储器访问MEM
- 写回WEB


###### 可见性
可见性是指一个线程修改了某一个共享变量的值，其他的线程是否能够立即知道这个修改。
- 编译器优化
- 硬件优化（如写吸收，批处理）

###### hapen-before规则
- 程序顺序原则：一个线程内保证语义的串行性 a=1;  
b=a+1;
- volatile规则：volatile变量的写，先发生于读，这保证了volatile变量的可见性
- 锁规则：解锁（unlock）必然发生在随后的加锁（lock）前
- 传递性：A先于B，B先于C，那么A必然先于C
- 线程的start()方法先于它的每一个动作
- 线程的所有操作先于线程的终结（Thread.join()）
- 线程的中断（interrupt()）先于被中断线程的代码
- 对象的构造函数执行结束先于finalize()方法


###### 线程安全的概念
是某个函数、函数库在多线程环境中被调用时，能够正确的处理各个线程的局部变量，是程序功能正确完成。  
加锁：


```
public class AccoutingSync implements Runable{  
   static  AccoutingSync instance = new AccoutingSync();  
   static int i=0;
   
   @Override  
   public void run(){
       for(int j=0;j<=1000000;j++){
           synchronize(instance){  
               i++;  
           }
       }
   } 
    
}
```
