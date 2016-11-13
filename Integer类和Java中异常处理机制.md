---
##Integer类
java中的数据类型：
<pre>
1.基本数据类型：</br>
byte short int long float double char boolean</br>
2.基本数据类型对应的包装类：</br>
Byte Short Integer Long Float Double Character Boolean
</pre>

Integer:
<pre >
1.获取Int类型的最大最小值</br>
2.获取十进制整数对应的二进制、八进制、十六进制的字符串形式</br>
3.将字符串转为int类型
</pre>

      public class TestInteger
      {
        public static void main(String [] args)
        {
          int n = 123;
      String s = n + “”;

      String s2 = “123”;
      int n2 = Integer.parseInt(s2);
      System.out.println(n2 + 100);
      //Long.parseLong(s2);
      //Double.parseDouble(s2);
      //可以在API文档里查看
        }
      }


***
##java中异常及其处理机制
异常：程序在运行过程中发生由于硬件设备问题、软件设计错误等导致的程序异常事件。
<pre>
异常分类：</br>
1.运行时异常（非检测时异常）</br>
NullPointerException、IndexOUtOfBoundsException、AritheticException、ClassCastException、NumberFormatException</br>
2.非运行时异常（检测时异常）
</pre>


	public class TestRuntimeException
	{
  
<pre> 
当一个对象为Null时，使用对象，来调用该对象的属性或方法，则会出现NullPointerException，出现异常提示，Eclipse会把出现的
问题也看成一个对象java.lang.NullPointerException，看API发现它继承了RunTimeException这个类。Throwable表示可以抛出的
能力（接口 ），那既然子类实现了这个接口，就代表着所有的异常都是可抛出的。
</pre>

    String s1 = null;
    char ch = s1.charAt(0);
    System.out.println(ch);

    String s2 = “abc”;
    int n2 = Integer.parseInt(s2);
    System.out.println(n2);//NumberFormatException
    //程序发生异常（生成了一个NullPointerException的对象，并且抛出给JVM,JVM将我们的程序直接干掉，程序就直接结束了）

    int [] niArr = {1,2,3};
    System.out.println(niArr[3]);
    //ArrayIndexOutOfBoundsException使用了父类的名称作为自己的后半部分，程序写完的时候没有问题，只会在运行的时候出现异常。
    FileInputStream fis = new FileInputStrean(new File(“E:/a.txt));写完这句代码，编译器会直接提示错误。这时候就必须要做
    一些异常处理了，经过编译，才能正常运行的
    }

**运行时异常、非运行时异常的处理方式：**

    public static void main(String [] args)
    {
    String s1 = null;
    try//放可能会发生异常的代码，比如说下面的两行代码
    {
      char ch = s1.charAt(0);//向上抛出一个NullPointerException的对象
      System.out.println(ch);
    }
    catch(Exception e)//当try中抛出异常时，接受该异常，并处理，Exception e = new NullPointerException();让父类变量来接收
    这个子类对象，属于多态的一个知识点了。
    {
    e.printlnStackTrace();//打印异常的堆栈信息(处理)
    //当然也可以自己设置解决方案了
    //System.out.pritln(“s1为null了”);
    //try catch 相当于if else的特殊结构吧
    }
    System.out.println(“其他的代码”);
    }
    m1 m2 m3 m4 main();
    一般来讲，第一行的错误提示是最致命的

<pre>
但是呢，运行时异常的时候，一般不能用作实际里面，为什么呢，因为运行时异常在我们写代码的过程中，会出现的很频繁。通常会做一些处
理，让我们的程序看起来更加健壮。
</pre>

    public class TestNullPointException
    {
    public static void main(String [] args)
    {
      String s1 = null;
      if(s1 != null)
      {
        char ch = s1.charAt(0);//对于运行时异常，可以进行条件判断
      }

      //对于非运行异常（即检测时异常），必须进行异常的处理
        FileInputStream is = new FileInputStream(new File(E:/a.txt));
    }
    }    
    
<pre>        
好像是按一下ctrl+1，有两种解决方案，一个是直接加一个try catch，之后打印的堆栈信息，就可以看看了，然后找到自己对应的文
件。try-catch-finally：finally指肯定会执行的代码，一般做临时文件的处理或者资源的关闭，在finally也是可以加try-catch的。
那对于finally是怎么来理解呢？如果try了，发生异常了，则会执行catch，进行异常处理。并且会执行finally语句，但是呢，如果没
有发生异常，即使说try-catch没有执行，但finnally语句仍然会执行的。所以说一般是用作临时文件的处理或者是资源的关闭，就是说
不管你有没有异常，最后都要把我这个异常给关闭了。在当前学习的课程体系里面，要关闭的其实并不多，一个是IO流，一个是关于数据
库的部分。比如说，你要先连接一个数据库，然后进行数据操作，不管你操作成功还是操作失败，不管你在操作的过程中，有没有发生异
常，最后都是要把这个数据库给关闭的，否则别人就连接不上了。
</pre>
	
**另一个处理方案：**

    pubic class TestThrows
    {
    public static void main(String [] args)
    {
      m2(); //最后在main方法里面调用m2方法


    }

    //	在main方法外声明一个m1的方法
    public static void m1()
    { 
    try
    {
      FileInputStream is = new FileInputStream(new File(“E:/a.txt));
    }
    catch(FileNotFoundException e)
    {
      e.printStackTrace();	
    }
    }
    //再声明一个m2的方法，在m2的方法里面调用m1
    public static void m2()
    {
    m1();
    }

    }

**那我们也可以不用try catch来处理的：**

    pubic class TestThrows
    {
    public static void main(String [] args)
    {
      m2(); //最后在main方法里面调用m2方法


    }

    //	在main方法外声明一个m1的方法
    public static void m1() throws FileNotFoundException
    {
      FileInputStream is = new FileInputStream(new File(“E:/a.txt));//这时候这句代码就不会报错了，但是呢，m2的方法体就
      报错了。
    }
    //再声明一个m2的方法，在m2的方法里面调用m1
    public static void m2()
    {
      m1();
    }

    }
    //try-catch-finally是真正的处理异常，或者说是积极的处理异常。
  
<pre>
那么throws呢,是消极的处理异常，并没有真正的处理异常，而是将异常抛给了调用者，是JVM在程序编译的时候，不再报编译错误，谁
调，就抛给了谁，不会在编译的时候，就直接报错。然后在具体调用的时候，针对具体的调用再来处理，上面的代码就是将异常抛给了m2，
但是呢，如果m2也不想处理这个异常，则可以继续往上抛：
</pre>

    public static void m2() throws FileNotFoundException,这个就是抛给虚拟机了。实际情况就try-catch处理一下就可以了。
    public class TestThrows
    {
      public static void main(String [] args)
      {
        try
        {
          m2(); 
        }
        catch(FileNotFoundException e)
        {
          e.printStatckTrace();
        }
      }

      public static void m1() throws FileNotFoundException
      {
        FileInputStream is = new FileInputStream(new File(“E:/a.txt));

      }

      public static void m2() throws FileNotFoundException
      {
        m1();
      }

    }

<pre>
那么来分析一下FileInputStream is = new FileInputStream(new File(“E:/a.txt));
通过API来看一下FileInputStream，我们创建了一个这样的一个对象之后，之所以要抛出异常，是因为源代码是这样写的：
</pre>

`public FileInputStream(File file)`
`throws FileNotFoundException`

<pre>
是因为它本来就抛出了一个异常了，所以肯定要进行异常处理了，所以所直接创建了这样的一个对象后，编译的时候就肯定会报错的。
事实上对于m1方法而言，都是默认有一个的向虚拟机抛出的异常的。比如：
</pre>

    public static void m1()
    {
      String s1 = null;
      char ch = s1.charAt(0);
      System.out.println(ch); 
    }
    其实呢，是隐藏了一个
    public static void m1 throws FileNotFoundException
    
<pre>
默认的是向上（JVM）抛出了一个空指针异常。throws只是会让代码在编译的时候，不去报编译错误，而针对上面的异常时，是属于运行时异
常。本身就不存在编译异常这么一种情况，所以呢，throws FileNotFoundException就没有必要去写了。
所以呢，回到之前所说的FileInputStream的那个关于创建对象的有一点要说的，就是它抛出的不仅仅是FileNotFoundException，还有一
个是SecurityException，但是呢，没有写出来，这就意味着SecurityException异常是一个运行异常了。事实情况上，也是的确如此的，它
是有一个父类，叫做RunTimeException的。
</pre>

**关于catch和finallly的补充说明：**

    public class TestCatch
    {
      pubcic static void main(String [] args)
    {
        try
      {
      //下面的这些异常都是不同类型的异常了，我们看一下catch是怎么来接收的
        String s1 = null;
        char ch = s1.charAt(0);
        FileInputStream is = new FileInputStream(new File(“E:/a.txt”));
        String s2 = “abc”;
        int n2 = Integer.parseInt(s2);
      }
      //肯定不能只写NullPointerException e，因为这个会忽略掉其他没有被抓到的异常了，所以这时候，就要写很多个
      catch(NullPointerException e)
      {
        e.printStatckTrace();
      }
      catch(FileNotFoundException e)
      {
        e.printStackTrace();
      }
      catch(NumberFormatException)
      {
        e.printStatckTrace();
      }
    }
	  }
    
<pre>
那这个时候，这三个条件里是没有任何的关系的，这个时候，我如果把NullPointerException改成RunTimeException的话，
你要知道 RunTimeException是包含了NullPointerException和NumberFormatException的，之前说过了，异常也是类的一种，
这个是RunTimeException就相当于是一个父类了那这时候就可以直接用catch(父类)了。 
</pre>
	
**再来看一个例子：**

    public static void main(String [] args)
    {
      int n = m();
      System.out.println(n);//那么会输出多少
    //会得到3，为什么呢？是因为finally是无论如何都会执行的，finally类里的内容会抢先catch执行。
    }
    public static int m()
    {
      try
    {
      String s1 = null;
      char ch = s1.charAt(0);
      return 1;
    }
    catch(Exception e)
    {
      e.printStackTrace();
    //e.printStackTrace和抛给JVM的时候，它们的输出的信息，还是有一点不一样的。这个会少了Exception in main…自己打印的
    是没有的。

      return 2;
    }
    finally
    {
      return 3;
    }
    }
    
    
**上面讲的是关于多个catch情况的补充，以及finally的一些补充说明吧。**
