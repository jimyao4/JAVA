###  																		第八章-Java混合编程

#### 第一节 Java调用Java程序（RMI)

1. Java混合编程

   - 众多编程语言,各有各的特点和应用范围

     -https://www.tiobe.com/tiobe-index/

   - 现实世界存在很多应用程序

     -由不同编程语言实现

     -分布式部署的

   -  Java混合编程

     -Java程序和其他应用程序进行通讯和数据交互

     -Java和Java/C/js/ Python/ Web Service/命令行的混合编程                                

2. RMI

   - 回顾下学习Java程序过程

     -在main函数里面完成所有功能

     -基于函数/方法将功能拆开,采用函数相互调用

     -类对象/继承/多态

     -A a=newA（）;a.f1();//完成某一个功能

   - 单虚拟机M上的程序运行

     -启动一个main程序,然后重复以下的2个步骤

     - new出一个对象
     - 调用对象的某一个方法

   - 多虚拟机VM的程序运行

     -启动多个main程序,这些程序可以部署在多个机器/虚拟机上

     -多个进程可通过网络互相传递消息进行协作

     -进程通过RM可调用另一个机器的aa的函数

   - RMI: Remote Method Invocation远程方法调用两个位于不同M虚拟机的aa程序互相请求访问

![image-20210718121633562](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210718121633562.png)



#### 第二节 Java调用C程序

1. JNI

   - Java和C互操作

     -JNI, Java Native Interface

     -Java和本地C代码进行互操作

     -Java调用C程序完成一些需要快速计算的功能(常见,重点

     -C调用ava程序(基于反射的方法)

![image-20210718130023431](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210718130023431.png)

- 在Java类中声明一个本地方法

- 调用 javac. exe编译,得到 hellonative.class, 

- 调用 javah.exe得到包含该方法(Java_HelloNative_greeting的头文件(HelloNative.h)

- 实现c文件(对应 HelloNative.h)

- 将c和文件,整合为共享库(DLL)文件

- 在Java类中,加载相应的共享库文件

- | Java类型 | C类型    | 字节 | Java类型 | C类型   |
  | -------- | -------- | ---- | -------- | ------- |
  | boolean  | jboolean | 1    | int      | jint    |
  | byte     | jbyte    | 1    | long     | jlong   |
  | char     | jchar    | 2    | float    | jfloat  |
  | short    | jshort   | 2    | double   | jdouble |

  

#### 第三节 Java调用Java

1. JavaScript

   - JavaScript语言,又称JS语言

     -1995年由 Netscape网景公司发布

     -脚本语言(解释型语言）

     - 便于快速变更,可以修改运行时的程序行为
     - 支持程序用户的定制化

     -可用于Web前端和后端开发(全栈）

     -JS基本教程,htp://w.w3 schoolcom cn/basp

2. Java调用JS

   - 脚本引擎, ScriptEngine

     -Nashorn,JDK8自带的S解释器DK6/7是 Rhino解释器)Scriptengine engine=new 

     -ScriptEngineManagero-getEngine ByName (" nashorn")

   - 主要方法eval,执行一段js脚本.eval( String str),eval( Reader reader)
   
     -put,设置一个变量
     
     -get,获取一个变量
     
     -create bindings,创建一个 Bindings 
     
     -setBindings,设置脚本变量使用的范围

#### 第四节 Java调用Python

1. Python

   - Python语言

     -1989年由 Guido van rossun设计发明

     -解释型脚本语言

     -可用于科学计算软件/Web/桌面软件开发

     -目前版本3

2. Jython

   - Jython(曾用名 JPython)

     -Jython是 Python语言在Java平台的实现

     -Jython是在VM上实现的 Python,由java编写

     -Jython将 Python源码编译成JVM字节码,由VM执行对应的字节码,因此能很好的与VM集成. Jython并不是Java和 Python的连接器.

     -http://www.jython.org当前版本2.7

   - 关键类

     -PythonInterpreter 

     - exec执行语句

     - set设置变量值

     - get获取变量值

     - execfile执行一个 python文件

       -PyObject 

       -PyFunction

#### 第五节 Java调用Web service

1. Web Service

   - Web service

     -由万维网联盟W3C, World wide Web Consortiun)提出

     -消除语言差异、平台差异、协议差异和数据结构差异,成为不同构件模型和异构系统之间的集成技术

     -Web Service是为实现跨网络操作而设计的软件系统提供了相关的操作接口,其他应用可以使用SOAP消息,以预先指定的方式来与 Web service进行交互.

   - ·服务提供者

   - 服务注册中心

   - 服务请求者

![image-20210718235118566](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210718235118566.png)

2. Java调用 Web Service

   - Java提供 reimport工具

     -%JAVA_HOME%\bn目录下

     -根据wsdl文档,自动产生客户端中间代码

     -wsimport-keep-verbose 

     http://ws.webxml. com. cn/WebServices/MobileCodeWS.asmx? WSDL

| 参数    | 说明                                  | 参数      | 说明                             |
| ------- | ------------------------------------- | --------- | -------------------------------- |
| p       | 定义生成包名称                        | s         | 指定客户端执行类的源文件存放目录 |
| d       | 指定客户端执行类的class文件的存放目录 | keep      | 表示生成客户端执行类的源代码     |
| verbose | 正在执行操作的信息                    | extension | 使用拓展来支持SOAP1.2            |

- Java调用Web Servise

  -调用 wsimport所产生客户端中间代码

  -提供相应参数

  -获取返回结果

- Java调用 Web service其他办法

  -Axis/Axis2(axis. apache. org)
  -采用 URLConnection访问 Web Service

  -采用 Httpclient访问 Web service

#### 第六节Java调用命令行

1. 命令行

   - 很多程序没有源码,但是可以执行

     -命令行的执行方式

     -可以带输入参数,可以有输出结果

2. Runtime

   - Java提供 Runtime类

     exec以一个独立进程执行命令 command,并返回 Process句柄

     当独立进程启动后,需要处理该进程的输出流/错误流

     - 调用 Process. getInputStream可以获取进程的输出流
     - 调用 Process. get ErrorStream可以获取进程的错误输出流

     -调用 Process. waitFor等待目标进程的终止(当前进程阻塞)

#### WORK

```JAVA
    import java.rmi.Naming;
    import java.rmi.registry.LocateRegistry;
     

    public class WarehouseServer {
     
    	public static void main(String[] args) throws Exception {
    		System.out.println("产生服务器对象");
    		WarehouseImpl centralWarehouse=new WarehouseImpl();
    		
    		System.out.println("将服务器对象绑定在8001端口，对外提供服务");
    		LocateRegistry.createRegistry(8001);//定义端口
    		Naming.rebind("rmi://127.0.0.1:8001/warehouse1", centralWarehouse);
    		System.out.println("等待客户端");
    		
    	}
     
    }

Remote接口和实现类：

    import java.rmi.Remote;
    import java.rmi.RemoteException;
    import java.util.List;
     
    public interface Warehouse extends Remote{
        List<String> cmdExec(String cmd)throws RemoteException;
    }

    import java.io.BufferedReader;
    import java.io.File;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.rmi.RemoteException;
    import java.rmi.server.UnicastRemoteObject;
    import java.util.ArrayList;
    import java.util.List;
     
    public class WarehouseImpl extends UnicastRemoteObject implements Warehouse{
        String cmd1="javac HelloWorld";
        String cmd2="java HelloWorld";
    	protected WarehouseImpl() throws RemoteException {
    		super();
    		
    	}
     
    	@Override
    	public List<String> cmdExec(String cmd) throws RemoteException {
    		List<String> result=new ArrayList<String>();
    		if(cmd1.equals(cmd)) {
    			Process p;
    			String[] cmds=new String[2];
    			cmds[0]="javac";
    			cmds[1]="D:/temp/HelloWord.java";
    			
    			try {
    				//执行命令
    				p=Runtime.getRuntime().exec(cmds);
    				//取得命令结果的输出流
    				InputStream fis=p.getInputStream();
    				//用一个读输出流去读
    				InputStreamReader isr=new InputStreamReader(fis);
    				//用缓冲器读行
    				BufferedReader br=new BufferedReader(isr);
    				String line=null;
    				//直到读完为止
    				while((line=br.readLine())!=null) {
    					result.add(line);
    				}
    				System.out.println("");
    				int exitVal=p.waitFor(); //获取进程最后返回状态
    				System.out.println("Process exitValue: "+exitVal);
    			}catch(Exception e) {
    				e.printStackTrace();
    			}
    			result.add("编译成功");
    			return result;
    		}else if(cmd2.equals(cmd)){
    			Process p;
    			String[] cmds=new String[2];
    			cmds[0]="java";
    			cmds[1]="HelloWorld";
    			
    			try {
    				//执行命令
    				p=Runtime.getRuntime().exec(cmds,null,new File("D:/temp"));
    				//取得命令结果的输出流
    				InputStream fis=p.getInputStream();
    				//用一个读输出流去读
    				InputStreamReader isr=new InputStreamReader(fis);
    				//用缓冲器读行
    				BufferedReader br=new BufferedReader(isr);
    				String line=null;
    				//直到读完为止
    				while((line=br.readLine())!=null) {
    					result.add(line);
    					System.out.println(line);
    				}
    				System.out.println("");
    				int exitVal=p.waitFor(); //获取进程最后返回状态
    				System.out.println("Process exitValue: "+exitVal);
    			}catch(Exception e) {
    				e.printStackTrace();
    			}
    			result.add("执行成功");
    			return result;
     
    		}else {
    			Process p;
    			
    			
    			try {
    				//执行命令
    				p=Runtime.getRuntime().exec(cmd);
    				//取得命令结果的输出流
    				InputStream fis=p.getInputStream();
    				//用一个读输出流去读
    				InputStreamReader isr=new InputStreamReader(fis);
    				//用缓冲器读行
    				BufferedReader br=new BufferedReader(isr);
    				String line=null;
    				//直到读完为止
    				while((line=br.readLine())!=null) {
    					result.add(line);
    				}
    				System.out.println("");
    				int exitVal=p.waitFor(); //获取进程最后返回状态
    				System.out.println("Process exitValue: "+exitVal);
    			}catch(Exception e) {
    				e.printStackTrace();
    			}
    			return result;
    		}
    		
    	}
     
    }

客户端代码：

    import java.rmi.RemoteException;
    import java.util.Arrays;
    import java.util.Enumeration;
    import java.util.List;
    import java.util.Scanner;
     
    import javax.naming.Context;
    import javax.naming.InitialContext;
    import javax.naming.NameClassPair;
    import javax.naming.NamingException;
     

    public class WarehouseClient {
     
    	public static void main(String[] args)throws NamingException,RemoteException{
    		Context namingContext=new InitialContext();
            
    		//开始查找RMI注册表上有哪些绑定的服务
    		System.out.print("RMI 注册表绑定列表：");
    		Enumeration<NameClassPair>e=namingContext.list("rmi://127.0.0.1:8001/");
    		while(e.hasMoreElements()) {
    			System.out.println(e.nextElement().getName());
    		}
    		//获取某一地址上的服务类
    		String url="rmi://127.0.0.1:8001/warehouse1";
    		Warehouse centralWarehouse=(Warehouse) namingContext.lookup(url);
    		
    		Scanner in=new Scanner(System.in);
    		System.out.println("Enter keywords:");
    		String kewords=in.nextLine();
    		List<String> result=centralWarehouse.cmdExec(kewords);
    		for(String res:result) {
    			System.out.println(res);
    		}
    		in.close();
    		
    	}
     
    }

```

