##                                                               										第一章 ：Maven

### 第一节——构建工具

#### 使用第三方库中现有函数的方法

1. 传统方法

- 搜索引擎搜索 Apache Comons Math

- 找到官网

- 确定下载版本和下载路径

- 下载到本地，找到里面的JAR文件

- 新建JAVA项目

- 将jar文件添加到Java Build Path

- 开始编码测试

- 优点：第三方库很强大，要学会在巨人的肩膀上工作

- 缺点：

  ​    ——搜索确定版本下载jar包工作量大且不易

  ​	——需要手动添加jar包

  ​	——代码拷贝到别人的机器需要同样的路径配置

2. Maven方法

- 创建Maven项目
- 在mvn中央仓库（mvnrepository.com)中搜索commons Math
- 将你需要调用的类的依赖文本加到项目pom.xml中
- 使用Apache Commons Math 类进行编码
- Maven编译和运行：右键项目->Run ai->Maven Build
- 程序运行

- Java构建工具构建工具功能

  ​	——自动帮程序员甄别和下载第三方库（jar）

  ​	——完成整个项目编译（调用javac.exe)

  ​	——完成项目单元测试流程（调用JUnit工具）——完成项目打包（jar/war等格式，调用jar.exe）

- 当前主要的Java构建工具

  ——Maven,Gradle,Ivy,Buildr,Ant等

### 第二节——Maven基础概念和实战

1. Maven基础概念

- Maven开发流程	

  ——新建Maven项目

  ——在中央仓库出招第三方jar的依赖文本

  ——拷贝依赖文本到项目的pom.xml

  ——执行maven build,编译/构建整个项目

- Maven是一个软件.

- Maven也有一个中心仓库

  ——包含很多第三方软件.可以有很多第三方的Maven仓库.

- Mave是一个构建工具动下载中心仓库的jar文件,存在本地进行管理，编译，测试，运行和打包发布Java项目

2. Maven编译工作流程

![image-20210705222915635](C:\Users\yjm\AppData\Roaming\Typora\typora-user-images\image-20210705222915635.png)

3. POM(Project Object Model)

- XML格式

- 把傲寒了项目信息、依赖信息、构建信息

- 构建信息（artifact)

  ——groupId：组织名

  ——artfactId：产品名称（项目名）

  ——version:版本

4. Maven reven repository(仓库）

- Maven仓库存放和管理各种构件

  ——本地仓库（本地用户的.m2文件夹）

  ——远程仓库

- 中央仓库

- 阿里云仓库

- 谷歌仓库

- ...

5. Maven项目的目录结构

- 基本目录结构

  ——src

  	#### main

  ​	-java/存放java文件

  ​	-resource/存放程序资源文件

  #### test

  -java/存放测试程序

  -resource/存放测试程序资源文件

  #### pom.xml

6. Maven构建生命周期

- 清理

- 编译

- 测试

- 打包

- 安装

- 部署

  

## HomeWork

### chinesetopinyin.java

```java
package chinesetopinyin;
import java.util.Scanner;
import net.sourceforge.pinyin4j.*;
import net.sourceforge.pinyin4j.format.HanyuPinyinOutputFormat;
import net.sourceforge.pinyin4j.format.HanyuPinyinToneType;
import net.sourceforge.pinyin4j.format.exception.BadHanyuPinyinOutputFormatCombination;
public class chinesetopinyin
{
         public static void main(String[] args)
         {       
                   Hanyu hanyu = new Hanyu();
                   Scanner sc = new Scanner(System.in);
                   String str = sc.next();
                   String strPinyin = hanyu.getStringPinYin(str);
                   System.out.println(strPinyin);
         }
}
class Hanyu
{
         private HanyuPinyinOutputFormat format = null;
         private String[] pinyin;        
         public Hanyu()
         {
                   format = new HanyuPinyinOutputFormat();
                   format.setToneType(HanyuPinyinToneType.WITHOUT_TONE);         
                   pinyin = null;
         }        
         //转换单个字符
         public String getCharacterPinYin(char c)
         {
                   try
                   {
                            pinyin = PinyinHelper.toHanyuPinyinStringArray(c, format);
                   }
                   catch(BadHanyuPinyinOutputFormatCombination e)
                   {
                            e.printStackTrace();
                   }                  
                   // 如果c不是汉字，toHanyuPinyinStringArray会返回null
                   if(pinyin == null) return null;                 
                   // 只取一个发音，如果是多音字，仅取第一个发音
                   return pinyin[0];   
         }      
         //转换一个字符串
         public String getStringPinYin(String str)
         {
                  StringBuilder sb = new StringBuilder();
                   String tempPinyin = null;
                   for(int i = 0; i < str.length(); ++i)
                   {
                            tempPinyin =getCharacterPinYin(str.charAt(i));
```



```java
                        if(tempPinyin == null)

                        {
                                 sb.append(str.charAt(i));
                        }
                        else
                        {
                                 sb.append(tempPinyin);
                        }
               }
               return sb.toString();
     }
```
}

### pom.xml

```maven
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>sjskkl</groupId>
  <artifactId>lkjknmm</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <!-- https://mvnrepository.com/artifact/com.belerweb/pinyin4j -->
   <dependencies> 
<dependency>
    <groupId>com.belerweb</groupId>
    <artifactId>pinyin4j</artifactId>
    <version>2.5.0</version>
</dependency>
  </dependencies> 
</project>
```

### 第一章作业笔记

1. pinyin4j基本用法：

通常情况下，只需要用到其中的PinyinHelper类中的静态方法toHanyuPinyinStringArray就可以了，比如：

```
String[] pinyinArray =PinyinHelper.toHanyuPinyinStringArray('单');

for(int i = 0; i < pinyinArray.length; ++i)

{

  System.out.println(pinyinArray[i]);

}
```

就会输出：

dan1

chan2

shan4

这三种发音，后面的数字代表第几声。可以看到静态方法toHanyuPinyinStringArray返回的数据类型是一个String数组，它用来接收一个汉字的多个发音，如果toHanyuPinyinStringArray中的参数不是汉字，那么它会返回null。

2. 格式支持

   ​		Pinyin4j支持拼音输出的格式化，比如，“黄”可以输出为“huang”、“huang2”、“huáng”等等，下面的代码就似是输出“huáng”的示例：

   ```java
   HanyuPinyinOutputFormat format= new HanyuPinyinOutputFormat();
   
   format.setToneType(HanyuPinyinToneType.WITH_TONE_MARK);
   
   format.setVCharType(HanyuPinyinVCharType.WITH_U_UNICODE);
                     
   
   String[] pinyinArray = null;
   
   try
   
   {
   
        pinyinArray = PinyinHelper.toHanyuPinyinStringArray('黄', format);
   
   }
   
   catch(BadHanyuPinyinOutputFormatCombination e)
   
   {
   
        e.printStackTrace();
   
   }
   
   for(int i = 0; i < pinyinArray.length; ++i)
   
   {
   
        System.out.println(pinyinArray[i]);
   
   }
   ```

   此外，还支持大小写转换、ü等等。
   