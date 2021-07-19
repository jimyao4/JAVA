### 															第五章——java多线程和并发编程

#### 第一节 多线程和多线程简介

1. 多线程概念

- 当前的操作系统都是多任务OS

- 每个独立执行的任务就是一个进程

- OS将时间划分为多个时间片(时间很短)

- 每个时间片内将CPU分配给某一个任务,时间片结束, CPU将自动回收,再分配给另外任务.从外部看,所有任务是同时在执行.但是在CPU上,任务是按照串行依次运行(单核CPU).如果是多核,多个进程任务可以并行.但是单个核上,多进程只能串行执行.

- 多线程的优点

  ——可以同时运行多个任务程序

  ​	-因IO堵塞时,可以释放CPU,让CPU为其他程序服务

  ​	-当系统有多个CPU时,可以为多个程序同时服务

  ​	-我们的CPU不再提高频率,而是提高核数

  ​	-2005年 Herb sutter t文章 The free lunch is over,指明多核和并行程序才是提高程序性能的唯一办法

  ——多进程的缺点

  -太笨重,不好管理

  -太笨重,不好切换



3. 多线程概念

   ​                                                                                                                                一个程序---可以包括多个子任务,可串/并行

   -每个子任务可以称为一个线程

   -如果一个子任务阻塞,程序可以将CPU调度另外一个子任务进行工作.这样CPU还是保留在本程序中,而不是被调度到别的程序(进程)去.这样,提高本程序所获得CPU时间和利用率.                                

   

4. 多进程和多线程对比

   -线程共享数据

   -线程通讯更高效

   -线程更轻量级,更容易切换

   -多个线程更容易管理

   

5. 示例

   -多进程执行:启动两个 Java.exe多线程执行:只启动一个 java.exe

#### 第二节 java多线程实现

1. 多线程创建

   java. lang Thread

   线程继承 Thread类,实现run方法

   ava. lang Runnable接口

   线程实现 Runnable接口,实现run方法

   ​		

2. java多线程启动

- 启动

  -start方法,会自动以新进程调用run方法

  -直接调用run方法,将变成串行执行

  -同一个线程,多次star会报错,只执行第一次start方法

  -多个线程启动,其启动的先后顺序是随机的

  -线程无需关闭,只要其run方法执行结束后,自动关闭

  -main函数(线程)可能早于新线程结束

  -整个程序并不终止整个程序终止是等所有的线程都终止(包括main函数线程)                                

3. java多线程实现对比

   ——Thread ys runnable Thread

   ​	-占据了父类的名额,不如 Runnable方便

   ​	-Thread类实现 Runnable 

   ​	-Runnable启动时需要 Thread类的支持

   ​	-Runnable更容易实现多线程中资源共享

   ——结论:建议实现 Runnable接口来完成多线程

#### 第三节 多线程信息共享

1. 多线程信息共享

   ——线程类

   ​	-诵过继承 Thread或实现 Runnable

   ​	-通过star方法,调用run方法,tun方法工作

   ​	-线程run结束后,线程退出

   ——粗粒度:子线程与子线程之间、和main线程之间缺乏交流

   ——细粒度:线程之间有信息交流通讯

   ​	-通过共享变量达到信息共享

   ​	-JDK原生库暂不支持发送消息(类似MPI并行库直接发送消息)

   ——通过共享变量在多个线程中共享消息

   ​	-static变量

   ​	-同一个 Runnable类的成员变量

   ——多线程信息共享问题

   ​	-工作缓存副本

   ​	-关键步骤缺乏加锁限制

   ——i++,并非原子性操作

   ​	-读取主存(正本)到工作缓存(副本)中

   ​	-每个CPU执行(副本)计1操作

   ​	-CPU将结果写入到缓存(副本)中

   ​	-数据从工作缓存(副本)刷到主存(正本)中

   ——变量副本问题的解决方法

   ​	-采用 volatile关键字修饰变量

   ​	-保证不同线程对共享变量操作时的可见性                              		                                

   ——关键步骤加锁限制

   ​	-互斥:某一个线程运行一个代码段(关键区),其他线程不能同时运行这个代码段

   ​	-同步:多个线程的运行,必须按照某一种规定的先后顺序来运行

   ​	-互斥是同步的一种特例

   ——互斥的关键字是 synchronized 

   ​	-synchronized代码块/函数,只能一个线程进入

   ​	-synchronized加大性能负担但是使用简便                                

#### 第四节 多线程管理

- 线程类

  -诵过继承 Thread或实现 Runnable

  -通过 start方法,调用run方法,tun方法工作

  -线程run结束后,线程退出                                

- 粗粒度：子线程与子线程之间，和main线程之间缺乏同步

- 细粒度：线程之间有同步协作

  -等待

  -通知/唤醒

  -终止

- 线程状态

  -NEW刚创建(new）

  -RUNNABLE就绪态( start ）

  -RUNNING运行中(run)

  -BLOCK阻塞(slee）

  -TERMINATED 结束

- Thread的部分API已经废弃

  -暂停和恢复 suspend/ resume

  -消亡stop/d estro y

- 线程阻塞和换醒

  -slep,时间一到,自己会醒来

  -wait/ notify/ notify,等待,需要别人来唤醒

  -join,等待另外一个线程结束

  -interrupt,向另外一个线程发送中断信号,该线程收到信号,会触发 InterruptedException(可解除   阻塞),并进行下一步处理                                

- 线程被动暂停和终止

  -依靠别的线程来拯救自己的

  -没有及时释放资源

- 线程主动暂停和终止

  -定期监测共享变量

  -如果需要暂停或者终止,先释放资源,再主动动作

  -暂停: Thread. sleep,休眠

  -终止:rumn方法结束,线程终止

- 多线程死锁

  -每个线程互相持有别人需要的锁(哲学家吃面问题)

  -预防死锁,对资源进行等级排序

- 守护后台进程

  -普通线程的结束,是run方法运行结束

  -守护线程的结束,是run方法运行结束,或main函数结束

  -守护线程永远不要访问资源,如文件或数据库等                                

- 线程查看工具jvisualvm

- 

#### 第五节 java 并发框架Executor

1. 并行计算

   ​	——业务:任务多,数据量大

   ​	——串行vs并行

   ​		-串行编程简单,并行编程困难

   ​		-单个计算核频率下降,计算核数增多,整体性能变高

   ​	——并行困难(任务分配和执行过程高度耦合)

   ​		-如何控制粒度,切割任务

   ​		-如何分配任务给线程,监督线程执行过程	

   ​	——并行模式

   ​		-主从模式 Master-Slave)

   ​		-Worker模式 Worker-Worker)

   ​	——Java并发编程

   ​		-Thread/ Runnable/ Thread组

   ​		-管理Executor

   ​		-Fork-Join框架

2. 线程组管理

   ​	——线程组 ThreadGroup

   ​	线程的集合

   ​	树形结构,大线程组可以包括小线程组

   ​	可以通过 enumerate方法遍历组内的线程,执行操作

   ​	能够有效管理多个线程,但是管理效率低

   ​	任务分配和执行过程高度耦合重复创建线程、关闭线程操作,无法重用线程                                

3. Excutor

   ​	——从JDK5开始提供 Executor FrameWork（java.util.concurrent.*）

   ​		-分离任务的创建和执行者的创建

   ​		-线程重复利用(new线程代价很大

   ​	——理解共享线程池的概念

   ​		-预设好的多个 Thread,可弹性增加

   ​		-多次执行很多很小的任务

   ​		-任务创建和执行过程解耦

   ​		-程序员无需关心线程池执行任务过程

   ​	——主要类: ExecutorService, ThreadPoolExecutor, Future

   ​		-Executors. new CachedThreadPool/ newFixed ThreadPool创建线程池

   ​		-ExecutorService线程池服务

   ​		-Callable具体的逻辑对象(线程类)

   ​		-Future返回结果

#### 第六节 Fork-in

​	——java7提供另一种并行框架:分解、治理、合并(分治编程)

​	——适合用于整体任务量不好确定的场合(最小任务可确定)

​	—— ForkJoinPool任务池

​		-RecutsiveAction

​		-RecursiveTask                                



#### 第七节 java并发数据结构

1. 并发数据结构

   ​	——常用的数据结构是线程不安全的

   ​		-ArrayList,, HashMap, HashSet非同步的

   ​		-多个线程同时读写,可能会拋出异常或数据错误

   ​	——传统 Vector, Hashtable等同步集合性能过差

   ​	——并发数据结构:数据添加和删除

   ​		-阻塞式集合:当集合为空或者满时,等待

   ​		-非阻塞式集合:当集合为空或者满时,不等待,返回nul或异常

   ​	——List 

   ​		-Vector同步安全,写多读少

   ​		-ArrayList不安全

   ​		-Collections. synchronizedList(List list)基于 synchronized,效率差

   ​		-CopyOn Write ArrayList读多写少,基于复制机制,非阻塞

   ​	——Set 

   ​		-HashSet不安全

   ​		-Collections. synchronizedSet(Set se基于 synchronized,效率差

   ​		-CopyOn Write ArraySet(基于 CopyOn Write ArrayList实现)读多写少,非阻塞

   ​	——Mat 

   ​		-Hashtable同步安全,写多读少

   ​		-HashMap不安全

   ​		-Collections. synchronizedMap(Map map)基于 synchronized,效率差

   ​		-ConcurrentHashMap读多写少,非阻塞

   ​	——Queue& Deque(队列,JDK1.5提出)

   ​		-ConcurrentLinkedQueue非阻塞

   ​		-Array BlockingQueue/ inked Queue阻塞

#### 第八节 java并发协作控制

1. 线程协作

   ​	——Thread/Executor/ Fork-Join

   ​		-线程启动,运行,结束

   ​		-线程之间缺少协作

   ​	——synchronized同步

   ​		-限定只有一个线程才能进入关键区

   ​		-简单粗暴,性能损失有点大⑧

2. lock

   ​	——lock也可以实现同步的效果

   ​		-实现更复杂的临界区结构

   ​		-tryLock方法可以预判锁是否空闲

   ​		-允许分离读写的操作,多个读,一个写

   ​		-性能更好

   ​	——Reentrantlock类,可重入的互斥锁

   ​	——ReentrantReadWriteLock类,可重入的读写锁

   ​	——lock和 unlock函数

3. semaphore

   ​	——信号量,由1965年 Dijkstra提出的

   ​	——信号量:本质上是一个

   ​	——计数器计数器大于0,可以使用,等于0不能使用

   ​	——可以设置多个并发量,例如限制10个访问

   ​	——Semaphore 

   ​		-acquire获取

   ​		-release释放

   ​	——比Lock更进一步,可以控制多个同时访问关键区

4. latch

   ​	——等待锁,是一个同步辅助类

   ​	——用来同步执行任务的一个或者多个线程

   ​	——不是用来保护临界区或者共享资源

   ​	——CountDownLatch 

   ​		-countDown0计数减1

   ​		-await0等待atch变成0

5. Barrier

   ​	——集合点,也是一个同步辅助类

   ​	——允许多个线程在某一个点上进行同步

   ​	——CyclicBarrier

   ​		-构造函数是需要同步的线程数量

   ​		-await等待其他线程,到达数量后,就放行

6. phaser

   ​	——允许执行并发多阶段任务,同步辅助类

   ​	——在每一个阶段结束的位置对线程进行同步,当所有的线程都到达这步,再进行下一步

   ​	——Phaser

   ​		-arrive

   ​		-arriveAndAwaitAdvanceO

7. Exchanger

   ​	——允许在并发线程中互相交换消息

   ​	——允许在2个线程中定义同步点,当两个线程都到达同步点,它们交换数据结构

   ​	——Exchanger 

   ​		-exchange（）线程双方互相交互

   ​		-数据交换数据是双向的

#### 第九节 java定时任务执行

1. 定时任务

   ​	——Thread/ Executor/ Fork-Join多线程

   ​		-立刻执行

   ​		-框架调度

   ​	——定时执行

   ​		-固定某一个时间点运行

   ​		-以某一个周期

   ​	——简单定时器机制

   ​		-设置计划任务,也就是在指定的时间开始执行某一个任务.

   ​		-TimerTask封装任务

   ​		-Timer类定时器

   ​	——Executor+定时器机制

   ​	——ScheduledExecutorservice

   ​		-定时任务

   ​		-周期任务

   ​	——Quartz

   ​		-Quartz是一个较为完善的任务调度框架

   ​		-解决程序中 Timer零散管理的问题

   ​		-功能更加强大

   ​			·Timer执行周期任务,如果中间某一次有异常,整个任务终止执行

   ​			·Quartz执行周期任务,如果中间某一次有异常,不影响下次任务执行

- WORK1

```JAVA

public class ThreadDemo {

	public static void main(String[] args) {
		int m=1; 
		int n=100000000;
		int quotient=n/6;     //商
		int remainder=n%6;    //余数
//		System.out.println(quotient);
//		System.out.println(remainder);
		
		TestThread t= new TestThread();
		
		//每个线程大小
		t.threadSize[0]=quotient+remainder;//=16666666+4
		for( int i=1;i<6;i++) {
			t.threadSize[i]=quotient;	
    	}
		//每个线程开始数字
		t.threadStart[0]=m;
		for (int i = 1; i < 6; i++) {
			t.threadStart[i]=t.threadSize[i-1]+t.threadStart[i-1];
		}
		
//		for (int i = 0; i < 6; i++) {
//			System.out.println();
//			System.out.println("size "+t.threadSize[i]);
//			System.out.println("start "+t.threadStart[i]);
//		}
		new Thread(t, "Thread0").start();
		new Thread(t, "Thread1").start();
		new Thread(t, "Thread2").start();
		new Thread(t, "Thread3").start();
		new Thread(t, "Thread4").start();
		new Thread(t, "Thread5").start();
		
		while (true) {
		try {
			Thread.sleep(100);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		//System.out.println("t.threadNum: "+t.threadNum);
		if (t.threadNum>5) {   //如果t.seq>5，则说明6个线程已经运行完毕，结束循环
			break;
		}
		}
		//输出最后的总和
		System.out.println("------------------\n"
		+"sum="+t.sum);
	}
	
}

class TestThread implements Runnable{

	volatile int[] threadSize =new int[6];//每个线程的大小
	volatile int[] threadStart = new int[6];//每个线程的开始数字
	
	volatile long sum=0;//总和
	volatile int threadNum=0;//代表当前线程的数字//?

	public void run() {
		int threadNum=getThreadNum();//?
		//System.out.println(threadNum);

		int size=threadSize[threadNum];
		int start=threadStart[threadNum];
		long partsum=0;
		
		//计算每个线程部分的总和
		for (int i = start; i < (size+start); i++) {
			partsum=partsum+i;
		}
		//System.out.println("i="+i);	
		total(partsum);
		System.out.println("Thread"+threadNum+"partsum = "+partsum);
		
	}
	
	private synchronized int getThreadNum() {
		return threadNum++;
	}
	private synchronized void total(long partsum) {
		this.sum+=partsum;	
	}
	
}

```



- WORK2

  ```JAVA
  import java.util.concurrent.*;
  
  public class FindNumberCount {
      public static void main(String[] args) throws InterruptedException, ExecutionException {
          int[] numbers = new int[100450];
          int targetNumber = 50;
          for (int i = 0; i < numbers.length; i++) {
              numbers[i] = (int) (Math.random() * 100);
          }
          System.out.println("findBySerial = " + findBySerial(numbers, targetNumber));
          System.out.println("findByExecutor = " + findByExecutor(numbers, targetNumber));
          System.out.println("findByForkJoin = " + findByForkJoin(numbers, targetNumber));
      }
  
      public static int findBySerial(int[] numbers, int targetNumber) {
          int cnt = 0;
          for (int i = 0; i < numbers.length; i++) {
              if (numbers[i] == targetNumber)
                  cnt++;
  
          }
          return cnt;
      }
  
      public static int findByExecutor(int[] numbers, int targetNumber) throws InterruptedException {
          ExecutorService executor = Executors.newCachedThreadPool();
  
          int increment = 1000; //每1000长度为一组
          int numOfThread = numbers.length / increment;
          CountDownLatch latch = new CountDownLatch(numOfThread);
  
          int startIndex = 0, endIndex = increment - 1;
          for (int i = 0; i < numOfThread; i++) {
              if (i == numOfThread - 1)
                  endIndex = numbers.length - 1;
              executor.execute(new ExecutorTask(numbers, startIndex, endIndex, targetNumber, latch));
  //            new Thread(new ExecutorTask(numbers, startIndex, endIndex, targetNumber, latch)).start();
              startIndex = endIndex + 1;
              endIndex = endIndex + increment;
          }
  
          latch.await();
          executor.shutdown();
          return ExecutorTask.getSumCnt();
      }
  
      public static int findByForkJoin(int[] numbers, int targetNumber) throws InterruptedException, ExecutionException {
          ForkJoinPool pool = new ForkJoinPool();
          ForkJoinTask<Integer> task = new MyForkJoinTask(numbers, 0, numbers.length - 1, targetNumber);
          task = pool.submit(task);
          Integer cnt = task.get();
          pool.shutdown();
          return cnt;
      }
  
  }
  
  class ExecutorTask implements Runnable {
      private static int sumCnt = 0;
      private int[] numbers;
      private int startIndex;
      private int endIndex;
      private int targetNumber;
      private CountDownLatch latch;
  
      public ExecutorTask(int[] numbers, int startIndex, int endIndex, int targetNumber, CountDownLatch latch) {
          this.numbers = numbers;
          this.startIndex = startIndex;
          this.endIndex = endIndex;
          this.targetNumber = targetNumber;
          this.latch = latch;
      }
  
      @Override
      public void run() {
          int cnt = 0;
          for (int i = startIndex; i <= endIndex; i++) {
              if (numbers[i] == targetNumber)
                  cnt++;
          }
  
          synchronized (ExecutorTask.class) {
              sumCnt += cnt;
          }
          latch.countDown();
      }
  
      public static int getSumCnt() {
          return sumCnt;
      }
  }
  
  class MyForkJoinTask extends RecursiveTask<Integer> {
      int[] numbers;
      int startIndex;
      int endIndex;
      int targetNumber;
  
      public MyForkJoinTask(int[] numbers, int startIndex, int endIndex, int targetNumber) {
          this.numbers = numbers;
          this.startIndex = startIndex;
          this.endIndex = endIndex;
          this.targetNumber = targetNumber;
      }
  
      @Override
      protected Integer compute() {
          int cnt = 0;
          if (endIndex - startIndex < 1000) {
              for (int i = startIndex; i <= endIndex; i++) {
                  if (numbers[i] == targetNumber)
                      cnt++;
              }
          } else {
              int midIndex = (startIndex + endIndex) / 2;
              MyForkJoinTask leftTask = new MyForkJoinTask(numbers, startIndex, midIndex, targetNumber);
              MyForkJoinTask rightTask = new MyForkJoinTask(numbers, midIndex + 1, endIndex, targetNumber);
  
  //            leftTask.fork();
  //            cnt = rightTask.compute() + leftTask.join();
  
              invokeAll(leftTask, rightTask);
              cnt = rightTask.join() + leftTask.join();
          }
  
          return cnt;
  
      }
  
  }
  
  ```

  