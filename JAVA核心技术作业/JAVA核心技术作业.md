### JAVA核心技术作业

- WORK02

  ![image-20210719143553118](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210719143553118.png)

![image-20210719143614846](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210719143614846.png)

- WORK03

- ```java
  import java.util.Scanner;
  public class test3_2 {
  
  	public static void main(String[] args) {//此程序可输出任意奇数层星塔；
  		Scanner input=new Scanner(System.in);
  		int n= input.nextInt();
  		int k,m;
  		if(n%2==0)
  			m=n/2;
  		else
  			m=n/2+1;
  			for(int i=1;i<=n;i++)
  			{
  				k=2*i-1;
  				if(i>m)
  				{
  					k=2*(n-i+1)-1;
  				}
  				for(int j=1;j<=(n-k)/2;j++)
  				{
  					System.out.print(" ");
  				}
  				for(int s=1;s<=k;s++)
  				{
  					System.out.print("*");
  					if(s==n)
  						System.out.print("\n");
  				}
  				for(int j=1;j<=(n-k)/2;j++)
  				{
  					System.out.print(" ");
  					if(j==(n-k)/2)
  					{
  						System.out.print("\n");
  					}
  				}
  			}
  		}
  	}
  
  
  ```

  

- WORK04

- ```JAVA
  import java.util.Scanner;
  public class Main
  
  {
  
  	public static void main(String[] args)
  
  	{
  
  		//创建Scanner对象
  
  		//System.in表示标准化输入，也就是键盘输入
  
                  Scanner sc = new Scanner(System.in);
  
                  //利用hasNextXXX()判断是否还有下一输入项
  
                  int a = 0;
  
                  int b = 0;
  
                  int c = 0;
  
                  if (sc.hasNext()) {
  
                      a = sc.nextInt();
  
                  }
  
                  if (sc.hasNext()) {
  
                      b = sc.nextInt();
  
                  }
  
                  if (sc.hasNext()) {
  
                      c = sc.nextInt();
  
                  }
  
                  if(a==0 || b==0 || c==0)
  
                  {
  
          	    System.out.println("输入不能为0");
  
          	    System.exit(-1);
  
                  }
  
          
  
                  MyNumber obj1, obj2, obj3;
                  obj1= new MyNumber();
                  obj2= new MyNumber();
                  obj3= new MyNumber();
                  obj1.num=a;
                  obj2.num=b;
                  obj3.num=c;
                  swap(obj1,obj2);
                  swap(obj1,obj3);
                  swap(obj2,obj3);
                  System.out.printf("%d %d %d",obj1.num,obj2.num,obj3.num);
  
  	}
  
  	
  
  	public static void swap(MyNumber m, MyNumber n)
  
  	{
  
  		if(m.num > n.num)
  
  		{
  
  			int s = m.num;
  
  			m.num = n.num;
  
  			n.num = s;
  
  		}
  
  	}
  
  }
  
  
  class MyNumber
  
  {
  
  	int num;
  
  }
  ```

  

- WORK07

```

```

- WORK08

  ```java
  import java.util.Scanner;
  public class JudgeIDNumber {
  
  	
  
  	public static void main(String[] args) {
  		Scanner input = new Scanner(System.in);
  		System.out.println("Please input the ID number!");
  		String IdNumber=input.next();
  		char c=IdNumber.charAt(17);
  		int j=1;
  		if(IdNumber.length()!=18)
  		{
  			j=0;
  		}
  		else
  		{
  			if(Character.isAlphabetic(c)||Character.isDigit(c))
  			{
  		    for(int i=IdNumber.length()-1;--i>=0;){
  		        int chr=IdNumber.charAt(i);
  		        if(chr<48 || chr>57) 
  		        {
  		        	j=0;
  		        }
  		       }
  	        }
  			else j=0;
  		}
  		if(j==0)
  		{
  			System.out.println("0000-00-00");
  		}
  		else
  		{
  			String y= IdNumber.substring(6,10);
  			String m= IdNumber.substring(10,12);
  			String d= IdNumber.substring(12,14);
  			System.out.print("生日:");
  			System.out.print(y+"-"+m+"-"+d);
  		}
  		int[] x= {0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0};
  		if(j!=0) {
  		for(int i=0;i<17;i++)
  		{
  			x[i]=IdNumber.charAt(i)-'0';
  		}
  		int y=(x[0]*7+x[1]*9+x[2]*10+x[3]*5+x[4]*8+x[5]*4+x[6]*2+x[7]*1+x[8]*6+x[9]*3+x[10]*7+x[11]*9+x[12]*10+x[13]*5+x[14]*8+x[15]*4+x[16]*2)%11;
  
  		char[] s= {'1','0','x','9','8','7','6','5','4','3','2'};
  		System.out.print("校验码为:"+s[y]);
  }
  }
  }
  ```

  

- WORK10

  ```JAVA
  package cn;
  import java.util.Arrays;
  import java.util.Scanner;
  class Currency {
  	private String name;        //货币名称
  	private int originalValue;  //原始值
  	private int value;          //转换为人民币后的值
  	public static String[] CURRENCY_NAME = { "CNY", "HKD", "USD", "EUR" };
  	public static int[] CURRENCY_RATIO = { 100, 118, 15, 13 };
  	public String getName() {
  		return name;
  	}
  	public void setName(String name) {
  		this.name = name;
  	}
  	public int getOriginalValue() {
  		return originalValue;
  	}
  	public void setOriginalValue(int originalValue) {
  		this.originalValue = originalValue;
  	}
  	public int getValue() {
  		return value;
  	}
  	public void setValue(int value) {
  		this.value = value;
  	}
  }
  class HKD extends Currency implements Comparable<Currency> {
  	HKD(int n)
  	{
  		setName(CURRENCY_NAME[1]);
  		setOriginalValue(n);
  		setValue(n/CURRENCY_RATIO[1]*CURRENCY_RATIO[0]);
  	};
  	public int compareTo(Currency o)
  	{
  		int a=o.getValue();
  		int b=this.getValue();
  		return a-b;
  	}
  
  }
  class USD extends Currency implements Comparable<Currency> {
  	USD(int n)
  	{
  		setName(CURRENCY_NAME[2]);
  		setOriginalValue(n);
  		setValue(n/CURRENCY_RATIO[2]*CURRENCY_RATIO[0]);
  	}
  	public int compareTo(Currency o)
  	{
  		int a=o.getValue();
  		int b=this.getValue();
  		return a-b;
  	}
  }
  class EUR extends Currency implements Comparable<Currency>{
  	EUR(int n)
  	{
  		setName(CURRENCY_NAME[3]);
  		setOriginalValue(n);
  		setValue(n/CURRENCY_RATIO[3]*CURRENCY_RATIO[0]);
  	}
  	public int compareTo(Currency o)
  	{
  		int a=o.getValue();
  		int b=this.getValue();
  		return a-b;
  	}
  }
  public class Money {
  		public static void main(String[] args) {
  			Currency[] cs = new Currency[3];
  			Scanner sc = new Scanner(System.in);
  	                int a = 0;
  	                int b = 0;
  	                int c = 0;
  	                if (sc.hasNext()) {
  	                    a = sc.nextInt();
  	                    cs[0] = new HKD(a);
  	                }
                      if (sc.hasNext()) {
  	                    b = sc.nextInt();
  	                    cs[1] = new USD(b);
  	                }
  	                if (sc.hasNext()) {
  
  	                    c = sc.nextInt();
  
  	                    cs[2] = new EUR(c);
  	                }
                 Arrays.sort(cs);
                 for (Currency currency : cs) {
           		System.out.println(currency.getName()+currency.getOriginalValue());
                 }
  		}
  }
  
  
  ```

- WORK11

  ```java
  import java.io.BufferedReader;
  import java.io.BufferedWriter;
  import java.io.FileInputStream;
  import java.io.FileOutputStream;
  import java.io.InputStreamReader;
  import java.io.OutputStreamWriter;
  import java.util.ArrayList;
  import java.util.Collections;
  import java.util.Comparator;
  import java.util.HashMap;
  import java.util.Iterator;
  import java.util.List;
  import java.util.Map;
  import java.util.regex.Matcher;
  import java.util.regex.Pattern;
  class MyComparator implements Comparator<Map.Entry<String,Integer>>{
      public int compare(HashMap.Entry<String,Integer> he1,HashMap.Entry<String,Integer> he2) {
          return he2.getValue()-he1.getValue();
      }
  }
  
  public class Test11 {
      static final int MAX = 50;
  
      public static void main(String[] args) {
          // TODO Auto-generated method stub
          HashMap<String, Integer> hm = new HashMap<String,Integer>();
          
          //文件读取
          try(BufferedReader br=new BufferedReader(new InputStreamReader(new FileInputStream("D:/a.txt")))){
              String line;
              while((line = br.readLine())!=null) {
                  Pattern p = Pattern.compile("\\s+");//正则匹配空格
                  String words[]= p.split(line);//获取的字符串进行分割单词
                  
                  for(String item : words) {
                      if(item.length()!=0) {
                          if(hm.get(item)==null)
                              hm.put(item, 1);//将数据放入map中
                          else
                              hm.put(item, hm.get(item)+1);
                      }
                  }
              }
          }catch(Exception e) {
              System.err.println(e.getMessage());
          }
          
          //HashMap转换为list，进行排序
          List<Map.Entry<String,Integer>> list = new ArrayList<Map.Entry<String,Integer>>(hm.entrySet());
          Collections.sort(list,new MyComparator());
          
          //将数据写入文件
          try(BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(new FileOutputStream("D:/b.txt")))){
              for(Map.Entry<String, Integer> item: list) {
                  bw.write(item.getKey()+","+item.getValue());
                  bw.newLine();
              }
          }catch(Exception e) {
              System.err.println(e.getMessage());
          }
          
      }
  
  }
  ```

- FinalTest

  ```java
  import java.util.Arrays;
  import java.util.Scanner;
  class Animal {    
      int age;//动物年龄
      int mage; //映射到人的年龄
      String name; //名字
      static int[] dog = {0,18,23,28,32,36,40,45,50,55,60};
      static int[] cat= {0,15,24,28,32,36,40,44,48,52,56};
  } 
  class Dog extends Animal implements Comparable<Animal>{
      Dog(String name,int age)
      {
      	this.age=age;
      	this.mage=dog[age+1];
      	this.name=name;
      }
      public int compareTo(Animal o)
      {
      	return this.mage-o.mage;
      }
  }
  class Cat extends Animal implements Comparable<Animal>{
     Cat(String name,int age)
     {
  	   this.age=age;
     	this.mage=cat[age+1];
     	this.name=name;
     }
     public int compareTo(Animal o)
     {
     	return this.mage-o.mage;
     }
  }
  public class CompareAnimal {
  	public static void main(String[] args) {
  		Animal[] as = new Animal[4];
  		// 初始化
  		Scanner sc = new Scanner(System.in);
  		// 利用hasNextXXX()判断是否还有下一输入项
  		if (sc.hasNext()) {
  			as[0] = new Dog("dog1", sc.nextInt());
  		}
  		if (sc.hasNext()) {
  			as[1] = new Cat("cat1", sc.nextInt());
  		}
  		if (sc.hasNext()) {
  			as[2] = new Dog("dog2", sc.nextInt());
  		}
  		if (sc.hasNext()) {
  			as[3] = new Cat("cat2", sc.nextInt());
  		}
          Arrays.sort(as);
          for(int i=0;i<4;i++)
          {
          	System.out.println(as[i].name+","+as[i].age);
          }
  	}
  
  }
  
  
  
  ```

  