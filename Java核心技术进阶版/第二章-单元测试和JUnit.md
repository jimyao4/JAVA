## 											第二章-单元测试和JUnit

### 第一节-单元测试

1. 软件测试

- 软件测试的定义：在规定的条件下对程序进行操作，以发现程序错误衡量软件质量，并对其是否能满足设计要求进行评估的过程

- 软件测试分类

  ——单元vs集成测试

  ——白盒vs黑盒测试

  ——自动vs手动测试

  ——回归测试

  ——压力测试

2. 单元和集成测试

- 单元测试（unit testing），是指对软件中的最小可测试单元进行检查和验证，通常是一个函数/方法
- 单元测试是已知代码结构进行的测试，属于白盒测试.
- 集成测试是将多个单元相互作用，形成一个整体，对整体协调性进行测试。
- 一般从构成系统的最小单元开始，持续推进到单元之间的接口知道集成为一个完成的软件系统为止.

3. 白盒和黑盒测试

- 白盒测试，全面了解程序内部逻辑结构，对所有的逻辑路径都进行测试，一般由程序员完成.
- 黑盒测试，又名功能测试，将程序视为一个不能打开的黑盒子。在完全不考虑程序内部结构和内部特性的情况下，检查程序功能是否按照需求规格说明书的规定正常使用。一般由独立的使用者完成.

4. 自动和手动测试

- 自动测试：用测试程序批量反复测试功能程序，并自动检查功能程序输出结果是否满足预定的要求.
- 手动测试：手动执行程序，手动输入所需要的的参数，手动检查程序结果是否满足预定的要求.

5. 回归测试

- 回归测试：修改旧代码后，重新进行测试以确定修改买有引入新的错误或导致其他代码产生错误.
- 回归测试在整个软件测试过程中占有很大的比重.软件快速迭代开发过程中，新版本的连续发布使得回归测试进行的更加繁琐.

6. 测试策略

- 基于main函数的策略

  ——优点：简单.

  ——缺点：

  ​				-无法自动判断被测对象的行为是否符合预期.

  ​				-main方法需要添加大量的代码，这些代码在发布时也需要手动删除.

  ​				-分散了程序员在开发时的关注点.

- 基于自动化测试框架的策略

  ——初始化->输入测试数据执行被测代码->获取系统实际结果->比较结果是否一致->输出测试结论.

### 第二节 JuUnt

jUint简介

- JUint:一个java语言的单元测试框架

  -Kent Beck(极限编程）和Erich Gamma(设计模式）建立的.

  -是xUint家族中最成功的一个

  -大部分的Java IDE都集成了JUint作为单元测试工具.


### Homework

1. main

```java

public class JudgeYear {
public static boolean judge(int year)
{
	boolean result= false;

	if((year%4==0&&year%100!=0)||year%400==0) 
	{
		result=true;
	}
	if(year<0||year>10000)
	{
		result=false;
	}
	return result;
}
}

```



2. test

```java
import static org.junit.Assert.*;
import org.junit.Test;
public class JudgeTest {
	@Test
public void test()
{
	assertEquals(true,JudgeYear.judge(-100));
	assertEquals(true,JudgeYear.judge(20000));
	assertEquals(true,JudgeYear.judge(2020));
	assertEquals(true,JudgeYear.judge(2019));
	assertEquals(true,JudgeYear.judge(2000));
	assertEquals(true,JudgeYear.judge(1900));
}
}

```

