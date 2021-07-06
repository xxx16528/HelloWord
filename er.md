#  2.17

## 枚举

确定的有限个对象，若只有一个对象可以看成是单例模式的一种实现方式

##### 手动创建枚举对象：

在类内部创建对象并对他赋值，也可以用的时候再赋值

#### enum

对象必须放在第一行，对象可以有属性是在类内部直接赋值，在对象的后面

***



* values返回一个数组，包含所有枚举对象

* valuesOf("")返回某一个对象

* 继承接口

​              

```java
  enum EnumTest emplements interface{
                     SPRING("",""){  
                       public void distinct(){}
                     }
                     SUMMER("",""){  
                       public void distinct(){}
                     }
                     AUTUMN("",""){  
                       public void distinct(){}
                     }
                     WINTER("",""){  
                       public void distinct(){}
                     }           

}
```

* int compareTo(E e)比较此枚举对象与指定对象的顺序

* int ordinal（）返回此枚举对象的序数

  ***

  

### 泛型，参数化类型

##### 泛型类

public Class Test1<T,K>{}在创建对象的时候传入实际的类型

##### 泛型方法

public <T> test1(T t1){}在调用方法的时候确定参数类型

##### 类型通配符，

就是把本来要在这里确定的类型在下一步确定，推迟确定

```java
public static void main(String[] args) {
    GenericClass<String> name = new GenericClass<String>();
    GenericClass<Integer> age = new GenericClass<Integer>();
	GenericClass<Number> number = new GenericClass<Number>();
	getData(name);
	getData(age);
	getData(number);
	}
	public static void getData(GenericClass<?> data) {
	    System.out.println("data :" + data.getValue());
}
```

##### 泛型只存在代码的编译阶段，不会进入到运行阶段，Class文件是没有泛型信息的

***



##### 上限，下线

```java
//接收GenericClass对象，范围上限设置为Number，所以只能接收数字类型
public static void fun(GenericClass< ? extends Number> temp){
System.out.println(“数字是：”+temp);
}

GenericClass< ? extends Number>只能是Number及其子类

GenericClass<? super String> 下限是String，此处泛型只能是String及其父类
```



###### 实例化和初始化

* 实例化，在内存中开辟一个空间
* 初始化，给对象的属性赋初始值
* 声明，在虚拟机栈里添加一个引用

##### Resource

getResource方法可以读取一个文件，在classpath或其他路径

#### 注解Annotation

**三个基本的注解**

@Override重写父类方法

@Overload方法重载

抑制编译器警告

方法已过时

@FunctionInterface函数式接口(只有一个抽象方法)注解

###### 定义annotation,

* 注解和他的变量不会对当前被自己修饰的类或方法起作用，它主要用于启动程序后通过反射获取类或方法的信息使用

* public  @interface  Table{}
* annotation只有成员变量没有方法
* 变量形式1：String  name()
* 变量形式2：String   name()   default   "AAA"

###### 元注解

* @Retention：指定annotation存活的时间
* @Target：指定annotation修饰的元素
* @Documented：表示本类可以被提取成doc文档
* @Inherited：指定annotation具有继承性

###### @Retention

* RetentionPolicy.SOURCE，只存在源代码中，编译时丢掉
* RetentionPolicy.CLASS ，存在class文件中，运行程序时丢掉
* RetentionPolicy.RUNTIME，存在class文件中，运行程序时，jvm可以通过反射获得注解的信息

###### @Target

* ElementType.TYPE：能修饰类、接口或枚举类型；
  ElementType.FIELD：能修饰成员变量；
  ElementType.METHOD：能修饰方法；
  ElementType.PARAMETER：能修饰参数；
  ElementType.CONSTRUCTOR：能修饰构造器；
  ElementType.ANNOTATION_TYPE：能修饰注解；

可以通过反射获得一个元素上的所有注解，指定类型注解，是否包含某种注解

### 2.24

#### 反射

反射是程序运行过程中，通过类名或类的地址或对象，去内存中找到对应的类的（不是对象的信息）信息。

这就是动态加载，new就是静态加载

万物都是对象：类也是对象是java.lang.Class类的实例的对象

java.lang.Class类的构造方法是私有地，那怎么表示一个类是Class类的实例对象呢：

1.Class c1=类名.class;

2.Class c2=对象.getClass();

3.Class c3=Class.forName("");

c1、c2、c3称为类类型的实例对象，就是代表了他是个什么类型的Class，每个类只能是Class类的一个实例，所以c1、c2、c3的==是为true的。

##### 类的加载

动态加载：运行时刻加载

静态加载：编译时加载

##### 反射的方法

* c1.newInstance()调用无参构造生成对象，生成的对象是Object类型的

#### 反射用处

动态加载类，可以在类运行时再决定到底加载哪一个类，使代码更方便更灵活，在运行时加载通过trycache就避免了编译不通过的问题

### 2.25

#### 多线程

继承Thread类或者实现Runable接口，有新建状态，就绪状态，运行状态，阻塞状态，死亡状态

* 等待阻塞：wait()方法

  wait()方法使用时必须在synchronized代码块内使用，用监视器对象来调用wait方法，是得到了同步锁的线程等待，notify()要同一个对象调用才行，表示唤醒本对象监视器上，wait方法是Object类的方法，因为所有的类都有可能是锁对象，释放cpu资源也释放锁资源，可以传参数，表示一定时间后开始等待

* 同步阻塞:synchronized同步锁

* 其他阻塞：sleep(),join()或发出Io请求时

  sleep方法是Thread类的静态方法，不能用线程.sleep()的方式调用，它是释放cpu资源但不释放锁资源

  join()方法，在main线程中调用t1.join()就是让t1线程先执行t1执行完后main再进入就绪状态，在底层实现就是main线程调用了t1对象的wait()方法进入等在，等t1线程执行完后main线程才会被唤醒进入就绪，在main线程休眠的过程不影响其他线程和t1的竞争。

  yield   使当前线程从运行状态转为就绪状态，cpu从新再选择要执行的线程。

  

###### synchronized

* 同步代码块：只能在方法内部使用，必须使用同一个对象作为锁对象，否则不能同步
* 同步方法：它的锁对象就是this，当一个线程访问一个对象中的某个同步方法时，其他线程不能访问该对象中的其他同步方法，但是普通方法，同步代码块，静态同步方法不会受影响；
* 静态同步方法：它的所对象是该类的class对象，当一个线程访问一个对象中的某个静态方法时，其他线程不能访问该类的所有对象中的所有静态同步方法，但是普通方法，同步代码块，同步方法不受影响；

需要有一个监视器对象，该对象只能有一个，否则同步失败，synchronized代码所在的类不能有多个对象

同步方法，它的锁对象是this



```java
//死锁，
//顺序打印，先定义布尔，是线程1就打印，并且唤醒其他线程，并把布尔改为FALSE，再让自己睡眠，线程2打印改布尔为TRUE，唤醒线程1，自己睡眠
//多个窗口买票
//生产者消费者的问题
public  synchronized void ectBread() {
	try {
		if(count<=0) {
			wait();
		}
		System.out.println("现在有面包，count"+count+"    id:"+id);
		count--;
		notify();
	} catch (Exception e) {
       e.printStackTrace();
	}

}
	public  synchronized void produce() {
		try {
          if(count>=1) {
			System.out.println("生产者—商品还有"+count);						
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}else {
			System.out.println("生产者—产品没了要生产"+count);
			count++;	
            notifyAll();
		}
	}
```
#### ExecutorService

**1.Runnable**：是线程的接口，接口的run方法没有返回值，

**2.Callable：**是线程的接口，接口的call方法有返回值，返回值为传入的类型。Callable一般配合ExecutorService来使用，因为callable和Thread类没有直接的关系所以不能使用start方法启动它

3.**Future：**是对Runnable或Callable的执行结果进行操作：取消，查询是否完成，查询结果



```java
public interface ExecutorService extends Executor {   
void shutdown();//顺次地关闭ExecutorService,停止接收新的任务，等待所有已经提交的任务执行完毕之后，关闭ExecutorService
List<Runnable> shutdownNow();//阻止等待任务启动并试图停止当前正在执行的任务，停止接收新的任务，返回处于等待的任务列表
```


```java
boolean isShutdown();//判断线程池是否已经关闭
boolean isTerminated();//如果关闭后所有任务都已完成，则返回 true。注意，除非首先调用 shutdown 或 shutdownNow，否则 isTerminated 永不为 true。
boolean awaitTermination(long timeout, TimeUnit unit)//等待（阻塞）直到关闭或最长等待时间或发生中断,timeout - 最长等待时间 ,unit - timeout 参数的时间单位  如果此执行程序终止，则返回 true；如果终止前超时期满，则返回 false 
    
<T> Future<T> submit(Callable<T> task);//提交一个返回值的任务用于执行，返回一个表示任务的未决结果的 Future。该 Future 的 get 方法在成功完成时将会返回该任务的结果。
```


```java
<T> Future<T> submit(Runnable task, T result);//提交一个 Runnable 任务用于执行，并返回一个表示该任务的 Future。该 Future 的 get 方法在成功完成时将会返回给定的结果。 
```

```java
Future<?> submit(Runnable task);//提交一个 Runnable 任务用于执行，并返回一个表示该任务的 Future。该 Future 的 get 方法在成功 完成时将会返回 null
```


    <T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks)//执行给定的任务，当所有任务完成时，返回保持任务状态和结果的 Future 列表。返回列表的所有元素的 Future.isDone() 为 true。
        throws InterruptedException;


```java
<T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks,                                  long timeout, TimeUnit unit)//执行给定的任务，当所有任务完成时，返回保持任务状态和结果的 Future 列表。返回列表的所有元素的 Future.isDone() 为 true。
    throws InterruptedException;
```


    <T> T invokeAny(Collection<? extends Callable<T>> tasks)//执行给定的任务，如果在给定的超时期满前某个任务已成功完成（也就是未抛出异常），则返回其结果。一旦正常或异常返回后，则取消尚未完成的任务。
        throws InterruptedException, ExecutionException;


```
<T> T invokeAny(Collection<? extends Callable<T>> tasks,                    long timeout, TimeUnit unit)        throws InterruptedException, ExecutionException, TimeoutException;
```

#### Executor


```java
public interface Executor {   
    void execute(Runnable command);//执行已提交的 Runnable 任务对象。此接口提供一种将任务提交与每个任务将如何运行的机制（包括线程使用的细节、调度等）分离开来的方法}
```

### Funtrue

https://www.cnblogs.com/dolphin0520/p/3949310.html，Future接口

https://blog.csdn.net/fwt336/article/details/81530581    线程池

使用普通的多线程时无法保证获得线程的执行结果，如果必须要就只能通过线程通信或共享变量的方式很麻烦

```java
 public static void main(String[] args) throws InterruptedException {
	long sta=System.currentTimeMillis();

	Thread t1=new Thread() {
		@Override
		public void run() {
			try {
				Thread.sleep(3000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	};
	t1.start();
	//t1.join();
	Runnable r1=new Runnable() {

		@Override
		public void run() {
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			
		}};
		Thread t2=new Thread(r1);
		t2.start();
		//t2.join();
	long end=System.currentTimeMillis();
		System.out.println(end-sta);

}
```
上面的代码的执行结果为0，t1和t2两个线程会执行，但是不能保证他们会在什么时候执行，所以获得的时间就不准确

***

##### Future

　Future就是对于具体的Runnable或者Callable任务的执行结果进行获取结果，取消、查询是否完成。必要时可以通过get方法获取执行结果，该方法会阻塞直到任务返回结果。

future获得的runnable的结果是null

Future是接收Callable的执行结果的东西。

```java
  public` interface` `Future<V> {
``boolean` `cancel(``boolean` `mayInterruptIfRunning);
``boolean` `isCancelled();
``boolean` `isDone();
``V get() ``throws` `InterruptedException, ExecutionException;
``V get(``long` `timeout, TimeUnit unit)
    ``throws` `InterruptedException, ExecutionException, TimeoutException;
```
​      

- cancel方法用来取消任务，如果取消任务成功则返回true，如果取消任务失败则返回false。

  参数mayInterruptIfRunning表示是否允许取消正在执行却没有执行完毕的任务，如果设置true，则表示可以取消正在执行过程中的任务。

  如果任务已经完成，则无论mayInterruptIfRunning为true还是false，此方法肯定返回false，

  即如果取消已经完成的任务会返回false；

  如果任务正在执行，若mayInterruptIfRunning设置为true，则返回true，若mayInterruptIfRunning设置为false，则返回false；

  如果任务还没有执行，则无论mayInterruptIfRunning为true还是false，肯定返回true。

- isCancelled方法表示任务是否被取消成功，如果在任务正常完成前被取消成功，则返回 true。

- isDone方法表示任务是否已经完成，若任务完成，则返回true；

- get()方法用来获取执行结果，这个方法会产生阻塞，会一直等到任务执行完毕才返回；

  阻塞就是当主线程执行到get方法的时候如果子线程还没执行完，就暂停主线程等子线程执行完了得到返回结果了主线程再继续执行

- get(long timeout, TimeUnit unit)用来获取执行结果，如果在指定时间内，还没获取到结果，就直接返回null。

######　FutureTask

是Future接口的唯一实现类，它实现了Future和Runnable两个接口，他有两个构造方法，相当于一个增强版的线程类，可以通过Future接口的方法获得线程信息，可以像普通线程一样通过Thread.start()方法启动线程

它的非常重要的作用是：本来Callable的线程和无法用start()的方式启动，现在把Callable加到FutureTask里面就可以了。

```java
//这里ft是一个runnable类型的线程对象    
FutureTask<String>  ft=new FutureTask<>(new Callable001());
//同时ft被包裹了很多东西，增加很多功能，ft线程对象启动后，可以获得他的执行结果
    new Thread(ft).start();
    System.out.println(ft.get());
```
​    

```java
public` `FutureTask(Callable<V> callable) {
}
//把Runnable的接口转换成一个Callable的接口,result是线程执行成功后返回的值
public` `FutureTask(Runnable runnable, V result) {
}
```

线程通信

##### 怎么拒绝的

#### 线程池

四种：

* newCachedThreadPool创建一个不固定线程数量的线程池，可以根据任务数量自动增减线程数量
* newFixedThreadPool 创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。
* newScheduledThreadPool 创建一个定长线程池，支持定时及周期性执行任务执行。
* newSingleThreadExecutor 创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行

![1574605928663](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1574605928663.png)

Executor工具类中提供了创建线程池的方法，返回的都是ThreadPoolExecutor对象

##### OOM

OOM是内存溢出，当代码中有死循环或者深层的递归或者时线程过多时，虚拟机分配的内存不够用了，就会报错程序执行失败。      

因为他们的任务队列是通过链表实现的，没有设置容量

```java
     1）FixedThreadPool 和 SingleThreadPool：  
        允许的请求队列长度为Integer.MAX_VALUE，可能会堆积大量的请求，从而导致OOM。
        
    2）CachedThreadPool 和 ScheduledThreadPool :
       允许创建的线程数量为Integer.MAX_VALUE，可能会创建大量的线程，从而导致OOM。
```

https://blog.csdn.net/qq_42447950/article/details/81435080



##### 自定义线程池

ThreadPoolExecutor对象

1.corePoolSize 核心线程数

* 默认情况下线程池中没有任何线程，要等任务来了才会创建线程
* 如果调用了prestartAllCoreThreads()或者prestartCoreThread()方法，就会预先创建线程，预先创建1个或者corePoolSize个
* 在没有预先创建线程的情况下，线程池中的线程数为0，当有任务来之后，就会创建一个线程去执行任务，当线程池中的线程数目达到corePoolSize后，就会把到达的任务放到缓存队列当中。核心线程在allowCoreThreadTimeout被设置为true时会超时退出，默认情况下不会退出。

2.maximumPoolSize 

* 当线程数大于或等于核心线程，且任务队列已满时，线程池会创建新的线程，直到线程数量达到maxPoolSize。如果线程数已等于maxPoolSize，且任务队列已满，则已超出线程池的处理能力，线程池会拒绝处理任务而抛出异常。

3.keepAliveTime 

* 当线程空闲时间达到keepAliveTime，该线程会退出，直到线程数量等于corePoolSize。如果allowCoreThreadTimeout设置为true，则所有线程均会退出直到线程数量为0。

4.unit 时间单位
5.workQueue 任务队列，用来存储等待执行的任务一般以下几种：

* ```java
  ArrayBlockingQueue;
  LinkedBlockingQueue;
  SynchronousQueue;
  PriorityBlockingQueue
  ```

6.threadFactory 线程工厂，用于创建线程，一般可以用默认的
7.handler 拒绝策略，当任务过多时候，如何拒绝任务。

创建核心线程数的线程（可以预创建也可以不预创建），任务超过核心线程时，把任务放在任务队列里面，如果队列满了，就会继续创建线程，当线程数达到最大线程数，并且任务队列也满了就会抛出异常，

在线程数大于核心线程时，当一个线程空闲达到一定的时间就会被回收，直到等于核心线程数停止，如果allowCoreThreadTimeout设置为true则会回收到0为止；

https://blog.csdn.net/qq_20009015/article/details/85953364

https://blog.csdn.net/suifeng629/article/details/95516946



## HTTP

物理层：定义物理设备如何传输数据

各个层的作用

#### http三次握手

客户端和服务器进行HTTP请求时需要创建一个TCP connection，因为HTTP没有连接的概念，只有请求和响应，请求和响应都是数据包需要一个通道，TCP连接会一直存在可以供多个HTTP请求使用。

客户端发送一个请求连接的包，标志位(表示创建请求)SYN=1，seq=X

服务端再发送标志位SYN=1，ACK=X+1，seq=Y

客户端再发送ACK=Y+1，seq=z

客户端发送一个数字作为标志位的码，服务器把标志码加一返给客户端，客户端就确认连接到服务器了，服务器同时还发送一个数字作为标志的码给客户端，客户端加一返回，服务器收到后也确认连接成功了。

为了防止服务端开启无用的连接，如果服务端收到第一次请求就连接的话，有可能返回给客户端的数据包丢失，客户端在等服务端的返回数据，而服务端在等客户端的返回数据，端口就一直开着会造成服务器开销浪费。

URI统一资源标志符，用来唯一的标识互联网上的信息资源，包含了URL和URN

URL统一资源定位符

格式：http://user:pass@host.com:80/path?query=string#hash
格式：

协议:

//如果需要特定身份才能访问这里是账号密码（不常用）

@服务器地址：

端口一台服务器会有很多的端口，同时多个web服务会监听各个端口，端口就是在服务器上找到某一个web服务，默认是80端口

/path在web服务中找到要访问的资源

？参数#hash当请求的内容非常大时，hash代表取其中的一个片段，锚点

URN永久统一资源定位符，当URN指定了一个资源后，资源移动了位置仍然可以找到

## 报文格式

Get，post，delete等请求方式只是一个纸面上的定义，没有语法等约束

###请求报文

起始行：请求方式，URL地址，协议版本（现在都是HTTP1.1）

###响应报文

起始行：协议版本，状态码，状态码的含义解释





### Stream

https://www.cnblogs.com/andywithu/p/7404101.html

https://www.cnblogs.com/haixiang/p/11029639.html

https://blog.csdn.net/yin__ren/article/details/79182703

#### lambda表达式

lambda表达式只适用于函数式接口(只有一个抽象方法)，主要适用于集合操作，有两个特点：匿名函数和可传递

1.匿名函数：当需要一个函数，但是又不想费神去命名一个函数的时候使用lambda表达式，所以lambda表达式表达的匿名函数应该是很简单的，如果复杂就应该定义一个函数来用。

2.可传递：把lambda表达式当成一个参数传递给其他函数

###### 语法形式为()->{}

()用来描述参数，{}用来描述方法体，不用再去定义实现类，把在实现类中要重写的方法，简便的完成。

```java
//lambda表达式用法
public interface NoReturnNoParam {
    void method();
}

NoReturnNoParam  m=()->{
        	System.out.println("888");
        	return "999";
        };
//m就是一个对象，所以()->{}这个表达式就是一个对象
        System.out.println(m.method());
```

```java
public interface ReturnOneParam {
int method(int a);
}

//在test1类中有一个方法
  public static int doubleNum(int a) {
        return a * 2;
   }
//可以这样
ReturnOneParam  p=a->doubleNum(a);
ReturnOneParam  p=test1::doubleNum;//接口的方法是接收一个int返回int，和doubleNum方法完全一样就可以这样替代，这种方式可以在任何情况使用，静态方法用类名：：，普通方法用对象：：调用。这个方式没啥卵用
```



* ()->()的方式使用，

* 本来是隐含return的，如果有多行表达式的时候就要显式的写出return

  (int x , int y)->{

  ​    int z=x*y;

     return z+x;

  }

* 双冒号：调用类的方法

* 在lambda表达式外定义的变量不能在表达式内做修改

**常用函数式接口**

1，Predicate<T>    ,通过流使用

* boolean  test(T  t)通过传入的条件来筛选元素
* add(Predicate)，和&&一样，用于多个条件组合筛选
* or(Predicate),就是||
* negate(Predicate)，就是！
* isEquals(Object)，底层就是equals实现的，判断是否相等，是static的：Predicate.isEquals("sss")

```java
List<Integer> list=new ArrayList<>();
Predicate<Integer> p1=i->i>5;
Predicate<Integer> p2=i->i<20;
Predicate<Integer> p3=i->i%2==0;
List test=list.stream().filter(p1.and(p2).and(p3)).collect(Collectors.toList());
List test=list.stream().filter(p1.and(p2).and(p3.negate())).collect(Collectors.toList());//取反
System.out.println(test.toString());
```

​     

2，Consumer<T>    void    accept(T  t)  对传入的参数进行操作foreach，和for循环差不多的。可以直接用也可以通过流,

3，Function<T,R>    R  apply(T,t)转换操作，输入T类型输出R类型map

https://www.cnblogs.com/andywithu/p/7404101.html

4，Comparator，排序的接口，返回返回正数负数或0，分别是升序或降序排列，collections.sort，Array.sort，Stream.sorted处使用。

###### Stream的方法

* foreach，遍历每个数据，和for循环类似
* filter，过滤筛选，产生一个过滤后的新的流
* limit，取流的前几个数据
* map，输入一种类型数据，输出另一种类型的数据
* sorted，排序，

**compareTo**

完全相同返回0

String比较时，如果不相同返回第一个不相同的字符的ASCII码值的差，

如果只有位数不同，返回相差的位数的长度

数字比较大于返回1小于返回-1相等返回0

comparator是一个函数式接口，用来做比较

compareTo是一个比较的方法在Integer和String的类中都有重写。

#### Stream

![1559603308138](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559603308138.png)

###### Stream特性

* Stream不存储数据

  我们在数组或集合的基础上创建stream，stream不会专门存储数据，对stream的操作也不会影响到创建它的数组和集合,对于stream的聚合、消费或收集操作只能进行一次，再次操作会报错，如下代码：

  ```java
  public void test1(){
      Stream<String> stream = Stream.generate(()->"user").limit(20);
      stream.forEach(System.out::println);
      stream.forEach(System.out::println);
  }
  ```

* Stream不改变源数据

* Stream延迟执行特性，所以在聚合操作前修改源数据是允许的。

  在collect方法执行之前，filter、sorted、map方法还未执行，只有当collect方法执行时才会触发之前转换操作

  ```java
  public void test() {
      Stream<Student> stream = Stream.of(stuArr).filter(this::filter);
      System.out.println("split-------------------------------------");
      List<Student> studentList = stream.collect(toList());
  }
  ```



##### 创建Stream

1.数组

```java
public void testArrayStream(){
    //1.通过Arrays.stream
    //1.1基本类型
    int[] arr = new int[]{1,2,34,5};
    IntStream intStream = Arrays.stream(arr);
    //1.2引用类型
    Student[] studentArr = new Student[]{new Student("s1",29),new Student("s2",27)};
    Stream<Student> studentStream = Arrays.stream(studentArr);
    //2.通过Stream.of
    Stream<Integer> stream1 = Stream.of(1,2,34,5,65);
    //注意生成的是int[]的流
    Stream<int[]> stream2 = Stream.of(arr,arr);
    stream2.forEach(System.out::println);
}
```

2.集合

```java
public void testCollectionStream(){
    List<String> strs = Arrays.asList("11212","dfd","2323","dfhgf");
    //创建普通流
    Stream<String> stream  = strs.stream();
    //创建并行流
    Stream<String> stream1 = strs.parallelStream();
}
```

3.空流

```java
public void testEmptyStream(){
    //创建一个空的stream
    Stream<Integer> stream  = Stream.empty();
}
```

4.无限流

```java
public void testUnlimitStream(){
    //创建无限流，通过limit提取指定大小
    Stream.generate(()->"number"+new Random().nextInt()).limit(100).forEach(System.out::println);
    Stream.generate(()->new Student("name",10)).limit(20).forEach(System.out::println);
}
```

5.规律的无限流

```java
public void testUnlimitStream1(){
    Stream.iterate(0,x->x+1).limit(10).forEach(System.out::println);
    Stream.iterate(0,x->x).limit(10).forEach(System.out::println);
    //Stream.iterate(0,x->x).limit(10).forEach(System.out::println);与如下代码意思是一样的
    Stream.iterate(0, UnaryOperator.identity()).limit(10).forEach(System.out::println);
}
```

##### 对Stream操作

map和filter这些方法只关心返回值，并不在意你如何实现，所以既可以用lambda表达式，说明是用的predicate和consumer，也可以用自己的方法

###### 数组和集合的区别

* 数组长度不能修改，集合可以修改长度
* 数组只能存一种类型，集合在不声明的情况下元素是Object的可以存多种类型
* 数组可以存基本类型也可以存对象类型，集合只能存对象

##### 使用

List.forEach()  里面是一个consumer对象，遍历集合并操作它

###### 数组的基本操作

* int[] arr = new int[]{1,2,34,5};
* Arrays.sort(arr);      从小到大排序
* Arrays.copyOf(arr,int newlength);   复制数组到一个新的数组，如果长度大于原来的数组，用零填充，小于则从数组的第一个元素开始截取，直到满足数组的长度
* copyOfRange（arr，int formIndex，int toIndex）；  复制指定位置的数组到新数组，包左不包右
* fill，对数组元素填充替换

###### 集合

*  List<String> strs = Arrays.asList("11212","dfd","2323","dfhgf");

* *//删除元素.*

* list.remove(1); list.remove("Alix");，不能在循环中删除，会出错在迭代器删除

* 是否包含元素，contains，String也有这个

* 修改        list.set(0, "Tom");

* 返回某个值的索引，num.indexOf(2)，num.lastIndexOf(2)

* num = num.subList(1, 4);截取一部分元素形成新的集合

* .isEmpty()判断是否为空

* list.toString();转为String

* String[] str = list.toArray()转为数组

  ​       

###### Set

```java
 boolean    add(E e) //如果 set 中尚未存在指定的元素，则添加此元素（可选操作）。
 boolean    addAll(Collection<? extends E> c) //如果 set 中没有指定 collection 中的所有元素，则将其添加到此 set 中（可选操作）。
 void    　　clear() //移除此 set 中的所有元素（可选操作）。
 boolean    contains(Object o) //如果 set 包含指定的元素，则返回 true。
 boolean    containsAll(Collection<?> c) //如果此 set 包含指定 collection 的所有元素，则返回 true。
 boolean    equals(Object o) //比较指定对象与此 set 的相等性。
 int    　　 hashCode() //返回 set 的哈希码值。
 boolean    isEmpty() //如果 set 不包含元素，则返回 true。
 Iterator<E>    iterator() //返回在此 set 中的元素上进行迭代的迭代器。
 boolean    remove(Object o) //如果 set 中存在指定的元素，则将其移除（可选操作）。
 boolean    removeAll(Collection<?> c) //移除 set 中那些包含在指定 collection 中的元素（可选操作）。
 boolean    retainAll(Collection<?> c) //仅保留 set 中那些包含在指定 collection 中的元素（可选操作）。
 int    　　 size() //返回 set 中的元素数（其容量）。
 Object[]   toArray() //返回一个包含 set 中所有元素的数组。
<T> T[]    toArray(T[] a) //返回一个包含此 set 中所有元素的数组；返回数组的运行时类型是指定数组的类型。
```



###### map

```
 for (Map.Entry<String, Integer> entry : maps.entrySet()) {
            System.out.println("key:" + entry.getKey() + ";value:" + entry.getValue());
        }
 maps.forEach((k,v)->
       System.out.println("key : " + k + "; value : " + v)
     );
```

* 添加元素，put
* 修改元素 maps.replace("F", 65);
* 删除 maps.remove("E");
* 查询 int f = maps.get("F");
* map.keySet
* map.Values

###### 集合->数组

list.toArray(数组)

Set.toArray()

###### 数组->集合

Arrays.asList(arr)



约定大于配置**：开发人员和计算机交流的过程中也就是开发过程，如果按照规则做就不需要额外的做配置，如果不按规则就要配置。



##### 计算方法执行时间Long startTime=System.currentTimeMillis();自1970年1月1号0点到现在的毫秒数





## JDBC

JDBC是java语言中与数据库连接的API

![1563011322260](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1563011322260.png)

获得数据库连接后，JDBC有三种方式发送sql命令，

* Statement：只能执行没有参数的sql，会有sql注入的风险

* PreparedStatement： sql可以多次使用，在preparedStatement接口运行时输入参数，防止sql注入

* CallableStatement ：执行存储过程。

  三种Statement使用后要显式的关闭连接，及connection的连接

  还可以通过Statement.addBatch()批量操作sql

  Statement的三个常用方法：

  * execute：可以执行任何类型的sql，如果得到的是ResoultSet，返回true，否则返回false
  *  executeUpdate ：执行增删改的操作，返回int，影响的行数
  *  executeQuery：返回ResoultSet对象，和迭代器类似。





# 网络编程

**网络编程**：对信息的发送和接收。

##### 7层网络模型

OSI模型（Open  System  Interconnect）开放式系统互联

* 物理层：将数据转换为可以通过物理介质传输的电子信号，

* 数据链路层：在网络层实体间提供数据发送和接收的功能和过程；提供数据链路的流控。

* 网络层：控制分组传送系统的操作、路由选择、拥护控制、网络互连等功能，它的作用是将具体的物理传送对高层透明。

* 传输层：提供建立、维护和拆除传送连接的功能；选择网络层提供最合适的服务；在系
  统之间提供可靠的透明的数据传送，提供端到端的错误恢复和流量控制。

* 会话层：提供两进程之间建立、维护和结束会话连接的功能；提供交互会话的管理功能，
  如三种数据流方向的控制，即一路交互、两路交替和两路同时会话模式 。

* 表示层：代表应用进程协商数据表示；完成数据转换、格式化和文本压缩。

* 应用层：提供OSI用户服务，例如事务处理程序、文件传送协议和网络管理等

  

osi七层模型是理想化的模型

基础层：物理层，数据链路层，网络层

传输层：TCＰ－ＵＤＰ协议，Socket

高级层：会话层，表示层，应用层



#### Java设计模式六大原则

* 单一原则： 一个类只实现一个功能，不能有多个导致类变更的原因；
* 里氏替换原则：子类可以拓展父类，但是不能修改父类已实现的方法，所有在使用父类的地方都能换成子类，而且程序正常执行；
* 接口隔离原则：如果一个类实现的接口中有它不需要的方法，那么这个接口需要拆分成更细分的接口；
* 依赖倒置原则：面向接口编程，实现类依赖接口，不是接口依赖实现类；
* 迪米特法则：一个对象应该尽量少的了解其他对象，方法和属性应尽量不public；
* 开闭原则：对拓展开放，对修改关闭；

##### 面向接口编程

接口是一种规范和约束是对业务逻辑的梳理总结，具体的实现由实现类去完成，当业务修改的时候，只需要从新编写实现类就可以，不用修改现有的代码，

降低耦合，耦合就是两个部分的联系紧密度，耦合越高联系越复杂越多，修改的时候对其他部分的影响越大

有利于系统的扩展，面向接口编程，每一个功能都对应一个接口方法，条理清晰泾渭分明，如果要扩展新功能直接加新方法就行；

##### 设计模式

###### 单例模式：包含懒汉式和饿汉式，双重锁模式；

* 构造方法私有化，在类内构造一个静态的对象，写一个public方法返回该对象；
* 优点：提供系统的唯一实例提供访问，对需要频繁创建和销毁的对象提高程序性能；
* 缺点：如果被回收会造成对象状态的丢失，数据库的链接池对象如果为单例的有可能造成连接池溢出，多线程不安全；

```java
public class SingleTon3 {
         private SingleTon3(){};//私有化构造方法
         private static volatile SingleTon3 singleTon=null;
       // 因为 singleton = new Singleton() 这句话可以分为三步：volatile可以防止jvm重排优化
       //在单线程的时候重排优化没问题，但是多线程时会导致线程获得一个没初始化的实例
       //  1. 为 singleton 分配内存空间；
       //  2. 初始化 singleton；
       //  3. 将 singleton 指向分配的内存空间。
         public static SingleTon3 getInstance(){
                 //第一次校验
                if(singleTon==null){  //第一个if为了提高效率，不用每次都获得锁   
                    synchronized(SingleTon3.class){
                        //假如线程1执行完上一个if后让给了线程2执行，线程2创建了对象，if就是防止线程1再创建对象
                        if(singleTon==null){     
                           singleTon=new SingleTon3();
                        }
                }
     }
    return singleTon;
}
```



###### 工厂模式

* 增强了扩展型，降低耦合

  

###### 适配器模式

* 一个类的接口不符合客户的使用条件时，就再加一层代理让他变成能用的；
* 优点：提高了复用性，更好的扩展；
* 缺点：大量使用时，代码非常乱；

###### 代理模式

* 某些情况下一个客户类不想或者不能直接引用委托对象，代理类可以在客户类和委托对象直间起到中介的作用，通过方法参数的形式传入委托对象；

* 代理类和委托类要实现相同的接口

* 除了中介的功能，还可以实现开闭原则，给代理类增加额外的功能

* 静态代理优点：可以使用开闭原则扩展功能，缺点：要手动为每一个类创建代理工作量大

* 动态代理：

  ```none
   public void test(){
          final IUserService target = new UserServiceImpl();//委托类的对象
          IUserService service = (IUserService) Proxy.newProxyInstance(
                  target.getClass().getClassLoader(),
                  target.getClass().getInterfaces(), 
                  new InvocationHandler() {
                      
                      @Override
                      public Object invoke(Object proxy, Method method, Object[] args)
                              throws Throwable {
                          //调用日志处理方法
                          OtherServiceUtil.doLog();
                          //调用事务处理方法
                          OtherServiceUtil.doTran();
                          //调用目标方法
                          Object result = method.invoke(target, args);
                          return result;
                      }
                  });
          
          service.login();//service是得到的代理类对象
      }
  ```

###### 观察者模式

* 当一个被观察的对象发生变化时，观察的对象会立刻知道；

* 实现：

      import java.util.Observable;
        //被观察者类
      public class NumObservable extends Observable {
          int data = 0;
      public void setData(int i) {
         data = i;
         setChanged();    //标记此 Observable对象为已改变的对象
         notifyObservers();    //通知所有观察者
        }
      }
  ​    
  ​    

      import java.util.Observable;
      import java.util.Observer;
       //观察者类
      public class NumObserver implements Observer{
      public void update(Observable o, Object arg) {    //有被观察者发生变化，自动调用对应观察者的update方法
         NumObservable myObserable=(NumObservable) o;     //获取被观察者对象
         System.out.println("Data has changed to " +myObserable.data);
        }
      }
  ```
  public class Test {
      public static void main(String[] args) {
         NumObservable number = new NumObservable();    //被观察者对象
         number.addObserver(new NumObserver());    //给number这个被观察者添加观察者(当然可以有多个观察者)
         number.setData(1);
         number.setData(2);
         number.setData(3);
      }
  }
  ```

  

###### 迭代器模式

* 让用户通过特定的接口访问容器的数据，不需要了解容器内部的数据结构；
* 优点：这样用户得到的是容器的副本数据，在进行操作时不会影响到原数据，更安全；



#### 哈希算法

哈希算法没有统一的标准，是把任意长度的输入通过散列算法变成固定长度的输出，这个输出的值就是散列值或哈希值

哈希算法是不可逆的无法根据结果得到原值，输入与输出一一对应，它可以用于加密，例如MD5 

Hash原理就是，把value经过哈希算法计算得到一个下标的值，就把它存到对应的位置上，再查找的时候，把value计算一下会得到它的下标值，直接去取就行了。

**HashCode**:它是哈希算法的一个例子，它是在Object类中的方法，它得到的是一个和对象的内存地址相关的一个码；

**例如**

Hashset是无序的集合不能重复，每一个存入的元素都要和已有的元素做比较，如果使用equals比较会消耗非常大，所以先比较哈西码，如果相同再用equals比较

##### Map的

HashCode()：方法会得到一个对象的码，和内存地址相关的；

HashMap和HashTable的底层实现都是数组加链表；

在Map中key对象的哈希码经过处理后会作为Entry的下标；

在Map中查找一个key时会先通过哈西码找到Entry，再通过equase方法比对对象，两个都对了才会认定是找到了；

所以如果使用自定义的对象作为key的话，要重写hashcode和方equals方法

##### hashcode和equase方法

同一个对象多次获取哈西码是相同的，前提是equase方法没有被重写；

两个方法都没有被重写的情况下，equase相等哈希码一定相等；但是哈希码相等equase不一定相等；





### Java基础

###### 分类：

* JavaSe：标准版，就是一般的Java程序
* JavaEE：企业版，包含了JavaSe,还包含了JavaWeb等。
* JavaMe:微型版，移动端设备的应用开发。

###### Jdk

* jdk:java开发工具包;
  * jre:Java运行时环境，
  * jvm：Java虚拟机；

###### 命名规则

* 大驼峰：类名，工程名；

* 小驼峰：变量名，方法名；

* 标识符：工程名，包名，变量名，方法名；

* 标识符命名：

  1，由字母数字下划线美元符组成；

  2，不能是数字开头；

  3，见名知意，规范大小写，不能使用Java保留字；

##### 二进制

* 源码，补码，反码；

  在计算机中数值都是以补码表示；

* 正数的源码补码反码都一样的；

* 负数：源码--反码，符号位不变，数值位取反；

* 负数：源码--补码，符号位不变，数值位取反，末尾加一；

在计算机中进行计算时没有减法的运算，所以减法换算为加一个负数，而正正相加或负负相加都可以算作加法，正负相加的问题就难以解决，

```java
所以采用补码，一个钟表的最大数是12，当指针指向10点钟时要让他指向8点钟怎么办，第一可以减2，第二可以加10，这个10就是最大值12减去2的结果,在计算机中这个10叫同余数

在一个4位二进制数中最大值是10000，也就是16
//我们下面的运算暂不考虑符号位
运算：6-2时，它的同余数是14
二进制：0110-0010
根据上面钟表的算法：6+14
0110+1110=10100，取后四位0100就是4
加-2和加14（1110）的结果是相同的，现在把第一位看成是符号位，那么-2（1010）的补码就是1110
所以补码是反码加一其实是巧合，真正的计算方式是如上的；
```



在byte中，127是0111 1111，-127是1111  1111，而-128的二进制是1000  0000，所以-128是-0，+0是0；

1+2+4+8+16+32+64=127；因为第一位是1，所以长度是7位但不是128；

其他的数据类型也是一样，-0表示最小的负数，正0表示0，在除去了符号位后其他位数的值是一样的；

**Integer对象从-128到127被放在缓存中，用==比是true，但是如果是new的就是false；**

##### 数据类型

* 基本数据类型
* 引用数据类型

###### 基本数据类型

![1566450717145](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1566450717145.png)



**chart没有符号位**

###### 位运算

<<左移，运算是乘以2，>>是右移，运算是除以2；

例如：3*8可转换为3<<3，5乘以16可转换为5<<4

###### switch

switch只能作用于32位及以下的数据，jdk1.7开始可以用于String，不能作用long；

每一个case都要有break；

```java
public void test() {
	switch (4) {
	case 8:
		System.out.println(8);
		break;
	case 4:
		System.out.println(4);
		break;
	case 1:
		System.out.println(1);
		break;
	default:
		System.out.println(0);
	}
}
```
###### 可变长度参数	

```java
  public void getIndex(int...num ) {//传入的参数相等于一个数组，在方法内就按照数组用
}
```



###### 方法重载**Overloading**

在一个类中，方法名相同，参数的个数类型顺序只要有一个不同即为重载，与返回值无关

###### 方法重写**Overiding**

在子类中重写父类的方法，方法名，参数列表，返回值完全相同，访问修饰符只能扩大，或不变；

使用时，优先调用子类的方法，如果子类没有重写会调用父类的；

###### static

静态的，它修饰的变量在类加载时就初始化，而非静态变量在对象被实例化的时候才初始化；

###### 获取一个对象的方式

* 实例化
* 反射
* 克隆
* 反序列化

###### 克隆

* 实现cloneable接口
* 重新clone方法，调用clone就返回本对象的克隆对象
* 浅克隆，只克隆基本数据类型，对象类型的属性还是同一个
* 深克隆，对象属性也不一样
* 实现深克隆，在clone方法中把属性对象也克隆一个，设置到返回的对象中
* 深克隆2，序列化反序列化

###### 序列化反序列化

* 实现Serializable接口

* 定义一个serialVersionUID，序列化的时候把它的值记录在序列化文件中，反序列化的时候，如果文件中的值相等就反序列化成功，否则失败

```java
  //序列化
User user = new User("id", "user");
  ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream("user.txt"));
            objectOutputStream.writeObject(user);
            objectOutputStream.close();
//反序列化
ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream("user.txt"));
            User user = (User) objectInputStream.readObject();
            objectInputStream.close();
```



###### 面向对象

* 封装，

  隐藏实现的细节，用户只能通过指定的方法访问，更安全，更方便。

* 继承，

  子类可以继承父类的所有非私有的方法和属性，可以重写父类的方法。

* 多态，

  多态是同一个接口的方法有不同的表现形式，子类继承父类或实现接口，父类引用指向子类实例；

* 抽象；

  对子类行为的规范，具体的实现由子类自己完成。

##### this

this代表本类的对象，

* 在构造方法中通过this调用其他构造方法，this要放在第一行，
* 普通方法不能用this调用构造方法，但可以用this调用普通方法

###### final

* 修饰类：不能有子类
* 修饰变量：一旦赋值不能修改
* 修饰方法：不能被重写；

String就是一个final类

|                      抽象类                      |              接口              |
| :----------------------------------------------: | :----------------------------: |
|                     abstract                     |           interface            |
| 可以有抽象方法也可以有普通方法，可以没有抽象方法 |         只能有抽象方法         |
|               只能声明，不能实例化               |      只能声明，不能实例化      |
|          父类可以是正常类，抽象类，接口          |         父类只能是接口         |
|                 属性和普通类一样                 | 属性只能是 public static final |
|          jdk1.8以后抽象方法可以有方法体          | jdk1.8以后抽象方法可以有方法体 |
|                                                  |                                |

###### 访问修饰符

|                   | 同类 | 同包 | 同包子类 | 外包 | 外包子类 |
| ----------------- | ---- | ---- | -------- | ---- | -------- |
| public            | Y    | Y    | Y        | Y    | Y        |
| protected受保护的 | Y    | Y    | Y        | N    | Y        |
| default           | Y    | Y    | Y        | N    | N        |
| private           | Y    | N    | N        | N    | N        |

##### 异常

**Throwable是所有异常和错误的父类**

* error：错误，jvm无法处理的问题，
* Exception：检查异常和非检查异常

###### Exception

* RuntimeException：非检查异常，人为的失误造成的，可以不用cache，例如;数组下标越界，空指针，除数为0，类型转换错误，参数非法
* checkedException:检查异常，必须要处理的；io异常，没有找到对应的类。

###### 自定义异常

继承Throwable类，写有参构造，调用super把参数传入，在有问题的地方抛出：throw new NumberException("aaa");

也可以直接抛出：throw new Exception("aaa");





### 集合

**集合常用操作**

**collection接口**

集合中只能存放引用数据类型，数组中引用数据类型和基本数据类型都可以存放；

* list接口，有序的，可以通过下标操作元素，允许重复

  * vector：底层是基于数组实现的，默认长度是10，当要增加长度时默认的增长一倍，不能有重复值，线程安全的；速度慢，线程安全；

  * ArrayList：底层是基于数组实现的，默认长度是10，当需要增加长度时默认的增长一半，可以有重复值，线程非安全；添加删除速度慢，查询速度快；
  * LinkedList：底层是基于链表实现的，同时实现了Queue接口，线程非安全；添加删除速度快，查询速度慢；

* set接口，无须的，不可以重复，允许有一个null

  * HashSet：底层是哈希算法，线程非安全；
  * TreeSet：底层是二叉树算法，线程非安全；

* queue接口（队列）

###### map接口，键值对，和collection没有任何关系

HashTable和HashMap的底层都是数组加链表的形式；

* HashTable：key和value不允许为null，线程安全；
* TreeMap：Key不能为null，Value可以为null，线程非安全；
* HashMap：Key和value都允许为null，线程非安全，初始长度16，当容量达到75%，就增加两倍；
* concurrentHashMap，线程安全的，而且高并发下速度快，插入采用cas算法，扩容采用同步锁

###### cas算法

线程会把主内存中的变量的值拷贝到自己的工作内存中作为期望值，当线程用到这个变量的时候会把自己的期望值和主内存的实际值比较，两者相同就继续执行，不同就说明其他线程修改过了，就会把自己的期望值改成现在主内存中的实际的值，再执行；

###### HashMap为什么线程不安全

当a线程插入一个值时，先计算key的Hash值得到一个位置，此时b线程也插入值，如果b的key的hash值和a的相同，b就会直接插入，a线程再插入就覆盖了b的值。扩容的时候会出现环形链表

如果两个key的hashcode相同时，再用equals方法比较，也相同就说明是key完全相同，会覆盖value，不相同，就会加在链表上。当链表达到一定长度就变成红黑树





###### 迭代器Iterator  

* next()：如果调用多次就会一直取下一个，所以在一次循环中只能用一下；
* remove()：删除；







#### volatile

两个特性：

###### 可见性

Java内存模型规定所有的变量都是存在主内存当中（物理内存），每个线程都有自己的工作内存（高速缓存）。线程对变量的所有操作都必须在工作内存中进行，而不能直接对主存进行操作。并且每个线程不能访问其他线程的工作内存。

所有多线程对变量操作时会出现线程安全的问题；

当变量被volatile修饰后，在多线程的情况下如果变量被线程a修改了，当线程b读取它时就会去主内存中去获取变量的值，而不使用自己的缓存中的值；

###### 有序性

当两行代码互不影响互相没有任何关系的时候，虚拟机进行编译的时候与可能会调整他们的位置；

但是有的时候调整了位置后会对后面的代码造成影响

这时候可以用volatile修饰一个变量，它可以保证本行代码之前的会先执行，之后的会后于它执行

**volatile不能保证一定会线程安全**

t=t+1，当线程a先执行但是还没有把结果写回内存中时，线程b就读取t的值，这时就会出现问题

**volatile安全的条件**

1，变量的值不是通过变量的当前值获得；



##### 原子操作

一个操作或多个操作要么全部执行并且执行过程不会被任何因素打断，要么就都不执行，和数据库的事务类似；



##### 线程本地变量

```java
	//它只有三个方法，表示在本线程中做存取删除的操作
    public static ThreadLocal<T> threadLocal = new ThreadLocal<T>();
    threadLocal.set(value);
    threadLocal.get();
    threadLocal.remove();
```



#### String

* char[]  toCharArray把字符串转换为字符数组
* replace用旧的字符替换新的字符
* String[]  split(String s)根基字符串把原来的字符串分隔
* subString根据下标截取字符串
* trim去掉首尾空格

#### StringBuffer，StringBuilder

是可修改的字符串，string是字符串常量，他俩是字符串变量

* 运算速度StringBuilder>StringBuffer>String
* StringBuffer是线程安全的，

###### 基本类型转String

* String的valuOf
* +""
* 基本类型的toString

###### String转基本类型

* 基本类型都有valueOf和parseXX的

valueOf返回包装类型

parseXXX返回基本类型





#### 时间日期

```java
Date  date=new Date();
```

* 没参数是获取当前时间
* 可以加入int参数年月日时分秒
* 可以单独获取date的年月日时分秒
* 可以加入毫秒数，表示1970-1-1  00:00:00后的一个时间点
* SimpleDateFormat，format方法设置Date的格式，parse方法把字符串的时间转换为Date类型
* System.currentTimeMillis()当前时间的毫秒数;
* date.getTime()当前时间的毫秒数;
* Date类型可以用after、before、equals比较

#### 数字操作

* 向上取整Math.ceil，如果是负数-15.2会取值15，整数15.2取16
* 向下取整Math.floor，
* 随机数Math.random()，产生0-1之间的一个随机数



##### 字节字符

* 字节：是一个8位的物理存储单元
* 字符：是一个表示字的大小的单位

一个字符等于2个字节

最开始的时候人们用8个可以开合的晶体管来组合成不同的状态，8个晶体管一共有256种不同的状态。从0到127被表示成特殊符号数字大小写的英文字母后面的状态是空闲的。这就是ASCII码

后来为了加入中文，采用两个字节来表达，第一个字节小于127的还是原来的ASCII码，第一个字节大于127，第二个字节大于127这样的用来表示汉字这是GB2312

再后来只要第一个大于127就表示汉字了，这是GBK

UNICODE：是统一了全球所有语言的编码，它用两个字节表示

UTF-8：是一种存储传输数据的编码格式，因为UNICODE在保存ASCII码可以表示的字符时会浪费，



##### Mysql数据库的锁

https://blog.csdn.net/qq_35642036/article/details/89554721

Mysql数据库的引擎有两种，InnoDB，MyISAM

InnoDb支持表级锁，行级锁

MyISAM支持表级锁

* 表级锁，开销小，加锁快，不会出现死锁，发生锁冲突的概率高，并发低
* 行级锁，开销大，加锁慢，会出现死锁，发生锁冲突概率低，并发度高
* 页面锁，开销和加锁时间介于表锁行锁之间，会出现死锁，并发度一般

###### MyISAM

只有表锁，分为读锁和写锁

* 对某表加了读锁，其他用户可以读但是不能写
* 对表加了写锁，其他用户的读写都不可以

myisam在select前会自动加读锁，在update，delete，insert前会自动加写锁不需要人为操作，显式的加锁是为了模拟事务，因为myisam没有事务的功能

在加锁后用户会一次性获得所有用到的表的锁，同时只能访问加锁的表，不能访问没加锁的表，所以不会出现死锁。

在MyiSam中写操作的优先级大于读，先写后读，所以它不适合大量读写的操作，可以通过参数调整优先级

###### InnoDB

InnoDB和myisam相比，支持行级锁，支持事务

###### 事务特性

* 原子性，对数据的修改要么全部完成要么全部不完成。
* 一致性，事务开始和完成时，数据要保持一致的状态
* 隔离性，事务执行时不会受外部并发操作的影响
* 永久性，事务完成后他对数据的修改是永久的

###### 事务并发的问题

* 丢失更新，两个事务同时对一个数据操作，后提交的会覆盖前一个做的修改
* 脏读，事务一对数据做了修改但还没提交，事务二就读取了数据
* 不可重复读，事务两次读取同一数据的结果不一样。
* 幻读，事务以相同的条件第二次查询数据，发现了其他事务新插入的数据

###### 事务的隔离级别

* 串行化，解决了全部问题，并发度低
* 可重复读，会出现幻读，mysql默认的隔离级别
* 可读已提交，幻读，不可重复读
* 读未提交，会脏读，幻读，不可重复读

InnoDB的行锁

* 共享锁，允许获得锁的用户去读，阻止其他用户获得本数据的排他锁

* 排他锁，允许获得锁的用户修改数据，阻止其他用户获得本数据的共享锁和排他锁

* InnoDB的行锁是通过索引实现的，只有操作加了索引的列才会触发行锁，否则是表锁。

* 对select自动加共享锁，对增删改自动加排他锁，显式加锁如下

  共享锁（Ｓ）：SELECT * FROM table_name WHERE ... LOCK IN SHARE MODE

  排他锁（X）：SELECT * FROM table_name WHERE ... FOR UPDATE

###### 使用InnoDB的注意

* 使用低的隔离级别
* 多个事务使用一组表时，使用的顺序相同
* 设计好索引
* 事务不能太大







#### 索引

索引就是把数据库表的某一列的值放到一个特定的数据结构中，使得以后再查询的时候可以借助数据结构的特点快速的查找到数据，

一般的是使用B树、B+树的结构，也有哈希表的方式

**数据库索引长度**

索引：单列索引、组合索引

* 普通索引

  **CREATE** **INDEX** indexName **ON** mytable(username(**length**));

* 唯一索引：列的值必须唯一，可以为null

  **CREATE** **UNIQUE** **INDEX** indexName **ON** mytable(username(**length**)) 

* 主键索引：特殊的唯一索引，不允许为null

* 组合索引

  1. **ALTER** **TABLE** mytable **ADD** **INDEX** name_city_age (**name**(10),city,age); 
  2. 组合索引只从最左边开始组合，就是说查询条件必须有name列才会生效
  3. 长度是索引要比较的长度，可以小于字符串的最大长度

* 全文索引：对文本域，char、varchar、text等建立索引，

###### 什么时候建立索引

* 在where或join中要用到的列
* 只有<，<=，=，>，>=，BETWEEN，IN，以及某些时候的LIKE的时候才会用到索引
* 当like以%开头时不会用到索引
* 应该选用差别度高的列，不经常修改的列，字符长度短的列

###### 索引的缺点

* 会降低更新表的速度insert、update、delete的时候既要更新表的数据也要更新索引的数据
* 索引会在磁盘上建立索引文件占用空间

###### 其他

* 索引不会保存null值，如果列的某个值是null，那么通过索引的方式不会找到他
* 如果一个很长的字符串的前几位是有很大区别的，那么就只查前几位不要把所有的都加入索引
* 不要在列上运算，运算会使索引失效而使用全表扫描
* not  in 、！=不能使用索引
* 使用or连接查询条件时，如果连接的条件都有单独的索引就会使用索引，一个列没有索引就不使用索引

##### sql优化

* 如果知道查询结果的条数用limit
* 使用索引
* 不要在列上做运算
* join的时候用小表驱动大表，A表10条数据，B表20条数据，使用A驱动B时查询被驱动表10次，使用B 驱动A时查询被驱动表20次
* select不要使用* ，把所有的列都写出来也比*好
* 把多个表的join转化成结果集：把join   t1变成join  （select  *  from  t1）,因为如果表锁定的化查询语句会一直等待
* insert时，使用批量插入



##### 树

树是多个节点的集合，一棵树的节点数量为0时是空树，每棵非空树有一个特定的根节点

每个节点的字树个数没有限制，但是他们一定互不相交

**一些定义**

* 节点的度：节点的子节点的个数
* 节点的层次：从根节点开始为第一层，根的孩子为第二层，以此类推
* 树的深度：树的最大层次树称为树的深度

##### 二叉树

* 是树的一种，每个节点最多有两个子节点
* 左字节点和右子节点是有顺序的，次序不能颠倒
* 即使只有一个子节点也要区分它是左还是右
* 二叉树存储数据会把比本节点小的数据放到左子节点，大的放到右子节点

###### 分类

* 斜树：所有节点只有左子节点的叫左斜树，还有右斜树

* 满二叉树：所有的节点都存在左子节点和右子节点，所有的叶子都在同一层上

* 完全二叉树：二叉树是分左右子树的，字树分布是先左后右，完全二叉树的定义是，对二叉树的节点编号，如果编号为a的节点和相同深度的满二叉树的编号为a的节点位置相同那么他就是完全二叉树，下图中少了G、FG、EFG都是完全二叉树

  从根节点开始，从左到右编号，如果编号连续就是完全二叉树

![1581225272195](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1581225272195.png)

![1581225291543](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1581225291543.png)

##### 二叉树的存储结构

###### 顺序存储

* 使用一维数组存储二叉树的节点，节点在数组中的下标位置就是节点在二叉树中的位置
* 完全二叉树会把数组填满，不完全二叉树会留有间隔，浪费空间

###### 二叉链表

* 把每一个节点的数据结构定义成一个数据和两个指针

##### 二叉树遍历

* 前序遍历：从根节点出发，第一次到达节点就输出数据，先向左再向右上图为ABDECF
* 中序遍历：从根节点出发，第二次到达节点时输出数据，先向左再向右上图为DBEAFC
* 后序遍历：从根节点出发，第三次到达节点时输出数据，先向左再向右上图为DEBFCA
* 层遍历：从上到下的遍历上图为ABCDEF

二叉树查找在极端的情况下会变成线性的链表，比如左斜树右斜树

###### B树

当使用二叉树查找数据时每查找一次就是一次磁盘IO开销很大，所以使用更加扁平的B树

* B树的阶：B树的所有节点中子节点最多的个数就是阶，叫M
* B树是平衡的，所以根节点要么没有子节点，要么至少两个子节点
* 除了根节点和叶节点，所有的节点至少有M/2个字节的
* 自平衡，所有的叶子节点都在同一层，如果有插入或删除会自动调整树的结构
* 每个节点可以含有多个元素，查找方式和二叉树类似，小的在左子树，大的在右子树

###### B+树

* 和B树比较B+树非叶子节点只具有索引的功能，不在记录数据
* 一个节点有K个子节点的也必然有k 个key
* 所有的叶子节点的值构成一个链表和上层的节点中的key对应

###### 红黑树





##### Redis

https://www.jianshu.com/p/56999f2b8e3b

redis是一个开源的key-value数据库

* redis数据库完全运行在内存中，使用磁盘仅用于持久化
* 读写速度快，提高系统性能

###### 应用条件

* 使用频率高，使用时读多写少，数据不要太大

###### 数据类型

* String：一个key对应一个value，可以储存图片和序列化的对象，最大能储存512M
* Hash：是一个键值对集合 key-(key-value，key-value，key-value，....)hash适合存储对象，可以做存储修改读取用户的属性
* List：一个字符串列表，按照插入顺序排序，可以做消息排行，消息队列
* Set：String类型的无序集合
* Zset：String类型的有序集合，不允许重复，每个元素会关联一个double类型的分数，安装分数大小给元素排序，元素不能重复分数可以重复，可以做排行榜，带权重的消息队列

###### 持久化

* rdb，redis会周期性的把数据保存到硬盘，生产一个rdb文件
* aof，redis把每一个执行的写命令都记录下来，

##### IO流

换行符是\r\n

![img](D:/md/img/20170105182342227.jpg)

流是一组有方向的数据集合，有起点和终点

* 字节流：以一字节，8位二进制为单位，能够处理所有的类型
* 字符流：它在读数据的时候去查码表，把字节转换为字符再传输，一次读写是16位二进制
* 纯文本使用字符流，其他使用字节流

###### inputstream

* reader()，读取一个字节，返回字节的ASCII码值，读完了返回-1，一次读一个字节效率低
* read(byte[])，把数据缓存在byte数组中，返回的是数组中元素个数，一次读一个数组的字节效率高
* read(byte[],len,cou)，读取cou个字节存在byte数组，位置是下标为len开始
* skip(long)，

###### outputstream

* write(int)，把这个字节写出
* write(byte[])，把数组写出
* write(byte[],len,cou)，把数组中第len个字节开始的cou个字节写出
* flush()，刷新此输入流，把流中的数据强制写出

文件流

###### Fileinputstream/out

* FileInputStream(File file)
*  FileInputStream(String name)，文件地址

###### FileoutPutStream

* FileInputStream(File file,boolean)，true是追加写入，false是覆盖

###### BufferreadInputStram，给流加了一个套，套在外面，读写的操作和原来一样

* BufferreadInputStram(inputstream)，默认缓冲区大小
* BufferreadInputStram(inputstream，int)，指定缓冲区大小

###### Reader和writer和inputstream一样，把byte换成char

###### InputStreamReader，字节字符转换流，in是把读到的字符变成字节输入，可以使用默认编码，也可以指定编码，out是把字节流变成字符流输出

*  String getEncoding() ，返回流使用的编码名称

###### BufferReader字符缓冲流

* BufferReader(Read  in)，默认大小的缓冲区
* BufferReader(Read  in，int  size)，指定缓冲区大小
*  String readLine()，读取一行，空行了是null
*  void newLine() ，写入一行

###### Inputstream抽象类，是所有字节输入流的父类

* ByteArrayinputstream，是从内存的字节数组中读写文件，和普通的字节数组没啥区别，它主要作用是流和数组直接的转换

* StringBufferinputstream，主要是流和字符串缓冲区的转换

* Fileinputstream

* Filterinputstream：装饰器模式的

  **BufferedInputStrean**缓冲流，**DataInputStream**数据流

* Objectinputstream，对象流

* inputstreamReadr：字节字符转换流

##### NIo

nio是非阻塞的，面向缓冲区，它是从内存到磁盘然后通过缓冲区运输数据

###### 存储过程

* 返回值有无都行，可以是多个
* 可以单独执行
* sql语句不能调用
* 参数类型，in,out,in out

```sql
CREATE PROCEDURE 创建的存储过程名字(OUT|IN|INOUT 参数名 数据类型,...,...)

begin

end 
call  procedureName;
```

###### 函数

* 必须有且只有一个返回值，可以是一个值或表
* 只能通过execute执行
* 可以在sql中使用，可以位于from后面
* 参数，mysql只有in,Oracle有in，out，inout

```sql
create  Function  name（参数）

return  返回值的类型
begin
sql代码
retuen 具体的返回值
end

select  name；
```

###### 在sql使用事务

```sql
begin tran
begin try
    insert into TEST_name values(1,1)
    insert into TEST_name values(2,null)
    insert into TEST_name values(3,2)
    commit tran
end try
begin catch
    select '执行异常，事务回滚'
    rollback tran
end catch
```

触发器，是一种特殊类型的存储过程，不能手动调用，和表紧密相连，当对表进行操作的时候会自动触发







##### json

* 对象    { "property":value, "property":value, "property":value, ....}
* 数组   [value,value,value...]
* 可以互相嵌套

##### 正则表达式



![1581410653788](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1581410653788.png)



![1581410702308](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1581410702308.png)

**分组（）表示括号中的字符串是一个整体**

^ab*表示a开头0或多个b组成的字符串

^(ab)*表示0或多个ab组成的字符串

**转义是把元字符限定字符或关键字转为普通的字符,在要转的字符前加\\***

```java
^(\(ab\))*
```

**条件或|**

**区间**[]，数字字母字符都可以

“abc”.match("正则")

#### webservice

是跨语言跨平台的远程调用技术

###### XSD

webservice使用Http协议传输数据，使用xml格式封装数据，XSD是一套在xml中使用的数据类型标签语言

###### SOAP

webservice使用http协议发送请求和接收结果，请求和结果的内容使用xml封装，并增加一些特定的消息头来说明内容的格式，这些消息头和xml内容格式就是SOAP协议

###### WSDl

服务端用一个wsdl文件来说明自己所提供的方法，方法的参数，返回值，地址，调用方式。wsdl是一个基于xml的语言，它存在于服务端

###### 使用jdk生成webservice

* 业务接口用webservice注解，业务方法用webmethod注解
* 实现类用webservice注解
* 发布类，Endpoint.publish(地址, new WebImpl());，地址中ip是本机ip后面的部分可以随便写，启动
* 在地址？wsdl查看wsdl文件
* 在cmd的客户端目录下运行：wsimport  -keep  地址？wsdl，自动生成代码
* 可以调用查询天气的接口，

###### 使用cxf框架

* 导入cxf的jar包
* 接口实现类正常写，
* 发布类，用jaxWsServiceFactorybean的对象，设置地址、实现类的Class、create、start
* 客户端类，得到一个client对象，通过client调用方法，返回的是Object类型

```java
 //通过CXF提供的JaxWsServerFactoryBean来发布webservice  
	 public void Server2() throws Exception {  
		 System.out.println("开始发布");
		 JaxWsServerFactoryBean factory = new JaxWsServerFactoryBean();  
		 //对外暴露的接口类
		 factory.setServiceClass(WebInterfaceImpl.class);   	  
		 //对外暴露地址
		 factory.setAddress("http://127.0.0.1:8080/webCXF");
		 //创建
		 org.apache.cxf.endpoint.Server server = factory.create();  
		 //启动
		 server.start();
		 System.out.println("发布成功：http://127.0.0.1:8080/webCXF");
     }  

//动态调用
	public void getCXFInfo(){
		 JaxWsDynamicClientFactory  f =  JaxWsDynamicClientFactory.newInstance();
		 Client c = f.createClient("http://127.0.0.1:8080/webCXF?wsdl");
		 try {
			 //invoke(调用地址的方法名，发送参数);
			 Object [] objects = 	c.invoke("HandleData", "ssss");
		 System.out.println("返回长度："+objects.length);
		 if(objects.length>0){
			 System.out.println("返回内容为："+objects[0].toString());
		 }
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
```

树形查询

webservice

AOP：面向切面编程，把一些非核心、大范围使用的业务不需要把他们挨个的加到每个方法，而是通过织入到每一个点让它们起作用。

IOC：依赖注入，类中需要的对象，由spring容器注入给他，避免使用new的方式，降低耦合，符合开闭原则





##### shiro

* subject，主体用户

* securityManager，安全管理器，shiro的核心

* realm，是数据源可以是ini文件，也可以是AuthorizingRealm的实现类，有getName和授权认证的两个方法，在方法内通过数据库获取数据，然后把这个类通过ini文件加载到系统

##### 数据库

###### 为什么要使用数据库

* 保证数据的一致性，都是数字或都是时间类型
* 保证数据安全
* 节省空间

###### 关系模型

把世界看成实体和实体之间的关系组成，实体就是在现实世界客观存在并可以相互区分的事物。

对象模型

###### 外键Foreign  key，用来表达表和表之间的关联关系，A表的外键通常是B表的主键

###### 一对一关系，A表中的一行只和B表中的一行对应



##### Git&Svn

本地代码库，远程个人代码库，远程代码库

* git是分布式，svn是集中式

* git支持本地代码库，本地分支，方便多线程工作
* git使用分支方便，建立合并等
* git可以直接开发人员之间交流代码















#### Mycat

水平拆分：把一个十条数据的表分成两个五条的表

垂直拆分：把表的字段拆分，通过主键联系

垂直拆分：垂直分库（把不同业务模块的表放到不同的数据库中），垂直分表（上面那样，把不经常用或字段长度较大的字段分出去）



**chart，short的字符数字**，对象类型转换























**Docker 属于 Linux 容器的一种封装，提供简单易用的容器使用接口**

**nginx:反向代理，负载均衡，服务器**



hashcodde  equese  二叉树



jdk1,8的变化

switch可以用string

抽象方法可以有方法体了















