### 																																					第六章-java网络编程

#### 第一节 网络基础知识

1. 网络基础知识

   ​	——网络是当前信息技术的第一推动力
   
   ​	——每个计算设备上都有若干个网卡
   
   ​	——每个网卡上有(全球唯一)单独的硬件地址,MAC地址                               	
   
   ——IP地址每个网卡/机器都有一个或多个P地址
   
   ​	-IPV4:1921680.100,每段从0到255
   
   ​	-IPV6:128bit长,分成8段,每段4个16进制数
   
   ​		·FE80:0000:0000:0000:AAAA:0000:00C2:0002
   
   ​		·https://baike.baidu.com/item/ipv6/172297?fr=aladdin
   
   ——查询: Windows平台 ipconfig, Linux/Mac平台 ifconfig
   
   ——port:端口0655350~1023,OS已经占用了,80是Web,23是 telnet
   
   ​	-1024~65535,一般程序可使用(谨防冲突)
   
   ——两台机器通讯就是在I+Por上进行的
   
   ——在 Windows/ Linux/Mac上都可以通过 netstat-an来查询
   
   ——保留ip:127.0.0.1本机
   
   ——公网(万维网/互联网和内网(局域网)
   
   ​	-网络是分层的
   
   ​	-最外层是公网/互联网
   
   ​	-底下的每层都是内网C: \Users\Tom.
   
   ​	-ip地址可以在每个层次的网重用
   
   ​	-tracert看当前机器和目标机器的访问中继
   
   ——通讯协议:TCP和UDP 
   
   ——TCP（Transmission Control Protocol)
   
   ​	-传输控制协议,面向连接的协议
   
   ​	-两台机器的可靠无差错的数据传输
   
   ​	-双向字节流传递
   
   ——UDP(User Datagram Protocol）
   
   ​	-用户数据报协议,面向无连接协议
   
   ​	-不保证可靠的数据传输
   
   ​	-速度快,也可以在较差网络下使用

#### 第二节 UDP编程

1. UDP

   ——计算机通讯:数据从一个P的port出发(发送方),运输到另外一个的port(接收方)

   ——UDP:无连接无状态的通讯协议

   ​	-发送方发送消息,如果接收方刚好在目的地,则可以接受.如果不在,那这个消息就丢失了

   ​	-发送方也无法得知是否发送成功

   ​	-UDP的好处就是简单,节省,经济

   —— Datagram Socket:通讯的数据管道

   ​	-send和 receive方法

   ​	-(可选,多网卡)绑定一个IP和Port

   ——DatagramPacket

   ​	-集装箱:封装数据

   ​	-地址标签:目的地IP+Port

   ——实例

   ​	-无主次之分

   ​	-接收方必须早于发起方执行

#### 第三节 java TCP编程

1. TCP

   

   ——TCP协议:有链接、保证可靠的无误差通讯

   ​	-服务器:创建一个 ServerSocket,等待连接

   ​	-客户机:创建一个 Socket,连接到服务器

   ​	-服务器: ServerSocket接收到连接,创建一个 Socket和客户的Socket建立专线连接,后续服务器和客户机的对话(这一对 Socket会在一个单独的线程(服务器端)上运行

   ​	-服务器的 ServerSocket继续等待连接,返回第一步

![image-20210714175730451](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210714175730451.png)





- ServerSocket：服务器码头

  -需要绑定port

  -如果有多块网卡,需要绑定一个卫地址

  ——Socket运输通道

  ​	-客户端需要绑定服务器的地址和Port

  ​	-客户端往 Socket输入流写入数据,送到服务端

  ​	-客户端从 Socket输出流取服务器端过来的

  ​	-数据服务端反之亦然

  ——服务端等待响应时,处于阻塞状态

  ——服务端可以同时响应多个客户端

  ——服务端每接受一个客户端,就启动一个独立的线程与之对应

  ——客户端或者服务端都可以选择关闭这对Sσcket的通道

  ——实例

  ​	-服务端先启动,且一直保留

  ​	-客户端后启动,可以先退出

#### 第四节 java HTTP编程

1. 网络访问

   ——网页是特殊的网络服务(HTTP,HypertextTransferProtocol)

   ​	-在浏览器输入URL地址

   ​	-浏览器将连接到远程服务器上(P+8OPort）

   ​	-请求下载一个HTML文件下来,放到本地临时文件夹中

   ​	-在浏览器显示出来

2. HTTP

   ——HTTP

   ​	-超文本传输协议( HyperText Transfer Protocol）

   ​	-用于从WwW( World Wide Web)服务器传输超文本到本地浏览器的传输协议

   ​	-1989年蒂姆·伯纳斯·李( Tim Berners lee)提出了一种能让远隔两地的研究者们共享知识的	设想	

   ​	-借助多文档之间相互关联形成的超文本( HyperText),连成可相互参阅的WWW

   ​	-1990年问世,1997年发布版本11,2015年发布版本2.0

   ​	-资源文件采用HTM编写,以URL形式对外提供

3. HTML

   -HTMI超文本标记语言( LyperText Markup Language)

   -标准语法http://www.w3school.com.cn/html/index.asp

   -表单form

```java
<html>
<tit1e>登陆</tit1e>
<body>
<form name=' form1>
id: <input type=' text name=id><br>
name: <input type='text' name=name><br>
<input type='submit' value='ok'>
</form>
</body>
</html>
```

4. HTTP访问方式

   ——访问方式

   ​	-GET:从服务器获取资源到客户端

   ​	-POST:从客户端向服务器发送数据

   ​	-PUT:上传文件

   ​	-DELETE:删除文件

   ​	-HEAD:报文头部

   ​	-OPTIONS:询问支持的方法

   ​	-TRACE:追踪路径

   ​	-CONNECT:用隧道协议连接代理

5. java HTTP 编程

   ——支持模拟成浏览器的方式去访问网页

   ——URL, Uniform Resource locator,代表一个资源http://www.ecnu.edu.cn/index.htmipa=1&B=2&cc=3

   ——URLConnection

   ​	-获取资源的连接器

   ​	-根据URL的 openConnection0方法获得 URLConnection 

   ​	-connect方法,建立和资源的联系通道ge

   ​	-getInputStream方法,获取资源的内容

#### 第五节 java HTTP编程

1. HttpClient

   ——JDK HTTP Client（JDK自带，从9开始）

   ——Apache HttpComponents的HttpClient（Apache出品）

2. JDK HttpClient

   ——JDK9新增,JDK10更新,JDK11正式发布

   ——java. net. http包

   ——取代 URLConnection

   ——支持HTTP/1.1和HTTP/2

   ——实现大部分HTTP方法

   ——主要类

   ​	-Httpclient 

   ​	-Httprequest 

   ​	-Httpresponse

3. HttpComponents

   ——hc. apache. org, Apache出品

   ——从 Httpclien进化而来

   ——是一个集成的java http工具包

   ​	-实现所有HTTP方法:get/post/put/delete

   ​	-支持自动转向

   ​	-支持https协议

   ​	-支持代理服务器等

#### 第六节 Java NIO编程

1. NIO

   ——Non-Blocking I/O

   ——提供非阻塞通讯等方式

   ——避免同步I/O通讯效率过低

   ——一个线程可以管理多个连接

   ——减少线程多的压力

   ——Non- Blocking I/O,非阻塞I/O,(又名NewI/O

   ——JDK14引入,17升级NIO2.0(包括了AIO

   ——主要在 java nio包中

   ——主要类

   ​	-Buffer缓存区

   ​	-Channel通道

   ​	-Selector多路选择器

   ——NIO服务端-客户端通讯示意图

   ![image-20210715123749119](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210715123749119.png)



- Channel通道

  ​	-全双工的,支持读/写(而 Stream流是单向的)

  ​	-支持异步读写

  ​	-和 Buffer配合,提高效率

  ​	-ServerSocketChannel服务器 TCP Socket接入通道,接收客户端

  ​	-SocketChannel TCP Socket通道,可支持阻塞/非阻塞通讯

  ​	-DatagramChannel UDP通道FileChannel文件通道

- Selector多路选择器

  ​	-每隔一段时间,不断轮询注册在其上的 Channel

  ​	-如果有一个 Channel有接入、读、写操作,就会被轮询出来

  ​	-根据 SelectionKey可以获取相应的 Channel,进行后续IO操作

  ​	-避免过多的线程

  ​	SelectionKey四种类型

  ​	· OP CONNECT

  ​	· OP ACCEPT

  ​	· OP READ OP WRITE

#### 第七节 java AIO编程

1. BIO

   ![image-20210715124203354](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210715124203354.png)

- 传统的java TCP通讯：Blocking I/O

2. NIO

   - Non-BlockingI/O

     -提供非阻塞等方式

     -避免I/O阻塞通讯效率过低

     -一个线程可以管理多个连接

     -减少线程多的压力

     -不是真异步

3. AIO

   - Asynchronous I/O,异步I/O 

   - JDK1.7引入,主要在 - Java nio包中

   - 异步I/O,采用回调方法进行处理读写操作

   - 主要类

     -Asynchronous Server Socket Channel服务器接受请求通道bind绑定在某一个端口 accept接受客户端请求

     -Asynchronous Socket Channel Socket通讯通道read读数据 write写数据

     -Completion Handler异步处理类completed操作完成后异步调用方法 failed操作失败后异步调用方法

4. 3种I/O的区别

|                       | BIO  | NIO    | AIO    |
| --------------------- | ---- | ------ | ------ |
| 阻塞方式              | 阻塞 | 非阻塞 | 非阻塞 |
| 同步方式              | 同步 | 同步   | 异步   |
| 编程难度              | 简单 | 较难   | 困难   |
| 客户机/服务器线程对比 | 1:1  | N：1   | N：1   |
| 性能                  | 低   | 高     | 高     |

#### 第八节 Netty编程

1. Netty

- Nettyhttp://netty.io

- 最早由韩国 Trustin Lee设计开发的

- 后来由Boss接手开发,现在是独立的 Netty Project

- 一个非阻塞的客户端-服务端网络通讯框架

- 基于异步事件驱动模型

- 简化Java的TCP和UDP编程

- 支持HTTP/2,SSL等多种协议

- 支持多种数据格式,如JSON等

- 关键技术

  ——诵道 Channel 

  ​	-ServerSocketChannel/NioServerSocketChannel/ 

  ​	-SocketChannel/ Nio SocketChannel

  ——事件 EventLoop

  ​	-为每个通道定义一个EventLoop,处理所有的I/O事件

  ​	-EventLoop注册事件

  ​	-EventLoop将事件派发给 ChannelHandler 

  ​	-EventLoop安排进一步操作

  ——事件

  ​	-事件按照数据流向进行分类

  ​	-入站事件:连接激活/数据读取/......

  ​	-出站事件:打开到远程连接/写数据/…

  ——事件处理 Channelhandler

  ​	-Channel通道发生数据或状态改变

  ​	-EventLoop会将事件分类,并调用 Channelhandler的回调函数程序员需要实

  ​	-Channelhandler内的回调函数ChannelInboundHandler/ChannelOutboundHandler

  ——Channelhandler工作模式:

  ​	-责任链责任链模式将

  ​		·请求的接收者连成一条链

  ​		·在链上传递请求,直到有一个接收者处理该请求

  ​		·避免请求者和接收者的耦合

  ​	-Channelhandler可以有多个,依次进行调用

  ​	-ChannelPipeline作为容器,承載多个 Channelhandler 

  ——ByteBuf

  ​	-强大的字节容器,提供丰富API进行操作

- Mina

  -ApacheMina,http://mina.apache.org 

  -NIO框架库

  -事件驱动的异步网络通讯

  -和Nett的区别

  ​	https://stackoverflow.com/questions/1637752/netty-vs-apache-

  ​	mina

#### 第九节 邮件基础知识

1. 邮件使用

   - 注册一个电子信箱帐号(唯一)

     -test@abc.com 

   - Web邮件管理界面

   - 邮件客户端软件( Outlook/ Foxmail等)

2. 邮件基本知识

   - 邮件:一封信,包括发件人/收件人/文本/图片/附件等

   - 邮件客户端

   - 邮件服务端

     -发送邮件服务器

     -接受邮件服务器

   - 邮件客户端

     -Foxmail 

     -OutLook(Express, Microsoft Outlook ）

     -Thunderbird(inux平台)

   - 邮件服务端

     -Microsoft Exchange Server 

     -IBM Lotus notes 

     -SendMail, Qmail, James

   - 主要协议(发送端口25,接收端口110）

     -发送,SM'TP, Simple mail transfer Protocol

     -接收,Pop3, Post office protocol3,(POP）

     -接收 IMAP, Internet Message Access Protocol, IMAP4

     ​	·摘要浏览

     ​	·选择下载附件

     ​	·多文件夹

     ​	·网络硬盘

   - 邮件格式

     -RFC822邮件格式:邮件头,文字邮件正文

     -MIMEMultiPurpose Internet Mail Extension)图片/音频/视频等等

   - 邮件编码

     -纯英文邮件,ASCⅡ编码,7Bit

     -8Bit编码

     -BASE64, 61bit, A-Za-z0-9+/ 

     -Quoted- printable对每个非ASCⅡ字符用"="加上这个字符的十六进制编码

   - 邮件中继:通过别人的邮件服务器(中继服务器)将你的邮件系统的邮件送到目标地址

   - 垃圾邮件（Spam)

   - 邮件和邮件服务器的安全

   - 邮件防火墙,垃圾邮件判定

   - 推荐材料

     -http://baike.baiducom/view/5450.htmi?tp=011

     -http://en.wikipediaorg/wiki/openmailrelay

#### 第十节 java Mail编程

1. Java Mail 服务器配置

   - 邮件服务器支持

     -需要在邮件服务内设置,可以查看相关邮件帮助

     -需要知道pop服务器和sm服务器信息

2. Java Mail 工具包

   - javax. mail包和 javax. mail.internet包

     -https://javaee.github.io/javamail目前1.6.2

     -mvn dependency

     ```XML
     <dependency>
     
     <groupId>com. sun. mail</groupId>
     
     kartifactId>javax. mail</artifactId>
     
     <version>1. 6.2</version>
     
     </dependency>
     ```

3. java Mail 核心 API

   - 关键类Session:邮件会话和 Httpsession不同

     -Store:邮件存储空间

     -Folder:邮件文件夹

     -Message:电子邮件

     -Address::邮件地址

     -Transport发送协议类

4. WORK1

   

```JAVA
    import java.net.ServerSocket;
    import java.net.Socket;
    import java.util.ArrayList;
    import java.util.List;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ThreadPoolExecutor;
    /**
     * 请编写一个群聊的程序，包括服务端程序和客户端程序。 
     * 服务端功能：收到某客户端的信息，将消息在控制台输出，然后，发给其他另外的客户端。
     * 客户端功能：每隔5秒发送一条信息给服务端。然后接收服务器转发过来的消息，并在控制台输出。
     * @author MSS
     *
     */
    public class ChatRoom {
       public static void main(String[] args) {
    	   //线程池
    	   ThreadPoolExecutor executor=(ThreadPoolExecutor)Executors.newFixedThreadPool(4);
    	   List<Socket> slist=new ArrayList<Socket>();
    	   int num=0;
    	   try { 
    		   ServerSocket ss=new ServerSocket(8001);
    		   while(true) {
    			   Socket s=ss.accept();
    			   slist.add(s);
    			   System.out.println("来了一个Client");
    			   executor.execute(new Worker(s,slist,num));
    			   num++;
    		   }
    	   }catch(Exception e) {
    		   e.printStackTrace();
    	   }
       }
    }

当有客户端接入时启动线程类 

    import java.io.BufferedReader;
    import java.io.DataOutputStream;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.OutputStream;
    import java.net.Socket;
    import java.util.List;
     
    class Worker implements Runnable{
        Socket s;
        List<Socket> slist;
        int num;
        
        public Worker(Socket s,List<Socket> slist,int num) {
        	this.s=s;
        	this.slist=slist;
            this.num=num;    	
        }
    	@Override
    	public void run() {
    		try {
    			System.out.println("服务人员已经启动");
    			InputStream ips=s.getInputStream();
    			BufferedReader br=new BufferedReader(new InputStreamReader(ips));
    			
    			
    			while(true) {
    				String strWord=br.readLine();
    				System.out.println("No."+num+" client said:"+strWord+":"+strWord.length());
    				if(strWord.equals("quit")) {
    					break;
    				}
    				if(strWord!=null) {
    				for(int i=0;i<slist.size();i++) {
    					Socket sc=slist.get(i);
    					OutputStream ops=sc.getOutputStream();
    					DataOutputStream dos=new DataOutputStream(ops);
    					dos.writeBytes("No."+num+" client said"+strWord+"---->"+System.getProperty("line.separator"));//向所有客户端发送消息
    				}
    				}	
    			}
    			br.close();
    			//关闭包装类，会自动关闭包装类的底层类。所以不用调用ips.close()
    			
    			s.close();
    		}catch(Exception e) {
    			e.printStackTrace();
    		}
    		
    	}
        
    }

客户端 

    import java.io.BufferedReader;
    import java.io.DataOutputStream;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.OutputStream;
    import java.net.InetAddress;
    import java.net.Socket;
     
    public class Client {
     
    	public static void main(String[] args) {
    		try {
    			Socket s=new Socket(InetAddress.getByName("127.0.0.1"),8001);//需要服务端先开启
    			
    			//同一个通道，服务端的输出流就是客户端的输入流，服务端的输入流就是客户端的输出流
    			
    			InputStream ips=s.getInputStream(); //开启通道的输入流
    			BufferedReader brNet=new BufferedReader(new InputStreamReader(ips));
    			
    			OutputStream ops=s.getOutputStream();//开启通道的输入流
    			
    			DataOutputStream dos=new DataOutputStream(ops);
    			
    			String msg="6666";
    			while(true) {
    				Thread.sleep(10000);
    			
    				dos.writeBytes(msg+System.getProperty("line.separator"));
    				System.out.println("Server said:"+brNet.readLine());
    			}
     
    		}catch(Exception e) {
    			e.printStackTrace();
    		}
     
    	}
     
    }

```

WORK2

- 服务端

- ```java
  import java.net.ServerSocket;
  import java.net.Socket;
  import java.util.ArrayList;
  import java.util.List;
  import java.util.concurrent.Executors;
  import java.util.concurrent.ThreadPoolExecutor;
  /**
   * 请编写一个群聊的程序，包括服务端程序和客户端程序。 
   * 服务端功能：收到某客户端的信息，将消息在控制台输出，然后，发给其他另外的客户端。
   * 客户端功能：每隔5秒发送一条信息给服务端。然后接收服务器转发过来的消息，并在控制台输出。
   * @author MSS
   *
   */
  public class ChatRoom {
     public static void main(String[] args) {
  	   //线程池
  	   ThreadPoolExecutor executor=(ThreadPoolExecutor)Executors.newFixedThreadPool(4);
  	   List<Socket> slist=new ArrayList<Socket>();
  	   int num=0;
  	   try { 
  		   ServerSocket ss=new ServerSocket(8001);
  		   while(true) {
  			   Socket s=ss.accept();
  			   slist.add(s);
  			   System.out.println("来了一个Client");
  			   executor.execute(new Worker(s,slist,num));
  			   num++;
  		   }
  	   }catch(Exception e) {
  		   e.printStackTrace();
  	   }
     }
  }
  
  ```

- 客户端

- ```java
  import java.io.BufferedReader;
  import java.io.DataOutputStream;
  import java.io.InputStream;
  import java.io.InputStreamReader;
  import java.io.OutputStream;
  import java.net.InetAddress;
  import java.net.Socket;
   
  public class Client {
   
  	public static void main(String[] args) {
  		try {
  			Socket s=new Socket(InetAddress.getByName("127.0.0.1"),8001);//需要服务端先开启
  			
  			//同一个通道，服务端的输出流就是客户端的输入流，服务端的输入流就是客户端的输出流
  			
  			InputStream ips=s.getInputStream(); //开启通道的输入流
  			BufferedReader brNet=new BufferedReader(new InputStreamReader(ips));
  			
  			OutputStream ops=s.getOutputStream();//开启通道的输入流
  			
  			DataOutputStream dos=new DataOutputStream(ops);
  			
  			String msg="6666";
  			while(true) {
  				Thread.sleep(10000);
  			
  				dos.writeBytes(msg+System.getProperty("line.separator"));
  				System.out.println("Server said:"+brNet.readLine());
  			}
   
  		}catch(Exception e) {
  			e.printStackTrace();
  		}
   
  	}
   
  }
  ————————————————
  
  ```

- 线程类

- ```java
  import java.io.BufferedReader;
  import java.io.DataOutputStream;
  import java.io.InputStream;
  import java.io.InputStreamReader;
  import java.io.OutputStream;
  import java.net.Socket;
  import java.util.List;
   
  class Worker implements Runnable{
      Socket s;
      List<Socket> slist;
      int num;
      
      public Worker(Socket s,List<Socket> slist,int num) {
      	this.s=s;
      	this.slist=slist;
          this.num=num;    	
      }
  	@Override
  	public void run() {
  		try {
  			System.out.println("服务人员已经启动");
  			InputStream ips=s.getInputStream();
  			BufferedReader br=new BufferedReader(new InputStreamReader(ips));
  			
  			
  			while(true) {
  				String strWord=br.readLine();
  				System.out.println("No."+num+" client said:"+strWord+":"+strWord.length());
  				if(strWord.equals("quit")) {
  					break;
  				}
  				if(strWord!=null) {
  				for(int i=0;i<slist.size();i++) {
  					Socket sc=slist.get(i);
  					OutputStream ops=sc.getOutputStream();
  					DataOutputStream dos=new DataOutputStream(ops);
  					dos.writeBytes("No."+num+" client said"+strWord+"---->"+System.getProperty("line.separator"));//向所有客户端发送消息
  				}
  				}	
  			}
  			br.close();
  			//关闭包装类，会自动关闭包装类的底层类。所以不用调用ips.close()
  			
  			s.close();
  		}catch(Exception e) {
  			e.printStackTrace();
  		}
  		
  	}
      
  }
  
  ```

  

