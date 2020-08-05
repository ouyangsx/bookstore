javaSE二

<!-- toc -->

### 面向对象OOP

#### 面向对象的高级特性

##### 包装类和字符串

###### 包装类

1. Java是面向对象的语言，但是不纯，它仍然保留C语言的八种基本数据类型，除了八种基本数据类型之外，都是引用数据类型，所以，后面涉及到的集合、泛型、...设计只针对引用数据类型，不允许基本数据类型的数据参与，为了八种基本数据类型也能和后面的技术融合为一体，Java想了一个办法，为八种基本数据类型设计了对应的包装类；

   byte-->Byte；

   short-->Short；

   int-->Integer；

   long-->Long；

   float-->Float；

   double-->Double；

   char-->Character；

   boolean-->Boolean；

2. 在jdk1.5之前，基本数据类型与包装类之间需要手动进行转换，之后的版本支持自动转换；

   + 装箱：基本数据类型-->包装类对象；目的是某些地方不支持基本数据类型，只支持引用数据类型；

     + 手动：
     + 自动：

   + 拆箱：包装类对象-->基本数据类型；目的是运算方便；

     + 手动：
     + 自动：

     ```java
     import org.junit.Test;
     
     public class TestWrapper {
         @Test
         public void test(){
             int a = 10;
             //手动装箱
             Integer in = new Integer(a);
             System.out.println(in);
             //手动装箱
             Integer of = Integer.valueOf(a);
             System.out.println(of);
         }
     
         @Test
         public void test1(){
             int a = 10;
             //自动装箱
             Integer in =a;
             System.out.println("in=" + in);
     
             //先自动装箱成Integer的对象，后向上转型成Object
             Object obj = a;
             System.out.println("obj=" + obj);
         }
     
         @Test
         public void test3(){
             Integer in = new Integer(20);
             //手动拆箱
             int num = in.intValue();
         }
     
         @Test
         public void test4(){
             Integer in = new Integer(20);
             //自动拆箱
             int num = in;
         }
     }
     ```

   数据类型转换：

   + 基本数据类型转换：自动类型转换与强制转换；
   + 引用数据类型转换：向上转型与向下转型；
   + 基本数据类型与包装类之间：装箱与拆箱；

3. 基本数据类型与字符串的转换：

   + 基本数据类型-->字符串：
   + 字符串-->基本数据类型：可以借助包装类的方法；

   ```java
   import org.junit.Test;
   
   /*
   基本数据类型与字符串之间的转换：
    */
   public class TestWrapperAPI {
       public static void main(String[] args) {
           for (int i = 0;i < args.length;i++){
               System.out.println(args[i]);
           }
   
           int a = 10;
           //基本数据类型-->字符串
           String str = a + "";
           String str2 = String.valueOf(a);
   
           //字符串-->基本数据类型
           int num1 = Integer.parseInt(args[0]);
           int num2 = Integer.parseInt(args[1]);
           System.out.println(num1 + num2);
   
           double num3 = Double.parseDouble(args[3]);
           double num4 = Double.parseDouble(args[4]);
           System.out.println(num3 + num4);
       }
   }
   ```

4. 包装类的作用：

   + 数据类型的范围：
     + Float和Double中还有正无穷大POSITIVE_INFINITY、负无穷大NEGATIVE_INFINITY，还有NaN，是Not a Number的缩写。NaN 用于处理计算中出现的错误情况，比如 0.0 除以 0.0 或者求负数的平方根。程序员可以利用这种定制的 NaN 值中的特定位模式来表达某些诊断信息。
   + 数据类型的转换：
     + 见上基本数据类型与字符串的转化；

5. 包装类的其他方法：

   + Integer类型：
     + public static String toBinaryString(int i) //把十进制转成二进制
     + public static String toHexString(int i)   //把十进制转成十六进制
     + public static String toOctalString(int i)  //把十进制转成八进制
   + Character类型：
     + public static char toUpperCase(char ch) //转成大写字母
     + public static char toLowerCase(char ch) //转成小写字母
   + equals：
     + 按照包装的基本数据类型的值比较；
   + comparaTo：
     + 按照包装的基本数据类型的值比较；

6. 缓存问题：

   我们在编程时大量需要值在-128到127范围之间的Integer对象。如果只能通过new来创建，需要在堆中开辟大量值一样的Integer对象。这是相当不划算的，IntegerCache.cache很好的起到了缓存的作用。

   ​	缓存

   ​	byte Byte -128–127

   ​	short Short -128–127

   ​	int Integer -128—127

   ​	long Long -128—127

   ​	float Float 不缓存

   ​	double Double 不缓存

   ​	char Character 0–127

   ​	boolean Boolean TURE，FALSE

###### String类型

1. String类概述：

   + java.lang.String：字符串对象；
     + 是引用数据类型；
     + 任何在程序种出现的“xxxx”都是String类的对象；
     + 字符串是常量，他们的值在创建之后不能修改==>所有对字符串的更改，都会产生新的对象；
     + 因为String对象是不可变的，所以可以共享==>字符串常量对象是共享的，存储在字符串常量池中；
     + String底层是用什么存储的：
       + jdk1.9之前：字符数组存储；
         + "hello"-->{'h','e','l','l','o'}
       + jdk1.9之后：字节数组存储；
   + 字符串常量池在哪里？
     + jdk1.6及之前：字符串常量池在方法区；
     + jdk1.7：字符串常量池在堆中；
     + jdk1.8：字符串常量池在元空间

   ```java
   import org.junit.Test;
   
   public class TestString {
       @Test
       public void test1(){
           //str是一个对象，因为字符串太频繁了，所以Java简化了它的对象创建；
           String str = "hello";
           String string = new String("world");
       }
   
       @Test
       public void test2(){
           String str = "";//空字符串对象
           String str2 = "2";
       }
   
       @Test
       public void test3(){
           //这里面有3个对象：hello,world,helloworld
           String str = "hello";
           str = str + "world";
       }
   
       @Test
       public void test4(){
           String s1 = "hello";
           String s2 = "hello";
   
           System.out.println(s1 == s2);//true
   
           String s3 = new String("hello");
           String s4 = new String("hello");
   
           System.out.println(s3 == s4);//false
           System.out.println(s1 == s3);//false
       }
   }
   ```

2. String的对象与比较：

   ![String的对象1](images/grammar/String的对象1.png)

   ![String的对象2](images/grammar/String的对象2.png)

   + 常量池+常量池一定在常量池中，常量池是共享的；

   + “+”左右两边只要有一个不是常量池中的对象进行拼接，结果一定在堆中，堆中不是共享的；

     ```java
     import org.junit.Test;
     
     import java.util.Scanner;
     
     public class TestStringInstance {
         @Test
         public void test1(){
             String str1 = "hello";
             String str2 = "hello";
             System.out.println(str1 == str2);//true
         }
     
         @Test
         public void test2() {
             String str1 = new String("hello");
             String str2 = new String("hello");
             System.out.println(str1 == str2);//false
         }
     
         @Test
         public void test3(){
             String str1 = new String("hello");
             String str2 = new String("hello");
     
             //问有几个对象?
             //3个
         }
     
         @Test
         public void test4(){
             String str1 = "hello";//常量池
             String str2 = "world";//常量池
             String str3 = "helloworld";//常量池
     
             String str4 = "hello" + "world";//常量 + 常量，结果还在常量池
             String str5 = str1 + "world";//str1是变量，变量+常量，结果在堆中
             String str6 = "hello" + str2;//常量+变量，结果在堆中
     
             System.out.println(str3 == str4);//true
             System.out.println(str3 == str5);//false
             System.out.println(str3 == str6);//false
     
             final String str7 = "hello";
             final String str8 = "world";
             String str9 = str7 + str8;//常量+常量，结果在常量池
             System.out.println(str3 == str9);//true
     
             final String str10 = new String("hello");
             final String str11 = new String("world");
             String str12 = str10 + str11;//堆中常量+堆中常量，结果在堆中
             System.out.println(str3 == str12);//false
         }
     
         @Test
         public void test5(){
             String str1 = "hello";
             String str2 = "world";
             String str3 = "helloworld";
     
             String str4 = str1 + str2;
             System.out.println(str3 == str4);//false
     
             String str5 = (str1 + str2).intern();//intern():把结果存储到常量池中
             System.out.println(str3 == str5);//true
         }
     
         @Test
         public void test6(){
             Scanner sc = new Scanner(System.in);
             System.out.println("用户名:");
             String user = sc.next();
     
             System.out.println("密码：");
             String password = sc.next();
     
             //假设用户名是admin,用户名是123
             //如果用户名密码正确，打印登录成功，否则登录失败
             if ("admin".equals(user) && "123".equals(password)){
                 System.out.println("登录成功");
             } else{
                 System.out.println("登录失败");
             }
         }
     }
     ```

3. String的API方法：

   + char charAt(index)：返回指定索引处的字符；

   + int length()：获取字符串的长度

   + boolean equals(Object obj)：重写了Object的equals方法，用来比较字符串的内容，区别大小写；

   + boolean equalsIngoreCase(Object obj)：忽略大小写比较；

   + String trim()：去掉字符串前后空格；

   + String concat()：拼接，等价于“+”；

     ```java
     import org.junit.Test;
     
     import java.util.Scanner;
     
     public class TestStringAPI {
         @Test
         public void test1(){
             Scanner sc = new Scanner(System.in);
             System.out.println("请输入性别：");
             //char gender = sc.next().charAt(0);
             String str = sc.next();
             char gender = str.charAt(0);//取字符串的第一个字符
     
             System.out.println("性别：" + gender);
         }
     
         @Test
         public void test2(){
             String name = "迪丽热巴";
             int length = name.length();
             System.out.println("字符串的长度：" + length);
         }
     
         @Test
         public void test3(){
             String name = "Alice";
             String str = "alice";
             System.out.println(name.equals(str));//false,区别大小写，例如用户名密码比较
             System.out.println(name.equalsIgnoreCase(str));//true,忽略大小写，例如验证码比较
         }
     
         @Test
         public void test4(){
             //web页面，文本框
             String userInput = "chai   ";
             String user = userInput.trim();//去掉前后空格，不会去掉中间的空格
             System.out.println(userInput.trim());
         }
     
         @Test
         public void test5(){
             String str1 = "hello";
             String str2 = "world";
             String string = str1.concat(str2);
             System.out.println(string);
         }
     }
     ```
     
   + 常用：
   
     + isEmpty()：判断是否是空字符串；
     + toLowerCase()：使用默认的语言环境将此String中的所有字符转换为小写；
     + toUpperCase()：使用默认的语言环境将此String中的所有字符转换为大写；
     + char[] toCharArray()：将此字符串转换为一个新的字符数组
   
     ```java
     public class testString {
         public static void main(String[] args) {
             Student stu = new Student();
             //stu.setName("");
             //stu.setName(new String(""));
             String name = stu.getName();
     
             if (name == null){
                 System.out.println("名字没有赋值");
             }
             if ("".equals(name)){
                 System.out.println("名字赋值为空字符串1");
             }
             if (name.isEmpty()){
                 System.out.println("名字赋值为空字符串2");
             }
             if ("" == name){
                 System.out.println("名字赋值为空字符串3");
             }
         }
     }
     ```
   
   + 和字符相关：
   
     + startWith()：是否以...开头；
   
     + endWith()：是否以...结尾；
   
     + replace系列：替换；
   
     + indexOf()：查找某个字符或子串在当前字符串中的索引位置，如果该子串不存在，返回-1；
   
     + lastIndexOf()：
   
     + subString(int begin)和subString(int begin, int end)：截取；
   
     + spilt()：拆分；遇到“.”和“|”的正则问题需要加“\ \”；
   
       ```java
       import org.junit.Test;
       
       import java.sql.SQLOutput;
       
       public class TestStringAPI2 {
           @Test
           public void test1(){
               String name = "欧阳桦";
               boolean flag = name.startsWith("欧");
               System.out.println(flag);
           }
       
           @Test
           public void test2(){
               String str = "好好学习，天天向上、向上、向上";
               String all = str.replaceAll("向上", "up");
               System.out.println(all);
           }
       
           @Test
           public void test3(){
               String str = "好好学习，天天向上、向上、向上";
               boolean b = str.contains("向上");
               System.out.println(b);
       
               int index = str.indexOf("向上");
               System.out.println(index);
       
               int index2 = str.lastIndexOf("向上");
               System.out.println(index2);
           }
       
           @Test
           public void test4(){
               String file = "E:\\newstart\\src\\day016\\test.txt";
               //截取出文件的后缀名
               int index = file.lastIndexOf(".");
               String ext = file.substring(index);
               System.out.println(ext);
               //截取出文件名，不带扩展名
               int index2 = file.lastIndexOf("\\");
               System.out.println(index2);
       
               String fileName = file.substring(index2+1,index);
               System.out.println(fileName);
           }
       
           @Test
           public void test5(){
               String str = "hello,java,hello,world";
               String[] strings = str.split(",");
               for (String string:strings) {
                   System.out.println(string);
               }
           }
       
           @Test
           public void test6(){
               String str = "hello.java.hello.world";
               String[] strings = str.split("\\.");
               for (String string:strings) {
                   System.out.println(string);
               }
           }
       
           @Test
           public void test7(){
               String str = "hello|java|hello|world";
               String[] strings = str.split("\\|");
               for (String string:strings) {
                   System.out.println(string);
               }
           }
       }
       ```
   
       
   
4. String编码与解码：

   + 编码：字符串-->字节；

     ```java
     byte[] getBytes()//默认按照平台的字符集
     byte[] getBytes("编码方式")
     ```

   + 解码：字节-->字符串；

     ```java
     new String(byte[])//默认按照平台的字符集
     new String(byte[],"编码方式")
     ```

   + 乱码的原因：

     + 编码的字符集与解码的字符集不一致；
     + 字节数不全；

     ```java
     import org.junit.Test;
     
     import java.io.*;
     
     public class TestStringAPIencoding  {
         @Test
         public void test1() throws IOException {
             //读取了一个文件的内容
             File file = new File("E:\\newstart\\src\\day016\\test.txt");
             FileInputStream fis = new FileInputStream(file);
             byte[] data = new byte[10];
             int len = fis.read(data);
             //解码
             String info = new String(data,0,10,"UTF-8");
     
             System.out.println(info);
         }
     
         @Test
         public void test() throws UnsupportedEncodingException {
             String str = "欧阳";//UTF-8
     
             //编码
             byte[] bytes = str.getBytes("GBK");
             //解码
             String name = new String(bytes,"GBK");//GBK
             System.out.println(name);
         }
     }
     ```

###### String排序

1. 自然排序：实现了java.lang.Comparable>public int compareTo(Sting anotherString)

   + 如果是ASCII范围内，按照ASCII值的顺序；
   + 按照Unicode编码值进行排序

2. 定制排序：实现了java.util.Comparator，java.text.Collator是属于String的定制比较器：Collator c = Collator.getInstance();；

   ```java
   import java.text.Collator;
   import java.util.Arrays;
   import java.util.Comparator;
   
   public class TestStringCompare {
       public static void main(String[] args) {
           Student[] array = new Student[3];
           array[0] = new Student("章登");
           array[1] = new Student("柴林燕");
           array[2] = new Student("朱一龙");
   
           Arrays.sort(array);
           System.out.println(Arrays.toString(array));
   
           //希望大体上按照汉语拼音，或者字段的顺序
           Arrays.sort(array,new MyComparator());
           System.out.println(Arrays.toString(array));
       }
   }
   
   //定制排序：实现的接口是java.util.Comparator,实现int compare(Object o1,Object o2)
   class MyComparator implements Comparator{
   
       @Override
       public int compare(Object o1, Object o2) {
           //学生的定制排序
           Student s1 = (Student) o1;
           Student s2 = (Student) o2;
           //学生对象转变成学生姓名的字符串对象进行定制排序
           //s1和s2的比较，变成s1.getName()和s2.getName()进行比较
           String name1 = s1.getName();
           String name2 = s2.getName();
           //name1.compareTo(name2)仍是自然排序
           //java.text.Collator是属于String的定制比较器
           Collator c = Collator.getInstance();
           return c.compare(name1,name2);
       }
   }
   
   //学生排序：按照姓名进行排序
   //自然排序规则：学生类型实现java.lang.Comaprable接口,实现compareTo方法
   class Student implements Comparable{
       private String name;
   
       public Student() {
       }
   
       public Student(String name) {
           this.name = name;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       @Override
       public String toString() {
           return "Student{" +
                   "name='" + name + '\'' +
                   '}';
       }
   
       @Override
       public int compareTo(Object o) {
           Student other = (Student) o;
   
           //因为name是String类型，String类型实现了java.lang.Comparable接口，表示字符串对象是可以比较大小的
           //暂时没考虑空指针异常
           //本来是this和other的大小比较，现在转换成this.name和other.name比较大小
           return this.name.compareTo(other.name);
       }
   }
   ```


###### StringBuffer和StringBuilder

1. 介绍：java.lang包下；是字符串的兄弟类；和String的最大区别在于是可变的字符序列；
2. StringBuffer和StringBuilder的区别：
   + 完全兼容的API，即方法相同；
   + 不同的是StringBuffer相对老一点，jdk1.0；StringBuilder新一点，jdk1.5；
   + StringBuffer是线程安全的，StringBuilder是线程不安全的；
3. StringBuilder在API中的描述：
   + 一个可变的字符序列。 此类提供与`StringBuffer`的API，但不保证同步。  此类设计用作简易替换为`StringBuffer`在正在使用由单个线程字符串缓冲区的地方（如通常是这种情况）。  在可能的情况下，建议使用这个类别优先于`StringBuffer` ，因为它在大多数实现中将更快。
4. 线程安全问题：
   + 只有在多个线程同时存在时，并操作同一个字符串缓冲区时才存在，即多个线程对同一个StringBuffer或StringBuilder对象操作时才和发生，即多个线程有共享资源；
   + StringBuffer线程安全：即其中一个线程使用时，它会锁上，其他线程进不来；慢
   + StringBuilder线程不安全：即其中一个线程使用时，它没有锁上，其他线程有可能进来；快
5. API：
   + 创建对象不同：
     + String直接创建对象；
     + StringBuffer和StringBuilder通过构造器创建对象；
   + 拼接不同：
     + 方式：
       + String的拼接可以使用+进行直接拼接；
       + StringBuffer和StringBuilder的拼接不能使用+，使用append方法；
     + 结果：
       + String拼接后会产生新的对象；
       + StringBuffer和StringBuilder拼接时直接对源对象进行修改；
     + 效率：
       + StringBuffer和StringBuilder的时间效率和空间效率高于String；
   + 可以修改字符序列：
     + insert()；
     + delete()；
     + append()；
     + reverse()；
   + 其他方法：
     + charAt；
     + indexOf；
     + lastIndexOf；

```java
import org.junit.Test;

public class TestStringBrother {
    @Test
    public void test1(){
        String str = "hello";
        StringBuilder sb= new StringBuilder("hello");
    }
    @Test
    public void test2(){
        String str = "hello";
        String str2 = str + "world";
        System.out.println("str = " + str);
        System.out.println("str2 = " + str2);

        StringBuilder sb= new StringBuilder("hello");
        StringBuilder sb2= new StringBuilder("world");
        //append()之后sb被修改；
        StringBuilder sb3 = sb.append(sb2);
        System.out.println(sb);
        //支持连写
        StringBuilder sb4 = sb.append(true).append(12345).append(sb2);
        System.out.println(sb4);
    }
}
```

##### 时间日期类

###### jdk1.8之前的日期类

1. System.currentTimeMillis()：获取当前时间的毫秒数；

2. java.util.Date类：
   + 构造器：
     + Date()；
     + Date(long 毫秒)；
   + long getTime()：把Date对象转成毫秒数；
   
3. java.util.Calendar类：
   + 创建对象：
     + new GregorianCalendar()；
     + getInstance()；
   + 获取具体的某个时间：
     + get(field)；
   
4. 日期时间的格式化：java.text.SimpleDateFormat

   + 构造器：SimpleDateFormat sf = new SimpleDateFormat("格式");

   + format：格式化，把日期转成字符串，public final String format(Date date)；
   + parse：解析，把字符串转成日期，public Date parse(String source)；

   ![日期时间格式化](images/grammar/日期时间格式化.png)

```java
import com.sun.scenario.effect.impl.sw.sse.SSEBlend_SRC_OUTPeer;
import org.junit.Test;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.*;
import java.util.concurrent.CancellationException;

public class TestDate {
    @Test
    public void test(){
        long millis = System.currentTimeMillis();
        System.out.println(millis);
    }

    @Test
    public void test1(){
        Date date = new Date();
        System.out.println(date);

        Date d = new Date(100000);
        System.out.println(d);

        Date d2 = new Date(Integer.MAX_VALUE);
        System.out.println(d2);
        Date d3 = new Date(Long.MAX_VALUE);
        System.out.println(d3);
    }

    @Test
    public void test2(){
        Date date = new Date();
        System.out.println(date.getTime());
    }

    @Test
    public void test3(){
        //Calendar c = new GregorianCalendar();
        Calendar c = Calendar.getInstance();
        System.out.println(c);
        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH)+1;//1月份从0开始
        int day = c.get(Calendar.DATE);
        System.out.println(year +"年"+ month + "月" + day + "日");

        int hour = c.get(Calendar.HOUR);
        int minute = c.get(Calendar.MINUTE);
        int second = c.get(Calendar.SECOND);
        System.out.println(hour + "时" + minute + "分" + second + "秒");
    }

    @Test
    public void test4(){
        int year = 2017;
        int month = 11;//月份是从0开始的
        int day = 15;

        Calendar c = Calendar.getInstance();
        c.set(year,month,day);
        int i = c.get(Calendar.DAY_OF_YEAR);
        System.out.println(i);
    }

    @Test
    public void test5(){
        Calendar c = Calendar.getInstance(TimeZone.getTimeZone("America/New_York"), Locale.US);

        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH)+1;//1月份从0开始
        int day = c.get(Calendar.DATE);
        System.out.println(year +"年"+ month + "月" + day + "日");

        int hour = c.get(Calendar.HOUR_OF_DAY);
        int minute = c.get(Calendar.MINUTE);
        int second = c.get(Calendar.SECOND);
        System.out.println(hour + "时" + minute + "分" + second + "秒");

//        String[] availableIDs = TimeZone.getAvailableIDs();
//        for (String string:
//             availableIDs) {
//            System.out.println(string);
//        }
    }

    @Test
    public void test6() throws ParseException {
        Date date = new Date();
        System.out.println(date);

        //希望显示的格式是：2018-1-13
        SimpleDateFormat sf = new SimpleDateFormat("yyy-MM-dd");
        //把日期转成字符串：格式化
        String string = sf.format(date);
        System.out.println(string);

        String str = "1996-5-7";
        SimpleDateFormat sf2 = new SimpleDateFormat("yyy-MM-dd");
        //把字符串转成日期：解析
        Date date2 = sf2.parse(str);
        System.out.println(date2);
    }

    @Test
    public void test7(){
        Date date = new Date();
        SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS毫秒 E 是这一年的第D天");
        String string = sf.format(date);
        System.out.println(string);
    }
}
```

###### jdk1.8的日期时间

1. 本地日期（LocalDate）、本地时间（LocalTime）、本地日期时间（LocalDateTime）：

   + LocalDate代表IOS格式（yyyy-MM-dd）的日期,可以存储 生日、纪念日等日期；
   + LocalTime表示一个时间，而不是日期；
   + LocalDateTime是用来表示日期和时间的，这是一个最常用的类之一。

   | 方法                                                         | **描述**                                                     |
   | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | now() / now(ZoneId zone)                                     | 静态方法，根据当前时间创建对象/指定时区的对象                |
   | of()                                                         | 静态方法，根据指定日期/时间创建对象                          |
   | getDayOfMonth()/getDayOfYear()                               | 获得月份天数(1-31) /获得年份天数(1-366)                      |
   | getDayOfWeek()                                               | 获得星期几(返回一个 DayOfWeek 枚举值)                        |
   | getMonth()                                                   | 获得月份, 返回一个 Month 枚举值                              |
   | getMonthValue() / getYear()                                  | 获得月份(1-12) /获得年份                                     |
   | getHours()/getMinute()/getSecond()                           | 获得当前对象对应的小时、分钟、秒                             |
   | withDayOfMonth()/withDayOfYear()/withMonth()/withYear()      | 将月份天数、年份天数、月份、年份修改为指定的值并返回新的对象 |
   | with(TemporalAdjuster t)                                     | 将当前日期时间设置为校对器指定的日期时间                     |
   | plusDays(), plusWeeks(), plusMonths(), plusYears(),plusHours() | 向当前对象添加几天、几周、几个月、几年、几小时               |
   | minusMonths() / minusWeeks()/minusDays()/minusYears()/minusHours() | 从当前对象减去几月、几周、几天、几年、几小时                 |
   | plus(TemporalAmount t)/minus(TemporalAmount t)               | 添加或减少一个 Duration 或 Period                            |
   | isBefore()/isAfter()                                         | 比较两个 LocalDate                                           |
   | isLeapYear()                                                 | 判断是否是闰年（在LocalDate类中声明）                        |
   | format(DateTimeFormatter t)                                  | 格式化本地日期、时间，返回一个字符串                         |
   | parse(Charsequence text)                                     | 将指定格式的字符串解析为日期、时间                           |

   ```java
   import org.junit.Test;
   
   import java.time.LocalDate;
   import java.time.LocalDateTime;
   import java.time.LocalTime;
   
   public class TestLocalDateAndTime {
       @Test
       public void test1(){
           LocalDate date1 = LocalDate.now();
           System.out.println(date1);
           LocalDate date2 = LocalDate.of(2016,12,12);
           System.out.println(date2);
   
           LocalTime time1 = LocalTime.now();
           System.out.println(time1);
           LocalTime time2 = LocalTime.of(12,0,12);
   
           LocalDateTime dt = LocalDateTime.now();
           System.out.println(dt);
       }
   
       @Test
       public void test2(){
           LocalDate date1 = LocalDate.now();
           System.out.println("年：" + date1.getYear());
           System.out.println("月：" + date1.getMonthValue());
           System.out.println("日：" + date1.getDayOfMonth());
           System.out.println("第几天：" + date1.getDayOfYear());
       }
   
       @Test
       public void test3(){
           LocalDate date = LocalDate.now();
           LocalDate localDate = date.withMonth(12);
           System.out.println(date);
           System.out.println(localDate);
       }
   
       @Test
       public void test4(){
           LocalDate date1 = LocalDate.now();
           LocalDate date2 = date1.plusDays(240);
   
           System.out.println(date1);
           System.out.println(date2);
       }
   
       @Test
       public void test5(){
           LocalDate date = LocalDate.now();
           boolean b = date.isLeapYear();
           System.out.println(b);
       }
   }
   ```
   
2. 时间日期的格式化：java.time.DateTimeFormatter

   + format：把日期时间对象转字符串；
   + parse：把字符串转日期时间格式；


##### 数学相关类

1. java.lang.Math：Math类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数；

2. java.math：
   + BigInteger：大整数
   + BigDecimal：定点数

```java
import org.junit.Test;

import java.math.BigDecimal;
import java.math.BigInteger;

public class TestMath {
    @Test
    public void test(){
        System.out.println(Math.PI);
        System.out.println(Math.sqrt(5));
        System.out.println(Math.pow(2,3));

        System.out.println(Math.ceil(1.567));//天花板，2.0
        System.out.println(Math.round(1.567));//四舍五入，2
        System.out.println(Math.floor(1.567));//地板，1.0

        System.out.println(Math.max(2.6,5));
        System.out.println(Math.min(2.6,5));
    }

    @Test
    public void test1(){
        //12345678998765432345678
        //12345676543234567765432

        //long a = 12345678998765432345678L;超出范围
        BigInteger a = new BigInteger("12345678998765432345678");
        BigInteger b = new BigInteger("12345676543234567765432");

        BigInteger sum = a.add(b);
        System.out.println(sum);
        System.out.println(a.subtract(b));
        System.out.println(a.multiply(b));
        System.out.println(a.divide(b));
        System.out.println(a.remainder(b));
        BigInteger[] array = b.divideAndRemainder(a);
        System.out.println(array[0]);
        System.out.println(array[1]);
    }

    @Test
    public void test2(){
        //12.65432456776543234567
        //56.56865434567896543232
        BigDecimal a = new BigDecimal("12.65432456776543234567");
        BigDecimal b = new BigDecimal("56.56865434567896543232");
        BigDecimal c = new BigDecimal("4");

        System.out.println(a.add(b));
        System.out.println(a.subtract(b));
        System.out.println(a.multiply(b));
        //System.out.println(a.divide(b));//报错，不能够被整除
        System.out.println(a.divide(c));
        System.out.println(a.divide(b,10,BigDecimal.ROUND_FLOOR));
    }
}
```

### 异常处理

异常是指正常情况下程序可以照常运行，只是偶尔因为一些不可控的因素导致程序无法运行；异常不包括语法错误和逻辑错误；

不可控因素：网络中断、用户非法输入、用户硬盘容量已满等；

希望当出现了如上情况时，使得程序能够正常运行，而不是奔溃了，这样的处理称为异常处理；

在Java中如何表示异常，如何处理异常？

Java一切皆为对象，异常也是用对象表示；

Java对异常的处理过程：当某句代码发生异常时，会在该代码处停下来，然后创建一个异常的对象，然后把这个异常的对象抛出来；jvm会检查在这个异常对象的外围是否有try...catch代码，可以捕获这个异常对象，如果可以捕获，那么按照catch中的代码进行处理，然后程序从catch下面开始继续运行；如果没用对应的catch把它捕获，jvm会把这个异常继续往上抛出，抛给调用者，如果调用者可以处理，那么继续，如果调用者也没有处理，一路往上抛，直到main方法，如果main也没用处理，那么回到jvm，程序奔溃。

#### 异常的类型

体系结构：

java.lang.Throwable：Java语言中所有错误或异常的超类；

+ 只有当对象是此类（或其子类之一）的实例时，才能通过Java虚拟机或者Java throw语句抛出；
+ 只有此类或其子类之一才可以是catch子句中的参数类型；
+ 简单的说：只有Throwable类型或它的子类的类型的实例对象才能“抛”，或者被捕获；

Throwable又分为两个类别：

+ 错误：Error，严重的异常称为错误，例如VirtualMachineError包括StackOverflowError栈溢出，OutOfMemoryError堆内存溢出(OOM)；

+ 异常，例外：Exception；

  + 编译时异常，受检异常：FileNotFoundException,SQLException；
  + 运行时异常，非受检异常：RuntimeException或它的子类；例如NullPointerException,ArrayIndexOutOfBoundsException,ClassCastException,ArithmeticException等；

  ![异常的体系结构](images/grammar/异常的体系结构.png)

#### 异常的处理

##### try...catch

只要是Throwable类型或它的子类，都可以被catch；

1. 语法：

   ```java
   try{
       可能发生异常的代码;
   }catch(异常的类型 e1){
       该异常的处理代码;
   }catch(异常的类型 e2){
       该异常的处理代码;
   }...
    finally{
       不管是否发生异常都要执行的代码（例如：释放资源）;
   }
   ```

2. 运行过程：

   + 如果try中的代码发生异常，那么程序就停下来，跳到对应的catch中处理；如果没有catch能够抓住，就往上抛；
   + catch可以多个，catch()中必须是异常类型；
   + catch的类型如果没有包含关系，顺序随意；如果有包含关系，那么子上父下；
   + finally如果有，那么无论是否发生异常都要执行；

   ```java
   public class TestExceptionExer {
       //从命令行参数传入两个整数，并求出它俩的商
       public static void main(String[] args) {
           try {
               int a = Integer.parseInt(args[0]);
               int b = Integer.parseInt(args[1]);
               int c = a/b;
               System.out.println(c);
           } catch (NumberFormatException e) {
               System.out.println("需要传两个参数");
           } catch (ArrayIndexOutOfBoundsException e){
               System.out.println("需要传两个命令行参数");
           } catch (ArithmeticException e){
               System.out.println("第二个参数不能是0");
           } finally {
               System.out.println("finally块");
           }
       }
   }
   ```

##### throws

throws表示当前方法中不出来某个异常，交由调用者处理；

1. 语法格式(方法的声明格式)：

   ```java
   【修饰符】返回值类型 方法名(形参列表) throws 异常类型1,异常类型2,...{
       
   }
   ```

   + <font color='red'>重写的要求：两同两小一大；</font>
     + 两同：方法名和形参列表必须相同；
     + 两小：
       + 返回值类型：如果是基本数据类型和void必须相同，如果是引用数据类型，<=的关系；
       + 抛出的异常类型是小于等于的关系；
     + 一大：权限修饰符是大于等于的关系；

   ```java
   import java.util.Scanner;
   
   public class TestThrows {
       public static void main(String[] args) {
           try {
               divide();
           } catch (NumberFormatException e) {
               e.printStackTrace();//把异常的详细信息打印出来，包括异常的类型、异常的堆栈信息
               System.out.println("");//当作普通信息打印
               System.err.println("输入的不是数字");
           } catch (ArrayIndexOutOfBoundsException e) {
               e.printStackTrace();
           } catch (ArithmeticException e) {
               e.printStackTrace();
           }
   
           for (int i = 0; i < 5; i++) {
               System.out.println("hello world");
           }
       }
   
       public static void divide() throws NumberFormatException,ArrayIndexOutOfBoundsException,ArithmeticException{
           Scanner sc = new Scanner(System.in);
           System.out.println("请输入第一个数：");
           String s1 = sc.nextLine();
   
           System.out.println("请输入第二个数：");
           String s2 = sc.nextLine();
   
           int a = Integer.parseInt(s1);
           int b = Integer.parseInt(s2);
           int c = a / b;
           System.out.println(c);
       }
   }
   
   class Father{
       public void method() throws RuntimeException{
           
       }
   }
   
   class Son extends Father{
       @Override
       //NullPointerException是小于RuntimeException的
       public void method()throws NullPointerException{
           
       }
   }
   ```


##### 自定义异常与throw

1. 注意：

   + 如果自定义异常继承了RuntimeException，那么这个自定义异常就是运行时异常；如果自定义异常继承了Exception，那么这个异常就是编译时异常；
   + 编译时异常必须在编译阶段，必须加try..catch或throws处理，否则编译不通过，而运行时异常不用非加try...catch或throws；
   + throw可以代替return语句(执行throw语句后，后面的return语句不执行)；

2. 语法结构：

   ```java
   【修饰符】class 自定义异常类型 extends Throwable或它的子类{
       public MyException() {
       }
   
       public MyException(String message) {
           super(message);
       }
   }
   ```

3. 要求：

   + 必须继承Throwable或它的子类，例如：Exception，RuntimeException；

   + 自定义异常的对象，只能通过throw进行抛出，JVM不会自动抛出；

   + 建议自定义异常实现java.io.Serializable，并增加一个版本ID，方便把异常打印到日志中：

       private static final long serialVersionUID = 1L;

   ```java
   import java.util.Scanner;
   
   public class TestMyException {
       public static void main(String[] args) {
           while (true){
               Scanner sc = new Scanner(System.in);
               System.out.println("请输入用户名：");
               String username = sc.nextLine();
               System.out.println("请输入密码：");
               String password = sc.nextLine();
   
               try {
                   login(username,password);
                   break;
               } catch (Exception e) {
                   //e.printStackTrace();
                   System.out.println(e.getMessage());
               }
           }
           System.out.println("...");
       }
   
       public static void login(String username,String password) throws MyException {
           if ("ouyang".equals(username) && "123456".equals(password)){
               System.out.println("登录成功");
           }else {
               System.out.println("登录失败");
               MyException m = new MyException("用户名或密码错误");
               throw m;
           }
       }
   }
   
   class MyException extends Exception{
       public MyException() {
       }
   
       public MyException(String message) {
           super(message);
       }
   }
   ```


##### finalize、final、finally的区别：

finalize：是属于Object的方法，实在对象被垃圾回收之前调用；

final：是一个修饰符，可以修饰类，表示不能被继承，可以修饰方法，表示不能被重写，可以修饰变量，表示值不能被修改；

finally：是属于异常处理的关键字，无论try语句块是否发生异常，finally语句都要执行；

### 集合

集合是在数组或链表这样的物理结构的基础上，重新封装的一种逻辑结构；对于使用这个集合的人来说，是不用考虑集合的扩容、元素的存储，还可以通过size()直接获取有效元素的个数；<font color='red'>对于一组对象来说，选择集合的话，肯定优先考虑集合；集合的元素都是对象，如果存储基本数据类型会自动装箱；</font>

```java
import java.util.ArrayList;

@SuppressWarnings("all")
public class TestCollection {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();

        list.add(12);
        list.add((new Integer(15)));

        for (Object obj:
             list) {
            //getClass()获取对象的运行时类型，运行时类型就是它的实际类型
            System.out.println(obj.getClass());
        }
    }
}
/**
class java.lang.Integer
class java.lang.Integer
*/
```

#### 动态数组

数组：一种容器，可以用来装一组数据，多个数据；元素可以是基本数据类型，也可以是对象；

特点：一旦创建，它的长度不能修改；无法通过数组直接获取有效元素的个数；可以通过索引、下标直接定位到某个元素；

在实际开发中，更多的用来处理基本数据类型数据；

在数组的基础上，可以设计更灵活的容器；

+ 物理结构：数组、链表；
+ 逻辑结构：动态数组、双向链表、栈、队列、树（二叉树）...

String：底层使用char[]或者byte[]存储；

```java
import java.util.Arrays;
/**
 * MyArrayList是我们自己设计的一种新容器
 * MyArrayList的一个对象就是一个容器，这个容器可以放很多对象、元素
 */
public class MyArrayList {
    private Object[] data = new Object[5];//这个数组就是物理结构，真正数据的存储位置
    private int total;

    /**
     * 往MyArrayList容器中添加元素的方法
     * @param element Object元素的类型是任意类型
     */
    public void add(Object element){
        if (total >= data.length){
            //数组已满时扩容
            data = Arrays.copyOf(data, data.length * 2);
        }
        data[total++] = element;
    }

    /**
     * 从MyArrayList容器中移除元素
     * @param index 移除元素的下标
     */
    public void delete(int index){
        checkIndex(index);
        System.arraycopy(data,index+1,data,index,total-index-1);
        data[--total] = null;
    }

    /**
     * 检查索引的范围是否合理
     * @param index 元素的索引
     */
    public void checkIndex(int index) {
        if (index < 0 || index >= total){
            throw new IndexOutOfBoundsException(index + "索引越界");
        }
    }

    /**
     * 返回index位置的元素
     * @param index 元素的索引
     * @return Object 是index位置的元素
     */
    public Object get(int index){
        checkIndex(index);
        return data[index];
    }

    /**
     * 返回当前元素中有效元素的个数
     * @return 实际存储的元素的个数
     */
    public int size(){
        return total;
    }

    /**
     * 返回元素中实际存储的元素
     */
    public Object[] getAll(){
        return Arrays.copyOf(data,total);
    }

    /**
     * 从MyArrayList容器中移除一个元素,只能删除找到的第一个
     * param obj 需要删除的元素对象
     */
    public void delete(Object obj){
        //1、找到bbj的位置index
        int index = find(obj);

        //2、删除index位置的元素
        delete(index);
    }

    /**
     * 用value替换index为主的元素
     * @param index 被替换元素的位置下标
     * @param value 新的元素
     */
    public void set(int index, Object value){
        //1、检查index
        checkIndex(index);

        //2、直接替换
        data[index] = value;
    }

    /**
     * 只替换找到的第一个元素，把MyArrayList中找到第一个old，替换为value
     * @param old
     * @param value
     */
    public void set(Object old, Object value){
        //1、找到old的位置
        int index = find(old);
        //2、替换为value
        set(index,value);
    }

    /**
     * 在MyArrayList中查找第一个obj的索引，如果没有这个元素就返回-1
     * @param obj
     */
    public int find(Object obj){
        int index = -1;
        if (obj ==null){
            for (int i = 0; i < total; i++) {
                if (data[i] == obj){
                    index = i;
                    break;
                }
            }
        }else{
            for (int i = 0; i < total; i++) {
                if (obj.equals(data[i])){
                    index = i;
                    break;
                }
            }
        }
        return index;
    }

    /**
     * 在index位置插入value元素
     * @param index 新插入的位置
     * @param value 新插入的元素
     */
    public void insert(int index,Object value){
        //先判断当前数组是否已满，如果满了，就扩容
        if (total >= data.length){
            data = Arrays.copyOf(data,data.length*2);
        }

        checkIndex(index);

        //1、先把index以及之后的元素往右移动
        System.arraycopy(data,index,data,index+1,total-index);

        //2、把index位置放入value
        data[index] = value;

        //3、元素个数增加
        total++;
    }

    /**
     * 在第一个target元素的位置插入value，然后target及右边的元素右移
     * @param target 被插入的目标元素
     * @param value 插入的新元素
     */
    public void insert(Object target, Object value){
        //1、找到target的index
        int index = find(target);
        checkIndex(index);

        //2、在index位置插入value
        insert(index,value);
    }
}
```

测试类：

```java
public class TestMyArrayList {
    public static void main(String[] args) {
        MyArrayList m = new MyArrayList();//创建一个容器对象
        //容器可以装、拿、查看等操作

        m.add("hello");
        m.add("world");
        m.add("java");
        m.add("mysql");
        m.add("oracle");
        m.add("php");

        System.out.println("实际存储的元素个数是："+ m.size());

        Object object = m.get(3);
        System.out.println(object);

        m.delete(3);
        System.out.println("实际存储的元素个数是："+ m.size());

        Object[] all = m.getAll();
        for (Object element:
             all) {
            System.out.println(element);
        }

        System.out.println("-----------------------------");
        m.delete("oracle");
        System.out.println("实际存储的元素个数是："+ m.size());

        all = m.getAll();
        for (Object element:
                all) {
            System.out.println(element);
        }

        System.out.println("-----------------------------");
        m.insert(2,"html");
        all = m.getAll();
        for (Object element:
                all) {
            System.out.println(element);
        }

        System.out.println("-----------------------------");
        m.insert("world","js");
        all = m.getAll();
        for (Object element:
                all) {
            System.out.println(element);
        }
    }
}
```

#### 链表

物理结构：链表

逻辑结构：链表的容器

特点：方便插入和删除；获取数据麻烦，需要遍历查找，比数组慢；

链表的实现原理：

+ 创建一个节点类，其中节点类包含两个部分，第一个是数据域（在节点里面存储的信息），第二个是引用域（相当于指针，单向链表有一个指针，指向下一个节点；双向链表有两个指针，分别指向下一个和上一个节点）；
+ 创建一个链表类，其中链表类包含三个属性：头节点、尾节点和大小，方法包含添加、删除、插入等方法；

##### 双向链表

```java
/**
 * MyLinkedList的一个对象就是一个容器，容器中可以存储各种类型的元素
 * MyLinkedList的元素实际上是一个个Node类型，通过first往右一个个串起来，或者从last往左一个个找到
 */
public class MyLinkedList {
    private Node first;
    private Node last;

    public void addLast (Object element){
        //默认添加到last的后面
        //新节点的上一个元素是last

        //1、创建新节点
        Node node = new Node(last,element,null);

        if (first == null){//说明当前链表是空链表
            //新节点是第一个节点
            first = node;
        }else {
            last.next = node;
        }

        //新节点变成了最后一个节点
        last = node;
    }

    /*
   	获得链表中的所有元素
    */
    public Object[] getAll(){
        Object[] all = new Object[3];

        Node node = first;
        for (int i = 0; i < all.length; i++) {
            all[i] = node.data;
            node = node.next;
        }
        return all;
    }

    public Object getFirst(){
        return first.data;
    }

    public Object getLast(){
        return last.data;
    }

    /**
    *创建双向链表的节点类
    */
    private class Node{
        private Node prev;
        private Object data;
        private Node next;

        public Node() {
        }

        public Node(Node prev, Object data, Node next) {
            this.prev = prev;
            this.data = data;
            this.next = next;
        }
    }
}
```

测试类：

```java
public class TestMyLinkedList {
    public static void main(String[] args) {
        MyLinkedList m = new MyLinkedList();
        m.addLast("hello");
        m.addLast("world");
        m.addLast("java");

        Object[] all = m.getAll();
        for (Object obj:
             all) {
            System.out.println(obj);
        }

        System.out.println("----------------------");
        System.out.println(m.getFirst());
        System.out.println(m.getLast());
    }
}
```

##### 单向链表

```
1、空链表：first = null;
2、只有一个节点：first != null,first.next = null;
3、多个节点：first != null，最后一个节点的next = null;
```

```java
public class OneWayLinked {
    private Node first;//只有链表头
    private int total;//记录有效元素的个数

    //所有的操作，都要从表头开始

    /**
     * 向链表中添加元素
     * @param element
     */
    public void add(Object element){
        //因为在链表中所有的元素都是节点，所以第一步要先创建节点
        //1、新建节点
        Node newNode = new Node(element,null);

        //2、把新节点和原来链表中的节点连起来
        //(1)当前链表是空的
        if (first == null){
            //新的节点就是链表头
            first = newNode;
        }else {
            //(2)当前链表不是空的
            //新节点要连接到原来的链表的最后一个节点的后面
            //（A）找到链表的最后一个节点
            Node temp = first;
            while (temp.next != null){//如果temp.next是空，退出循环，temp就是最后一个节点
                temp = temp.next;
            }

            //temp就是原来的最后一个节点
            temp.next = newNode;//把当前新节点连接到原来最后一个节点的后面
        }

        //3、元素的个数增加
        total++;
    }

    /**
     * 返回链表中元素的个数
     * @return
     */
    public int size(){
        return total;
    }

    /**
     * 返回链表的元素
     * @return
     */
    public Object[] getAll(){
        Object[] all = new Object[total];

        if (first != null){//表示当前链表不是空链表
            Node temp = first;
            for (int i = 0; i < total; i++) {
                all[i] = temp.data;
                temp = temp.next;
            }
        }
        return all;
    }

    /**
     * 删除节点中的元素
     * @param target 被删除元素的位置
     */
    public void delete(Object target){
        //找到target的位置
        if (first != null){//表示当前链表不是空链表
            Node temp = first;
            int index = -1;
            for (int i = 0; i < total; i++) {
                if (temp.data.equals(target)){//如果temp.data是和target一样的，那么temp是要被删除的节点
                    //index是temp的位置
                    index = i;
                    break;
                }
                temp = temp.next;
            }
            //确定的是：temp是要被删除的节点，它的位置是index
            if (index != -1){
                if (index == 0){//要被删除的是第一个
                    first = first.next;
                }else {
                    //要删除的不是第一个
                    //把temp的前一个的next指向temp的下一个节点
                    //（1）先找到temp的前一个节点
                    Node dropLeft = first;
                    for (int i = 0; i < index-1; i++) {
                        dropLeft =dropLeft.next;
                    }

                    //(2)重新指向
                    dropLeft.next = temp.next;

                    //(3)把temp变成垃圾可以回收的节点
                    temp.data = null;
                    temp.next = null;

                    //(4)元素的数量减少
                    total--;
                }
            }
        }
    }

    /**
     * 创建单向链表的节点类
     */
    private class Node{
        Object data;
        Node next;

        public Node() {
        }

        public Node(Object data, Node next) {
            this.data = data;
            this.next = next;
        }
    }
}
```

测试类：

```java
public class TestOneWayLinked {
    public static void main(String[] args) {
        //1、创建容器
        OneWayLinked my = new OneWayLinked();

        my.add("hello");
        my.add("world");
        my.add("java");
        my.add("mysql");

        System.out.println("元素的个数是："+ my.size());
        Object[] all = my.getAll();
        for (Object obj:
             all) {
            System.out.println(obj);
        }

        my.delete("java");
        System.out.println("元素的个数是："+ my.size());
        all = my.getAll();
        for (Object obj:
                all) {
            System.out.println(obj);
        }
    }
}
```

#### Collection:单值集合

数组的缺点：容量不可变；无法直接获取有效元素的个数；

jdk中提供了更多的容器：

+ Collection：这个系列的容器都是存储一个个对象的；
  + List：有序的（和添加的顺序有关）、可重复的；
    + 动态数组；
    + 链表；
    + 队列；堆栈
  + Set：无序的（和添加的顺序无关），不可重复的：相当于数学中集合的概念；
    + HashSet：
    + TreeSet：
    + LinkedHashSet：

+ Map：这个系列的容器都是存储一对一对的关系的；
  + HashMap：
  + Hashtable：
  + TreeMap：
  + LinkedHashMap：
  + Properties：

Collection层次结构的根接口，Collection表示一组对象，这些对象也称为collection的元素；一些collection允许有重复的元素，而另一些则不允许；一些collection是有序的，而另一些是无序的；jdk不提供次接口的任何直接实现：它提供更具体的子接口（如Set和List）实现；

List：有序的，可重复的；

Set：无序的、不可重复的；

##### Collection方法

###### ArrayList：动态数组

+ API（Collection中没有关于删除的方法）：
  + add(Object obj)：添加元素；
  + size()：获取有效元素的个数；
  + Object[] toArray()：返回所有元素；
  + remove()：删除元素，如果有重复的元素，只删除第一个；<font color='red'>list、Arraylist中的remove方法无法直接删除类对象，需要重写类中的equals方法；</font>
  + clear()：清空集合；
  + contains(Object o)：是否包含某个元素；
  + isEmpty()：判断集合是否为空；
  + 和All相关：
    + addAll(Collection other)：把另一个集合中的所有元素，一一添加到当前集合中;
    + containsAll(Collection other)：当前集合中是否包含另一个集合的所有元素；
    + removeAll(Collection other)：从当前集合中移除和另一个集合中的元素中一样的元素：A = A - A∩B；
    + retainAll()：把当前集合与指定集合的交集保留到当前集合中：A = A ∩ B；

  ```java
  import org.junit.Test;
  
  import java.util.ArrayList;
  import java.util.Collection;
  
  public class TestCollectionInter {
      @Test
      public void test(){
          Collection coll = new ArrayList();//多态引用
  
          //添加元素
          coll.add("hello");
          coll.add("world");
          coll.add("java");
  
          System.out.println("有效元素的个数是:" + coll.size());
  
          Object[] all = coll.toArray();
          for (Object obj:
               all) {
              System.out.println(obj);
          }
  
          coll.remove("hello");
          System.out.println("有效元素的个数是:" + coll.size());
  
          coll.clear();
          System.out.println("有效元素的个数是:" + coll.size());
      }
  
      @Test
      public void test1(){
          Collection coll = new ArrayList();
  
          //添加元素
          coll.add("hello");
          coll.add("world");
          coll.add("java");
  
          boolean result = coll.contains("java");
          System.out.println(result);
  
          boolean res1 = coll.isEmpty();
          System.out.println(res1);
      }
  
      @Test
      public void test3(){
          Collection c1 = new ArrayList();
          c1.add("1");
          c1.add("2");
          c1.add("3");
  
          Collection c2 = new ArrayList();
          c2.add("3");
          c2.add("4");
          c2.add("5");
  
          c1.addAll(c2);
          System.out.println("c1的元素的个数是：" + c1.size());
          System.out.println("c1的元素的个数是：" + c2.size());
      }
  
      @Test
      public void test4(){
          Collection c1 = new ArrayList();
          c1.add("1");
          c1.add("2");
          c1.add("3");
          c1.add("4");
  
          Collection c2 = new ArrayList();
          c2.add("1");
          c2.add("2");
          c2.add("3");
  
          boolean b = c1.containsAll(c2);
          System.out.println(b);
      }
  
      @Test
      public void test5(){
          Collection c1 = new ArrayList();
          c1.add("1");
          c1.add("2");
          c1.add("3");
          c1.add("4");
  
          Collection c2 = new ArrayList();
          c2.add("1");
          c2.add("2");
          c2.add("3");
  
          c1.removeAll(c2);
          System.out.println("c1的元素的个数是：" + c1.size());
          System.out.println("c1的元素的个数是：" + c2.size());
      }
  
      @Test
      public void test6() {
          Collection c1 = new ArrayList();
          c1.add("1");
          c1.add("2");
          c1.add("3");
          c1.add("4");
  
          Collection c2 = new ArrayList();
          c2.add("1");
          c2.add("2");
          c2.add("3");
  
          c1.retainAll(c2);
  
          System.out.println("c1的元素的个数是：" + c1.size());
  
          Object[] obj1 = c1.toArray();
          for (Object obj:
               obj1) {
              System.out.println(obj);
          }
  
          System.out.println("c1的元素的个数是：" + c2.size());
          Object[] obj2 = c1.toArray();
          for (Object obj:
               obj2) {
              System.out.println(obj);
          }
      }
  }
  ```

+ 集合遍历：

  + foreach遍历：for(元素的类型  元素名:数组/集合名)

    + 如果只看，用foreach更简洁，效率更高
  + 在遍历的同时是不能做修改元素的个数这样的事情的，可以理解为foreach是得到一个匿名迭代器，它只是在一开始获得集合中的元素信息，如果遍历过程中修改了元素个数等，那么通过集合的remove()方法删除了元素，而迭代器不知道就会出问题；
  
    ```java
    @Test
    public void test7() {
        Collection c1 = new ArrayList();
        c1.add("1");
        c1.add("2");
        c1.add("3");
        c1.add("4");
    
        //for(元素的类型  元素名:数组/集合名)
        for (Object obj:
             c1) {
            System.out.println(obj);
        }
    }
    ```
  
+ Iterator迭代：
  
  + 如果在遍历的同时，想要删除元素、添加元素等，只能使用迭代器，不能使用foreach；
  
    ```java
    @Test
    public void test8() {
        Collection c1 = new ArrayList();
        c1.add("1");
        c1.add("2");
        c1.add("3");
        c1.add("4");
    
        //Iterator迭代器，专门用来遍历，迭代集合用；
        //
        Iterator iter = c1.iterator();
        while (iter.hasNext()){
            Object next = iter.next();
            if ("4".equals(next)){
                //通过迭代器对象对集合元素进行删除
                iter.remove();
            }
            System.out.println(next);
        }
        System.out.println("元素个数：" + c1.size());
    }
    ```

###### 迭代器

![迭代器](images/grammar/迭代器.png)

每一个Collection集合中都有一个关于Iterator接口的实现类，是作为内部类来实现的；

+ 迭代器的方法：
  + hasNext()：用于判断集合是否还有下一个元素；
  + Next()：取出下一个元素；
  + remove()：删除刚刚被迭代器访问的那个元素；通过迭代器自己的方法remove()删除了集合中的元素，那么迭代器自己知道，所以不会报错；

```java
import java.util.ArrayList;
import java.util.Iterator;

@SuppressWarnings("all")
public class TestIterator {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();

        //左边是接口，右边的iterator()方法中返回了Iterator的实现类Itr的对象
        Iterator iter = list.iterator();
    }
}
```

##### List接口

List是collection中的一个分支，有序的、可重复的；它的实现类有：

（1）ArrayList：新版动态数组；

（2）Vector：旧版动态数组；

（3）LinkedList：双向链表；

（4）Stack：栈；

（5）Queue：队列；

List的方法：比Collection多了关于索引index的信息；

###### ArrayList

+ 添加：add(Object)；addAll(Collection)；

  + add(index , Object)：吧obj添加到当前集合的index位置；
  + addAll(index, Collection)：是other集合中的元素一一添加到当前集合中的index位置，一次添加多个；

+ 删除：remove(Object)；removeAll(Collection)；clear()；

  + remove(int index)：删除指定位置的元素；

+ 查找：contains(Object)；containsAll(Collection)；isEmpty()；

  + indexOf(Object)：返回Object的下标，如果有重复的元素，只返回第一个，如果没有返回-1；
  + lastIndexOf(obj)：功能同indexOf，只是从右边往左边找；
  + get(index)：获取指定索引处的元素；

+ 替换、修改：set(index, Object)：把index位置的元素修改为obj；

+ 其他方法：

  + 获取有效元素个数：size()；
  + 获取所有元素：Object[] toArray()；

+ 遍历集合：

  + foreach：

  + Iterator迭代：

    ```java
    @Test
    public void test4(){
        List list = new ArrayList();
            
        list.add("hello");
        list.add("world");
    
        Iterator iter = list.iterator();
        while (iter.hasNext()){
            Object next = iter.next();
            System.out.println(next);
    }
    ```

  + ListIterator迭代：是Iterator的子接口；

    + 比Iterator多的方法：
      + 从后往前迭代：
    + hasPrevious：判断是否有前一个元素；
        + previous：取出前一个元素；
    + nextIndex：返回下一个元素的索引；
        + previousIndex：获取前一个元素的索引；
      + 在遍历集合的同时增加、删除、修改集合的元素：
        + add：
        + set：
    + next()：不包含index
    + previews()：包含index
    
    ![ListIteratorAPI](images/grammar/ListIteratorAPI.png)
    
    ```java
    import org.junit.Test;
    
    import java.util.ArrayList;
    import java.util.Iterator;
    import java.util.List;
    import java.util.ListIterator;
    
    @SuppressWarnings("all")
    public class TestListImpl {
        @Test
        public void test4(){
            List list = new ArrayList();
    
            list.add("hello");
            list.add("world");
    
            Iterator iter = list.iterator();
            while (iter.hasNext()){
                Object next = iter.next();
                System.out.println(next);
            }
        }
    
        @Test
        public void test5(){
            List list = new ArrayList();
    
            list.add("hello");
            list.add("world");
    
            ListIterator iter = list.listIterator();
            //从前往后迭代
            while (iter.hasNext()){
                Object next = iter.next();
                System.out.println(next);
            }
    
            //从后往前迭代，iter的指针指向最后一个元素
            System.out.println("从后往前迭代");
            while (iter.hasPrevious()){
                Object previous = iter.previous();
                System.out.println(previous);
            }
        }
    
        @Test
        public void test6() {
            List list = new ArrayList();
    
            list.add("hello");
            list.add("world");
    
            ListIterator iter = list.listIterator(list.size());
            //从后往前迭代
            System.out.println("从后往前迭代");
            while (iter.hasPrevious()){
                Object previous = iter.previous();
                System.out.println(previous);
            }
        }
    
        @Test
        public void test7() {
            List list = new ArrayList();
    
            list.add("hello");
            list.add("world");
            list.add("A");
            list.add("B");
            list.add("C");
    
            ListIterator iter = list.listIterator(3);
            System.out.println("从中间往前迭代");
    //        while (iter.hasPrevious()){
    //            Object previous = iter.previous();//不包含index:3
    //            System.out.println(previous);
    //        }
    
            System.out.println("从中间往后迭代");
            while (iter.hasNext()){
                System.out.println(iter.next());//包含index:3
            }
        }
    }
    ```

###### List实现类的区别

1. ArrayList（使用频率最高）：新版动态数组；
   
   + jdk1.2才有；线程不安全的；
   + 不够了扩容的算法是1.5倍；
   + 只支持新的迭代，不再支持Enumration迭代；
   + 初始容量：新版本中如果用无参构造创建集合对象，一开始是创建长度为0的数组，在添加第一个元素时，初始化为长度为10的数组；
2. Vector：旧版动态数组；
   
   + jdk1.0就有，最早的集合，线程安全的；
   + 不够了扩容的算法是2倍；
   + 支持旧版的迭代器Enumration迭代和新版本的Iterator迭代；
   + 初始容量：如果用无参构造创建集合对象，直接创建长度为10的数组；
3. LinkedList：物理结构是双向链表；
   + 双向链表与动态数组一起比较：
     + 动态数组的物理结构是数组；双向链表的物理结构是链表，元素是节点Node；
     
       ```java
       Node{
           Node pre;
           Object element;
           Node next;
       }
       ```
     
     + 在增加、删除、插入时，动态数组涉及到大量元素的复制、移动等，效率比较低；而双向链表的增加、删除、插入，只会涉及到它的前后节点，和其他元素无关，效率比较高；（元素的动态数组的插入和删除要涉及到复制移动一些元素，而双向链表在插入和删除时只要关注它的前后节点的修改即可）
     
     + 在查找、替换时，动态数组效率高，可以直接通过index获取；双向链表要通过first或last一一链接，统计才能定位到index位置；
4. Stack：栈；
   
   + 先进后出（后进先出）；
5. Queue：队列；
   
   + 先进先出；

##### Set系列集合

Set接口也是Collection的一种：无序的、不重复的；Set都继承Collection接口，与Collection的方法一致；

判断对象是否相等的依据是equals（如果是Object中的equals，和==的效果一样），即通过equals方法决定了不可重复；

无序：根据hashcode值来决定存储的位置，散列存储；

Set底层是Map；Map存一对(key,value)；Set存的是(key,固定的Object对象)；

```java
//他们的value是同一个Object常量对象，即private static final Object PRESENT = new Object();
set.add(new String("张三 "));
set.add(new String("李四 "));
set.add(new String("王五 "));
set.add(new String("赵六 "));
```

###### Set的实现类

+ HashSet-->HashMap；
  
  + 按照元素的哈希值散列存储；<元素是通过hashcode值决定了存储的位置，通过equals方法决定了不可重复，换句话说，放到HashSet中的元素，是依赖于它的hashcode和equals方法>
  
+ TreeSet-->TreeMap；
  
  + 按照元素的大小进行排序：依据元素的自然排序或定制排序；
    + <font color='red'>TreeSet set = new TreeSet()：依据元素的自然排序，要求元素类型必须实现java.lang.Comparable接口，重写int compareTo(Object obj)方法；</font>
    + <font color='red'>TreeSet set = new TreeSet(Comparator的实现类对象)：依据元素的定制排序，要求为元素写一个类实现java.util.Comparator接口，重写int Compare(Object o1, Object o2)方法；</font>
    + 它的元素不能重复，依据元素的大小：认为两个元素大小相等，就是相同的元素；
  
+ LinkedHashSet-->LinkedHashMap；

  + 是HashSet的子类，在HashSet的基础上多维护了元素的添加顺序（变成了有序的、不可重复的集合）；

  + 物理结构在HashSet的物理结构的基础上，增加了链表，记录了前后节点的属性；
  
    ```java
    import java.lang.String;
    import org.junit.Test;
    import sun.dc.pr.PRError;
    
    import java.util.*;
    
    @SuppressWarnings("all")
    public class TestSet {
        @Test
        public void test(){
            HashSet set = new HashSet();
            set.add("张三");
            set.add("李四");
            set.add("王五");
            set.add("赵六");
            set.add("赵六");//不可重复
    
            for (Object obj:set) {
                System.out.println(obj);
            }
        }
    
        @Test
        public void test2(){
            ArrayList set = new ArrayList();
            set.add("张三");
            set.add("李四");
            set.add("王五");
            set.add("赵六");
            set.add("赵六");//有序，可重复
    
            for (Object obj:set) {
                System.out.println(obj);
            }
        }
    
        @Test
        public void test3(){
            HashSet set = new HashSet();
    
            set.add(new Teacher("张三"));
            set.add(new Teacher("李四"));
            set.add(new Teacher("王五"));
            set.add(new Teacher("赵六"));
            set.add(new Teacher("赵六"));
    
            Iterator iter = set.iterator();
            while (iter.hasNext()){
                System.out.println(iter.next());
            }
        }
    
        @Test
        public void test4(){
            HashSet set = new HashSet();
    
            set.add(new String("张三 "));
            set.add(new String("李四 "));
            set.add(new String("王五 "));
            set.add(new String("赵六 "));
            set.add(new String("赵六 "));
    
            Iterator iter = set.iterator();
            while (iter.hasNext()){
                System.out.println(iter.next());
            }
        }
    
        @Test
        public void test5(){
            //通过定制比较器比较年龄
            class MyComparator implements Comparator{
    
                @Override
                public int compare(Object o1, Object o2) {
                    Teacher t1 = (Teacher)o1;
                    Teacher t2 = (Teacher)o2;
                    return t1.getAge() - t2.getAge();
                }
            }
    
            TreeSet set = new TreeSet(new MyComparator());//会按照元素大小顺序进行存储，默认按照元素的自然顺序排序，即要求元素实现java.lang.Compare接口
            set.add(new Teacher("Jack",23));
            set.add(new Teacher("Lily ",25));
            set.add(new Teacher("Tom ",26));
            set.add(new Teacher("Alice ",21));
    
            Iterator iter = set.iterator();
            while (iter.hasNext()){
                System.out.println(iter.next());
            }
        }
    }
    
    class Teacher implements Comparable{
        private String name;
        private int age;
    
        public Teacher() {
    
        }
    
        public Teacher(String name) {
            this.name = name;
        }
    
        public Teacher(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public int getAge() {
            return age;
        }
    
        public void setAge(int age) {
            this.age = age;
        }
    
        @Override
        public String toString() {
            return "Teacher{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    '}';
        }
    
        @Override
        public boolean equals(Object o) {
            if (this == o) {
                return true;
            }
            if (o == null || getClass() != o.getClass()) {
                return false;
            }
            Teacher teacher = (Teacher) o;
            return getName().equals(teacher.getName());
        }
    
        @Override
        public int compareTo(Object o) {
            Teacher other = (Teacher) o;
    
            //有bug，当this.name = null时会报空指针
            return this.name.compareTo(other.getName());
        }
    }
    ```

#### Map:对值集合(映射关系的集合)

Map：存对值，映射关系（key, value）；

说明：Map的key是不能重复的，其他的map是依据key的equals方法判定，如果返回true就认为重复，TreeMap如果两个key通过调用compareTo或compare如果返回0，就认为相等；参加比较的属性，一旦添加到Map中，不要修改，修改会影响比较值；

实现类：HashMap等；

##### Map方法

+ API：

  + put(key,value)：添加，key不能重复；

  + putAll(Map other)：把另一个map的映射关系添加到当前Map中；key不能重复；

  + size()：有效关系的映射的个数；

  + remove(Object key)：根据key删除一对映射关系，返回被删除map的value；

  + get(Object key)：根据key获取对应的value；

  + containsKey(Object key)：是否包含某个key；

  + containsValue(Object value)：是否包含某个value；

  + clear()：移除所有映射关系；

  + isEmpty()：如果集合不包含映射关系，返回true；

  + Set keySet()：返回Map集合中包含key的Set视图；

  + Collection values()：返回Map集合中包含value的Collection视图；

  + Set entrySet()：返回Map集合中包含映射的Set视图；

    ```java
    import org.junit.Test;
    
    import java.util.HashMap;
    import java.util.Map;
    
    @SuppressWarnings("all")
    public class TestMap {
        @Test
        public void test1(){
            Map map = new HashMap();
            map.put("1","张登");//key是1，value是张登，这里key是字符串类型，value是字符串类型
            map.put("2","如花");
    
            map.size();
            System.out.println(map.size());//两对
        }
    
        @Test
        public void test2(){
            Map map = new HashMap();
            map.put("1","张登");
            map.put("2","如花");
    
            map.remove("1");//根据key删除value
            System.out.println(map.size());
        }
    
        @Test
        public void test3() {
            Map map = new HashMap();
            map.put("1", "张登");
            map.put("2", "如花");
    
            Object o = map.get("1");
            System.out.println(o);
        }
    
        @Test
        public void test4(){
            Map map = new HashMap();
            map.put("1", "张登");
            map.put("2", "如花");
    
            Map map2 = new HashMap();
            map2.put("3","哈嘿");
            map2.put("4","world");
    
            map.putAll(map2);
            System.out.println(map.size());//4对
        }
    
        @Test
        public void test5(){
            Map map = new HashMap();
            map.put("1", "张登");
            map.put("2", "如花");
    
            Map map2 = new HashMap();
            map2.put("1","哈嘿");
            map2.put("2","world");
    
            map.putAll(map2);
            System.out.println(map.size());//2对，key不能重复
        }
    }
    ```

+ 遍历：

  + Map本身是不支持foreach遍历的，原因是它没有继承java.lang.Iterable接口；Collection接口继承了java.lang.Iterable接口，因此Collection系列的集合可以直接foreach遍历；

  + 遍历它的所有的key：

    + Set keySet()：返回Map集合中包含key的Set视图；

    + 遍历set：

      ```java
      @Test
      public void test6() {
          Map map = new HashMap();
          map.put("1", "张登");
          map.put("2", "如花");
      
          Set keySet = map.keySet();
          for (Object key:keySet) {
              System.out.println(key);
          }
      }
      ```
    
  + 遍历它的所有的value：
  
    + Collection values()：返回Map集合中包含value的Collection视图；
  
    + 遍历collection：
  
    ```java
    @Test
    public void test6() {
          Map map = new HashMap();
        map.put("1", "张登");
          map.put("2", "如花");
      
          Collection values = map.values();
          for (Object val:values) {
              System.out.println(val);
          }
      }
    ```
  
  + 遍历成对的映射关系：
  
    + 为了能够用foreach或Iterator来迭代映射关系，只能把Map变成一个Collection系列的集合才可以；因为key不会重复，key+value也不会重复，把映射关系看成一个整体的对象，那么此时Map就变成了一个大的Set；一个key+value就是一个元素，这个元素是一个复杂的类型：Entry类型，这个类型是Map的内部类型；
  
    + Set entrySet()，元素是Entry类型，Entry的Map的内部类：返回Map集合中包含映射的Set视图；
  
    + 遍历Set；
  
    ```java
      @Test
    public void test7() {
          Map map = new HashMap();
        map.put("张登", "如花");
          map.put("季彭","如花");
          map.put("张三","如花");
      
          Set entrySet = map.entrySet();//这个Set中的元素是Entry类型
      
          for (Object obj:entrySet) {
              Map.Entry entry = (Map.Entry) obj;
              System.out.println(entry.getKey() + "->" + entry.getValue());
          }
      }
    ```
  
      ```java
      /*
      存储明星夫妻的姓名到Map中并遍历
      */
    import java.util.Collection;
      import java.util.HashMap;
      import java.util.Map;
      import java.util.Set;
      
      public class TestExer1 {
          public static void main(String[] args) {
              Map map = new HashMap();
              map.put("黄晓明","杨颖");
              map.put("冯绍峰","赵丽颖");
              map.put("邓超","孙俪");
      
              //遍历丈夫>妻子
              Set set = map.entrySet();
              for (Object obj:set) {
                  Map.Entry entry = (Map.Entry) obj;
                  System.out.println(entry.getKey() + ":" + entry.getValue());
              }
      
              //遍历妻子
              Collection values = map.values();
              for (Object val:values) {
                  System.out.println(val);
              }
      
              //遍历丈夫
              Set set1 = map.keySet();
              for (Object se:set1) {
                  System.out.println(se);
              }
          }
      }
      ```
  ```java
      /**
       * 存储学生对象到Map中，并遍历(编号，学生对象)
       * 编号是整数类型，学生对象是Student类型
       *Student{name,age}
     */
      
      import java.util.HashMap;
      import java.util.Map;
      import java.util.Set;
      
      @SuppressWarnings("all")
      public class TestExer2 {
          public static void main(String[] args) {
              Map map = new HashMap();
      
              map.put(1,new Student("张登",20));
              map.put(2,new Student("张锦茹",23));
              map.put(3,new Student("孟子怡",22));
      
              Set entrySet = map.entrySet();
              for (Object obj:entrySet) {
                  System.out.println(obj);
      
                  Map.Entry enty = (Map.Entry)obj;
                  System.out.println(enty);
              }
          }
      }
      
      class Student{
          private String name;
          private int age;
      
          public Student() {
          }
      
          public Student(String name, int age) {
              this.name = name;
              this.age = age;
          }
      
          @Override
          public String toString() {
              return "Student{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      '}';
          }
      }
  ```
  
      ```java
  /**
       * 存储小组信息到Map中，并遍历(组号，该组所有学生对象)
       * 组号是整数类型
       * 改组所有学生对象是多少人
       * XueSheng{name,age}
     */
      
      import java.util.ArrayList;
      import java.util.HashMap;
      import java.util.Map;
      import java.util.Set;
      
      @SuppressWarnings("all")
      public class TestExer3 {
          public static void main(String[] args) {
              Map map = new HashMap();
      
              ArrayList list1 = new ArrayList();
              list1.add(new XueSheng("李海",79));
              list1.add(new XueSheng("李恒",75));
      
              ArrayList list2 = new ArrayList();
              list2.add(new XueSheng("张勇",89));
              list2.add(new XueSheng("张锦茹",89));
      
              ArrayList list3 = new ArrayList();
              list3.add(new XueSheng("张登",89));
              list3.add(new XueSheng("珠珠",89));
      
              ArrayList list4 = new ArrayList();
              list4.add(new XueSheng("田硕",89));
              list4.add(new XueSheng("王佳慧",89));
      
              map.put("第一组",list1);
              map.put("第二组",list2);
              map.put("第三组",list3);
              map.put("第四组",list4);
      
              Set set = map.entrySet();
      
              for (Object obj:
                   set) {
                  Map.Entry enty = (Map.Entry)obj;
                  System.out.println("组号:" + enty.getKey());
                  System.out.println("该组的成员有：");
                  Object value = enty.getValue();
                  ArrayList list = (ArrayList) value;
                  for (Object xs:
                       list) {
                      System.out.println(xs);
                  }
              }
          }
      }
      
      class XueSheng{
          private String name;
          private int score;
      
          public XueSheng() {
          }
      
          public XueSheng(String name, int age) {
              this.name = name;
              this.score = age;
          }
      
          @Override
          public String toString() {
              return "XueSheng{" +
                      "name='" + name + '\'' +
                      ", age=" + score +
                      '}';
          }
      }
      ```

##### Map的实现类

###### Properties

+ Map中的一个实现类：java.util.Properties；
+ 特殊：它的key和value都是字符串；通常用在加载配置文件的地方；继承自Hashtable，相对于Hashtable是较新版本，在jdk1.2引入；线程不安全的；
+ 可以通过调用setProperty(key,value)添加一对配置信息，也可以在流中加载配置信息；

```java
import org.junit.Test;

import java.io.IOException;
import java.util.Map;
import java.util.Properties;
import java.util.Set;

@SuppressWarnings("all")
public class TestProperties {
    @Test
    public void test1(){
        Properties pro = new Properties();

        pro.setProperty("user","ouyang");
        pro.setProperty("password","123456");

        System.out.println(pro.getProperty("user"));
        System.out.println(pro.getProperty("password"));
    }

    @Test
    public void test2(){
        Properties pro = new Properties();
        try {
            //从jdbc.properties的文件中加载
            pro.load(ClassLoader.getSystemResourceAsStream("jdbc.properties"));
        } catch (IOException e) {
            e.printStackTrace();
        }

        System.out.println(pro.getProperty("user"));
        System.out.println(pro.getProperty("password"));
    }

    @Test
    public void test3(){
        //系统资源
        Properties pro = System.getProperties();
        Set entries = pro.entrySet();
        for (Object obj:
             entries) {
            System.out.println(entries);
        }
    }
}
```

###### TreeMap

+ 映射关系有顺序，按照key的大小顺序排列：

+ key必须实现java.lang.Comaprable接口，重写compareTo()方法；或在创建TreeMap时传一个实现了java.util.Comparator接口的实现类对象，从写compare(Object O1,Object o2)，作为定制排序的规则，这个方法中是用来为key类型的对象进行排序；

+ key不能重复，认为两个”相等“的key是同一个key，后进去的value会覆盖先添加进去的value；

  ```java
  import org.junit.Test;
  
  import java.util.Comparator;
  import java.util.Set;
  import java.util.TreeMap;
  
  @SuppressWarnings("all")
  public class TestMapImp1 {
      @Test
      public void TreeMap(){
          TreeMap tree = new TreeMap();
  
          //key是String,String实现了Comparable接口
          tree.put("Jack","18110081129");
          tree.put("Alice","18810881120");
          tree.put("Tom","18110081121");
          tree.put("Mack","18110081122");
          tree.put("John","18110081123");
  
          Set entrySet = tree.entrySet();
          for (Object obj:entrySet) {
              System.out.println(obj);
          }
      }
  
      @Test
      public void TreeMap2(){
          TreeMap tree = new TreeMap();
  
          tree.put(new Employee("Jack"),"18110081129");
          tree.put(new Employee("Alice"),"18810881120");
          tree.put(new Employee("Tom"),"18110081121");
          tree.put(new Employee("Mack"),"18110081122");
          tree.put(new Employee("John"),"18110081123");
  
          Set entrySet = tree.entrySet();
          for (Object obj:entrySet) {
              System.out.println(obj);//Employee{name='Jack'}=18110081123：Employee中的compareTo返回0,认为所有key相等;
          }
      }
  
      //通过定制比较器排序，实现了java.util.Compatator接口
      @Test
      public void TreeMap3(){
          TreeMap tree = new TreeMap(new Comparator() {
              @Override
              public int compare(Object o1, Object o2) {
                  Employee e1 = (Employee) o1;
                  Employee e2 = (Employee) o2;
                  return e1.getName().compareTo(e2.getName());
              }
          });
  
          tree.put(new Employee("Jack"),"18110081129");
          tree.put(new Employee("Alice"),"18810881120");
          tree.put(new Employee("Tom"),"18110081121");
          tree.put(new Employee("Mack"),"18110081122");
          tree.put(new Employee("John"),"18110081123");
  
          Set entrySet = tree.entrySet();
          for (Object obj:entrySet) {
              System.out.println(obj);//Employee{name='Jack'}=18110081123：Employee中的compareTo返回0,认为所有key相等;
          }
      }
  }
  
  class Employee implements Comparable{
      private String name;
  
      public Employee(String name) {
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      @Override
      public String toString() {
          return "Employee{" +
                  "name='" + name + '\'' +
                  '}';
      }
  
      @Override
      public int compareTo(Object o) {
          return 0;
      }
  }
  ```

###### LinkedHashMap

+ 是HashMap的子类，在HashMap的基础上又维护了前后映射关系的添加顺序，即遍历时会按照添加的顺序遍历；在添加和删除时，效率比HashMap要低；

###### Hashtable

+ 从jdk1.0开始，哈希表；线程安全的（它的线程安全靠synchronized<同步锁>实现的）；

###### <font color='red'>HashMap</font>

HashMap：散列存储，相对于HashMap的一个改版，jdk1.2引入；线程不安全

1. jdk1.7：底层存储的是数组+链表；

   + 当创建一个HashMap对象时，会先创建一个数组table，初始长度为16；

   + 当添加(put)一对映射关系(key,value)到HashMap中时，会计算出key的hashcode值，即调用hashcode()方法来计算；

   + 根据key的hash值，与数组的长度length进行运算，结果就得到了一个索引index，范围一定在[0，table.length-1]之间；

   + 此时就决定映射关系存入哪个数组的元素中table[index]；

   + 先判断table[index]位置是否为空，如果是空的，那么直接把这对映射关系封装为一个Entry对象放到table[index]中；

   + 如果table[index]不为空，用key和table[index]或者它下面的链表中的元素的key做equals比较，如果其中一个和新添加的key的equals返回true，说明key重复了，直接把新的value替换原来的value；

   + 如果新的映射关系的key和table[index]或者它下面的链表中的元素的key做equals比较，没有一个相等的，那么把新的映射关系封装为Entry的对象，放到table[index]中，原来table[index]及其下面的元素连接到新的这个后面，即新添加的作为链表头，再上面，原来的连接到后面；

   + 如果table这个数组的大部分（长度的0.75倍）都有元素了，这个时候会考虑扩容，数组长度扩大为原来的两倍；如果元素的特别均匀的存放，那么再0.75倍时不会扩容，元素个数与数组长度一致时才会扩容；如果元素不是均匀存放的，那么size达到数组长度的0.75倍时扩容；一旦扩容，原来HashMap中的所有的映射关系要全部重新计算位置。

2. jdk1.8：底层存储是数组+链表/红黑树；

   + 当创建一个HashMap对象时，会先创建一个数组table，初始长度为16；
   + 当添加(put)一对映射关系(key,value)到HashMap中时，会计算出key的hashcode值；
   + 根据key的hash值，与数组的长度length进行运算，结果就得到了一个索引index，范围一定在[0，length-1]之间；
   + 此时就决定映射关系存入哪个数组的元素中table[index]；
   + 先判断table[index]位置是否为空，如果是空的，那么直接把这对映射关系封装为一个Entry对象放到table[index]中；
   + 如果table[index]不为空，用key和table[index]或者它下面的链表、红黑树中的元素的key做equals比较，如果其中一个和新添加的key的equals返回true，说明key重复了，直接把新的value替换原来的value；
   + 如果新的映射关系的key和table[index]或者它下面的链表、红黑树中的元素的key做equals比较，没有一个相等的，那么：
     + 如果table[index]的下面是红黑树，那么把新的映射关系封装为TreeNode叶子节点，连接到这个红黑树的一个叶子节点上；
     + 如果table[index]的下面是链表，要看当前链表的元素的个数是否达到8个：
       + 如果没有达到8个，直接把映射关系封装为Node节点对象，连接到链表的尾部；
       + 如果达到8个，看数组的长度是否达到64，没有达到64，那么先扩容，把新的映射关系封装为Node（也属于Entry类型），连接到链表的后面（下面）；
       + 如果达到8个，而且数组的长度已经达到64，那么把当前的分支的链表，变成一棵树；把新的映射关系封装为TreeNode，连接到叶子上；
     + 如果总的size超过0.75也会扩容；
   + 如果在删除时，有可能存在从树变成链表的过程（当树中的节点个数小于6个，然后再删除时，就会变成链表）

##### hashcode与equals

+ 默认情况下，没有重写Object类中的hashcode与equals方法，那么Object中的hashcode方法根据对象的地址、属性信息等混合运算出来的一个整数值，equals相当于”==“；

+ 如果重写了Object类中的hashcode和equals方法，有一个要求，必须一起重写；而且所有参与equals比较的属性，也要参与hashcode的计算；

+ 如果对象存放到像Hash系列的容器中，如果是作为key放进去的，那么参与hash值计算的属性不能修改；所以实际开发中，一般用String/Integer作为key比较多；

+ hashcode和equals方法的关系的结论：

  + 如果两个对象的equals方法返回true，说明这两个对象是”相等“的，那么他们的hashcode值一定相等；

  + 如果两个对象的hashcode值不相等，那么这两个对象不需要调用equals方法，就算调用equals方法，一定返回false，即两者是不同的对象；

  + 如果两个对象的hashcode值相等，那么这个时候调用equals方法可能返回true，也可能返回false；

  + 不同的对象，hashcode值可能相等；相同的对象，hashcode值一定相等；

    ```java
    import java.util.Objects;
    
    public class TestHashcodeEquals {
        public static void main(String[] args) {
            System.out.println(new Teacher("欧阳"));
            System.out.println(new Teacher("上官"));
            System.out.println(new Teacher("西门"));
    
            Teacher t = new Teacher("欧阳");
            System.out.println(t.hashCode());
    
            String str1 = "Aa";
            String str2 = "BB";
            System.out.println(str1.hashCode());//2112
            System.out.println(str2.hashCode());//2112
        }
    }
    
    class Teacher{
        private String name;
        private int age;
    
        public Teacher(String name) {
            this.name = name;
        }
    
        @Override
        public boolean equals(Object o) {
            if (this == o) {
                return true;
            }
            if (o == null || getClass() != o.getClass()) {
                return false;
            }
            Teacher teacher = (Teacher) o;
            return age == teacher.age &&
                    name.equals(teacher.name);
        }
    
        @Override
        public int hashCode() {
            return Objects.hash(name, age);
        }
    }
    ```

#### 集合框架关系图

![集合框架关系图](images/grammar/集合框架图.png)

### 泛型

+ 泛型：参数化的类型；

+ 语法：

  ```java
  <泛型形参>：声明时叫的；
      class ArrayList<E>{}//E就是泛型形参/类型形参
  <泛型实参>：使用时叫的，必须是引用数据类型
      ArrayList<Integer> list = new ArrayList<Integer>()；//Integer就是泛型实参/类型实参；
      这里的E和Integer都是代表类型；E是代表未知的类型，Integer是具体的类型；
  ```

+ jdk1.5之前：所有的集合的元素都按照Object处理；jdk1.5之后，所有的集合可以通过泛型指定元素的具体类型，如果没有指定，还是按照Object处理；

+ 最初时，泛型是为集合服务，后来延伸到其他地方，只要是类型不确定，那么就可以把类型参数化；

+ 为什么要使用泛型：

  + 安全；
  + 简单；
  + 类型更灵活

#### 泛型的形式

##### 泛型类、泛型接口

###### 系统中的泛型类和泛型接口

java.util.Iterable<E>、

java.util.Collection<E>、

java.util.List<E>、

java.util.ArrayList<E>、

java.util.Vector<E>、

java.util.LinkedList<E>



java.util.Set<E>、

java.util.HashSet<E>、

java.util.TreeSet<E>、

java.util.LinkedHashSet<E>



java.util.Map<K,V>、

java.util.HashMap<K,V>、

java.util.TreeMap<K,V>、

java.util.LinkedHashMap<K,V>、

java.util.HashTable<K,V>



java.util.Iterator<E>、



java.lang.Comparable<T>、

java.util.Comparator<T>

```java
import org.junit.Test;
import sun.reflect.generics.tree.Tree;

import java.util.*;

public class TestGenericFenLei {
    @Test
    public void test(){
        ArrayList<String> list = new ArrayList<String>();
        list.add("Hello");
        list.add("World");

        String s = list.get(0);

        for (String str:list) {
            System.out.println(str);
        }

        Iterator<String> iter = list.iterator();
        while (iter.hasNext()){
            System.out.println(iter.next());
        }
    }

    @Test
    public void test2(){
        HashMap<Integer,Student> map = new HashMap<Integer,Student>();
        map.put(1,new Student("张登",20));

        //遍历所有的key
        Set<Integer> integers = map.keySet();
        for (Integer in:integers) {
            System.out.println(in);
        }

        //遍历所有的value
        Collection<Student> values = map.values();
        Iterator<Student> iterator = values.iterator();
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }

        //遍历所有的映射关系
        //Set的元素类型是Entry，Entry的key是Integer,value是Student
        Set<Map.Entry<Integer, Student>> entries = map.entrySet();
        for (Map.Entry<Integer, Student> entry : entries) {
            Integer key = entry.getKey();
            Student value = entry.getValue();
            System.out.println(key);
            System.out.println(value);
        }
    }

    @Test
    public void test3(){
        HashMap<String,ArrayList<Employee>> map = new HashMap<String,ArrayList<Employee>>();

        ArrayList<Employee> list = new ArrayList<Employee>();
        list.add(new Employee("张登"));
        list.add(new Employee("王凡"));

        map.put("第一组",list);

        Set<Map.Entry<String, ArrayList<Employee>>> entries = map.entrySet();
        for (Map.Entry<String, ArrayList<Employee>> entry : entries) {
            System.out.println(entry.getKey() + ":" + entry.getValue());
        }
    }

    @Test
    public void test4(){
        TreeSet<Staff> set = new TreeSet<Staff>();

        set.add(new Staff("jack",27));
        set.add(new Staff("Alice",25));

        for (Staff staff : set) {
            System.out.println(staff);
        }
    }
}

class Staff implements Comparable<Staff>{
    private String name;
    private int age;

    public Staff() {
    }

    public Staff(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Staff{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
    
    @Override
    public int compareTo(Staff o) {
        return this.age - o.age;
    }
}
```

###### 自定义的泛型类和泛型接口

+ 语法格式：

  ```java
  【修饰符】 class/interface 类名/接口名称<泛型形参列表>{
      泛型形参在类中可以作为属性的类型，可以作为方法的返回值类型，可以作为方法的形参类型使用；
  }
  ```

+ 类/接口上的泛型形参可以用于哪些位置（只能用于非静态成员中）：

  + 属性的类型
  + 方法的形参类型
  + 方法的返回值类型
  + 局部变量的类型

+ 这个类上的泛型形参：

  + 创建它的对象时，由泛型实参决定或按照Object处理；
  + 当子类继承父类时，可以指定父类的泛型；

+ 要求：

  + 泛型类/接口上的泛型形参，是不能指定为基本数据类型的；

  + 泛型类/接口上的泛型形参，是不能用于静态成员上的；

  + 泛型类/接口上的泛型形参，在声明时可以指定它的上限；

    ```java
    import org.junit.Test;
    
    /**
     * 声明一个学生类型，有姓名和成绩，数学老师登记成绩是按double类型登记，例如：87.5;
     * 语文老师登记成绩按int类型等级，例如：90;
     * 体育老师登记成绩是按照String类型，例如：合格、优秀、不合格；
     * 英语老师登记成绩是按照char类型，例如:A\B\C;
     */
    public class TestMyGenericClass {
        @Test
        public void test1() {
            XS x = new XS();//成绩score按照Object处理
            XS<Integer> xs = new XS<Integer>();//成绩score按照Integer处理
            EnglishXS e = new EnglishXS();//成绩按照Character处理
        }
    
        @Test
        public void test2(){
            //MyClass<String> my = new MyClass<String>();//因为String类型不是Person类型或它的子类,不能指定为String
            //MyClass<Animal> my = new MyClass<Animal>();//因为Animal类型不是Animal类型或它的子类,不能指定为Animal
            MyClass<Person> my1 = new MyClass<Person>();
            MyClass<Man> my2 = new MyClass<Man>();
        }
    }
    
    class XS<T>{
        private String name;
        private T score;
    
        public XS() {
        }
    
        public XS(String name, T score) {
            this.name = name;
            this.score = score;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public T getScore() {
            return score;
        }
    
        public void setScore(T score) {
            this.score = score;
        }
    
        @Override
        public String toString() {
            return "XS{" +
                    "name='" + name + '\'' +
                    ", score=" + score +
                    '}';
        }
    }
    
    class EnglishXS extends XS<Character>{
    
    }
    
    class Animal{
    
    }
    
    class Person extends Animal{
    
    }
    class Man extends Person{
    
    }
    //声明了泛型形参的上限，对应的泛型实参只能是Person或Person的子类
    class MyClass<T extends Person>{
    
    }
    ```


##### 泛型方法

+ 语法格式：

  ```java
  【修饰符】<泛型的形参列表> 返回值类型 方法名(形参列表) 抛出的异常列表{
      
  }
  ```

+ 说明：

  + 泛型方法中的泛型形参，只在这一个方法中有用，和其他方法无关；

  + 泛型方法可以是静态方法，也可以是非静态方法，和类是不是泛型类无关；

  + 泛型方法声明的泛型形参可以用于表示本方法的形参类型、或返回值类型、或局部变量类型；

  + 泛型方法同样不能是基本数据类型；

  + 泛型方法中的泛型形参代表的具体类型，是在调用这个方法时，由实参决定；

    ```java
    import java.util.Date;
    
    public class TestGenericMethod {
        public static void main(String[] args) {
            MyGenericClass m = new MyGenericClass();
            String hello = m.test1("hello");//"hello"是传给t的，那么t的类型T，由实参的类型决定
            Integer integer = m.test2(12);
    
            Date test = test(new Date());
    
            Other<String> t = new Other<String>();
            Integer t1 = Other.test(12);
        }
    
        //形参的值和类型都由实参决定
        public static <T> T  test(T t){
            return t;
        }
    }
    
    class  MyGenericClass{
        //这就是声明了一个泛型方法
        //以下两个方法的T，互不影响
        public <T> T test1(T t){
            return t;
        }
    
        public <T> T test2(T t){
            return t;
        }
    }
    
    class Other<T>{
        //类中的T和方法中的T无关
        //此时泛型方法中的T和类上的T也无关
        public static <T> T  test(T t){
            return t;
        }
    
        //此时用的就是类上的泛型
        public void method(T t){
    
        }
    
        //会引起误解，最好换一个字母
        public <U> void otherMethod(U u){
    
        }
    }
    
    /*
    比较两个参数的大小
    */
    public class TestGenericMethod2 {
        public static void main(String[] args) {
            int max = getMax(12, 41);
            System.out.println(max);
    
            String max1 = getMax("hello", "world");
            System.out.println(max1);
    
            Goods max2 = getMax(new Goods("鼠标", 699), new Goods("键盘", 799));
            System.out.println(max2);
        }
    
        public static int getMax(int a, int b){
            if (a > b) {
                return a;
            }else {
                return b;
            }
        }
    
        public static <T extends Comparable<T>> T getMax(T t1, T t2){
            if (t1.compareTo(t2) > 0){
                return t1;
            }else {
                return t2;
            }
        }
    }
    
    class Goods implements Comparable<Goods>{
        private String name;
        private double price;
    
        public Goods() {
        }
    
        public Goods(String name, double price) {
            this.name = name;
            this.price = price;
        }
    
        @Override
        public String toString() {
            return "Goods{" +
                    "name='" + name + '\'' +
                    ", price=" + price +
                    '}';
        }
    
        @Override
        public int compareTo(Goods o) {
            if (this.price > o.price) {
                return 1;
            }else if (this.price < o.price) {
                return -1;
            }else {
                return 0;
            }
        }
    }
    ```

#### 泛型通配符

泛型类、泛型接口没有通配符；泛型类、反省接口只能指定泛型的上线；

##### ?

+ 表示任意类型，可以接收任意类型的集合，但是这个集合list只能遍历，不能添加元素，因为？类型不确定

+ <font color='red'>泛型的<>是不包含多态的概念的类型，类型必须一致；</font>

+ add()方法只能添加null；

  ```java
  import java.util.ArrayList;
  
  public class TestWildcard {
      public static void main(String[] args) {
          ArrayList<Father> list1 = new ArrayList<Father>();
          ArrayList<Son> list2 = new ArrayList<Son>();
  
          test1(list1);
          test1(list2);
  
          //错误
          //test2(list1);//隐含ArrayList<Object> list = new ArrayList<Father>();
          //test2(list2);//隐含ArrayList<Object> list = new ArrayList<Son>();
          //不属于多态
          //ArrayList<Object> left = new ArrayList<String>();
      }
  
      //?代表这个集合的元素可以是任意类型，但是不确定
      public static void test1(ArrayList<?> list){
          //因为这里不能确定？的具体类型，因此这个list不能添加任何元素，除了null;
          //list.add("hello");//错误
          //list.add(12);//错误
          list.add(null);
  
          //遍历可以，按照Object处理
          for (Object o : list) {
  
          }
      }
  
      //表示元素的类型是Object
      public static void test2(ArrayList<Object> list){
          list.add("hello");
      }
  }
  
  class Father{
  
  }
  
  class Son extends Father{
  
  }
  ```

##### ? extends 父类

+ 表示上限，使用时指定的类型必须是继承某个类，或者实现某个接口，即<=；

+ 例如ArrayList<? extends T> list：可以接收ArrayList<T>、ArrayList<T的子类>的集合；

+ add()方法只能添加null；

  ```java
  import java.util.ArrayList;
  
  public class TestWildcard2 {
      public static void main(String[] args) {
          ArrayList<Object> list1 = new ArrayList<Object>();
          ArrayList<Fruit> list2 = new ArrayList<Fruit>();
          ArrayList<Apple> list3 = new ArrayList<Apple>();
          ArrayList<HongApple> list4 = new ArrayList<HongApple>();
          ArrayList<Pear> list5 = new ArrayList<Pear>();
  
          //test(list1);//错误，Object不是extends Fruit
          test(list2);
          test(list3);
          test(list4);
          test(list5);
      }
  
      public static void test(ArrayList<? extends Fruit> list){
          //不能添加，因为？不知道是什么类型，可能是Apple，也可能是Pear
          //list.add(new Apple());//错误
          
  		list.add(null);
          //遍历可以，按照Fruit遍历
          for (Fruit fruit : list) {
              
          }
      }
  }
  class Fruit{
  
  }
  
  class Apple extends Fruit{
  
  }
  
  class HongApple extends Fruit{
  
  }
  
  class Pear extends Fruit{
      
  }
  ```

##### ? super 子类

+ 表示下限，使用时指定的类型不能小于操作的类，即>=；

+ 例如ArrayList<? extends T> list：可以接收ArrayList<T>、ArrayList<T的父类>的集合；

+ 可以遍历，也可以添加元素，add()方法只能添加T和T的子类

  ```java
  import java.util.ArrayList;
  
  public class TestWildcard3 {
      public static void main(String[] args) {
          ArrayList<Object> list1 = new ArrayList<Object>();
          ArrayList<Car> list2 = new ArrayList<Car>();
          ArrayList<BWM> list3 = new ArrayList<BWM>();
          ArrayList<Benz> list4 = new ArrayList<Benz>();
          
          test(list1);
          test(list2);
          test(list3);
          //test(list4);//错误，Benz super BWM,不是
      }
      
      public static void test(ArrayList<? super BWM> list){
          //因为？最低是BWM类型
          list.add(new BWM());
          list.add(new MiniBWM());
  
          //遍历可以，不确定上到谁，按照Object
          for (Object o : list) {
              
          }
      }
  }
  
  class Car{
      
  }
  
  class BWM extends Car{
      
  }
  
  class MiniBWM extends BWM{
      
  }
  
  class Benz extends Car{
      
  }
  ```

#### 泛型的其他小点

+ 泛型没有多态；

+ 建议要么左右两边的泛型都一样，要么都不写；

  + jdk1.7可以进行简化

    ```java
    ArrayList<String> list3 = new ArrayList<>();//元素确定为String类型
    ```

+ 泛型类或接口不适合用于声明数组==>没有泛型数组；

+ 异常类型（try，throws）不能用泛型形参；

  ```java
  public class TestGenericOther {
      public static void main(String[] args) {
          ArrayList<String> list1 = new ArrayList<String>();
          ArrayList list2 = new ArrayList();//按照Object处理
  
          //jdk1.7可以进行简化；
          ArrayList<String> list3 = new ArrayList<>();//元素确定为String类型
  
          //NewPerson<String>[] array = new NewPerson<String>[5];//错误
          //NewPerson[] array2 = new NewPerson[5];//警告
      }
  }
  
  class NewPerson<T>{
  
  }
  ```

#### Collections工具类

Collections 是一个操作 Set、List 和 Map 等集合的工具类；

Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法；

+ public static <T> boolean addAll(Collection<? super T> c,T... elements)：将所有指定元素添加到指定 collection 中；

  ```java
  @Test
  public void test1(){
      ArrayList<String> list = new ArrayList<String>();
  
      Collections.addAll(list,"hello","world");//T是String类型，?也是String类型
      //Collections.addAll(list,1,2,3);//错误，T是Integer，?是String
  
      ArrayList<Object> list2 = new ArrayList<Object>();
      Collections.addAll(list2,"hello","world");//T是String类型，?是Object类型,? super String
      Collections.addAll(list2,1,2,3);//T是Integer,?是Object，? super Integer
  
      for (Object o : list2) {
          System.out.println(o);
      }
  }
  ```

+  public static <T> int binarySearch(List<? extends Comparable<? super T>> list,T key)：在List集合中查找某个元素的下标，但是List的元素必须是T或T的子类对象，而且必须是可比较大小的，即支持自然排序的。而且集合也事先必须是有序的，否则结果不确定；

+ public static <T> int binarySearch(List<? extends T> list,T key,Comparator<? super T> c)：在List集合中查找某个元素的下标，但是List的元素必须是T或T的子类对象，而且集合也事先必须是按照c比较器规则进行排序过的，否则结果不确定；

+ public static <T extends Object & Comparable<? super T>> T max(Collection<? extends T> coll)：在coll集合中找出最大的元素，集合中的对象必须是T或T的子类对象，而且支持自然排序；

  ```java
  @Test
  public void test2(){
      //public static <T extends Object & Comparable<? super T>> T max(Collection<? extends T> coll)
      //public static T max(Collection coll):在coll集合中找出最大值
      List<Integer> list = Arrays.asList(1, 2, 3, 4, 52, 35, 21, 6);
  
      Integer max = Collections.max(list);
      System.out.println(max);
  
      List<Student> list2 = Arrays.asList(new Student(), new Student(), new Student());
      //Collections.max(list2);//报错的原因是Student没有实现Comparable
  }
  ```

+  public static <T> T max(Collection<? extends T> coll,Comparator<? super T> comp)：在coll集合中找出最大的元素，集合中的对象必须是T或T的子类对象，按照比较器comp找出最大者；

+ public static void reverse(List<?> list)：反转指定列表List中元素的顺序；

+  public static void shuffle(List<?> list) List ：集合元素进行随机排序，类似洗牌；

+ public static <T extends Comparable<? super T>> void sort(List<T> list)：根据元素的自然顺序对指定 List 集合元素按升序排序；

+ public static <T> void sort(List<T> list,Comparator<? super T> c)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序；

+ public static void swap(List<?> list,int i,int j)：将指定 list 集合中的 i 处元素和 j 处元素进行交换；

+ public static int frequency(Collection<?> c,Object o)：返回指定集合中指定元素的出现次数；

+ public static <T> void copy(List<? super T> dest,List<? extends T> src)：将src中的内容复制到dest中；

+ public static <T> boolean replaceAll(List<T> list，T oldVal，T newVal)：使用新值替换 List 对象的所有旧值；

+ Collections 类中提供了多个 synchronizedXxx() 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题；

  ```java
  @Test
  public void test3(){
      ArrayList<String> list = getList();
          
      //如果下面的操作需要线程安全的
      //把list变成线程安全的
      //其中一种解决方案如下，newList就是线程安全的
      List<String> newList = Collections.synchronizedList(list);
  }
      
  public ArrayList<String> getList(){
      ArrayList<String> list = new ArrayList<>();
      return list;
  }
  ```

+ public static <T> List<T> unmodifiableList(List<? extends T> list)：返回指定列表的不可修改视图。 该方法允许模块向用户提供对内部列表的“只读”访问。将返回的列表上的查询操作“读取”到指定的列表，并尝试修改返回的列表，无论是直接还是通过其迭代器，都会导致UnsupportedOperationException；

  ```java
  @Test
  public void test4(){
      ArrayList<String> list = new ArrayList<String>();
      list.add("Hello");
  
      //希望把list变成只读的集合
      List<String> newList = Collections.unmodifiableList(list);
      newList.add("world");//UnsupportedOperationException,因为newList现在是只读的，不能修改
  }
  ```

### 文件与IO

IO：输入和输出，Input、Output、数据的输入和输出；

其中一种方式就是文件的读和文件的写，从文件输入、输出到文件；

#### java.io.File类

java.io.File类型：文件和目录的路径名的抽象表示形式；

不管是文件还是目录（文件夹）都是用File表示；

不管是文件还是目录都是用路径名表示；

不管是文件还是目录，都是File的对象；

```java
import org.junit.Test;

import java.io.File;

public class TestFile {
    @Test
    public void test1(){
        File dir = new File("F:/notebook/gitbook");
        File file = new File("F:/notebook/gitbook/SUMMARY.md");//绝对路径

        System.out.println(File.separator);

        File dir2 = new File("D:" + File.separator + "notebook" + File.separator + "gitbook");
    }

    @Test
    public void test2(){
        File dir = new File("F:/notebook/gitbook");//绝对路径
        File dir2 = new File("gitbook/SUMMARY.md");//相对路径

        System.out.println(dir2.getAbsolutePath());
        System.out.println(dir2.getPath());
    }
}
```

##### File的常用方法

+ 获取名称
  
+ getName()：获取文件名；
  
+ 获取路径

  + getPath()：路径，文件原来的路径是什么，结果就是什么；

  + getAbsolutePath()：获取绝对路径；

    ```java
    @Test
    public void test1() throws IOException {
        File file = new File("day21_上课资料\\day21_note\\day21_mornig.txt");
        String name = file.getName();
        System.out.println("文件名" + name);
    
        System.out.println("文件的路径：" + file.getPath());//不区分绝对和相对
        System.out.println("文件的路径：" + file.getAbsolutePath());//绝对路径
    
        System.out.println("规范路径：" + file.getCanonicalPath());
        File file1 = new File("day21_上课资料\\..\\day21_mornig.txt");
        System.out.println("规范路径：" + file1.getCanonicalPath());//把..规范化，去掉..，正确解释为他的上一级
    }
    ```

+ 是否存在：

  + exists()：判断文件是否存在，返回boolean<文件的路径需要是绝对路径>

+ 是否是文件或目录：

  + isFile()：当且仅当它存在，并且是个文件才返回true，否则返回false；

  + isDirectory()：当且仅当它存在，并且是个目录才返回true，否则返回false；

    ```java
    @Test
    public void test3(){
        File file = new File("F:\\javavideo\\note\\day21_上课资料\\day21_note\\day21_mornig.txt");
        print(file);
     }
    
    public void print(File file){
        if (file.isFile()){
            System.out.println("是一个文件");
        } else if (file.isDirectory()){
            System.out.println("是一个目录");
        }else{
            System.out.println("既不是文件也不是目录");
        }
    }
    ```

+ 输出上层目录：

  + getParent()：返回此抽象路径名父目录的路径名字符串，只能获取一级；如果没有指定父目录，返回null；

  + getParentFile()：返回此抽象路径名父目录的抽象路径名，如果此路径没有指定父目录，返回null；

    ```java
    @Test
    public void test4(){
        File file = new File("F:\\javavideo\\note\\day21_上课资料\\day21_note\\day21_mornig.txt");
        System.out.println("上一级" + file.getParent());
        File p = file.getParentFile();
        System.out.println(p.getParent());
    
        File file1 = new File("download/1.txt");
        System.out.println(file1.getParent());
    }
    ```

+ 属性判断：

  + isHidden()：是否隐藏；
  + canRead()：是否可读；
  + canWrite()：是否可写；
  + isExecute()：是否可执行；

+ 文件的大小：

  + length()：返回文件的大小，字节，如果文件不存在，返回0；如果此抽象路径表示一个路径，则返回值是不确定的；

+ 获取目录的下一级：

  + list()：返回值类型是String[]；

  + listFiles()：返回值类型是File[]；

    ```java
    @Test
    public void test7() {
        File dir = new File("D:/PCSoftWare");
        listDir(dir);
    
        long dirSize = getDirSize(dir);
        System.out.println(dirSize);
    }
    
    public long getDirSize(File file){
        if (file.isFile()){
            return file.length();
        }else if (file.isDirectory()){
            long sum = 0;
            //把file的所有的下一级的大小全部累加起来
            File[] subfiles = file.listFiles();
            for (File sub : subfiles) {//sub是file的下一级
                sum += getDirSize(sub);
            }
            return sum;
        }else{
            return 0;
        }
    }
    
     /**
     * 如果file是文件，打印它，如果file是目录，列出它的下一级
     * @param file
     */
    public void listDir(File file){
        if (!file.isDirectory()){
            System.out.println(file);
        }else {
            File[] subfiles = file.listFiles();
            for (File sub : subfiles) {
                //对于每一个sub来说，sub可能是一个文件，也可能是目录，如果是目录，继续列出下一级
                listDir(sub);//递归，自己调用自己
            }
        }
    }
    ```

  + 递归：

    ```java
    public class TestDiGui {
    
        public static void main(String[] args) {
            int sum = getSum(10);
            System.out.println(sum);
        }
        /**
         * 计算的是0-n的累加和
         * @return
         */
        public static int getSum(int n){
            int sum = 0;
            if (n != 0){
                sum += n + getSum(n-1);
                return sum;
            }else {
                return 0;
            }
        }
    }
    ```

+ 获取最后修改时间：

  + lastModified()：返回值是long类型，毫秒数；

    ```java
    @Test
    public void test8(){
        File file = new File("F:\\javavideo\\note\\day21_上课资料\\day21_note\\day21_mornig.txt");
        long time = file.lastModified();
        System.out.println(time);
    
        Date date = new Date(time);
        System.out.println(date);
    
        SimpleDateFormat s = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String format = s.format(date);
        System.out.println(format);
    }
    ```

+ 文件和目录的操作：

  + 创建文件：creatNewFile()，要求文件的父目录是存在的；

    ```java
    @Test
        public void test1(){
            File file = new File("download/1.txt");
            try {
                file.createNewFile();//想要创建的是1.txt
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    ```

  + 创建目录：

    + mkdir()：创建一级目录；

    + mkdirs()：创建多级目录；

      ```java
      @Test
      public void test2(){
          File file = new File("download");
          file.mkdir();
      }
      
      @Test
      public void test3(){
          File file = new File("myjava/io/file");
          file.mkdirs();
      }
      ```

  + 删除文件：delete()；

    ```java
    @Test
    public void test4(){
        File file = new File("download/1.txt");
        file.delete();
    }
    ```

  + 删除目录：delete()：

    + 只能删除空目录；

  + 重命名：renameTo()，谨慎使用，如果文件系统格式不一样，移动有问题

    ```java
    @Test
    public void test5() throws IOException {
        File file = new File("download/1.txt");
        file.createNewFile();
        File file2 = new File("myjava/io/2.txt");
        file.renameTo(file2);
    }
    ```


#### IO流概述

IO：数据传输的过程，IO流、数据流动；

+ 分类：
  + 根据方向：
    + 输入流：从输入流中只读数据；
    + 输出流：只能往输出流写数据；
  + 根据数据的处理方式：
    + 字节流：以字节为单位，byte；
    + 字符流：以字符为单位，char，和字符编码方式有关，有的一个char对应一个byte，有的一个char对应2个字节，有的一个char对应3个字节；只能处理纯文本数据，例如：.java，.txt，.js，.xml等；非纯文本文件：.doc，.exe，.zip，.MP4，.avi...；
  + 根据IO流的功能不同：
    + 节点流：负责和节点相连接，例如：文件流；
    + 处理流：负责在节点流的基础上增加其他辅助功能，例如：编码与解码功能、缓存功能、序列化功能等；
      + 缓冲流：增加缓冲区，期望提高效率(8198是最合适的缓冲区，new byte[]，new char[] 数组的长度一般是以8的倍数进行)
      + 转换流：编码（字符-->字节）与解码（字节-->字符）；

IO流：装饰者设计模式

+ IO流的四个抽象基类/抽象父类：
  + InputStream：所有字节输入流的根父类；
    + int read()：读取一个字节；
    + int read(byte[] data)：读取多个字节，最多读data.length个；读取后的数据存在data数组中，从[0]开始存储；
    + int read(byte[] data,int offset,int len)：读取多个字节，最多读len个；读取后的数据存在data数组中，从[offset]开始存储；
    + 如果到达流末尾，返回-1；
    + close()；
  + OutputStream：所有字节输出流的根父类；
    + write()：写一个字节；
    + write(byte[] data)：把整个字节数组中的数据全部写到输出流中；
    + write(byte[] data,int start, int len)：把data字节数组，从data[start]开始，一共写len个；
    + close()；
  + Reader：所有字符输入流的根父类，例如阅读read；
    + int read()：读取一个字符，返回这个字符的Unicode码；
    + int read(char[] data)：读取多个字符，最多读data.length个；读取后的数据存在data数组中，从[0]开始存储；
    + int read(char[] data,int offset,int len)：读取多个字节，最多读len个；读取后的数据存在data数组中，从[offset]开始存储；
    + 如果到达流末尾，返回-1；
    + close()；
  + Writer：所有字符输出流的根父类，例如写write；
    + write()：写一个字节；
    + write(char[] data)：把整个字符数组中的数据全部写到输出流中；
    + write(char[] data,int start, int len)：把data字节数组，从data[start]开始，一共写len个；
    + write(String str)：把整个字符串写到输出流中；
    + write(String str,int start, int len)：把字符串写到输出流中，从str的[start]索引开始，一共写len个；
    + close()；
    + flush()：
+ 和文件相关的有四个：
  + FileInputStream;
  + FileOutputStream;
  + FileReader;
  + FileWriter;

##### 文件流

###### FileInputStream

1. 作用：文件的字节输入流，从文件读取到程序中，从文件加载数据，可以读取任意类型的文件；数据的读和写都只能针对文件，不针对目录；

2. 方法：

   + 如果InputStream中没有数据可读，则返回-1；

   + int Read()：一次读取一个字节，返回该字节的值；

   + int Read(byte[] data)：一次读取多个字节，返回本次读取的总字节数，数据读完后存到byte[]数组中，从data[0]开始存储；最多可以读取data.length，也可能少于data.length个；

   + int Read(byte[] data,int offset,int len)：一次读取多个字节，返回本次读取的总字节数，数据读完后存到byte[]数组中，从data[offset]开始存储；最多可以读取len个字节，也可能少于len个；

     ```java
     import java.io.File;
     import java.io.FileInputStream;
     import java.io.FileNotFoundException;
     import java.io.IOException;
     import java.util.Arrays;
     
     public class TestFileInputStream {
         //public static void main(String[] args) throws FileNotFoundException,IOException {
         //因为FileNotFoundException是IOException的子类，所以抛出IOException即可；
         public static void main(String[] args) throws IOException{
             //1、创建一个输入流
             File file = new File("src/day22/io/first.txt");
             FileInputStream fis = new FileInputStream(file);
     
             FileInputStream fis2 = new FileInputStream("src/day22/io/first.txt");
     
             //2、读取数据
             //(1)一次读取一个字节
             int data = fis.read();//返回这个字节的值
             System.out.println(data);//104
     
             //(2)一次读取多个字节
             byte[] data1 = new byte[10];
             int len = fis.read(data1);
             System.out.println("本次读取了" + len + "个字节");
             System.out.println(Arrays.toString(data1));
     
             //如果想要在控制台显示，需要解码：把字节变成字符
             String string = new String(data1);
             System.out.println(string);
         }
     }
     ```

     ```java
     import java.io.FileInputStream;
     import java.io.FileNotFoundException;
     import java.io.IOException;
     
     public class TestFileInputStream2 {
         public static void main(String[] args) throws IOException {
             //1、创建一个输入流
             FileInputStream fis = new FileInputStream("src/day22/io/first.txt");
     
             //2、读取全部的数据
     //        while (true){
     //            int data =fis.read();
     //            if (data == -1) {
     //                break;
     //            }
     //            System.out.println(data);
     //        }
     
     //        StringBuilder sb = new StringBuilder();
     //        byte[] data = new byte[10];
     //        while (true){
     //            int len = fis.read(data);
     //            if (len == -1) {
     //                break;
     //            }
     //            //System.out.println(new String(data,0,len));
     //            sb.append(new String(data,0,len));
     //        }
     //        System.out.println(sb);
     
             StringBuilder sb = new StringBuilder();
             byte[] data = new byte[10];
             int len;
             while ((len = fis.read(data)) != -1){
                 sb.append(new String(data,0,len));
             }
             System.out.println(sb);
     
             //3、释放资源
             fis.close();
         }
     }
     ```


###### FileOutputStream

1. 文件的字节输出流；

   + 如果仅是文件不存在，它会自动创建这个文件；
   + 如果这个文件的上层目录也不存在，则会报错FileNotFoundException；

2. 方法：

   + write(int)：写一个字节；

   + write(byte[] data)：把整个字节数组都写进去；

   + write(byte[] data,int offset,int len)：从data[offset]开始写len个字节；

     ```java
     import java.io.FileNotFoundException;
     import java.io.FileOutputStream;
     import java.io.IOException;
     
     public class TestFileOutputStream {
         public static void main(String[] args) throws IOException {
             //1、创建输出流
             FileOutputStream fos = new FileOutputStream("src/day22/io/info.txt");
             //创建输出流对象FileOutputStreaam
             //如果仅仅是info.txt不存在，他会自动创建这个文件
             //如果io/info.txt文件和文件夹都不存在，报错FileNotFoundException
     
             //2、写数据
             //a
             int data = 'a';
             fos.write(data);//将指定的字节写入此输出流
     
             String str = "very good";
             //把字符变成字节：编码
             byte[] bytes = str.getBytes();//按照平台默认的字符编码方式进行编码
     
             fos.write(bytes);
     
             byte[] bt = new byte[10];
             bt[0] = 97;
             bt[1] = 98;
             //只想写两个字节
             fos.write(bt,0,2);
     
             //3、释放资源
             fos.close();
         }
     }
     ```

###### FileReader

1. 字符输入流：如果明确要处理的文件的纯文本文件，那么使用字符流更合适；

2. <font color='red'>只能读纯文本文件，而且只能读与平台默认的字符集一致的纯文本文件</font>；

   ```java
   import java.io.FileNotFoundException;
   import java.io.FileReader;
   import java.io.IOException;
   
   public class TestFileReader {
       public static void main(String[] args) throws IOException {
           //读文件
           //1、创建字符输入流
           FileReader fr = new FileReader("src/day22/io/info.txt");
   
   //        //2、读取数据
   //        int read = fr.read();//一次一个字符,返回的是读取字符对应的Unicode值
   //        System.out.println(read);//97,a的Unicode编码值
   //        int num = 'a';
   //        System.out.println(num);
   
           char[] data = new char[5];
           int len = fr.read(data);
           System.out.println("本次读取了：" + len + "个字符");
           System.out.println(new String(data,0,len));
   
           //3、释放资源
           fr.close();
       }
   }
   ```

###### FileWrite

1. 字符输出流：<font color='red'>只能写纯文本文件，而且只能按照平台默认的字符集处理编码方式</font>；

2. 将写的数据刷出的方法：

   + fw中有一个非常小的缓冲区，如果满了，会自动把数据写到文件中；
   + fw.flush()手动刷出去；
   + fw.close()关闭输出流，也会自动把数据刷出去

   ```java
   import java.io.FileWriter;
   import java.io.IOException;
   
   public class TestFileWrite {
       public static void main(String[] args) throws IOException {
           //创建文件的字符输出流
           FileWriter fw = new FileWriter("src/day22/io/info.txt");
   
           //2、写数据
           fw.write('b');
   
           //(1)fw中有一个非常小的缓冲区，如果满了，会自动把数据写到文件中
           //(2)fw.flush()手动刷出去
           //(3)关闭输出流，也会自动把数据刷出去
           //fw.flush();
   
           String str = "稍等，马上吃饭";
           fw.write(str);
           fw.write(str,1,2);
   
           //3、释放资源，当释放资源时，会把fw中的所有数据写到文件中
           fw.close();
       }
   }
   ```


##### 文件的复制

###### 字节流

1. 创建输入流和输出流；

   ```java
   FileInputStream fis = null;
   FileOutputStream fos = null;
   ```

2. 一边读一边写；

   + 数据先从fis输入流中读取到data，然后在从data写到fos中；

   ```java
   byte[] data = new byte[10];//用来转移、运送数据的,影响速度
   //数据先从fis输入流中读取到data，然后在从data写到fos中
   int len;
   //len=fis.read(data)把数据从fis读取到data中，每次读取了len个字节
   while ((len = fis.read(data)) != -1){
   	//从data[0]中把数据写到fos中，每次写len个字节，每次写len个字节
   	fos.write(data,0,len);
   }
   ```

   ```java
   import org.junit.Test;
   
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   
   public class TestFileCopy {
       @Test
       public void test1() {
           //复制io下的动漫.MP4,是一个非纯文本文件，只能使用字节流
           //io/视频.avi→myjava/视频.avi
           //1、创建输入流、输出流
           FileInputStream fis = null;
           FileOutputStream fos = null;
           try {
               fis = new FileInputStream("src/day22/io/视频.avi");
               fos = new FileOutputStream("src/day22/myjava/视频.avi");
   
               //2、一边读一边写
               byte[] data = new byte[10];//用来转移、运送数据的,影响速度
               //数据先从fis输入流中读取到data，然后在从data写到fos中
               int len;
               //len=fis.read(data)把数据从fis读取到data中，每次读取了len个字节
               while ((len = fis.read(data)) != -1){
                   //从data[0]中把数据写到fos中，每次写len个字节，每次写len个字节
                   fos.write(data,0,len);
               }
           } catch (FileNotFoundException e) {
               e.printStackTrace();
           } catch (IOException e) {
               e.printStackTrace();
           } finally {
               try {
                   if (fis != null) {
                       fis.close();
                   }
                   if (fos != null) {
                       fos.close();
                   }
               } catch (IOException e) {
                   e.printStackTrace();
               }
           }
       }
   }
   ```

###### 字符流

1. 创建输入流和输出流；
2. 一边读一边写；

```java
import org.junit.Test;

import java.io.*;

public class TestFileCopy {
    @Test
    public void test2(){
        //day22/TestFileInputStream.java复制到myjava/TestFileInputStream.java
        FileReader fr = null;
        FileWriter fw = null;
        try {
            fr= new FileReader("src/day22/TestFileInputStream.java");
            fw = new FileWriter("src/day22/myjava/TestFileInputStream.java");

            char[] data = new char[1024];
            int len;

            while((len = fr.read(data)) != -1){
                fw.write(data,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fr != null) {
                    fr.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (fw != null){
                    fw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

##### 文件的工具类

###### 抽取文件复制

```java
import java.io.*;

public class FileUtils {
    public static void main(String[] args) {
        try {
            copyFile("io/视频.avi","myjava/视频.avi");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * 将源文件复制到目标文件
     * @param src 源文件
     * @param desc 目标文件
     * @throws IOException
     */
    public static void copyFile(File src,File desc) throws IOException {
        FileInputStream fis = new FileInputStream(src);
        FileOutputStream fos = new FileOutputStream(desc);

        byte[] data = new byte[1024];
        int len;
        while ((len = fis.read(data)) != -1){
            fos.write(data,0,len);
        }

        fis.close();
        fos.close();
    }

    /**
     * 将源文件路径复制到目标文件路径
     * @param srcPath 源文件路径
     * @param descPath 目标文件路径
     * @throws IOException
     */
    public static void copyFile(String srcPath,String descPath) throws IOException {
//        //方法一：
//        FileInputStream fis = new FileInputStream(srcPath);
//        FileOutputStream fos = new FileOutputStream(descPath);
//
//        byte[] data = new byte[1024];
//        int len;
//        while ((len = fis.read(data)) != -1){
//            fos.write(data,0,len);
//        }
//
//        fis.close();
//        fos.close();

        //方法二：
        File src = new File(srcPath);
        File desc = new File(descPath);
        copyFile(src,desc);
    }
}
```

###### 抽取目录复制

```java
import java.io.*;

public class TestDirCopy {
    public static void main(String[] args) throws IOException {
        copyDir(new File("io"),new File("myjava"));
    }

    /**
     * 把src所在的文件夹复制到desc中
     * @param src
     * @param dest
     */
    public static void copyDir(File src, File dest) throws IOException {
        //src现在是文件夹，desc也是文件夹
        //在myjava中建立一个io的文件夹，新文件夹的路径：myjava/io
        if (src.isDirectory()) {
            //1、在desc中建立一个src代表的文件夹
            File newDesc = new File(dest.getPath() + "/" + src.getName());
            newDesc.mkdir();

            //2、把src中的下一级，一一复制到newDest中
            File[] listFiles = src.listFiles();
            for (File sub : listFiles) {
                //把sub复制到newDest中
                copyDir(sub,newDesc);
            }
        }else if (src.isFile()) {
            //src文件放到dest中,src是文件，dest是文件夹
            FileInputStream fis = new FileInputStream(src);
            FileOutputStream fos = new FileOutputStream(dest.getParentFile() + "/" + src.getName());

            byte[] data = new byte[1024];
            int len;
            while ((len = fis.read(data)) != -1){
                fos.write(data,0,len);
            }

            fis.close();
            fos.close();
        }
    }
}
```

###### 文件的追加

在输出流中添加boolean类型的参数；

```java
import java.io.FileWriter;
import java.io.IOException;

public class TestAppend {
    public static void main(String[] args) throws IOException {
        String info = "我陪你去看电影";
        FileWriter fw = new FileWriter("src/day22/io/info.txt",true);
        fw.write(info);
        fw.close();
    }
}
```

##### try...with_resource:资源自动关闭

1. 语法：

   ```java
   try(需要关闭的资源的声明)
   {
       对资源的操作，可能发生异常的逻辑代码
   }catch（异常类型 e）{
       处理异常的代码
   }catch（异常类型 e）{
       处理异常的代码
   }
   ```

2. 作用：资源不需要关闭，不管是否发生异常，都会自动关闭

   ```java
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   
   public class TestTryWithResource {
       public static void main(String[] args) {
           //1、创建输入流、输出流
           try (FileInputStream fis = new FileInputStream("src/day22/io/视频.avi");
                FileOutputStream fos = new FileOutputStream("src/day22/myjava/视频.avi")
           ) {
               //2、一边读一边写
               byte[] data = new byte[10];//用来转移、运送数据的,影响速度
               //数据先从fis输入流中读取到data，然后在从data写到fos中
               int len;
               //len=fis.read(data)把数据从fis读取到data中，每次读取了len个字节
               while ((len = fis.read(data)) != -1){
                   //从data[0]中把数据写到fos中，每次写len个字节，每次写len个字节
                   fos.write(data,0,len);
               }
           } catch (FileNotFoundException e) {
               e.printStackTrace();
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   }
   ```

##### 缓冲流

1. 缓冲流（处理流）：
   + BufferedInputStream：针对InputStream系列的IO流进行缓冲；

     ```java
     FileInputStream fis = new FileInputStream("...");
     BufferedInputStream bis = new BufferedInputStream(fis);
     ```

   + BufferedOutputStream：针对OutputStream系列的IO流进行缓冲；

     ```java
     FileOutputStream fos = new FileOutputStream("...");
     BufferedOutputStream bos = new BufferedOutputStream(fos);
     ```

   + BufferedReader：针对Reader系列的IO流进行缓冲；

     ```java
     FileReader fr = new FileReader("...");
     BufferedReader br = new BufferedReader(fr);
     ```

     + 可以包装InputStreamReader的对象：

       ```java
       FileInputStream fis = new FileInputStream("...");
       InputStreamReader isr = new InputStreamReader(fis);
       BufferedReader br = new BufferedReader(isr);
       ```

     + 常用的方法：

       + 除了从Reader集成的方法外：
       + <font color='red'>String ReaderLine()：如果到达流末尾，返回null</font>；

   + BufferWriter：针对Writer系列的IO流进行缓冲；

     ```java
     FileWriter fw = new FileWriter("...");
     BufferedWriter bw = new BufferedWriter(fw);
     ```

     + 可以包装OutputStreamWriter的对象：

       ```java
       FileWriter fw = new FileWriter("...");
       OutputStreamWriter osw = new OutputStreamWriter(fw);
       BufferedWriter bw = new BufferedWriter(osw);
       ```

     + 常用的方法：

       + 除了从Write继承的方法外：
       + newLine()：写一个换行符；
2. 目的：缓冲流的作用是为了增加效率；
3. 比喻：缓冲区比如送水的车，一车可以运多桶水；如果没有缓冲区，相当于一次运一桶水；
4. 缓冲流的缓冲区默认大小是8192（8×1024）个字节或字符；

###### 字节缓冲流

```java
import org.junit.Test;

import java.io.*;

public class TestBuffer {
    @Test
    public void test1() throws FileNotFoundException {
        //复制文件
        FileInputStream fis = null;
        FileOutputStream fos = null;

        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;

        try {
            //节点流
            fis = new FileInputStream("src/day22/io/视频.avi");
            fos = new FileOutputStream("src/day22/myjava/视频.avi");

            //处理流，处理流需要包装节点流
            bis = new BufferedInputStream(fis);//bis看成套在fis的外面，先new的fis，
            bos = new BufferedOutputStream(fos);//bos看成套在fos的外面

            //此时数据已经从fis-bis中；
            //数据从bis中读取

            byte[] data = new byte[1024];
            int len;
            while ((len = bis.read(data)) != -1){
                //数据先写到bos中，然后等缓冲区满了会一次写到fos中
                bos.write(data,0,len);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (bis != null) {
                    bis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (bos != null){
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (fis != null){
                    fis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (fos != null){
                    fos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    @Test
    public void test2() throws FileNotFoundException {
        //复制文件
        try(FileInputStream fis = new FileInputStream("src/day22/io/视频.avi");
            FileOutputStream fos = new FileOutputStream("src/day22/myjava/视频.avi");

            BufferedInputStream bis = new BufferedInputStream(fis);
            BufferedOutputStream bos = new BufferedOutputStream(fos)
             ) {
            byte[] data = new byte[1024];
            int len;
            while ((len = bis.read(data)) != -1) {
                //数据先写到bos中，然后等缓冲区满了会一次写到fos中
                bos.write(data, 0, len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    
    @Test
    public void test3(){
        try(
                //fis、fos使用匿名对象
            BufferedInputStream bis = new BufferedInputStream(new FileInputStream("src/day22/io/视频.avi"));
            BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("src/day22/myjava/视频.avi"))
        ) {
            byte[] data = new byte[1024];
            int len;
            while ((len = bis.read(data)) != -1) {
                //数据先写到bos中，然后等缓冲区满了会一次写到fos中
                bos.write(data, 0, len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

###### 字符缓冲流

```java
import org.junit.Test;
import java.io.*;

public class TestBuffer2 {
    @Test
    public void test1() {
        //纯文本文件才能用字符缓冲流
        try (FileReader fr = new FileReader("src/day22/io/first.txt");
             FileWriter fw = new FileWriter("src/day22/io/second.txt");

             BufferedReader br = new BufferedReader(fr);
             BufferedWriter bw = new BufferedWriter(fw);) {

            char[] data = new char[1024];
            int len;
            while ((len = br.read(data)) != -1) {
                bw.write(data, 0, len);
            }
        } catch (IOException e1) {
            e1.printStackTrace();
        }
    }

    @Test
    public void test2(){
        try (FileReader fr = new FileReader("src/day22/io/first.txt");
             FileWriter fw = new FileWriter("src/day22/io/third.txt");

             BufferedReader br = new BufferedReader(fr);
             BufferedWriter bw = new BufferedWriter(fw);) {

            String line;
            while ((line = br.readLine()) != null){
                bw.write(line);
                //进行换行
                //bw.write("\r\n");
                bw.newLine();
            }
        } catch (IOException e1) {
            e1.printStackTrace();
        }
    }
}
```

##### 转换流

+ InputStreamReader：把字节流转成字符流，可以指定解码的字符集；

  + 其他IO流先把字节的数据传给InputStreamReader，然后我们从它中读取，就变成了读取字符流；

  + 可以在构造它的对象时，传字符编码方式；

    ```java
    FileInputStream fis = new FileInputStream("...");
    InputStreamReader isr = new InputStreamReader(fis);
    BufferedReader br = new BufferedReader(isr);
    ```

+ OutputStreamReader：把字符流转成字节流，可以指定编码的字符集；

  + 写到OutputStreamWriter中的是字符流，从它出去的就变成了字节流；

  + 可以在构造它的对象时，传字符编码方式；

    ```java
    FileWriter fw = new FileWriter("...");
    OutputStreamWriter osw = new OutputStreamWriter(fw);
    BufferedWriter bw = new BufferedWriter(osw);
    //数据先写到bw-->osw-->（编码）-->fw-->文件中
    ```

```java
import org.junit.Test;

import java.io.*;

public class TestTransfer {
    @Test
    public void test1() throws Exception{
        //纯文本文件
        //3.txt是按照GBK进行编码的
        //FileReader默认按照平台的字符集进行编码，utf-8
        FileReader fr= new FileReader("src/day22/io/3.txt");
        BufferedReader br = new BufferedReader(fr);
        String readLine = br.readLine();
        System.out.println(readLine);

        br.close();
        fr.close();
    }

    /**
     * InputStreamReader：把字节流转成字符流，可以指定解码的字符集
     * OutputStreamReader：把字符流转成字节流，可以指定编码的字符集
     */
    @Test
    public void test2() throws Exception{
        //纯文本文件才会涉及到编码问题
        //解码的工作不能交给FileReader,因为它只能按照平添默认的字符集进行解码
        //只能自己解码，这个读取的数据，应该是字节数据
        FileInputStream fis = new FileInputStream("src/day22/io/3.txt");
        //最终要把字节数据变成字符数据
        //这个IO流可以把字节数据变成字符数据，而且可以指定字符集
        InputStreamReader isr = new InputStreamReader(fis,"GBK");
        //从fi--> isr
        //从字节流--> 字符流
        BufferedReader br = new BufferedReader(isr);
        String readLine = br.readLine();
        System.out.println(readLine);

        br.close();
        isr.close();
        fis.close();
    }

    @Test
    public void test3() throws Exception{
        String str = "同学们都着急了";

        //FileWriter只能按照平添默认的字符集进行编码，GBK
        FileWriter fw = new FileWriter("src/day22/io/3.txt",true);
        fw.write(str);
        fw.close();
    }

    @Test
    public void test4() throws Exception{
        String str = "同学们都着急了";

        //把数据写到文件中，需要指定字符集进行编码
        //把字符流--> 字节流，因此和文件相关联的是字节流，和程序数据来源相连的是字符流
        FileOutputStream fos = new FileOutputStream("src/day22/io/3.txt",true);

        OutputStreamWriter osw = new OutputStreamWriter(fos,"GBK");

        //数据先写到osw --> fos --> io/3.txt
        BufferedWriter bw = new BufferedWriter(osw);

        //数据先写到bw --> osw --> fos --> io/3.txt

        bw.newLine();
        bw.write(str);

        bw.close();
        osw.close();
        fos.close();
    }
}
```

##### 数据IO流

数据流：处理基本数据类型的数据，基本数据类型/字符串>字节；

+ DataInputStream：解码，数据输入流允许应用程序以与机器无关的方式从底层输入流中读取java基本数据类型；

  + 方法：
    + writeUTF(String);
    + writeInt();
    + writeChar();
    + ....；

+ DataOutputStream：编码，数据输出流允许应用程序以适当方式将基本java数据类型写入输出流中；

  + 方法：
  + readUTF(String);
    + readInt();
    + readChar();
    + ....；
  
+ 注意：

  + 读和写的顺序要一致；

  ```java
  import org.junit.Test;
  
  import java.io.*;
  
      @Test
      public void test1() throws Exception{
          String name = "张登";
          int age = 21;
          char gender = '男';
          double score = 89;
  
          FileOutputStream fos = new FileOutputStream("src/day23/data/stu.dat");
          DataOutputStream dos = new DataOutputStream(fos);//把各种数据类型的数据“转换”成字节数据
  
          //数据先写到dos中，负责处理各种数据类型-->byte-->fos-->文件
  
          dos.writeUTF(name);
          dos.writeInt(age);
          dos.writeChar(gender);
          dos.writeDouble(score);
  
          dos.close();
          fos.close();
      }
  
      @Test
      public void test2() throws Exception{
          FileInputStream fis = new FileInputStream("src/day23/data/stu.dat");
          DataInputStream dis = new DataInputStream(fis);
  
          //文件-->fis-->dis-->按照每一个数据的数据类型分别处理
          //顺序必须和写的顺序一致
          String name = dis.readUTF();
          int age = dis.readInt();
          char gender = dis.readChar();
          double score = dis.readDouble();
  
          System.out.println(name);
          System.out.println(age);
          System.out.println(gender);
          System.out.println(score);
  
          dis.close();
          fis.close();
      }
  }
  ```

##### 对象IO流

+ ObjectOutputStream(序列化)：编码，对象输出流，负责把对象转成二进制写到输出流中；

  + 方法：
  + writeObject(Object boj);

+ ObjectInputStream(反序列化)：解码，对象输入流，负责把二进制重构成一个对象；

  + 方法：
  + readObject(Object obj);
  + 注意：
    + 只能将支持java.io.Serializable接口（序列化接口：把对象变成字节序列）的对象写入流中；每个Serializable对象的类都将被编码，编码内容包括类名和类签名、对象的字段值和数组值，以及从初始对象中引用的其他所有对象的闭包；
    + 对象中有引用数据类型，那么这些引用数据类型也要实现序列化接口；
    + 凡是实现序列化接口的类型，都应该增加一个序列化版本ID的字段，以防修改了类后原来的数据还能正常的反序列化，否则每次修改类重新编译都会自动生成一个版本ID，和原来已经序列化的数据中的版本ID会对不上；
    + private static final long serialVersionUID = -2554006070147415889L;
    + 如果某些属性不想被序列化，那么可以给属性加一个关键字：transient，不进行读取；
  
  ```java
  import org.junit.Test;
  
  import java.io.*;
  
  public class TestObjectOutputStream {
      @Test
      public void test1() throws IOException {
          Student stu = new Student("谢志浩", 23, '男', 89);
          FileOutputStream fos = new FileOutputStream("src/day23/object/stu.dat");
          ObjectOutputStream oos = new ObjectOutputStream(fos);
  
          oos.writeObject(stu);
  
          oos.close();
          fos.close();
      }
  
      @Test
      public void test2() throws IOException, ClassNotFoundException {
          FileInputStream fis = new FileInputStream("src/day23/object/stu.dat");
          ObjectInputStream ois = new ObjectInputStream(fis);
  
          Object object = ois.readObject();
          if (object instanceof Student) {
              Student stu = (Student)object;
              System.out.println(stu);
          }
  
          ois.close();
          fis.close();
      }
  
      @Test
      public void test3() throws IOException {
          Student stu = new Student("谢志浩", 23, '男', 89,new Teacher());
          FileOutputStream fos = new FileOutputStream("src/day23/object/stu.dat");
          ObjectOutputStream oos = new ObjectOutputStream(fos);
  
          oos.writeObject(stu);
  
          oos.close();
          fos.close();
      }
  
      @Test
      public void test4() throws IOException, ClassNotFoundException {
          test2();
      }
  }
  
  class Student implements Serializable {
      private static final long serialVersionUID = 2554006070147415889L;
      private String name;
      private int age;
      private char gender;
      private transient double score;
      //这个属性要被序列化，也得支持序列化接口
      private Teacher teacher;
  
  
  //    public Student() {
  //    }
  
      public Student(String name, int age, char gender, double score) {
          this.name = name;
          this.age = age;
          this.gender = gender;
          this.score = score;
      }
  
      public Student(String name, int age, char gender, double score, Teacher teacher) {
          this(name,age,gender,score);
          this.teacher = teacher;
      }
  
      public static long getSerialVersionUID() {
          return serialVersionUID;
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "name='" + name + '\'' +
                  ", age=" + age +
                  ", gender=" + gender +
                  ", score=" + score +
                  ", teacher=" + teacher +
                  '}';
      }
  }
  
  class Teacher implements Serializable{
      private static final long serialVersionUID = 2554006070147415889L;
  }
  ```

##### 打印流

+ PrintStream：System.out；

  + append();
  + print();
  + println();

+ PrintWriter：JavaWeb中的getWriter();

  + append();
  + print();
  + println();
  
  ```java
  import org.junit.Test;
  
  import java.io.FileInputStream;
  import java.io.FileNotFoundException;
  import java.io.PrintStream;
  import java.util.Date;
  import java.util.Scanner;
  
  public class TestPrintIO {
      public static void main(String[] args) {
          PrintStream out = System.out;
  
          out.append("hello");
          out.append("world");
  
          out.print(123);
  
          out.println(456L);
  
          out.println(new Date());
      }
  
      @Test
      public void test1() throws FileNotFoundException {
          System.setOut(new PrintStream("src/day23/print/1.txt"));
          //此时System.out对应控制台，不是一个文件
          PrintStream out = System.out;
  
          out.println("helloworld");
          
          out.close();
      }
  
      @Test
      public void test2() throws Exception{
          FileInputStream fis = new FileInputStream("src/day23/print/1.txt");
          Scanner sc = new Scanner(fis);
          while(sc.hasNextLine()){
              String line = sc.nextLine();
              System.out.println(line);
          }
          sc.close();
      }
  }
  ```

#### NIO

1. NIO与IO的区别：1.4引入，1.7得到扩展
   + NIO：Non-Blocking IO，非阻塞式IO；IO是阻塞式IO；
   + NIO是面向缓冲区和通道的IO操作。既可以单向，也可以双向；
     + 缓冲区的对象本身：既可以读又可以写，当然也可以设置为只读等；
   + IO是面向流的IO操作，单向：
     + InputStream：只能读；
     + OutputStream：只能写；
   + NIO支持选择器，更适合多线程；IO不支持选择器，多线程程序比较麻烦；
2. 相同点：目的和作用都是为了数据的读和写，即数据传输；

##### NIO的Path,Paths,Files

+ 原来的IO：File，文件和目录的路径名的抽象表现形式，不管是文件还是目录都用路径来标识；

NIO：Path，一个文件或目录对应一个Path对象；

###### Paths工具类：

+ Path get(URL url)：得到网络资源路径；

+ Path get(String parent,String ... args)：得到本地资源路径；

  + Path getFileName() : 返回与调用 Path 对象关联的文件名；

  + Path getName(int idx) : 返回指定索引位置 idx 的路径名称；

  + Path getParent() ：返回Path对象包含整个路径，不包含 Path 对象指定的文件路径；

  + Path getRoot() ：返回调用 Path 对象的根路径；

  + boolean startsWith(String path) : 判断是否以 path 路径开始；

  + boolean endsWith(String path) : 判断是否以 path 路径结束；

  + boolean isAbsolute() : 判断是否是绝对路径；

  + Path toAbsolutePath() : 作为绝对路径返回调用 Path 对象；

  + Path resolve(Path p) :合并两个路径，返回合并后的路径对应的Path对象；

  + int getNameCount() : 返回Path 根目录后面元素的数量

  + String toString() ： 返回调用 Path 对象的字符串表示形式；

  + File toFile(): 将Path转化为File类的对象；

    ```java
    Path path = Paths.get("io", "java", "1.txt");
    System.out.println("toString:"+path);
    		
    System.out.println("startsWith:"+path.startsWith("io"));
    System.out.println("endsWith:"+path.endsWith("1.txt"));
    		
    System.out.println("parent:"+path.getParent());//io/java
    System.out.println("root:"+path.getRoot());//null  只有绝对路径才有根
    System.out.println("fileName"+path.getFileName());
    		System.out.println("FileSystem.separator:"+path.getFileSystem().getSeparator());
    		
    System.out.println("nameCount:"+path.getNameCount());
    System.out.println("name(1):"+path.getName(1));
    		
    		System.out.println("isAbsolutePath:"+path.isAbsolute());
    System.out.println("toAbsolutePath:"+path.toAbsolutePath());
    		
    Path parent = Paths.get("io", "java");
    Path f = Paths.get("1.txt");
    Path p = parent.resolve(f);
    System.out.println("resolve:"+p);
    
    File file = path.toFile();
    System.out.println(file);
    ```

###### Files工具类：

+ copy(Path src, Path dest, CopyOption … how)：复制文件；
+ createFile(src)：创建文件；如果文件已存在，报出异常；与File中的方法creatNewFile()相比，createNewFile如果文件存在，不会报异常；
+ delete(src)：删除文件，如果文件不存在报出异常NoSuchFileException；与File中的方法delete()相比，delete()如果文件不存在，不会报异常；
+ deleteIfExists(src)：如果文件不存在，不进行操作；如果文件存在，删除文件；
+ getLastModifiedTime(src)：返回文件的最后一次修改时间；
+ readAllLines(src,Charset.forName("..."))：从文件中读取所有行，读取的是纯文本文件；
+ Path createDirectory(Path path, FileAttribute<?> … attr) : 创建一个目录；
+ Path createDirectories(Path dir, FileAttribute<?>... attrs) 创建一个目录，通过创建所有不存在的父目录；
+ Path createLink(Path link, Path existing) 创建一个新的链接（目录项）为现有的文件（可选操作）；
+ Path move(Path src, Path dest, CopyOption…how) : 将 src 移动到 dest 位置；
+ long size(Path path) : 返回 path 指定文件的大小；

```java
import org.junit.Test;

import java.io.File;
import java.io.IOException;
import java.nio.charset.Charset;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.attribute.FileTime;
import java.util.Iterator;
import java.util.List;

public class TestPath {
    @Test
    public void test1(){
        File file = new File("download/io/first.txt");
        Path p = Paths.get("download","io","first.txt");

        Path fileName = p.getFileName();
        Path parents = p.getParent();
        boolean b = p.endsWith("first.txt");
        int nameCount = p.getNameCount();
        System.out.println(fileName);//first.txt
        System.out.println(parents);//download\io
        System.out.println(b);//true
        System.out.println(nameCount);//3
    }

    @Test
    public void test2() throws IOException {
        Path src = Paths.get("src","day23","download","io","first.txt");
        Path desc = Paths.get("src","day23","download","io","second.txt");
        Files.copy(src,desc);
    }

    @Test
    public void test3() throws IOException {
        Path src = Paths.get("src","day23","download","io","first.txt");
        Files.createFile(src);

        //下面代码文件已存在，但是没有报异常
//        File file = new File("src/day23/download/io/first.txt");
//        file.createNewFile();
    }

    @Test
    public void test4() throws IOException {
        //下面delete代码如果文件不存在不报错
//        File file = new File("src/day23/download/io/first.txt");
//        file.delete();

        //下面delete代码如果文件不存在报错：NoSuchFileException
        Path src = Paths.get("src","day23","download","io","first.txt");
        Files.delete(src);

        //下面代码表示如果文件不存在，不进行操作，如果文件存在，将其删除，返回值是boolean类型
        Files.deleteIfExists(src);
    }

    @Test
    public void test5() throws IOException {
        Path src = Paths.get("src","day23","download","io","second.txt");
        FileTime time = Files.getLastModifiedTime(src);
        System.out.println(time);
    }

    @Test
    public void test6() throws IOException {
        Path src = Paths.get("src","day23","download","io","third.txt");
        Charset set = Charset.forName("UTF8");
        List<String> strings = Files.readAllLines(src,set);

        for (String string : strings) {
            System.out.println(string);
        }

        Iterator<String> iterator = strings.iterator();
        while(iterator.hasNext()){
            String next = iterator.next();
            System.out.println(next);
        }
    }
}
```

```java
	public static void main(String[] args) throws IOException {
		Path dir = Paths.get("first", "second","io");
		
//		Path createDirectory(Path path, FileAttribute<?> … attr) : 创建一个目录
//		Path createDirectories(Path dir, FileAttribute<?>... attrs) 
//		Files.createDirectory(dir);//类似于mkdir()父目录如果不存在，会报错
//		Files.createDirectories(dir);//类似于 mkdirs()
		
		Path file = Paths.get("first", "second","io", "1.txt");
//		Path createFile(Path path, FileAttribute<?> … arr) : 创建一个文件
		
//		Files.createFile(file);
//		Path link = Paths.get("first", "second","io", "1.txt_hardlink");
//		Files.createLink(link, file);
		
//		void delete(Path path) : 删除一个文件，如果不存在，执行报错
//		Files.delete(link);
//		void deleteIfExists(Path path) : Path对应的文件如果存在，执行删除，如果不存在，就什么也不干
//		Files.deleteIfExists(link);
		
//		Path copy(Path src, Path dest, CopyOption … how) : 文件的复制，目标目录不存在则报错
//		Path dest = Paths.get("first", "second","io", "2.txt");
//		Files.copy(file, dest, StandardCopyOption.REPLACE_EXISTING);
		
//		Path move(Path src, Path dest, CopyOption…how) : 将 src 移动到 dest 位置
//		Path target = Paths.get("io", "2.txt");
//		Files.move(file, target, StandardCopyOption.REPLACE_EXISTING,StandardCopyOption.ATOMIC_MOVE);
		
//		long size(Path path) : 返回 path 指定文件的大小
//		long size = Files.size(file);
//		System.out.println(size);
	}
}

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.LinkOption;
import java.nio.file.Path;
import java.nio.file.Paths;

import org.junit.Test;

public class TestLink {
	@Test
	public void testCopy() throws IOException{
	//	Path src = Paths.get("1", "2");
	//	Path dest = Paths.get("12");
//		Files.copy(src, dest);//创建了一个新目录，源目录中的内容不会复制，适用于文件到文件的复制
		
//		Path src = Paths.get("1", "2");
//		Path s_link = Paths.get("12");
//		Files.createSymbolicLink(s_link, src);//创建一个符号连接
		
		Path s_link = Paths.get("12");//是一个符号连接
		Path link = Paths.get("12_link");//另一个符号连接
		Files.copy(s_link, link, LinkOption.NOFOLLOW_LINKS);//复制一个符号连接
	}
	
	@Test
	public void testHardLink() throws IOException{
		Path path = Paths.get("1", "2");
		Path h_link = Paths.get("12");
		Files.createLink(h_link, path);//添加硬链接，只能给文件创建
		//可以比喻对象的引用，只要还有引用执行某个对象，那么这个对象就不会被回收
		//即删除源文件还是硬链接，只要还有一个这个文件的引用，那么就不会真删除这个文件
		//当您移动或删除原始文件时，硬链接不会被破坏，因为它所引用的是文件的物理数据而不是文件在文件结构中的位置。
		//虽然会显示大小，但实际上没有大小，和源文件共享大小，共享内容，共享存储空间
		//只能引用同一文件系统中的文件。即只能在本分区中做 link。
	}
	
	@Test
	public void testSymbolicLink() throws IOException{
		Path path = Paths.get("1", "2");
		Path s_link = Paths.get("12");
		Files.createSymbolicLink(s_link, path);//添加符号链接，可以给目录或文件创建
		//符号链接,又称为软连接：它是一个指针，指向文件在文件系统中的位置。
		//符号链接可以跨文件系统，甚至可以指向远程文件系统中的文件。
		//符号链接只是指明了原始文件的位置，用户需要对原始文件的位置有访问权限才可以使用链接。
		//如果原始文件被删除，所有指向它的符号链接也就都被破坏了。它们会指向文件系统中并不存在的一个位置。
		
		//区别与快捷方式：快捷方式是windows才有的，而且快捷方式是个文件，单独的文件，占大小
	}
}
```

###### Files常用方法

+ 用于判断：

  + boolean exists(Path path, LinkOption … opts) : 判断文件是否存在；
  + boolean notExists(Path path, LinkOption … opts) : 判断文件是否不存在
  + boolean isDirectory(Path path, LinkOption … opts) : 判断是否是目录；
  + boolean isRegularFile(Path path, LinkOption … opts) : 判断是否是文件；
  + boolean isHidden(Path path) : 判断是否是隐藏文件；
  + boolean isReadable(Path path) : 判断文件是否可读；
  + boolean isWritable(Path path) : 判断文件是否可写；

+ 用于操作内容：

  + SeekableByteChannel newByteChannel(Path path, OpenOption…how) : 获取与指定文件的连接，how 指定打开方式；

  + DirectoryStream<Path> newDirectoryStream(Path path) : 打开 path 指定的目录；

  + InputStream newInputStream(Path path, OpenOption…how):获取 InputStream 对象；

  + OutputStream newOutputStream(Path path, OpenOption…how) : 获取 OutputStream 对象；

    ```java
    public class TestChannel {
    	public static void main(String[] args) throws IOException {
    		Path file = Paths.get("first", "second","io","1.txt");
    		InputStream is = Files.newInputStream(file, StandardOpenOption.READ);
    		byte[] data = new byte[1024];
    		int len;
    		while((len=is.read(data))!=-1){
    			System.out.println(new String(data,0,len));
    		}
    	}
    }
    	public static void main(String[] args) throws IOException {
    		Path file = Paths.get("first", "second","io","1.txt");
    		//StandardOpenOption.CREATE：如果不存在就创建，如果存在就什么也不干
    		//StandardOpenOption.CREATE_NEW：如果不存在就创建，如果存在就报错
    //		StandardOpenOption.APPEND：如果不存在就报错，如果存在就追加
    		//StandardOpenOption.WRITE：从头开始写
    		//StandardOpenOption.TRUNCATE_EXISTING：清空原文件
    		OutputStream os = Files.newOutputStream(file, StandardOpenOption.TRUNCATE_EXISTING);
    		String str = "java";
    		os.write(str.getBytes());
    		os.close();
    	}
    	public static void main(String[] args) throws IOException {
    		Path file = Paths.get("d:\\");
    		DirectoryStream<Path> ds = Files.newDirectoryStream(file);
    		Iterator<Path> iter = ds.iterator();
    		while(iter.hasNext()){
    			Path next = iter.next();
    			System.out.println(next);
    		}
    	}
    ```

##### NIO的缓冲区：Buffer

Java NIO系统的核心在于：通道(Channel)和缓冲区(Buffer)。通道表示IO源到 IO 设备(例如：文件、套接字)的连接。若需要使用 NIO 系统，需要获取用于连接 IO 设备的通道以及用于容纳数据的缓冲区。然后操作缓冲区，对数据进行处理。简而言之，Channel 负责传输， Buffer 负责存储数据

![IO](images\grammar\IO.png)

从输入流中只能读取数据，只能往输出流中写入数据

Java IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。

![NIO](images\grammar\NIO.png)

缓冲区就好比是“地铁车厢”，通道就好比“地铁线路”，“地铁线路”负责运输数据，而缓冲区负责存储（承载）数据，即装“乘客”。地铁车厢在通道中来回走，在任何一端都可以上人和下车。

+ NIO的缓冲区：Buffer是一个用于特定数据类型(boolean除外)的容器，底层使用数组存储；

+ 缓冲区类型（除了boolean外有7种）：缓冲区的管理方式几乎一致，通过 allocate() 获取缓冲区。

  + ByteBuffer(最多)：>MappedByteBuffer物理内存映射
  + ShortBuffer：
  + IntBuffer：
  + LongBuffer：
  + FloatBuffer：
  + DoubleBuffer：
  + CharBuffer：

+ 缓冲区的属性：

  + capacity：总容量，一旦创建，容量确定；

  + position：指针，当前正在读/写的位置；

  + limit：当前最多可读/写的长度限制；

  + mark：标记可重复读/写的位置，通过 Buffer 中的 mark() 方法将mark标记为当前position位置。 之后可以通过调用 reset() 方法将 position恢复到标记的mark处；

    + 0<=mark<=position<=limit<=capacity

    ![buffer1](images\grammar\buffer1.png)

    ![buffer2](images\grammar\buffer2.png)

+ 缓冲区的方法：

  + put：装数据，存入数据到缓冲区中；
  + get：取数据，获取缓冲区中的数据；
  + flip()：从写变成读的状态，从装载到卸载；
  + clear()：清空一切标记，缓冲区还原到初始状态，主要还原limit和position；（如果继续用flip()方法，这次能够写的个数是上次的limit的限制个数）

  ```java
  import java.nio.ByteBuffer;
  
  public class TestBuffer {
      public static void main(String[] args) {
          ByteBuffer bf = ByteBuffer.allocate(10);//非直接缓冲区
          System.out.println("缓冲区的capacity：" + bf.capacity());
          System.out.println("缓冲区的position:" + bf.position());
          System.out.println("缓冲区的limit:" + bf.limit());
  
          System.out.println("--------------------");
  
          String str = "hello";
          byte[] bytes = str.getBytes();//5
          //System.out.println(bytes.length);
          bf.put(bytes);//往缓冲区装了5个字节的数据
  
          System.out.println("缓冲区的capacity：" + bf.capacity());
          System.out.println("缓冲区的position:" + bf.position());
          System.out.println("缓冲区的limit:" + bf.limit());
  
  //        byte[] data = {1,2,3,4,5,6};
  //        for (int i = 0; i < data.length; i++) {
  //            bf.put(data[i]);
  //        }
  
          bf.flip();//从装载变成卸载操作
          System.out.println("---------------------------");
          System.out.println("缓冲区的capacity：" + bf.capacity());
          System.out.println("缓冲区的position:" + bf.position());
          System.out.println("缓冲区的limit:" + bf.limit());
  
          byte r1 = bf.get();
          System.out.println((char)r1);
  
          byte r2 = bf.get();
          System.out.println((char)r2);
  
          byte r3 = bf.get();
          System.out.println((char)r3);
  
          byte r4 = bf.get();
          System.out.println((char)r4);
  
          byte r5 = bf.get();
          System.out.println((char)r5);
  
  //        byte r6 = bf.get();越界
  //        System.out.println((char)r6);
  
          bf.clear();
          System.out.println("---------------------------");
          System.out.println("缓冲区的capacity：" + bf.capacity());
          System.out.println("缓冲区的position:" + bf.position());
          System.out.println("缓冲区的limit:" + bf.limit());
      }
  }
  ```
  
+ 缓冲区的其他方法：

  | **方** **法**          | **描** **述**                                                |
  | ---------------------- | ------------------------------------------------------------ |
  | Buffer flip()          | 将limit设置为当前position，将position设置为 0,mark设置为-1   |
  | Buffer rewind()        | 将position设为为 0， mark设为-1。可重复读                    |
  | Buffer clear()         | 将limit设为capacity,将position设为0，并将mark设为-1。数据没有清空 |
  | Buffer mark()          | 对缓冲区设置mark                                             |
  | Buffer reset()         | 将位置positio转到以前设置的mark所在的位置                    |
  | boolean hasRemaining() | 判断缓冲区中是否还有元素                                     |
  | int remaining()        | 返回position和limit之间的元素个数                            |
  | Xxx[] array()          | 返回XxxBuffer底层的Xxx数组                                   |
  | int capacity()         | 返回 Buffer 的 capacity 大小                                 |
  | int limit()            | 返回 Buffer 的界限(limit) 的位置                             |
  | Buffer limit(int n)    | 将设置缓冲区界限为 n, 并返回一个具有新 limit 的缓冲区对象    |
  | int position()         | 返回缓冲区的当前位置 position                                |
  | Buffer position(int n) | 将设置缓冲区的当前位置为 n , 并返回修改后的 Buffer 对象      |

###### 直接缓冲区和非直接缓冲区

+ 非直接缓冲区(或传统IO)：通过xxxBuffer类的静态方法allocate(int) 分配缓冲区，将缓冲区建立在 JVM 的内存中

+ 直接缓冲区：效率比非直接缓冲区高；

  + 通过xxxBuffer类的静态方法allocateDirect(int)分配直接缓冲区，将缓冲区建立在物理内存中;
  + 还可以通过 FileChannel对象的map() 方法 将文件区域直接映射到内存中来创建，该方法返回ByteBuffer的子类：MappedByteBuffer ;

  ![非直接缓冲区](images\grammar\非直接缓冲区.png)

  ![直接缓冲区](images\grammar\直接缓冲区.png)

##### NIO的通道

传统的IO：节点流既负责连接，由负责传输数据；处理流负责对数据进行处理（缓冲、解码与编码等）；

NIO的通道：负责和数据源或目的地进行连接，只负责连接，缓冲区只负责传输数据；通道即轨道，缓冲区即车厢；

+ Channel的分类：

  + FileChannel：和文件连接；
  + ServerSocketChannel：和网络TCP的服务端连接；
  + SocketChannel：和网络TCP通信的两端的Socket连接；
  + DatagramChannel：和网络的UDP的通信的两端的DatagramSocket连接；

+ 如何创建Channel对象：

  + 对传统的IO流做了改进，使得其对新的NIO提供支持：getChannel()；
  + jdk1.7后通过通道类自己的静态方法来获取：
    + FileChannel fc = FileChannel.open(path);
  + jdk1.7后使用Files工具类的静态方法:
    + SeekableByteChannel seekableByteChannel = Files.newByteChannel(path);

+ Channel的常用方法：

  + read(缓冲区)：往缓冲区装在数据，相当于调用缓冲区的put方法；
  + write(缓冲区)：从缓冲区把数据写到当前通道中，相当于调用缓冲区的write方法；
  + 从read-->write，需要调用缓冲区的flip()；从write-->read，需要调用缓冲区的clear()；
  
  ```java
  import org.junit.Test;
  
  import java.io.IOException;
  import java.nio.ByteBuffer;
  import java.nio.MappedByteBuffer;
  import java.nio.channels.FileChannel;
  import java.nio.channels.SeekableByteChannel;
  import java.nio.file.Files;
  import java.nio.file.Path;
  import java.nio.file.Paths;
  import java.nio.file.StandardOpenOption;
  
  public class TestChannel {
      @Test
      public void test1() throws IOException {
          Path path = Paths.get("src","day23","io","first.txt");
          FileChannel fc = FileChannel.open(path);
          SeekableByteChannel seekableByteChannel = Files.newByteChannel(path);
      }
  
      @Test
      public void test2() throws IOException {
          Path src = Paths.get("src","day23","download","io","first.txt");
          //和src、first.txt文件连接的通道
          FileChannel srcChannel = FileChannel.open(src,StandardOpenOption.READ);
  
          Path dest = Paths.get("src","day23","download","io","third.txt");
          //和dest、third文件连接的通道
          FileChannel destChannel = FileChannel.open(dest, StandardOpenOption.WRITE, StandardOpenOption.CREATE);
  
          ByteBuffer bb = ByteBuffer.allocate(10);
  
          //从srcChannel通道把数据装到bb缓冲区
          //srcChannel.read(bb);
          while (srcChannel.read(bb) != -1){
              //从装载到卸载
              bb.flip();
              //从bb缓冲区把数据卸载到destChannel中
              destChannel.write(bb);
              //清空所有标记，重复使用所有缓冲区
              bb.clear();
          }
      }
  
      @Test
      public void test3() throws IOException {
          //物理映射
          Path src = Paths.get("src","day23","download","io","first.txt");
          //和src、first.txt文件连接的通道
          FileChannel srcChannel = FileChannel.open(src,StandardOpenOption.READ);
  
          Path dest = Paths.get("src","day23","download","io","third.txt");
          //和dest、third文件连接的通道
          FileChannel destChannel = FileChannel.open(dest,StandardOpenOption.READ,StandardOpenOption.WRITE, StandardOpenOption.CREATE);
  
          MappedByteBuffer srcMap = srcChannel.map(FileChannel.MapMode.READ_ONLY,0,srcChannel.size());
          MappedByteBuffer destMap = destChannel.map(FileChannel.MapMode.READ_WRITE,0,srcChannel.size());
  
          destMap.put(srcMap);
  
          destChannel.close();
        srcChannel.close();
      }
  }
  ```

### 线程与进程

#### 线程

1. 相关概念：
   + 程序（program）：为了完成某个任务或功能，而选择一种编程语言而编写的一组代码，最终是一组指令，程序是静态的；
   + 进程（process）：程序的一次执行，操作系统是以进程为单位来进行管理，进程是操作系统分配资源的最小单位，进程是动态的；
   + 线程（Thread）：是进程中的其中一条执行路径；
     + 一个进程至少有一个线程，如果只有一个线程，我们就称为单线程程序；线程是CPU调度的最小单位；
     + 一个进程中的多个线程会共享同一个进程的物理内存；但是每一个线程也有自己独立的栈内存，即局部变量是独立的，成员变量的共享的，静态变量更是共享的；
     + 如果一个进程中有多个线程，那么给用户的感觉是多个线程同时运行的，但是实际上同一时间CPU只会执行其中的一个线程，因为CPU非常快，而且给每一个线程分配的时间非常短，其中一个线程执行一会儿，立马切换到另一个线程执行，所以用户的感觉是同时进行的；多个线程谁被CPU调度是随机的，大家会抢CPU的资源，即CPU执行权；
     + Java程序至少有一个主方法，即主线程；

##### 线程创建方式

+ 继承线程类java.lang.Thread；

  + 继承Thread类；

  + 必须重写run()方法；

    ```java
    public void run(){
        线程体：这个线程要完成的任务代码；
    } 
    ```

  + 创建线程对象；

  + 启动线程：start()启动线程；

    + 当CPU调度当前线程时，JVM会自动调度它的run()，不用手动调度run()；

    ```java
    public class TestMyThread {
        public static void main(String[] args) {
            MyThread m = new MyThread();
            m.start();
    
            MyThread m2 = new MyThread();
            m2.start();
    
            for (int i = 0; i <= 100; i++) {
                System.out.println("主线程：" + i);
            }
        }
    }
    
    class MyThread extends Thread{
        @Override
        public void run() {
            for (int i = 0; i <= 100; i++) {
                System.out.println(getName() + "自定义线程：" + i);
            }
        }
    }
    ```
  
+ 实现java.lang.Runnable接口；

  + 实现Runnable接口；

  + 必须实现Runnable接口抽象方法；

    ```java
    public void run() {
        线程体：该线程要完成的任务；
    }
    ```

  + 创建线程对象；

  + 借助于Thread类的对象启动线程：start()；

    + 找代理帮助启动线程；
  + 主题：Runnable；
      + 被代理者：自定义的线程类对象；
      + 代理者：Thread的对象；
    + 要求：
      + 代理者和被代理者都实现了Runnable接口；
      + 通过代理类的构造器，把被代理者传到代理者中；
      + 当执行代理者的run()时，核心业务代码，还是调用被代理者的run()；
    
    ```java
    public class TestMyRunnable {
        public static void main(String[] args) {
            MyRunnable m = new MyRunnable();
    
            //代理对象
            Thread t = new Thread(m);
            t.start();
    
            for (int i = 0; i <= 100; i++) {
                System.out.println("主线程：" + i);
            }
        }
    }
    
    class MyRunnable implements Runnable{
        @Override
        public void run() {
            for (int i = 0; i <= 100; i++) {
                System.out.println(Thread.currentThread().getName() + "自定义线程" + i);
            }
        }
    }
    ```
  
+ <font color='red'>区别：</font>

  + 启动方式不一样；
    + 继承Thread：直接启动；
    + 实现Runnable：借助Thread对象启动；
  + 共享数据的实现方式：
    + 继承Thread：通过静态数据实现共享；
    + 实现Runnable：通过同一个线程对象即可；
  + 同步锁：
    + 继承Thread：要么自定义一个静态的锁对象，要么使用类名.class作为锁对象，要么从外面传一个共同的锁对象
    + 实现Runnable：可以直接使用this；

##### 代理模式的体现

1. 代理有三个角色：代理者和被代理者必须实现同一个接口；

   + 主题：接口；

   + 被代理者；

   + 代理者；

     ```java
     public class TestProxy {
         public static void main(String[] args) {
             Customer customer = new Customer();
             Agent agent = new Agent(customer);
     
             agent.rent();
         }
     }
     
     //主题
     interface Rent{
         void rent();
     }
     
     //被代理者
     class Customer implements Rent{
         @Override
         public void rent() {
             System.out.println("交钱，拿钥匙，入住");
         }
     }
     
     class Agent implements Rent{
         //被代理者
         private Rent target;
     
         public Agent(Rent target) {
             this.target = target;
         }
     
         @Override
         public void rent() {
             System.out.println("找房源。。。");
             target.rent();
             System.out.println("善后工作");
         }
     }
     ```
   
2. 线程中的代理模式：

   + 主题：Runnable；

   + 代理者：Thread，实现了Runnable接口；

   + 被代理者：MyRunnable，实现了Runnable接口；

   + 代理者中需要保存被代理者的引用；

     ```java
     public class TestMyRunnable {
         public static void main(String[] args) {
             MyRunnable m = new MyRunnable();
     
             //代理对象
             Thread t = new Thread(m);
             t.start();
     
             for (int i = 0; i <= 100; i++) {
                 System.out.println("主线程：" + i);
             }
         }
     }
     
     class MyRunnable implements Runnable{
         @Override
         public void run() {
             for (int i = 0; i <= 100; i++) {
                 System.out.println(Thread.currentThread().getName() + "自定义线程" + i);
             }
         }
     }
     ```

##### 线程的生命周期

1. 每一个线程对象都有自己的生命周期：

   + 出生：new；
   + 就绪：等着被CPU调度，CPU可以调度，只有就绪状态的线程才能被CPU调度；

     + 只有出生的线程调用了start方法，或者说新建线程对象被启动了，才能从出生状态变成就绪状态；
   + 运行：正在被CPU调度，正在运行的线程，这个时间非常短；

     + 去到死亡状态：
       + 正常执行完；
       + 遇到异常，没有进行处理；
       + 调用stop()方法等，已过时；
     + 回到就绪状态：
       + 时间到了；
       + 遇到了yield()方法，主动让出CPU资源；
     + 去到阻塞状态：
       + 遇到了sleep()；
       + 遇到了wait()；
       + 遇到了join()；
       + 等待锁；
   + 阻塞：从阻塞状态必须恢复到就绪状态才能被CPU调度；
     + 遇到了sleep()：
       + 自然醒；
       + 被打断；
     + 遇到了wait()：
       + 被notify()或notifyAll()；
       + wait()的时间到了，醒来后需要重新判断条件；
     + 遇到了join()：阻塞线程完事，回到就绪状态；
     + 等待锁：别人释放了锁；
   + 死亡：从运行状态到死亡状态；

     + 任务完成，正常死亡；
     + 遇到异常，没有处理，这个线程崩溃；
     + 被其他线程stop等：终止；

   ![线程生命周期](images\grammar\线程生命周期.png)

2. sleep的wait的区别与联系：

   + 相同点：
     + 都会使当前线程从运行状态变为阻塞状态；
   + 不同点：
     + 声明的类不同：
       + sleep()在Thread类中声明，是个静态方式；
       + wait()在Object类中声明，是非静态方法；
     + 调用者不同：
       + sleep()由Thread类名调用；
       + wait()必须由锁对象调用；
     + 关于锁的释放不同：
       + sleep()可以在没有锁的代码中运行，如果没有锁，不涉及释放锁；sleep()也可以在锁的代码中运行，如果有锁，当前线程就算遇到sleep()方法，如果手上持有锁，也不会释放；
       + wait()方法，当前线程遇到wait()一定会释放锁；
     + 被唤醒的机制不同：
       + sleep()要么时间到，要么被打断；
       + wait()更多的时候是通过notify()或notifyAll()唤醒的；

##### 线程Thread类的方法

1. 构造器：

   + Thread();
   + Thread(Sting name)；
   + Thread(Runnable target)；

2. start()；

3. run()；

4. sleep()：线程休眠，静态方法；

5. join()：当前线程被某个线程other加塞，直到other线程死亡，当前线程才能继续被CPU调度；

6. getName()：获取线程的名字；

7. currentThread()：获取当前线程对象，这句代码哪个线程在运行，就是哪个线程对象，静态方法；

8. 守护线程：守护线程是为用户线程服务的，主要任务是为用户线程服务；当它所守护的用户线程都结束后，它就自动结束了；守护线程是不能单独存在的，必须有被守护对象；例如：垃圾回收线程；

   + setDaemon()：

   + isDaemon()

9. 优先级：主线程的默认优先级是5，优先级的范围是[1,10]；

   + MIN_PRIORITY = 1，NORM_PRIORITY = 5，MAX_PRIORITY = 10；
   + 优先级高的CPU会更多地关注它，调用它的可能性更高，不能让业务逻辑依赖优先级；
   + getPriority()：获取线程的优先级；
   + setPriority()：设置线程的优先级；

   ```java
   public class TestThreadMethod {
       public static void main(String[] args) throws InterruptedException {
           Thread main = Thread.currentThread();
           System.out.println("这是主线程：" + main);
   
           main.setPriority(10);
           System.out.println(main.getPriority());
   
           TwoThread t = new TwoThread();
           t.start();
   
           for (int i = 10; i > 0; i--) {
               try {
                   //线程休眠：1000毫秒
                   Thread.sleep(1000);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
   
               if (i % 3 == 0) {
                   OtherThread other = new OtherThread();
   
                   other.start();
   
                   //当前的主线程被other线程加塞，直到other做完它的事，主线程再回到继续状态等待CPU调度
                   other.join();
               }
               System.out.println("i = " + i);
           }
       }
   }
   
   class OtherThread extends Thread {
       @Override
       public void run() {
           for (int i = 10; i > 0; i--) {
               System.out.println(getName() + "OtherThread线程" + i);
           }
       }
   }
   
   class TwoThread extends Thread {
       @Override
       public void run() {
           for (int i = 1000; i > 0; i--) {
               try {
                   Thread.sleep(100);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
               System.out.println(getName() + "TwoThread线程" + i);
           }
       }
   }
   ```

#### 线程的安全问题与同步

1. 线程安全问题：

   + StringBuilder线程不安全，StringBuffer线程安全；
   + HashMap线程不安全，Hashtable线程安全；
   + ArrayList线程不安全，Vector线程安全；
     + 上面部分是怎么实现线程安全的
       + 同步锁synchronized；
   + 单例设计模式中的懒汉式线程不安全；饿汉式线程安全；

2. 为什么会出现线程安全问题：

   + 前提条件：
     + 有多个线程；
     + 有共享数据；
     + 每个线程有多条语句操作共享数据；
   + 其中一个线程在对多个共享数据进行操作时，工作没有全部完成，可能被阻塞了，或者CPU时间到了，这个线程就失去了CPU的执行权，其他线程就会对这个共享数据进行操作，就会影响我的线程；

3. 解决方案：

   + Java中提供了一种解决线程安全的问题：同步（加锁）；
   + 同步锁是其中的一种解决方案，后面再JUC（java.util.concurrent）中有更全面的说明；

4. 同步的关键字：synchronized；

5. 同步的形式：

   + 同步代码块：

     ```java
     synchronized(锁对象) {
         被锁的代码；
     }
     ```

   + 同步方法：

     ```java
     [修饰符]synchronized 返回值类型 ([static]) 方法名(形参列表)抛出的异常列表 {
         
     }
     ```

     + <font color='red'>同步方法的锁对象是谁：</font>
       + <font color='red'>非静态的方法：默认的锁对象是this；</font>
       + <font color='red'>静态的方法：默认的锁对象是当前类的Class对象；一个类被加载到内存中，只会在内存中生成唯一的Class对象；内存中的Class对象只有一个；</font>

6. 锁：

   + 同步的锁对象：可以说任意类型对象；
   + 同步锁的要求：必须保证这几个使用同一个共享数据的线程（多个线程必须是同一个锁），使用同一把锁，即承认同一个锁对象；
   + 锁的范围：锁代码的范围，不能太大，也不能太小，锁一次任务，所有涉及到的操作共享数据的代码都应该锁进来；
     + 锁太大：一个人全干了；
     + 锁太小：没解决安全问题；
   + 如何选择锁对象：
     + 类型不重要；
     + 重要的是这几个线程，共享数据的是不是同一个对象；

7. 如何选择锁：

   + 类型不重要，重要的是这几个线程共享同一个对象；

##### 继承Thread类与同步代码块

```java
/**
 * 卖票，总票数为10张，分为3个窗口同时卖票，每张票大概100毫秒卖出。
 */
public class TestTicket {
    public static void main(String[] args) {
        Ticket t1 = new Ticket();
        Ticket t2 = new Ticket();
        Ticket t3 = new Ticket();

        t1.start();
        t2.start();
        t3.start();
    }
}

class Ticket extends Thread {
    private static int total = 10;//
    private static final Object obj = new Object();

    @Override
    public void run(){
        while (true) {
            synchronized (obj) {
                if (total > 0) {
                    System.out.println (getName () + "卖出一张票");
                    try {
                        Thread.sleep (100);
                    } catch (InterruptedException e) {
                        e.printStackTrace ();
                    }
                    total--;
                    System.out.println ("现在的余票还有：" + total);
                } else {
                    break;
                }
            }
        }
    }
}
```

##### 实现Runnable接口与同步代码块

+ 推荐使用实现Runnable接口的方式创建多线程对象；
  + 创建锁对象简单，可以直接用this锁对象；
  + 共享数据可以不用声明为static类型；

```java
public class TestWindow {
    public static void main(String[] args) {
        Window w = new Window (1001);
        Thread t1 = new Thread (w);
        Thread t2 = new Thread (w);
        Thread t3 = new Thread (w);

        t1.start ();
        t2.start ();
        t3.start ();

        Window w2 = new Window (1002);
        Thread t4 = new Thread (w2);
        Thread t5 = new Thread (w2);
        Thread t6 = new Thread (w2);

        t4.start ();
        t5.start ();
        t6.start ();
    }
}

class Window implements Runnable {
    private int total = 10;//共享数据
    private int number;


    public Window() {
    }

    public Window(int number) {
        this.number = number;
    }

    //流动红旗，哪个线程手上握着obj对象，哪个线程就拥有被锁住代码的执行权；如果没有obj对象，就算它
    //抢到了CPU执行权，也必须进行等待；
    //private static final Object obj = new Object ();

    @Override
    public void run() {
        while (true) {
            synchronized (this) {
                if (total > 0) {
                    System.out.println (Thread.currentThread ().getName () + "卖出一张票--" + number);
                    try {
                        Thread.sleep (100);
                    } catch (InterruptedException e) {
                        e.printStackTrace ();
                    }
                    total--;
                    System.out.println ("现在的余票还有：" + total);
                } else {
                    break;
                }
            }
        }
    }
}
```

##### 继承Thread类与同步方法

```java
public class TestTicketMethod {
    public static void main(String[] args) {
        Saler s1 = new Saler ();
        Saler s2 = new Saler ();
        Saler s3 = new Saler ();

        s1.start ();
        s2.start ();
        s3.start ();

        Class<Saler> salerClass = Saler.class;
        System.out.println (salerClass);
    }
}

class Saler extends Thread {
    private static int total = 10;

    @Override
    public void run(){
        while (true) {
            if (total > 0){
                sale ();
            }else {
                break;
            }
        }
    }

    //调用一次，卖一张票
    //如果是非静态方法，锁对象是this
    //如果是静态方法，锁对象是Saler.Class()
    private synchronized static void sale() {
        if (total > 0) {
            System.out.println (Thread.currentThread ().getName () + "卖出一张票");
            try {
                Thread.sleep (100);
            } catch (InterruptedException e) {
                e.printStackTrace ();
            }
            total--;
            System.out.println (Thread.currentThread ().getName () + "现在的余票还有：" + total);
        }
    }
}
```

##### 实现Runnable接口与同步方法

```java
public class TestPiaoMethod {
    public static void main(String[] args) {
        Piao p = new Piao ();
        Thread t1 = new Thread (p);
        Thread t2 = new Thread (p);
        Thread t3 = new Thread (p);

        t1.start ();
        t2.start ();
        t3.start ();
    }
}

class Piao implements Runnable {
    private int total = 10;

    @Override
    public void run() {
        while (true){
            if (total > 0) {
                sale ();
            } else {
                break;
            }
        }
    }

    //非静态的方法，锁对象是this
    private synchronized void sale() {
        if (total > 0) {
            System.out.println (Thread.currentThread ().getName () + "卖出一张票");
            try {
                Thread.sleep (100);
            } catch (InterruptedException e) {
                e.printStackTrace ();
            }
            total--;
            System.out.println (Thread.currentThread ().getName () + "查看现在的余票：" + total);
        }
    }
}
```

#### 生产者与消费者问题(线程通信)

##### 单个生产者与消费者

有两个或多个数据，其中一个或多个线程是生产数据，另外一个或多个线程是消费数据，装数据的缓冲区，比喻成仓库，大小是有限的。当生产者线程不断往仓库生产数据，如果消费者线程慢，会导致仓库装满，此时生产者停下来，等消费者消耗了数据，生产者再进行生产；当消费者线程不断去仓库取数据，如果消费者线程快，会导致仓库空了，此时消费者应该停下来等生产者生产了数据，消费者再继续消费数据；

+ 问题：
  + 数据缓冲区是一个共享资源：
    + 有线程安全问题，需要同步解决；
  + 数据缓冲区容量有限的问题：线程通信，协作；
    + wait()；
    + notify()/notifyAll()；
    + 通信的纽带，锁对象：只要是同一个锁对象的线程，就可以被唤醒；

+ 线程的监视者：锁对象；Object中的方法

  + wait()：线程等待，方法必须由锁对象调用，不是锁对象不能调用wait()；
    + 为什么要把wait()等声明在Object类中而不是Thread类中，因为它必须由锁对象调用，而锁对象可以是任意类型对象；
      + 静态方式的锁对象是HouseWare.class；
      + 非静态方法是锁对象是this；
  + notify()：唤醒在此对象监视器上等待的单个线程；
    + 必须由锁对象调用；
  + notifyAll()：唤醒在此对象监视器上等待的所有线程；
    + 必须由锁对象调用；

  ```java
  public class TestWorkerAndCustomer {
      public static void main(String[] args) {
          HouseWare h = new HouseWare ();
  
          Woker w = new Woker (h);
          Salers s = new Salers (h);
  
          w.start ();
          s.start ();
      }
  }
  
  //模拟小米的仓库，生产电视机
  class HouseWare {
      private static final int MAX_VALUE = 10;
      //private static final Object obj = new Object ();//使用obj作为锁对象
      private int total;
  
      //非静态方法，默认锁对象是this
      public synchronized void put(){
          //当仓库满了，生产者线程停下来
          if (total >= MAX_VALUE) {
              //这个方法是由生产者线程调用的
              //当前线程停下来
              try {
                  //obj.wait ();//使用obj作为锁对象
                  this.wait ();
              } catch (InterruptedException e) {
                  e.printStackTrace ();
              }
          }
          total++;
          try {
              Thread.sleep (100);
          } catch (InterruptedException e) {
              e.printStackTrace ();
          }
          System.out.println ("生产了一台电视机，现在的库存量是：" + total);
  
          //唤醒在此监视器对象this等待的单个线程；因为现在只有两个线程，它唤醒的就是
          //对象，即消费者线程
          this.notify();
      }
  
      public synchronized void get(){
          //当仓库空了，消费者线程停下来
          if (total <= 0){
              try {
                  //这个方法是由消费者线程调用的
                  //obj.wait ();//使用obj作为锁对象
                  this.wait ();
              } catch (InterruptedException e) {
                  e.printStackTrace ();
              }
          }
          total--;
          try {
              Thread.sleep (100);
          } catch (InterruptedException e) {
              e.printStackTrace ();
          }
          System.out.println ("卖了一台电视机，现在的库存量是：" + total);
  
          //唤醒在此监视器对象this等待的单个线程；因为现在只有两个线程，它唤醒的就是
          //对象，即生产者线程
          this.notify ();
      }
  }
  
  class Woker extends Thread {
      private HouseWare h;
  
      public Woker(HouseWare h){
          super();
          this.h = h;
      }
  
      @Override
      public void run(){
          //不断的生产，不断的往仓库放
          while (true){
              h.put();
          }
      }
  }
  
  class Salers extends Thread {
      private HouseWare h;
  
      public Salers(HouseWare h){
          super();
          this.h = h;
      }
  
      @Override
      public void run(){
          //不断的售卖，不断的往仓库拿
          while (true){
              h.get();
          }
      }
  }
  ```

##### 多个生产者与消费者

![多个生产者与消费者](images\grammar\多个生产者与消费者.png)

+ 解决方案：
  + 生产者指定唤醒的是消费者，消费者唤醒的是生产者，juc；
  + 在被唤醒的地方，醒来后不是急于做工作，而是判断最新的条件是否满足，使用while作为判断条件；
  + 要求：
    + wait()+notifyAll()；
    + 在wait()被唤醒之后，一定要重新判断条件；

#### 死锁问题

多个线程互相持有对方想要的资源，互不相让，就会发生死锁；

```java
public class TestDeadLock {
    public static void main(String[] args) {
        Object money = new Object ();
        Object girl = new Object ();

        BangFei bang = new BangFei (money,girl);
        BoyFried boy = new BoyFried (money,girl);

        bang.start ();
        boy.start ();
    }
}

class BangFei extends Thread {
    private Object money;
    private Object girl;

    public BangFei(Object money,Object girl){
        super();
        this.money = money;
        this.girl = girl;
    }

    @Override
    public void run(){
        synchronized (girl) {
            System.out.println ("你给我500w，我放了你女朋友");
        }
        synchronized (money){
            System.out.println ("放人");
        }
    }
}

class BoyFried extends Thread {
    private Object money;
    private Object girl;

    public BoyFried(Object money,Object girl){
        super();
        this.money = money;
        this.girl = girl;
    }
    @Override
    public void run(){
        synchronized (money){
            System.out.println ("你先放了，我给你500w");
        }
        synchronized (girl){
            System.out.println ("给钱");
        }
    }
}
```

#### 龟兔赛跑问题

```java
/**
 * 1. 案例题目描述:编写龟兔赛跑多线程程序，设赛跑长度为30米
 * 1)乌龟和兔子每跑完10米输出一次结果。
 * 2)兔子的速度是10米每秒,兔子每跑完10米休眠的时间10秒
 * 3)乌龟的速度是1米每秒,乌龟每跑完10米的休眠时间是1秒
 * 2. 案例完成思路要求：
 * 1)乌龟一个线程,兔子一个线程
 * 2)两个线程同时开启
 * 3)提示：可以使用Thread.sleep(毫秒数)来模拟耗时
 */
public class TestExam2 {
    public static void main(String[] args) {
        WuGui w = new WuGui ();
        TuZi t = new TuZi ();

        w.start ();
        t.start ();
    }
}

class WuGui extends Thread {
    private static final int DISTANCE = 30;
    private int length;
    @Override
    public void run(){
        while (true){
            try {
                Thread.sleep (1000);//模拟跑的时间，1米/秒
            } catch (InterruptedException e) {
                e.printStackTrace ();
            }

            length++;

            if (length % 10 ==0){
                System.out.println ("乌龟已经跑了" + length + "米");
                try {
                    Thread.sleep (1000);//模拟乌龟跑了每10米后休息1秒
                } catch (InterruptedException e) {
                    e.printStackTrace ();
                }
            }

            if (length >= DISTANCE){
                System.out.println ("乌龟已经到达终点");
                break;
            }
        }
    }
}

class TuZi extends Thread {
    private static final int DISTANCE = 30;
    private int length;
    @Override
    public void run(){
        while (true){
            try {
                Thread.sleep (100);//模拟跑的时间，1米/0.1秒
            } catch (InterruptedException e) {
                e.printStackTrace ();
            }

            length++;

            if (length % 10 ==0){
                System.out.println ("兔子已经跑了" + length + "米");
                try {
                    Thread.sleep (10000);//模拟兔子跑了每10米后休息10秒
                } catch (InterruptedException e) {
                    e.printStackTrace ();
                }
            }

            if (length >= DISTANCE){
                System.out.println ("兔子已经到达终点");
                break;
            }
        }
    }
}
```

```java
public class TestExam3 {
    public static void main(String[] args) {
        Race r1 = new Race ("乌龟", 1000, 1000);
        Race r2 = new Race ("兔子", 100, 10000);

        r1.start ();
        r2.start ();
    }
}

class Race extends Thread {
    private static final int DISTANCE = 30;
    private int length;
    private long speed;//每秒需要的时间,单位毫秒
    private long rest;//每10米需要休息的时间，单位毫秒

    public Race(String name,long speed,long rest) {
        super(name);
        this.speed = speed;
        this.rest = rest;
    }

    @Override
    public void run(){
        long start = System.currentTimeMillis ();
        while (true){
            try {
                Thread.sleep (speed);
            } catch (InterruptedException e) {
                e.printStackTrace ();
            }

            length++;

            if (length >= DISTANCE){
                System.out.println (getName() + "已经到达终点");
                break;
            }

            if (length % 10 == 0){
                System.out.println (getName() + "已经跑了" + length + "米");
                try {
                    Thread.sleep (rest);//模拟乌龟跑了每10米后休息1秒
                } catch (InterruptedException e) {
                    e.printStackTrace ();
                }
            }
        }

        long end = System.currentTimeMillis ();
        System.out.println (getName () + "一共花了" + (end - start)/1000 + "秒");
    }
}
```

### 反射

#### 反射的概念与获取

##### 概念

1. 目的：希望代码的灵活度更高，耦合度（相互依赖）更低；

2. Java是一个强类型的语言，所有的操作都要先知道类型，然后造对象，最后调用方法等，是静态语言，在声明变量之前需要先确定类型；

3. Java又是一个准动态语言，希望实现动态语言能实现的效果：在运行期间再确定对象的数据类型， 动态的调用方法；因此引入了反射机制；

4. 因为Java中把每一种类型，在运行时加载到内存中，然后生成一个唯一的Class对象来代表这个类型，或者说用Class对象来存储这个类型的所有信息；

   例如：String -->Class对象，通过Class对象就可以得到String类型的所有对象，也可以通过Class对象创建String对象，也可以调用String的任意方法；

5. Class就是反射的根源；

6. <font color='red'>反射机制的原理：</font>

   + 在Java中，每一种类型被加载到内存中后，都会生成一个唯一的Class对象来表示这个类型，Class是反射的根源；
   + 通过这个Class对象，我们可以获取这个类型的所有信息，包括包、修饰符、名称、父类、父接口、属性、构造器、方法等；
   + 通过这个Class对象的newInstance方法或通过Class对象获取Constructor对象都可以创建这个类型的实例；
   + 通过这个Class对象可以获取某个属性，并且设置该属性的值或获取该属性的值；
   + 通过这个Class对象，在运行时调用该类型的任意一个方法；
   + 从而实现Java的准动态语言的特性，在运行时创建任意类型的对象，操作任意对象的属性和方法，而不是在编译时；

##### Class对象的四种获取方式

+ 注意：

  + Class对象不是程序员创建的，而是在类加载的过程中，类加载器负责创建的；
  + 要先加载到内存中，在运行期间才能获取到；
  + 反过来说，在运行是，这个类型是存在的，如果这个类型不存在，那么会报异常，ClassNotFoundException；

+ 获取方式：

  + Class.forName("包.类名")；

    ```java
    Class c = Class.forName("com.atezsvs.bean.Student");
    ```

  + ClassLoader对象.loadClass(“包.类名”)；

    + 先得到类加载器的对象：

      ```java
      ClassLoader loader = ClassLoader.getSystemClassLoader();
      ```

    + 通过类加载器的对象去加载，获取某个类的Class对象；

      ```java
      Class c = loader.loadClass("java.lang.String");
      ```

  + 如果说某个类型在编译期间就存在，可以通过类名.class获取；

    ```java
    Class c = String.class;
    ```

  + 可以通过对象，获取这个对象的类型对应的class对象；
  
    ```java
    实例对象.getClass()//获取对象的运行时类型，是属于Object的方法
    ```

```java
import org.junit.Test;

import java.util.Date;

public class TestClass {
    @Test
    public void test1() {
        try {
            Class c = Class.forName("com.atezsvs.bean.Student");
            Object obj = c.newInstance();//创建Student的对象
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    @Test
    public void test2() throws ClassNotFoundException {
        ClassLoader loader = ClassLoader.getSystemClassLoader();
        //loader.loadClass("com.atezsvs.bean.Student");
        Class c = loader.loadClass("java.lang.String");
        System.out.println(c);
    }

    @Test
    public void test3(){
        Class c = String.class;
        System.out.println(c);
    }

    public void method(Object obj){
        Class c = obj.getClass();//获取对象的运行时类型，Object是它的编译时类型
        System.out.println(c);
    }

    @Test
    public void test4(){
        method(new Date());
    }
}
```

#### Class的API

##### 在运行时创建任意类型的对象

###### 通过Class对象来创建该类型的实例对象

```java
Object obj = Class的对象.newInstance()；
```

+ 要求：
  + 类型必须有公共的无参构造；

```java
import org.junit.Test;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.Date;

public class TestClassMethod {
    @Test
    public void test1() throws IllegalAccessException, InstantiationException {
        Class clazz = String.class;
        Object str = clazz.newInstance();

        Class clazz2 = Date.class;
        Object date = clazz2.newInstance();
        System.out.println(date);
    }

    @Test
    public void test2() throws IllegalAccessException, InstantiationException, ClassNotFoundException {
        Class clazz = Class.forName("day25.Student");
        Object obj = clazz.newInstance();
        System.out.println(obj);
    }
}
```

###### 用Class对象获取构造器的信息，然后用构造器创建对象

+ 步骤：

  + 先得到构造器对象；

    + 得到Student的对象的构造器；

      ```java
      Constructor[] cs1 = clazz.getConstructors();
      ```

    + 得到Student的所有构造器；

      ```java
      Constructor[] cs2 = clazz.getDeclaredConstructors();
      ```

    + 得到Student的其中一个公共的构造器；

      ```java
      Constructor c = clazz.getConstructor(int.class, String.class);
      ```

    + 得到Student的其中一个声明的构造器；

      ```java
      Constructor c2 = clazz.getDeclaredConstructor(String.class, int.class);
      ```

  + 通过构造器对象.newInatance(Object... args)创建对象；

    ```java
    Object stu = c2.newInstance("张三", 25);
    ```

```java
import org.junit.Test;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.Date;

    @Test
    public void test3() throws IllegalAccessException, InstantiationException, ClassNotFoundException, NoSuchMethodException, InvocationTargetException {
        Class clazz = Class.forName("day25.Student");

        //1、得到Student的对象的构造器
        //(1)得到Student的所有公共的构造器
        //Constructor[] cs1 = clazz.getConstructors();
        //(2)得到Student的所有构造器
        //Constructor[] cs2 = clazz.getDeclaredConstructors();
        //(3)得到Student的其中一个公共的构造器
        //多个重载的构造器靠形参列表的类型与个数决定
        //Constructor c = clazz.getConstructor(int.class, String.class);
        //(4)得到Student的其中一个构造器
        Constructor c2 = clazz.getDeclaredConstructor(String.class, int.class);

        //2、用构造器创建对象
        Object stu = c2.newInstance("张三", 25);

        System.out.println(stu);
    }
}
```

##### 通过Class对象操作属性

1. 得到某个属性：Class对象.getField()系列；

   + 得到所有的公共属性：

     ```java
     Field[] fs1 = clazz.getFields();
     ```

   + 得到所有的属性，包括公共的和私有的；

     ```java
     Field[] fs2 = clazz.getDeclaredFields();
     ```

   + 得到其中的一个属性，公共的；

     ```java
     Field field = clazz.getField("age");
     ```

   + 得到声明过的一个属性，包括私有的；

     ```java
     Field field2 = clazz.getDeclaredField("age");
     ```

   ```java
   import org.junit.Test;
   
   import java.lang.reflect.Field;
   
   public class TestClassMethod2 {
       @Test
       public void test1() throws ClassNotFoundException, NoSuchFieldException {
           Class clazz = Class.forName("day25.Student");
   
           //(1)得到所有的公共属性
   //        Field[] fs1 = clazz.getFields();
   //        for (Field field : fs1) {
   //            System.out.println(field);
   //        }
   
           //(2)得到所有的属性
   //        Field[] fs2 = clazz.getDeclaredFields();
   //        for (Field field : fs2) {
   //            System.out.println(field);
   //        }
   
           //(3)得到其中的一个属性，公共的
           //Field field = clazz.getField("age");
   
           //(4)得到声明过的一个属性，包括私有的
           Field field2 = clazz.getDeclaredField("age");
           System.out.println(field2);
       }
   }
   ```

2. 获取某个实例对象的属性值；

3. 设置某个实例对象的属性值；

   ```java
   import org.junit.Test;
   
   import java.lang.reflect.Constructor;
   import java.lang.reflect.Field;
   import java.lang.reflect.InvocationTargetException;
   
   public class TestClassMethod2 {
       @Test
       public void test1() throws ClassNotFoundException, NoSuchFieldException, IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
           Class clazz = Class.forName("day25.Student");
   
           //(1)得到所有的公共属性
   //        Field[] fs1 = clazz.getFields();
   //        for (Field field : fs1) {
   //            System.out.println(field);
   //        }
   
           //(2)得到所有的属性
   //        Field[] fs2 = clazz.getDeclaredFields();
   //        for (Field field : fs2) {
   //            System.out.println(field);
   //        }
   
           //(3)得到其中的一个属性，公共的
           //Field field = clazz.getField("age");
   
           //(4)得到声明过的一个属性，包括私有的
           Field field2 = clazz.getDeclaredField("age");
           System.out.println(field2);
   
           //field2对象代表age属性
           //Object stu = clazz.newInstance();//通过无参构造创建一个学生对象
           Constructor c2 = clazz.getDeclaredConstructor(String.class, Integer.class);
           Object stu = c2.newInstance("张三", 25);
   
           //field2因为是私有的，无法直接访问，Java的安全机制，默认是不能访问私有的成员的
           //可以设置field2可以被访问
           field2.setAccessible(true);
           Object age = field2.get(stu);
           System.out.println(age);
   
           //得到name的属性值
           Field field3 = clazz.getDeclaredField("name");
           field3.setAccessible(true);
           Object name = field3.get(stu);
           System.out.println(name);
       }
   
       @Test
       public void test2() throws ClassNotFoundException, IllegalAccessException, InstantiationException, NoSuchFieldException {
           Class clazz = Class.forName("day25.Student");
           Object stu = clazz.newInstance();
   
           //想要设置stu的age的属性值
           Field field = clazz.getDeclaredField("age");
           field.setAccessible(true);
           field.set(stu,26);
   
           //想要设置stu的name属性值
           Field field2 = clazz.getDeclaredField("name");
           field2.setAccessible(true);
           field2.set(stu,"李四");
   
           System.out.println(stu);
       }
   }
   ```

##### 通过Class对象操作方法

1. 得到某个类型的任意一个方法

   + 得到所有的公共的方法；

     ```java
     Method[] ms1 = clazz.getMethods();
     ```

   + 得到所有的方法；

     ```java
     Method[] ms2 = clazz.getDeclaredMethods();
     ```

   + 得到一个公共的方法；

     + getMethod("方法名",该方法的形参列表的类型列表)；
     + 如果无参，那么该方法的形参列表的类型列表就空着；

     ```java
     Method ms3 = clazz.getMethod("getInfo");
     ```

   + 得到一个方法，包括私有的；

     ```java
     Method ms4 = clazz.getDeclaredMethod("getInfo");
     ```

   + 如果某个方法不是公共的，可以将setAccessible设置为true进行访问；

     ```java
     ms4.setAccessible(true);
     ```

   ```java
   import org.junit.Test;
   
   import java.lang.reflect.InvocationTargetException;
   import java.lang.reflect.Method;
   
   @SuppressWarnings("all")
   public class TestClassMethod3 {
       @Test
       public void test1() throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException {
           Class clazz = Class.forName("day25.Student");
   
   
           //得到方法
           //(1)得到所有的公共的方法
           Method[] ms1 = clazz.getMethods();
   
           //(2)得到所有的方法
           Method[] ms2 = clazz.getDeclaredMethods();
   
           for (Method method : ms2) {
               System.out.println(method);
           }
   
           //(3)得到一个公共的方法
           //getMethod("方法名",该方法的形参列表的类型列表)
           //如果无参，那么该方法的形参列表的类型列表就空着
           Method ms3 = clazz.getMethod("getInfo");
   
           //(4)得到一个方法，包括私有的
           Method ms4 = clazz.getDeclaredMethod("getInfo");
           ms4.setAccessible(true);//如果这个方法不是公共的，可以设置为此进行访问
           System.out.println(ms4);
       }
   }
   ```

2. 调用任意一个方法；

   + 需要先获得class类对象，再进行调用方法；

   ```java
   import org.junit.Test;
   
   import java.lang.reflect.InvocationTargetException;
   import java.lang.reflect.Method;
   
   @SuppressWarnings("all")
   public class TestClassMethod3 {
       @Test
       public void test1() throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException {
           Class clazz = Class.forName("day25.Student");
   
   
           //得到方法
           //(1)得到所有的公共的方法
           //Method[] ms1 = clazz.getMethods();
   
           //(2)得到所有的方法
   //        Method[] ms2 = clazz.getDeclaredMethods();
   //
   //        for (Method method : ms2) {
   //            System.out.println(method);
   //        }
   
           //(3)得到一个公共的方法
           //getMethod("方法名",该方法的形参列表的类型列表)
           //如果无参，那么该方法的形参列表的类型列表就空着
           //Method ms3 = clazz.getMethod("getInfo");
   
           //(4)得到一个方法，包括私有的
           Method ms4 = clazz.getDeclaredMethod("getInfo");
           ms4.setAccessible(true);//如果这个方法不是公共的，可以设置为此进行访问
           System.out.println(ms4);
   
           //调用这个方法
           //先创建类对象
           Object stu = clazz.newInstance();
           //调用类对象的无参方法
           Object returnValue = ms4.invoke(stu);
   
           System.out.println(returnValue);
       }
   
       @Test
       public void test2() throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException {
           Class clazz = Class.forName("day25.Student");
   
           //(4)得到Student的setName(String name)方法
           Method ms = clazz.getDeclaredMethod("setName", String.class);//String.class属于setName的形参列表
           System.out.println(ms);
   
           //调用这个方法
           //先创建类对象
           Object stu = clazz.newInstance();
           //调用这个对象的有参方法
           Object returnValue = ms.invoke(stu,"张三");//“张三”属于实参列表
   
           System.out.println(returnValue);
   
           System.out.println(stu);
       }
   }
   ```

##### 通过Class对象获取类型的详细信息

+ getName()：获取类型名；

+ getPackage()：获取包名；

+ getModifiers()：获取修饰符；

+ getSuperClass()：获取父类；

+ getInterfaces()：获取实现的接口；

  ```java
  import java.lang.reflect.Modifier;
  
  public class TestClassMethod4 {
      public static void main(String[] args) throws Exception {
          Class clazz = Class.forName("day25.Student");
  
          System.out.println("类型的名称：" + clazz.getName());
  
          Package pack = clazz.getPackage();
          System.out.println("包名：" + pack);
  
          int mod = clazz.getModifiers();
          System.out.println("修饰符：" + mod);
          String string = Modifier.toString(mod);
          System.out.println(string);
  
          Class superclass = clazz.getSuperclass();
          System.out.println("父类：" + superclass);
  
          Class[] interfaces = clazz.getInterfaces();
          System.out.println("实现的接口们：");
          for (Class anInterface : interfaces) {
              System.out.println(anInterface);
          }
      }
  }
  ```

##### 通过Class对象获取注解信息

如果想要被反射获取到这个注解信息，该注解的声明周期必须是RUNTIME，即声明这个注解时，在注解的上面必须有一个元注解：@Retention(RentionPolicy.RUNTIME)；

###### 得到类上的注解信息

1. 得到Class；
2. 得到类上的注解对象；
3. 得到注解的配置参数值；

```java
import org.junit.Test;

import java.lang.annotation.Annotation;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.reflect.Method;

public class TestClassMethod5 {
    @Test
    public void test1(){
        //得到MyClass类上面的注解的value属性值
        //(1)得到Class
        Class clazz = MyClass.class;

        //(2)得到类上的注解对象
        Annotation annotation = clazz.getAnnotation(MyAnnotion.class);
        MyAnnotion my = (MyAnnotion)annotation;

        //(3)得到注解的配置参数值
        String value = my.value();
        System.out.println(value);
    }
}

@MyAnnotion("尚硅谷")
@YourAnnotion
class MyClass{

    @MyAnnotion("欧阳")
    public void test(){

    }
}

@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotion{
    String value() default "atguigu";
}

@interface YourAnnotion{
    String info() default "atguigu";
}
```

###### 得到方法上的注解信息

1. 得到Class；
2. 得到method对象；
3. 得到方法上的注解对象；
4. 得到注解的配置参数值；

```java
import org.junit.Test;

import java.lang.annotation.Annotation;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.reflect.Method;

public class TestClassMethod5 {
    @Test
    public void test2() throws NoSuchMethodException {
        //得到MyClass类上面的注解的value属性值
        //(1)得到Class
        Class clazz = MyClass.class;

        //(2)得到method对象
        Method method = clazz.getDeclaredMethod("test");

        //(3)得到方法上的注解对象
        Annotation annotation = method.getAnnotation(MyAnnotion.class);
        MyAnnotion my = (MyAnnotion)annotation;

        //(4)得到注解的配置参数值
        String value = my.value();
        System.out.println(value);
    }
}

@MyAnnotion("尚硅谷")
@YourAnnotion
class MyClass{

    @MyAnnotion("欧阳")
    public void test(){

    }
}

@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotion{
    String value() default "atguigu";
}

@interface YourAnnotion{
    String info() default "atguigu";
}
```

##### 通过Class对象来获取父类的泛型信息

###### 在类外得到泛型信息

1. 得到子类的Class对象；

   ```java
   Class<Son> clazz = Son.class;
   ```

2. 得到带泛型的父类的Type对象；

   ```java
   Type type = clazz.getGenericSuperclass();
   ```

3. 把Type类型强制转成ParameterizedType，参数化的类型；

   ```java
   ParameterizedType p = (ParameterizedType)type;
   ```

4. 得到泛型实参的类型；

   ```java
   Type[] actualTypeArguments = p.getActualTypeArguments();
   ```

```java
import org.junit.Test;

import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

@SuppressWarnings("all")
public class TestClassMethod6 {
    @Test
    public void test1(){
        //（1）得到子类的Class对象
        //得到Son在继承父类时，指定的泛型实参类型
        Class<Son> clazz = Son.class;
        //getSuperclass方法只能得到父类，不包含泛型信息
//        Class<? super Son> s = clazz.getSuperclass();
//        System.out.println(s);

        //（2）得到带泛型的父类的Type对象
        //如果想要得到带泛型的父类，必须使用getGenericSuperclass()，而不能使用getSuperclass()
        Type type = clazz.getGenericSuperclass();

        //（3）把Type类型强制转成ParameterizedType，参数化的类型
        //Father<String>属于Type中的ParameterizedType(参数化的类型)
        ParameterizedType p = (ParameterizedType)type;

        //（4）得到泛型实参的类型
        //ParameterizedType有一个方法可以获取泛型实参
        Type[] actualTypeArguments = p.getActualTypeArguments();
        for (Type t : actualTypeArguments) {
            System.out.println(t);
        }
    }
}

//泛型类
//T：泛型形参

abstract class Father<T,U> {

}

//子类不是泛型类，但它的父类是一个泛型类
//String:泛型实参
class Son extends Father<String,Integer> {

}
```

###### 在泛型父类中得到泛型信息

1. 得到子类的Class对象；
2. 得到子类的父类的Type对象，带泛型信息的父类；
3. 强制转换类型；
4. 得到泛型实参；

```java
import org.junit.Test;

import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

@SuppressWarnings("all")
public class TestClassMethod6 {
    @Test
    public void test2(){
        Son son = new Son();
        Class t1 = son.gettType();
        Class t2 = son.getuType();

        System.out.println(t1);
        System.out.println(t2);
    }
}

//泛型类
//T：泛型形参
abstract class Father<T,U> {
    //在Father类型中得到T的实际类型
    //只有在某个类型继承Father时，才能确定T的实际类型
    private Class tType;
    private Class uType;

    public Class gettType() {
        return tType;
    }

    public Class getuType() {
        return uType;
    }

    public Father(){
        //（1）得到子类的Class对象
        Class clazz = this.getClass();//this在构造器中代表的是正在创建的那个实例对象

        //（2）得到子类的父类的Type对象，带泛型信息的父类
        Type type = clazz.getGenericSuperclass();

        //(3)强转类型
        ParameterizedType p = (ParameterizedType)type;

        //(4)得到泛型实参
        Type[] actualTypeArguments = p.getActualTypeArguments();
        tType = (Class)actualTypeArguments[0];
        uType = (Class)actualTypeArguments[1];
    }
}

//子类不是泛型类，但它的父类是一个泛型类
//String:泛型实参
class Son extends Father<String,Integer> {

}
```

#### Class小结

1. Class是所有反射的根源；
2. 四种获Class对象的方式：
   + 已知类型：类型.class；
   + 持有对象：对象.getClass()；
   + 需要知道类型的全名称：Class.forName("包名.类名")；
   + 需要知道类型的全名称：ClassLoader.getSystemClassLoader().loadClass("包名.类名")；
3. Class的API：
   + 用Class对象创建类型的实例对象；
     + 通过Class对象的newInstance()：要求该类型必须有无参构造；
     + 通过Class对象先得到该类型的构造器对象，然后通过构造器对象.newInstance(...)；
   + 用Class对象获取某个属性，并设置或获取属性值；
     + 先得到属性对象Field；
     + 得到实例对象，因为属性是属于某个实例的；
     + 设置或获取属性值：
       + Field对象.set(实例对象，新的属性值)；
       + Object  属性值 = Field对象.get(实例对象)；
   + 用Class对象获取某个方法，并调用这个方法；
     + 先得到方法对象Method；
     + 得到实例对象，因为方法是属于某个实例；
     + 调用方法：
       + Object 方法的返回值 = Method对象.invoke(实例对象，方法的实参列表)；
   + 用Class对象获取类型的其他信息（包、修饰符、不带反省的父类、不带泛型的接口...）：
   + 用Class对象获取注解；
   + 用Class对象获取泛型；

#### 什么类型有Class对象

1. 8中基本数据类型；
2. void类型；
3. 数组类型；
4. 类；
5. 接口；
6. 枚举；
7. 注解；
8. Type；

+ 注意：

  + Object是Class的父类，但是Object这个类型被加载到内存，也是用一个Class对象表示的；

  + Class类型是一类事务的抽象表现形式，这类食物有公共的特征；

  + Method：所有方法的抽象表现形式；

    ```java
    [修饰符] 返回值类型 方法名(形参列表) 抛出的异常列表{
        
    }
    ```

    + 共同的行为：被调用，invoke；

  + Constructor：

    ```java
    [修饰符] 构造器名称(形参列表) 抛出的异常列表{
        
    }
    ```

    + 共同的行为：创建实例，newInstance；

  + Field：

    ```java
    修饰符 数据类型 属性名;
    ```

    + 共同的行为：get/set；

```java
import com.sun.corba.se.spi.ior.ObjectKey;
import com.sun.org.apache.bcel.internal.generic.Type;
import org.junit.Test;

import java.io.Serializable;

public class TestClassType {
    @Test
    public void test1() {
        System.out.println(int.class);
        System.out.println(char.class);

        System.out.println(void.class);

        int[] array = new int[5];
        //array数组类型：int[]
        //array元素类型：int
        //array是一个对象,这个对象的类型是数组类型，是int[]
        Class c1 = int[].class;
        Class c2 = array.getClass();
        System.out.println(c1 == c2);//true

        int[] newArray = new int[10];
        Class c3 = newArray.getClass();
        System.out.println(c2 == c3);//true

        int[][] two = new int[4][5];
        //two是一个二维数组，其数组类型是：int[][]
        Class c4 = two.getClass();
        System.out.println(c2 == c4);//false
    }

    @Test
    public void test2(){
        Class c1 = String.class;
        Class c2 = "".getClass();
        System.out.println(c1 == c2);//true
    }

    @Test
    public void test3(){
        Class c1 = Serializable.class;
        Class c2 = Week.class;
        Class c3 = Override.class;
        Class<Type> c4 = Type.class;
    }

    @Test
    public void test4(){
        Class c = Object.class;
        Object obj = c;//向上转型
        Class cc = Class.class;
    }
}

enum Week{
    MONDAY,TUESDAY
}
```

#### 类加载ClassLoader

##### 类加载的作用

1. 加载类：负责加载某个类型（加载它的.class字节码），并完成类的初始化，在内存中生成一个class对象；
2. 加载资源文件：配置文件、图片等；
   + 要求必须是类路径下的资源才能使用类加载器加载；

##### 类加载的过程

##### 类加载器的层次结构

###### 层次结构

1. 引导类加载器：bootstrap class loader；
   + 负责加载Java的核心库（JAVA_HOME/jre/lib/rt.jar或sun.boot.class.path路径下的内容），最核心的部分，这个类加载器不是用java语言实现的；
   + 引导类加载器的getClassLoader()为null；
2. 扩展类加载器：extensions class loader；
   + 负责加载Java的扩展库（JAVA_HOME/jre/ext/*.jar或java.ext.dirs路径下的内容）；
   + Class对象.getClassLoader()得到类加载器对象；
   + 扩展类加载器把引导类加载器认作父母，即”父类加载器“；
3. 应用程序类加载器：application class loader；
   + 负责加载用户自定义的类型；
   + 应用程序类加载器把扩展类加载器认作父母，即”父类加载器“；
4. 自定义类加载器：tomcat的类加载器就是自定义的；
   + 要求继承ClassLoader类型；

###### java的类加载器的设计：双亲委托模式

应用程序类加载器接到一个加载某个类的任务，不是自己去找这个.class，而是先交给它的”父类加载器“即扩展类加载器，扩展类加载器又把这个任务交给它的父类加载器即引导类加载器，如果引导类加载器可以加载这类，就由它加载；如果引导类加载器在它的管辖范围内找不到这个类，把任务重新交给扩展类加载器，它开始在它的管辖范围内查找，如果找到就找到了，如果它也没找到，重新交给应用程序类加载器，它在它的管辖范围内查找，如果找到就加载，如果找不到，报ClassNotFoundException；

如果某个类已经加载过，应用程序类加载器接到一个加载某个类的任务，会在内存中先搜索，如果内存中可以找到对应的Class对象，那么它是不会把任务往上传的，直接就返回内存中的Class对象；

+ 为什么使用双亲委托模式：这是为了安全考虑；阻止我们写和JDK的核心类库一样的类型，不会覆盖核心类库；

##### 使用类加载器和FileInputStream加载资源文件

+ 方式一：在src目录下，使用ClassLoader的静态方法，只适用于JavaSE；

  + src路径即Java的类路径bin，在类路径下的文件，可以使用类加载器；

    + 在src的根目录下：

      ```java
      pro.load(ClassLoader.getSystemResourceAsStream("info.properties"));
      ```

    + 在src的其他路径下：

      ```java
      pro.load(ClassLoader.getSystemResourceAsStream("day25/info.properties"));
      ```

+ 方式二：在非src路径下，可以使用IO流FileInputStream进行加载

  + 在项目的根路径下：

    ```java
    FileInputStream fis = new FileInputStream("info.properties");
    pro.load(fis);
    ```

  + 在项目的其他文件夹下：

    ```java
    FileInputStream fis = new FileInputStream("download/info.properties");
    pro.load(fis);
    ```

+ 方式三：使用ClassLoader的对象加载，适用于SE和EE；

  ```java
  Class c = TestClassLoaderResource.class;   pro.load(c.getClassLoader().getResourceAsStream("info.properties"));
  ```

```java
import java.io.FileInputStream;
import java.util.Properties;

public class TestClassLoaderResource {
    public static void main(String[] args) throws Exception{
        //在src下，即在bin下，类路径下
        //在类路径下的文件，可以使用类加载器
        Properties pro = new Properties();

        //(1)方式一：ClassLoader的静态方法，只适用于SE
        //在src的根目录下
        //pro.load(ClassLoader.getSystemResourceAsStream("day25/info.properties"));

        //在src的某个包中
     //pro.load(ClassLoader.getSystemResourceAsStream("info.properties"));

        //(2)方式二：非src路径下
        //在项目的根目录下
        //FileInputStream fis = new FileInputStream("info.properties");
        //pro.load(fis);

        //在项目的其他文件夹下面
        FileInputStream fis = new FileInputStream("download/info.properties");
        pro.load(fis);

        //(3)方式三：ClassLoader的对象加载，适用于SE和EE
        //如果web项目中，src下的资源文件怎么加载
        //因为tomcat自定义了类加载器
        Class c = TestClassLoaderResource.class;
      pro.load(c.getClassLoader().getResourceAsStream("info.properties"));

        String username = pro.getProperty("user");
        String password = pro.getProperty("pass");

        System.out.println("用户名：" + username);
        System.out.println("密码：" + password);
    }
}
```

#### 反射的应用

##### 静态代理

+ 三个角色：
  + 主题：接口；
  + 被代理者；
  + 代理者；
+ 如果多个主题，然后代理者做的事情是一样的，这个时候就会出现很多代理类，而这些代理类的相似度非常高，重复代码很多；

```java
import javax.print.attribute.standard.MediaSize;

public class TestJingTaiProxy {
    public static void main(String[] args) {
        UserDAOImpl ud = new UserDAOImpl();//被代理者
        DAOProxy up = new DAOProxy(ud);//代理者
        up.add();

        GoodsDAOImpl gd = new GoodsDAOImpl();//被代理者
        DAOProxy dp = new DAOProxy(gd);//代理者
        dp.add();
    }
}

//1、主题1
interface DAO {
    void add();
}

//另一个主题2
interface OtherSubjects{
    void method();
}

//2、主题1被代理者
class UserDAOImpl implements DAO {
    @Override
    public void add() {
        System.out.println("添加一个用户");
    }
}

//2、主题1被代理者
class GoodsDAOImpl implements DAO{
    @Override
    public void add() {
        System.out.println("添加一个商品");
    }
}

////3、主题1代理者
//class UserProxy implements DAO{
//    private DAO target;
//
//    public UserProxy() {
//    }
//
//    public UserProxy(DAO target) {
//        this.target = target;
//    }
//
//    @Override
//    public void add() {
//        System.out.println("权限验证");
//        target.add();
//        System.out.println("记录日志");
//    }
//}
//
////4、主题1代理者
//class GoodsProxy implements DAO {
//    private DAO target;
//
//    public GoodsProxy() {
//    }
//
//    public GoodsProxy(DAO target) {
//        this.target = target;
//    }
//
//    @Override
//    public void add() {
//        System.out.println("权限验证");
//        target.add();
//        System.out.println("记录日志");
//    }
//}


//将主题1代理者3、4合并为一类
class DAOProxy implements DAO{
    private DAO target;

    public DAOProxy() {
    }

    public DAOProxy(DAO target) {
        this.target = target;
    }

    @Override
    public void add() {
        System.out.println("权限验证");
        target.add();
        System.out.println("记录日志");
    }
}

//主题2被代理者
class OtherImpl implements OtherSubjects {
    @Override
    public void method() {
        System.out.println("另一个主题的被代理者的方法实现");
    }
}

//主题2代理者
class OtherProxy implements OtherSubjects {
    private OtherSubjects target;

    public OtherProxy() {
    }

    public OtherProxy(OtherSubjects target) {
        this.target = target;
    }

    @Override
    public void method() {
        System.out.println("权限验证");
        target.method();//被代理者的方法
        System.out.println("记录日志");
    }
}
```

##### 动态代理

+ 三个角色：

  + 主题；
  + 代理者；
  + 被代理者；

+ 动态代理的步骤：

  + 写主题；

  + 写被代理者；

  + 代理任务处理器：写代理者要替被代理者完成的代理任务；

    + 要求：必须声明一个处理器的类型，该类型必须实现一个接口InvocationHandler；

  + 写代理类及代理类的对象；

    + 动态生成代理类；

      + ```java
        //Proxy.getProxyClass(被代理者类加载器对象,被代理者实现的接口)
        Proxy.getProxyClass(loader,interfaces)
        ```

      + ```java
        //Proxy.newProxyInstance(被代理者的类加载器对象，被代理者实现的接口，代理任务的处理器对象)
        Proxy.newProxyInstance(loader，interfaces,h)
        ```

```java
import org.junit.Test;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class TestDongTaiProxy {
    @Test
    public void test1() throws Exception{
        UserDAOImpl ud = new UserDAOImpl();//被代理者
        //1、动态生成代理类
        Class clazz = ud.getClass();//ud的Class类对象
        ClassLoader loader = clazz.getClassLoader();//udClass类对象的类加载器

        Class[] interfaces = clazz.getInterfaces();

        //得到的是代理类的Class对象
        //Proxy.getProxyClass(ud.getClass().getClassLoader(),interfaces);
        Class proxyClass = Proxy.getProxyClass(loader, interfaces);

        //2、创建代理类的对象
        Object proxy = proxyClass.newInstance();

        //3、如果假设主题已知
        DAO dao = (DAO)proxy;//代理类和被代理类实现了同一个接口
        dao.add();
    }

    @Test
    public void test2(){
        UserDAOImpl ud = new UserDAOImpl();//被代理者
        //1,2合并，直接得到代理类的对象
        Object proxy = Proxy.newProxyInstance(ud.getClass().getClassLoader(), ud.getClass().getInterfaces(), new MyHandler(ud));

        DAO dao = (DAO)proxy;
        dao.add();

        OtherImpl other = new OtherImpl();//被代理者
        Object p2 = Proxy.newProxyInstance(other.getClass().getClassLoader(), other.getClass().getInterfaces(), new MyHandler(other));
        OtherSubjects s = (OtherSubjects)p2;
        s.method();
    }
}
//1、主题1
interface DAO {
    void add();
}

//1、主题2
interface OtherSubjects{
    void method();
}

//2、被代理者1
class UserDAOImpl implements DAO {
    @Override
    public void add() {
        System.out.println("添加一个用户");
    }
}

//2、被代理者2
class GoodsDAOImpl implements DAO{
    @Override
    public void add() {
        System.out.println("添加一个商品");
    }
}

//2、被代理者3
class OtherImpl implements OtherSubjects {
    @Override
    public void method() {
        System.out.println("另一个主题的被代理者的方法实现");
    }
}

//3、代理任务处理器
class MyHandler implements InvocationHandler{
    private Object target;//被代理者对象

    public MyHandler() {
    }

    public MyHandler(Object target) {
        this.target = target;
    }

    /**
     * @param proxy 是代理类的对象
     * @param method 被代理者要执行的方法对象
     * @param args 被代理者要执行的方法所需要的实参列表
     * @return
     * @throws Throwable
     */
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("权限验证");
        //调用被代理者的方法
        Object returnValue = method.invoke(target, args);

        System.out.println("记录日志");
        return returnValue;
    }
}
```

### 网络编程

#### 基本概念

1. 网络：把分布在不同地理区域的计算机与专门的外部设备用通信线路互连成一个规模大、功能强的网络系统，从而使众多的计算机可以方便地互相传递信息、共享硬件、软件、数据信息等资源。

2. 网络编程：为了实现直接或间接的网络通信而编写的代码；

3. 网络通信：

   + 通信要素：

     + 地址：IP地址，192.168.31.147    [0,255]；127.0.0.1为本机IP地址；

       + 在Java中用InetAddress类型的对象表示IP地址；

       + InetAddress：表示主机名/IP地址；
     
       + InetAddress.getLocalHost()：本机的IP地址和主机名；
     
       + InetAddress.getByName(“主机名/IP/域名”)；
     
       + InetAddress.getByAddress(byte[])：例如InetAddress.getByAddress({192,168,18,42})；
     
       + InetAddress对象.getHostAddress()：获取其中的IP；
     
       + InetAddress对象.getHostName()：获取其中的主机名；
     
         ```java
         import java.net.InetAddress;
         import java.net.UnknownHostException;
         
         public class TestNet {
             public static void main(String[] args) throws UnknownHostException {
               InetAddress net = InetAddress.getLocalHost();
                 InetAddress[] net2 = InetAddress.getAllByName("www.baidu.com");
         
                 for (InetAddress inetAddress : net2) {
                   System.out.println(inetAddress);
               }
                 System.out.println(net);
                 System.out.println(net2);
             }
         }
         
         ```
       
     + 谁接收：port端口号；
     
       + 0~65535中间的一个数字，但是0~1023之间被知名服务占用，用于特定服务；
       + 其他常见端口：tomcat8080，mysql3306，oracle1521，http80；https443；sql server1433；qq1080；
     
     + 共同的语言：通信(网络)协议；
   
4. 网络协议：

   + 网络的分层模型：

     ![网络协议模型](images\grammar\网络协议模型.png)

   + 传输层：

     + TCP协议(Transmission Control Protocol，传输控制协议)：是一种面向连接的、可靠的、基于字节流的传输协议；分为服务器端和客户端；客户端和服务器端必须先建立连接才能通信；客户端主动与服务器端建立连接；在正式的通信之前，会先经过“三次握手”；断开时进行四次挥手；
     
       ```
       三次握手
       1.	客户端通过向服务器端发送一个SYN来创建一个主动打开，作为三路握手的一部分。客户端把这段连接的序号设定为随机数 A。
       2.	服务器端应当为一个合法的SYN回送一个SYN/ACK。ACK 的确认码应为 A+1，SYN/ACK 包本身又有一个随机序号 B。
       3.	最后，客户端再发送一个ACK。当服务端受到这个ACK的时候，就完成了三路握手，并进入了连接创建状态。此时包序号被设定为收到的确认号 A+1，而响应则为 B+1。
       
       四次挥手
       客户端或服务器均可主动发起挥手动作，在socket编程中，任何一方执行close()操作即可产生挥手操作。
       （1）客户端A发送一个FIN，用来关闭客户A到服务器B的数据传送。 
       （2）服务器B收到这个FIN，它发回一个ACK，确认序号为收到的序号加1。和SYN一样，一个FIN将占用一个序号。 
       （3）服务器B关闭与客户端A的连接，发送一个FIN给客户端A。 
       （4）客户端A发回ACK报文确认，并将确认序号设置为收到序号加1。 
       ```
     
     + UDP协议(User Datagram Protocol，用户数据报协议)：是一种非面向连接的，不可靠的传输协议；传输较快，只能传输小的数据，64k以内；UDP的发送端只管发，不管对方是否收到；

5. Socket：

   + 不管是TCP、UDP协议的编程，Java编程的通信两端都需要一个Socket对象；

     ![Socket数据传输过程](images\grammar\Socket数据传输过程.png)

   + 作用：

     + 负责与网卡驱动打交道；
     + 有了Socket，网络通信其实就是Socket间的通信，Socket允许程序把网络连接当成一个流，数据在两个Socket间通过IO进行传输；

   + 分类：

     + 基于流的Socket，用于TCP编程；

       + ServerSocket：只负责建立TCP连接；

         ```java
         //表示服务器在此端口号等待连接，进行通信
         ServerSocket server = new ServerSocket(端口号);
         ```

       + Socket：只负责传输数据；

         ```java
         //客户端的Socket
         Socket(InetAddress address,int port);
         Socket(String host,int port);
         //服务端的Socket
         Socket socket = server.accpet();
         ```

     + 基于数据报的Socket，用于UDP编程：

       + DatagramSocket：只负责传输和接收数据报包；

   + 工作步骤：

     + 发送端：
       + 应用程序会先创建一个Socket对象；
       + Socket对象去和网卡驱动打交道，告诉他我要发送消息了；
       + 把要发送的数据给Socket对象；
       + 网卡驱动就会把Socket对象中的数据发送出去；
     + 接收端：
       + 先创建一个Socket对象；
       + Socket对象去和网卡驱动打交道，告诉他如果有xx端口号的数据，你给我拿过来；
       + 如果网卡接收到消息，传给对应的Socket；
       + 应用程序就会从Socket中取出来；

   + 分类：

     + TCP：流套接字（stream socket），使用TCP提供可依赖的字节流服务；
     + UDP：数据报套接字（datagram socket），使用UDP提供”尽力而为“的数据报服务；

#### SocketAPI

+ Socket：

  + 发送消息：

    ```java
  OutputStream out = socket.getOutputStream();
    ```
  
    + 可以对字节输出流进行再次包装；

      ```java
    //可以包装成PrintStream，可以调用println()按行输出
      PrintStream ps = new PrintStream(out)；
      //可以包装成BufferedWriter对象,调用write(str),newLine()
      OutputStreamWriter osw = OutputStreamWriter(out);
      BufferedWriter bw = new BufferedWriter(osw);
      //可以包装成ObjectOutputStream对象
      ObjectOutputStream oos = new ObjectOutputStream(out)；
      //可以包装成数据流,DataOutputStream
      DataOutputStream dos = new DataOutputStream(out);
      ```
    
  + 接收消息：
  
    ```java
    InputStream in = socket.getInputStream();
    ```
  
    + 可以对字节输出流进行包装：
  
      ```java
      //可以包装成BUfferedReader对象,可以调用readLine()方法
      InputStreamReader isr = new InputStreamReader(in);
      BufferedReader br = new BufferedReader(isr);
      //可以包装成对象流，ObjectInputStream,调用readObject()
      ObjectInputStream ois = new ObjectInputStream(in);
      //可以包装成数据流，DataInputStream
      DataInputStream dis = new DataInputStream(in);
      ```
  
  + 关闭消息：
  
    ```java
    //一旦调用这个方法，输入和输出都不能进行了，彻底地断开连接
    socket.close();
    //只关闭输出通道，输入通道还在继续
    socket.shutDownOutput()；
    //之关闭输入通道，输出通道还在继续
    socket.shutDownInput();
    ```
  
+ DatagramSocket：

  + 发送端：

    ```java
    //默认使用本地的IP地址，端口号随机选择
    DatagramSocket socket = new DatagramSocket();
    socket.send("数据报");
    socket.close();
    ```

  + 接收端：

    ```java
    //指定端口号
    DatagramSocket socket = new DatagramSocket(端口号);
    socket.receive("数据报");
    socket.close();
    ```

+ DatagramPacket

  + 发送端：

    ```java
    DatagramPacket dp = new DatagramPacket(数据的字节数组，数组的长度，接收方的IP地址的InetAddress对象，接收方的端口号);
    ```

  + 接收端：

    ```java
    DatagramPacket dp = new DatagrmaPacket(用来结束数据的数组，以及数组的长度);
    //获取数据
    byte[]  data = dp.getData();
    //获取实际接收的数据的长度
    int len = dp.getLength();
    ```

#### UDP网络编程

+ 发送端：

  + 先产生一个Socket对象；

    ```java
    DatagramSocket ds = new DatagramSocket();
    ```

  + 准备一个数据报；

    ```java
    DatagramPacket dp = new DatagramPacket(byte buf[], int length,
                              InetAddress address, int port);
    ```

  + 发送数据；

    ```java
    ds.send(dp);
    ```

  + 关闭数据发送；

  ```java
  import java.io.IOException;
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  import java.net.InetAddress;
  
  //UDP:用户数据报协议
  //报文：发送者、接收者、数据的内容、长度
  public class Send {
      public static void main(String[] args) throws IOException {
          //1、先产生一个Socket对象
          DatagramSocket ds = new DatagramSocket();
  
          //2、准备一个数据报/包
          String info = "大家新年好";
          byte[] bytes = info.getBytes();
          InetAddress address = InetAddress.getLocalHost();//对方，接收方的IP地址
          int port = 8988;//接收方的端口号
          DatagramPacket dp = new DatagramPacket(bytes,bytes.length,address,port);
  
          //3、发送数据
          ds.send(dp);
          System.out.println("发送完毕");
  
          //4、关闭
          ds.close();
      }
  }
  ```

+ 接收端：

  + 先产生一个Socket，告知网卡驱动如果有发送到8988的信息就告诉我；

    ```java
    DatagramSocket ds = new DatagramSocket(8988);
    ```

  + 准备一个数据报；

    ```java
    byte[] data = new byte[64*1024];
    DatagramPacket dp = new DatagramPacket(data,data.length);
    ```

  + 接收数据，这是一个阻塞操作；

    ```java
    ds.receive(dp);
    ```

  + 取出数据进行展示；

    ```java
    byte[] data1 = dp.getData();
    ```

  ```java
  import java.io.IOException;
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  
  public class Receiver {
      public static void main(String[] args) throws IOException {
          //1、先产生一个Socket,告知网卡驱动如果有发送到8988的信息就给我
          //在8989这个端口上监听是否有数据
          DatagramSocket ds = new DatagramSocket(8988);
  
          //2、准备一个数据报
          byte[] data = new byte[64*1024];
          DatagramPacket dp = new DatagramPacket(data,data.length);
  
          //3、接收数据，这个是一个阻塞操作
          System.out.println("准备接收数据...");
          ds.receive(dp);
  
          //4、取出数据进行显示
          byte[] data1 = dp.getData();//实际接收的数据
          int len = dp.getLength();//实际接收的数据的长度
          System.out.println(new String(data1,0,len));
  
          //5、关闭
          ds.close();
      }
  }
  ```

##### 重复发送

+ 发送端：

  ```java
  import java.io.IOException;
  import java.net.*;
  
  //UDP:用户数据报协议
  //报文：发送者、接收者、数据的内容、长度
  public class Send {
      public static void main(String[] args) throws IOException, InterruptedException {
          //1、先产生一个Socket对象
          DatagramSocket ds = new DatagramSocket();
          for (int i = 0; i < 100; i++) {
              //2、准备一个数据报/包
              String info = "第" + (i + 1) + "个\"大家新年好\"";
              byte[] bytes = info.getBytes();
              InetAddress address = InetAddress.getLocalHost();//对方，接收方的IP地址
              int port = 8988;//接收方的端口号
              DatagramPacket dp = new DatagramPacket(bytes,bytes.length,address,port);
  
              //3、发送数据
              ds.send(dp);
              Thread.sleep(1000);
  
              System.out.println("第" + (i + 1) + "个已经发送完毕");
          }
  
          System.out.println("发送完毕");
  
          //4、关闭
          ds.close();
      }
  }
  ```

+ 接收端：

  ```java
  import java.lang.String;
  import java.io.IOException;
  import java.net.DatagramPacket;
  import java.net.DatagramSocket;
  
  public class Receiver {
      public static void main(String[] args) throws IOException {
          //1、先产生一个Socket,告知网卡驱动如果有发送到8988的信息就给我
          //在8989这个端口上监听是否有数据
          DatagramSocket ds = new DatagramSocket(8988);
  
          while (true){
              //2、准备一个数据报
              byte[] data = new byte[64*1024];
              DatagramPacket dp = new DatagramPacket(data,data.length);
  
              //3、接收数据，这个是一个阻塞操作
              System.out.println("准备接收数据...");
              ds.receive(dp);
  
              //4、取出数据进行显示
              byte[] data1 = dp.getData();//实际接收的数据
              int len = dp.getLength();//实际接收的数据的长度
              System.out.println(new String(data1,0,len));
          }
      }
  }
  ```

#### TCP网络编程

+ 服务端：

  + 开启服务器，服务器指定端口号监听；

    ```java
    ServerSocket server = new ServerSocket(9999);//ServerSocket只管连接
    ```

  + 服务器在指定端口开启监听，先监听是否有客户端来进行连接；一个socket只能和一个客户端通信，如果有多个客户端，必须有多个socket；

    ```java
    Socket socket = server.accept();//Socket管数据的接收与发送
    ```

  + 通过socket接收或发送数据，接收数据通过输入流，且为字节输入流；

    ```java
    InputStream in = socket.getInputStream();
    byte[] data = new byte[1024];
    	while ((len = in.read(data))!=-1) {//如果in输入流到达流末尾，read()发给发才会返回-1
    		System.out.println(new String(data,0,len));
    }
    ```

  + 接收完毕，和某个客户端断开，关闭服务器；

    ```java
    //(1)和某个客户端断开
    socket.close();
    //(2)关闭服务器
    server.close();
    ```

  ```java
  import java.io.IOException;
  import java.io.InputStream;
  import java.io.OutputStream;
  import java.net.ServerSocket;
  import java.net.Socket;
  
  //服务端
  public class Server {
      public static void main(String[] args) throws IOException {
          //1、开启服务器，服务器指定端口号监听
          ServerSocket server = new ServerSocket(9999);//ServerSocket只管连接
  
          System.out.println("服务器已开启，等待客户端的连接");
  
          //2、服务器在9999端口开启监听，先监听是否有客户端来连接我
          //一个Socket只能和一个客户端通信，如果有多个客户端，必须有多个Socket
          Socket socket = server.accept();//Socket管数据的接收与发送
          System.out.println("一个客户端已连接");
  
          //3、通过Socket接收或发送数据
          //接收数据：通过输入流，字节输入流
          InputStream in = socket.getInputStream();
  
          byte[] data = new byte[1024];
          int len;
          while ((len = in.read(data))!=-1) {//如果in输入流到达流末尾，read()发给发才会返回-1
              System.out.println(new String(data,0,len));
          }
  
          //回复消息
          OutputStream out = socket.getOutputStream();
          String str = "老地方见";
          out.write(str.getBytes());
          System.out.println("回复完毕");
  
          socket.shutdownInput();
  
          //4、接收完毕
          //(1)和某个客户端断开
          socket.close();
  
          //(2)关闭服务器
          server.close();
      }
  }
  ```

+ 客户端：

  + 创建一个Socket，主动连接服务器，需要写服务器的IP和端口号；

    ```java
    Socket socket = new Socket("192.168.31.147",9999);
    ```

  + 准备发送或接收数据，通过socket发送，发送消息通过输出流，且是字节输出流；

    ```java
    String str = "约吗？";
    //通过socket发送
    //发送消息，通过输出流，字节输出流
    OutputStream out = socket.getOutputStream();
    out.write(str.getBytes());
    ```

  + 关闭，断开连接；

    ```java
    socket.close();
    ```

  ```java
  import java.io.IOException;
  import java.io.InputStream;
  import java.io.OutputStream;
  import java.net.Socket;
  
  //客户端
  @SuppressWarnings("all")
  public class Client {
      public static void main(String[] args) throws IOException {
          //1、创建一个Socket
          //主动连接服务器，需要写服务器的IP地址和端口号
          Socket socket = new Socket("192.168.31.147",9999);
          System.out.println("连接成功");
  
          //2、准备发送或接收消息
          String str = "约吗？";
  
          //通过socket发送
          //发送消息，通过输出流，字节输出流
          OutputStream out = socket.getOutputStream();
          out.write(str.getBytes());
  
          socket.shutdownOutput();//半关闭，只关闭输出通道
  
          //可以接收消息
          InputStream in = socket.getInputStream();
          byte[] data = new byte[1024];
          int len;
          System.out.println("从服务器接收的消息是：");
          while ((len = in.read(data)) != -1) {
              System.out.println(new String(data,0,len));
          }
  
          //3、关闭，断开连接
          socket.close();
      }
  }
  ```


##### 多次通信/从键盘输入

+ 客户端

  ```java
  import java.io.*;
  import java.net.Socket;
  import java.util.Scanner;
  
  //客户端
  @SuppressWarnings("all")
  public class Client {
      public static void main(String[] args) throws IOException {
          //1、服务器端口号是8888
          Socket socket = new Socket("192.168.31.147",8888);
  
          //2、从键盘输入消息，给服务器发送，输入单词，直到输入stop为止
          //等待服务器返回消息，服务器会把单词逆转返回：hello-->olleh
          Scanner sc = new Scanner(System.in);
          OutputStream out = socket.getOutputStream();
          //把out对象包装成可以按行发送消息的IO流：BufferedWriter,PrintStream
          PrintStream ps = new PrintStream(out);
          InputStream in = socket.getInputStream();
  
          //把in对象包装成可以按行读取的IO流，BufferedReader
          //因为BufferedReader只能包装Reader的字符输入流对象
          //需要把in转成Reader的对象
          InputStreamReader isr = new InputStreamReader(in);
          BufferedReader br = new BufferedReader(isr);
          while (true) {
              System.out.println("请输入单词：");
              String word = sc.nextLine();
              if ("stop".equals(word)) {
                  break;
              }
  
              //给服务器发送过去
              //out.write(word.getBytes());//这个方法没法按行处理
              ps.println(word);
              ps.flush();
  
  //            //没法按行处理
  //            byte[] data = new byte[1024];
  //            int len;
  //            while ((len = in.read(data))!=-1){
  //                in.read(data);
  //            }
  
              String str = br.readLine();
              System.out.println("从服务器返回的单词是：" + str);
          }
          
          socket.close();
      }
  }
  ```

+ 服务端：

  ```java
  import java.io.*;
  import java.net.ServerSocket;
  import java.net.Socket;
  
  //服务端
  public class Server {
      public static void main(String[] args) throws IOException {
          //1、指定服务器的端口号是8888
          ServerSocket server = new ServerSocket(8888);
  
          //2、接收客户端的连接
          Socket socket = server.accept();
  
          //3、接收一个单词，反转后返回
          InputStream in = socket.getInputStream();
          InputStreamReader isr = new InputStreamReader(in);
          BufferedReader br = new BufferedReader(isr);
  
          OutputStream out = socket.getOutputStream();
          OutputStreamWriter osw = new OutputStreamWriter(out);
          BufferedWriter bw = new BufferedWriter(osw);
  
          String str;
          while ((str =br.readLine()) != null){
              System.out.println("客户端发送的单词是：" + str);
  
              //把单词反转，返回
              //方式一：把str对象转成char[]的数组进行反转
              //方式二：用StringBuffer或StringBuilder有反转的方法
              StringBuilder sb = new StringBuilder(str);
              sb.reverse();
  
              bw.write(sb.toString());
              bw.newLine();
              bw.flush();
          }
  
          //4、关闭
          socket.close();
          server.close();
      }
  }
  ```

##### 多人在线的客户端与服务端

+ 客户端：

  ```java
  import java.io.*;
  import java.net.Socket;
  import java.util.Scanner;
  
  public class Client {
      public static void main(String[] args) throws IOException, InterruptedException {
          //1、连接服务器
          Socket socket = new Socket("192.168.31.147",9999);
  
          //2、从键盘输入
          //发消息是一个线程
          Scanner sc = new Scanner(System.in);
          SendThread send = new SendThread(socket);
          send.start();
  
          //收消息是一个线程
          Receive receive = new Receive(socket);
          receive.start();
  
          send.join();//join()等待线程死亡，它输入了byebye就结束
  
          socket.close();
      }
  }
  
  class SendThread extends Thread{
      private Socket socket;
  
      public SendThread() {
      }
  
      public SendThread(Socket socket) {
          this.socket = socket;
      }
  
      @Override
      public void run(){
          Scanner sc = new Scanner(System.in);
          try {
              OutputStream out = socket.getOutputStream();
              PrintStream ps = new PrintStream(out);
              while (true){
                  System.out.println("请输入要发送的消息：");
                  String message = sc.nextLine();
  
                  if ("byebye".equals(message)){
                      break;
                  }
  
                  ps.println(message);
                  ps.flush();
              }
          } catch (IOException e) {
              e.printStackTrace();
          }
  
          sc.close();
      }
  }
  
  class Receive extends Thread{
      private Socket socket;
  
      public Receive() {
      }
  
      public Receive(Socket socket) {
          this.socket = socket;
      }
  
      @Override
      public void run(){
          try {
              InputStream in = socket.getInputStream();
              InputStreamReader isr = new InputStreamReader(in);
              BufferedReader br = new BufferedReader(isr);
              while (true){
                  String string = br.readLine();//接收服务器转发的其他客户端的消息
                  if (string == null){
                      break;
                  }
                  System.out.println(string);
              }
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

+ 服务端：

  ```java
  import java.io.*;
  import java.net.ServerSocket;
  import java.net.Socket;
  import java.util.ArrayList;
  import java.util.Iterator;
  
  public class Server {
      public static void main(String[] args) throws IOException {
          //1、指定服务器的端口号
          ServerSocket server = new ServerSocket(9999);
  
          ArrayList<Socket> online = new ArrayList<Socket>();//所有与服务器连接的客户端的Socket
  
          //2、等待很多个客户端连接
          int count = 0;
          while (true){
              Socket socket = server.accept();
              //添加到online中
              online.add(socket);
  
              count++;
              System.out.println(count + "个客户端");
              String ip = socket.getInetAddress().getHostAddress();//客户端的IP地址
              System.out.println(ip + "上线了");
  
              MessageHanderThread m = new MessageHanderThread(socket,online);
              m.start();
          }
      }
  }
  
  //负责与某一个客户端通信的线程
  @SuppressWarnings("all")
  class MessageHanderThread extends Thread{
      private Socket socket;
      ArrayList<Socket> online;
  
      public MessageHanderThread() {
      }
  
      public MessageHanderThread(Socket socket,ArrayList<Socket> online) {
          this.socket = socket;
          this.online = online;
      }
  
      @Override
      public void run(){
          String ip = socket.getInetAddress().getHostAddress();//客户端的IP地址
          try {
              //把这个客户端的消息接收到，并转发到其他客户端
              InputStream is = socket.getInputStream();
              InputStreamReader isr = new InputStreamReader(is);
              BufferedReader br = new BufferedReader(isr);
              while (true){
                  String string = br.readLine();//接收服务器转发的其他客户端的消息
                  if (string == null){
                      zhuanfa(ip,"下线了");
                      break;
                  }
                  System.out.println(ip +":" + string);
                  //给其他人转发
                  //先通过其他客户端的Socket对象得到它的输出流通道，给他发送
                  //通过iter进行迭代
  //                Iterator<Socket> iter = online.iterator();
  //                while (iter.hasNext()){
  //                    Socket on = iter.next();
  //                    if (!on.equals(socket)){//如果不是自己，就转发
  //                        try {
  //                            OutputStream out = on.getOutputStream();
  //                            PrintStream ps = new PrintStream(out);
  //
  //                            ps.println(ip + string);
  //                        } catch (IOException e) {
  //                            online.remove(on);
  //                        }
  //                }
  
  //                //通过foreach进行迭代
  //                ArrayList<Socket> offLine = new ArrayList<Socket>();
  //                for (Socket on : online) {
  //                    if (!on.equals(socket)){//如果不是自己，就转发
  //                        try {
  //                            OutputStream out = on.getOutputStream();
  //                            PrintStream ps = new PrintStream(out);
  //
  //                            ps.println(ip + string);
  //                        } catch (IOException e) {
  //                            offLine.add(on);
  //                        }
  //                    }
  //                }
  //
  //                //统一处理所有已下线的人
  //                for (Socket off : offLine) {
  //                    online.remove(off);
  //                    //转发谁下线了
  //                }
                  zhuanfa(ip, string);//转发正常消息
              }
          } catch (IOException e) {
              online.remove(socket);//如果某个客户端自己有问题，自己掉线了
              //转发我掉线了的消息
              zhuanfa(ip,"掉线了");//转发自己掉线的消息
          }
      }
  
      private void zhuanfa(String ip, String string) {
          //通过foreach进行迭代
          ArrayList<Socket> offLine = new ArrayList<Socket>();
          for (Socket on : online) {
              if (!on.equals(socket)){//如果不是自己，就转发
                  try {
                      OutputStream out = on.getOutputStream();
                      PrintStream ps = new PrintStream(out);
  
                      ps.println(ip + string);
                  } catch (IOException e) {
                      offLine.add(on);
                  }
              }
          }
  
          //统一处理所有已下线的人
          for (Socket off : offLine) {
              online.remove(off);
              //转发谁下线了
              zhuanfa(off.getInetAddress().getHostAddress(),"下线了");//转发其他客户端掉线的消息
          }
      }
  }
  ```


#### URL编程

url：统一资源定位符，即网址；

tomcat:服务器ServerSocket+socket；

浏览器:客户端Socket

```java
import java.io.*;
import java.net.Socket;
import java.net.URL;
import java.net.URLConnection;

public class TestURL {
    public static void main(String[] args) throws IOException {
        //Socket socket = new Socket("192.168.31.147",8080);
        //InputStream is = socket.getInputStream();

//        OutputStream out = socket.getOutputStream();
//        String info ="http://oa2.ezsvsbox.com:8081/";
//        out.write(info.getBytes());
//        out.flush();

        URL url = new URL("http://oa2.ezsvsbox.com:8081/");
        URLConnection uc = url.openConnection();
        InputStream is = uc.getInputStream();


        System.out.println("发送完毕");

        //从网页接收用户名和密码，因为是纯文本数据
        BufferedReader br = new BufferedReader(new InputStreamReader(is,"utf-8"));

        String str;
        while ((str = br.readLine())!=null){
            System.out.println(str);
        }
        //socket.close();
    }
}
```

### Lambda表达式与函数式接口

#### Lambda表达式

##### Lambda表达式概述

+ 概念：

  + Lamabda是一个匿名函数/方法，可以把Lambda理解为一段可以传递的代码（希望Java可以吗把方法体作为参数进行传递，也就是说要传递一段代码），jdk1.8中引入；
  + Lambda表达式代表的不仅是匿名函数，也代表一个匿名内部类的一个匿名方法，这个匿名内部类肯定是某个函数式接口的实现类，这个方法就是这个函数式接口的抽象方法；
  + Lambda表达式是在函数式接口的变量和形参时使用；

+ 语法：

  ```java
  (形参列表) -> {方法体：Lambda体};
  ```

  Lambda用来代替原来的匿名内部类，一种函数式接口的匿名内部类；函数式接口是一种特殊的接口：只有一种抽象方法，例如：Runnable、Conparator；

+ 形式：

  + 无参无返回值；
  + 有参无返回值；
  + 无参有返回值；
  + 有参有返回值；

##### 无参无返回值

+ 语法：

  ```java
  () -> {方法体：Lambda体};
  ```

+ 说明：

  + 虽然是无参的，但是()不能省略；
  + 如果方法体/Lamabda体只有一一个语句，那么{;}可以省略；

```java
import org.junit.Test;

public class TestLambdaYufa1 {
    @Test
    public void test1(){
        //Lambda代表的是Runnable接口的匿名实现类的run()方法的方法体
        Runnable run = () -> System.out.println("hello world");

        Runnable run1 = () -> {
            System.out.println("hello");
            System.out.println("world");
        };

        new Thread(() -> System.out.println("hello world"));

        //Lambda表达式代表MyInterface的匿名内部类的test()方法的方法体
        MyInterface m = ()-> System.out.println("Lambda表达式的测试方法");

        method(m);
        method(()-> System.out.println("Lambda表达式的测试方法"));
    }

    public void method(MyInterface m){
        m.test();
    }
}

interface MyInterface{
    void test();
}
```

##### 有参无返回值

+ 语法：

  ```java
  (形参列表)->{方法体，Lambda体};
  ```

+ 说明：

  + 如果只有一个语句，{;}可以省略；
  + 如果只有一个形参，而且类型是确定的，那么(数据类型)可以省略；
  + 如果有多个形参，但是数据类型是确定的，那么数据类型可以省略，但是括号不能省略；

```java
import org.junit.Test;

public class TestLambdaYufa2 {
    @Test
    public void test1(){
        MyInter m = (String str)->{
            System.out.println(str);
        };

        MyInter m1 = str -> {
            System.out.println(str);
        };

        Inter i = (a,b)->{
            System.out.println("a="+a+",b="+b);
        };

        //a,b按照Integer处理
        JieKou<Integer> jiekou = (a,b)->{
            System.out.println("a="+a+",b="+b);
        };

        //a,b按照Object处理
        JieKou jiekou1 = (a,b)->{
            System.out.println("a="+a+",b="+b);
        };
    }
}


interface MyInter{
    void test(String str);
}

interface Inter{
    void test(int a,int b);
}

interface JieKou<T>{
    void test(T a,T b);
}
```

##### 无参有返回值

+ 语法：

  ```java
  ()->{方法体，Lambda体};
  ```

+ 说明：

  + 如果{}没有省略，那么{}中必须有return返回值的语句；
  + 如果只有一个语句，{;}可以省略，并且return也要省略；
  + 虽然是无参，但是()不能省略；

```java
import org.junit.Test;

import java.util.Random;

public class TestLambdaYufa3 {
    @Test
    public void test1(){
        MyInter m1 = ()->{return "hello";};
        MyInter m2 = ()->"hello";

        Random rand = new Random();
        Inter i1 = ()->{return rand.nextInt(10);};
        Inter i2 = ()->rand.nextInt(10);
    }
}

//只要是MyInter类型的变量或形参都可以传递一个Lambda表达式给他
interface MyInter{
    String test();
}

interface Inter{
    int test();
}
```

##### 有参有返回值

+ 语法：

  ```java
  (形参列表)->{方法体，Lambda体}；
  ```

+ 说明：

  + 如果{}没有省略，{}中必须有return返回值的语句；
  + 如果方法体中只有一个语句，那么{;}还有return都可以省略；
  + 如果形参是多个且类型是确定的，那么类型可以省略，但是()不能省略；
  + 如果形参只有一个，类型是确定的，那么类型和()都可以省略；

```java
import org.junit.Test;

import java.util.Comparator;

public class TestLambdaYufa4 {
    @Test
    public void test1(){
        Comparator<String> com1 = (String s1,String s2)->{return s1.compareTo(s2);};
        Comparator<String> com2 = (String s1,String s2)->s1.compareTo(s2);
        Comparator<String> com3 = (s1,s2)->s1.compareTo(s2);

            MyInterface m1 = (double num)->{return Math.sqrt(num);};
            MyInterface m2 = (double num)->Math.sqrt(num);
            MyInterface m3 = (num)->Math.sqrt(num);
            MyInterface m4 = num->Math.sqrt(num);
    }
}

interface MyInterface{
    double sqrt(double num);
}
```

#### 函数式接口

+ 概念：
  + 函数式接口是一种特殊的接口：SAM(Single Abstract Method)类型的接口，即只有一个抽象方法的接口，定义了这种类型的接口，使得以其为形参的方法，可以在调用时，使用一个lambda表达式作为实参；
  + 这种接口类型的变量，可以使用一个lambda表达式为其赋值；
+ 小结：
  + 只有函数式接口的形参和变量才能使用Lambda表达式，其他情况是不能使用Lambda表达式的；
+ 注意：
  + 从SAM原则上讲，这个接口中，只能有一个函数需要被实现，但是也有如下例外：
    + 默认方法与静态方法并不影响函数式接口的契约，可以任意使用；
    + 可以有Object中覆盖的方法，也就是equals、toString、hashcode等方法；
  + 如果某个接口明确是函数式接口，那么可以在接口上加注解：@FunctionalInterface；

```java
public class TestFunctionInter {
    public static void main(String[] args) {
        test(()-> System.out.println("hello"));//为形参run赋值
        Runnable run = ()-> System.out.println("hello");//为变量run赋值

        method((a, b) -> a>b?a:b);//为形参m赋值
        MyInter m = (a,b)->a>b?a:b;//为变量m赋值

        //print(()-> System.out.println("hello"));//错误，因为Object不是函数式接口的形参

        //dao(()-> System.out.println("hello"));//错误，因为Inter不是函数式接口的形参
    }

    public static void test(Runnable run){

    }

    public static void method(MyInter m){

    }

    public static void print(Object obj){

    }

    public static void dao(Inter inter){

    }
}

@FunctionalInterface
interface MyInter{
    int getMax(int a,int b);

    default void fangfa(){
        System.out.println("默认方法");
    }

    static void jingtai(){
        System.out.println("静态方法");
    }

    @Override
    boolean equals(Object object);
}

interface Inter{
    void add();
    void update();
}
```

##### 四种函数式接口

java.util.function

+ 消费型：

  ```java
  Interface Consumer<T>:void accept(T t);
  ```

  + 有参无返回值类型的接口，相当于在accpet()方法中把t这个数据消耗了，没有给调用者返回接口；
  + 如果在开发中需要声明一个这样特征的接口，就不需要重新声明了，直接用它就行；

  ```java
  import org.junit.Test;
  
  import java.util.ArrayList;
  import java.util.function.Consumer;
  
  public class TestFunctionalInterfaceTypes {
      @Test
      public void test1(){
          ArrayList<String> list = new ArrayList<String>();
          list.add("hello");
          list.add("world");
          list.add("java");
  
          //ArrayList--> List--> Collection-->Iterable
          Consumer<String> c1 = (String str) -> {
              System.out.println(str);
          };
  
          Consumer<String> c2 = str -> System.out.println(str);
  
          list.forEach(c2);
  
          list.forEach(str -> System.out.println(str));
      }
  }
  ```

+ 供给型接口：

  ```java
  Interface Supplier<T>: T get();
  ```

  + 无参有返回值，相当于调用者不需要提供给我参数，我给返回一个结果；
  + 如果开发中需要声明一个类型这样特征的接口，就不用重新声明了，直接调用即可；

  ```java
  import org.junit.Test;
  
  import java.util.ArrayList;
  import java.util.Optional;
  import java.util.function.Consumer;
  import java.util.function.Supplier;
  
  public class TestFunctionalInterfaceTypes {
      @Test
      public void test2(){
          //Class Optional<T>
          Optional<String> address = Optional.of("北京");
          Supplier<String> s = () -> {return "上海";};
          //如果Optional对象没有包装任何值，那么就用Supplier接口的实现类的get方法提供的值代替
          //如果Optional对象包装了值，那么就用原来的值
          String other = address.orElseGet(s);
          String other1 = address.orElseGet(() -> "上海");
          System.out.println(other);
      }
  }
  ```

+ 函数型接口：

  ```java
  Interface Function<T,R>： R apply(T t);
  ```

  + 有参有返回值；
    + BiFunction<T,U,R> : R apply(T t, U u);
    + DoubleFunction<R> : R apply(double d)；
    + ...；

+ 断定型接口：

  ```java
  Predicate<T> boolean test(T t);
  ```

  + 有参有返回值，返回值是固定的boolean，用来条件判断；判断t对象是否满足什么条件，如果慢则返回true，如果不满足返回false；
  + 衍生：
    + IntPredicate： boolean test(int i)：判断某个int整数是否满足什么条件；
    + LongPredicate：boolean test(long t)：判断某个long类型参数是否满足什么条件；

#### 方法与构造器引用

##### 方法引用

+ 语法：

  ```java
  类名/对象名::方法名
  ```

+ 使用情况：

  + 对象::实例方法名：

    + 当Lambda体是调用另一个对象的实例方法来完成功能的；
    + Lambda表达式的形参，正好是给这个实例方法是实参；

    ```java
    import org.junit.Test;
    
    import java.util.Arrays;
    import java.util.List;
    
    public class TestFunctionReference {
        @Test
        public void test1(){
            List<String> list = Arrays.asList("hello", "world", "java");
    //        //使用Lambda表达式
    //        list.forEach((element) -> System.out.println(element));
    
            /**
             * System.out.println(element)
             * Lambda体通过调用System.out对象的println()方法来完成的；
             */
            //方法引用
            list.forEach(System.out::println);
        }
    }
    ```

  + 类::静态方法名：

    + 当Lambda体通过调用另一个类的静态方法来完成的功能；
    + Lambda表达式的形参，正好是给这个实例方法是实参；

    ```java
    import org.junit.Test;
    
    import java.util.function.Function;
    import java.util.function.Supplier;
    
    public class TestFunctionReference {
        @Test
        public void test2(){
            //Supplier供给型的接口：T get()
            Supplier<Double> su = () -> Math.random();
    
            Supplier<Double> su2 = Math::random;
    
            //Function<T,R>:R apply(T t)
            Function<Integer,Double> fun = (Integer num) ->Math.sqrt(num);
    
            Function<Integer,Double> fun2 = Math::sqrt;
        }
    }
    ```

  + 类名::实例方法名：

    + 当Lambda体是通过调用一个对象的实例方法来完成功能；
    + 这个对象正好是我们其中的一个形参，剩下的形参正好是传给该实例方法的实参；

    ```java
    import org.junit.Test;
    
    import java.util.Comparator;
    
    public class TestFunctionReference {
        @Test
        public void test3(){
            //Comparator<T> :int compare(T t1,T t2)
            Comparator<String> com = (String s1, String s2) -> s1.compareTo(s2);
            Comparator<String> com2 = String::compareTo;
        }
    }
    ```

##### 构造器引用

+ 语法：

  ```java
  引用数据类型::new
  ```

+ 使用情况：

  + 当Lambda体是通过构造一个对象来完成的；
  + Lambda表达式的形参列表正好是给构造器的实参；

  ```java
  import org.junit.Test;
  
  import java.util.function.BiFunction;
  import java.util.function.Function;
  import java.util.function.Supplier;
  
  public class TestConstructorReference {
      @Test
      public void test1(){
          //Supplier<T>: T get()
          Supplier<String> su = () -> new String("hello");
          Supplier<String> su2 = String :: new;
  
          //BiFunction<T,U,R>: R apply(T t,U u)
          BiFunction<Integer,String,Student> bi = (id,name) -> new Student(id,name);
          BiFunction<Integer,String,Student> bi2 = Student::new;
  
          Student apply = bi2.apply(1001, "张三");
          System.out.println(apply);
      }
  }
  
  class Student{
      private int id;
      private String name;
  
      public Student(int id, String name) {
          this.id = id;
          this.name = name;
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "id=" + id +
                  ", name='" + name + '\'' +
                  '}';
      }
  }
  ```

##### 数组对象引用

+ 语法格式：

  ```java
  数组类型::new
  ```

  ```java
  import org.junit.Test;
  
  import java.util.function.Function;
  
  public class TestConstructorReference {
      @Test
      public void test1(){
          //Function<T,R>:R apply(T t)
          Function<Integer,int[]> fun = (Integer len) -> new int[len];
          Function<Integer,int[]> fun2 = int[]::new;
      }
  }
  ```

### Stream API

#### 概念

+ 使用Stream API对集合数据进行操作，就类似于使用SQL执行的数据库查询；简言之，Stream API提供了一种高效且易于使用的处理数据的方式；

+ Stream API对集合、数组这样的数据进行处理；
+ Stream是数据渠道，用于操作数据源（集合、数组等）所生成的元素序列，“集合讲的是数据，Stream讲的是计算”；
+ 类似于生活中的生产线，有源头-->很多道中间的操作-->最终的结果；
+ 注意：
  + Stream不会存储元素；
  + Stream不会改变元对象，相反，他们会返回一个持有结果的新的Stream；
  + Stream操作是延迟执行的，这意味着他们会等到需要结果的时候才执行；
+ Stream的三个操作：
  + 创建流；
  + 中间操作（0~n个）；
  + 终结操作；

#### 创建Stream流

+ Collection系列的集合对象.stream()；
+ 数组工具类Arrays.stream(数组对象)；
+ Stream.of(T... args)；
+ 得到无限的数据流；
  + Stream.generate()；
  + Stream.iterate()；

```java
import org.junit.Test;

import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

public class TestStream {
    @Test
    public void test1(){
        List<String> list = Arrays.asList("hello", "world", "java");
        Stream<String> stream = list.stream();
    }

    @Test
    public void test2(){
        String[] array = {"hello","world","java"};
        Stream<String> stream = Arrays.stream(array);
    }

    @Test
    public void test3(){
        Stream<String> stream = Stream.of("hello", "world", "java");
    }

    @Test
    public void test4(){
        //参数是一个Supplier：T get()
        Stream<Double> stream = Stream.generate(() -> Math.random());
        stream.forEach(System.out::println);
    }

    @Test
    public void test5(){
        //函数型：Function:R apply(T t)
        Stream<Integer> stream = Stream.iterate(1, x -> x + 2);//1->1+2 3+2 5+2
        stream.forEach(System.out::println);
    }
}
```

#### Stream中间操作

##### 过滤

```java
Stream<T> filter(Predicate<? super T> predicate)
```

##### 去重

```java
Stream<T> distinct()
```

##### 取有限个

```java
Stream<T> limit(long maxSize)
```

##### 跳过

```java
Stream<T> skip(long n)
```

##### 排序

```java
Stream<T> sorted()//自然排序
Stream<T> //定制排序
```

##### 映射

+ map系列：

  ```java
  //把Function的Lambda体映射到每一个元素上
  <R> Stream<R> map(Function<? super T, ? extends R> mapper)
  IntStream mapToInt(ToIntFunction<? super T> mapper)
  LongStream mapToLong(ToLongFunction<? super T> mapper)
  ```

+ flat系列：

  ```java
  <R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
  ```

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.stream.Stream;

public class TestStreamMiddle {
    @Test
    public void test1(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "java", "world","ouyang","shuangxue","middle");

        //2、中间的操作
        //（1）过滤:把字符串长度小于5的单词去掉
        //Predicate<? super T> predicate :boolean test(T t)
        stream = stream.filter(t ->t.length()>5);

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test2(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间的操作
        stream = stream.distinct();

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test3(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间的操作
        stream = stream.limit(3);

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test4(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间的操作
        stream = stream.skip(2);

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test5(){
        //1、创建流
        Stream<Integer> stream = Stream.of(5,8,3,1,8,6,9);

        //2、中间的操作
        stream = stream.sorted();

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test6(){
        //找出流中的最小值
        //1、创建流
        Stream<Integer> stream = Stream.of(5,8,3,1,8,6,9);

        //2、中间的操作
        stream = stream.sorted();
        stream = stream.limit(1);

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test7(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",10000));
        list.add(new Employee("安防",10000));
        list.add(new Employee("呈贡",10000));

        //1、创建流对象
        Stream<Employee> stream = list.stream();

        //2、排序
        stream = stream.sorted((e1,e2) -> Double.valueOf(e1.getSalary()).compareTo(e2.getSalary()));

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test8(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",10000));
        list.add(new Employee("安防",10000));
        list.add(new Employee("呈贡",10000));

        //1、创建流对象
        Stream<Employee> stream = list.stream();

        //Function:R apply(T t)
        stream = stream.map(e -> {e.setSalary(e.getSalary()+1000);return e;});

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test9(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",10000));
        list.add(new Employee("安防",10000));
        list.add(new Employee("呈贡",10000));

        //1、创建流对象
        Stream<Employee> stream = list.stream();

        //Function:R apply(T t)
        //把员工的薪资涨1000，然后返回所有人的薪资
        Stream<Double> map = stream.map(e -> e.getSalary()+1000);

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test10(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作
        //把hello拆分成h,e,l,l,o,字符组成了一个Stream
        //把world拆分为w,o,r,l,d，字符组成了一个Stream
        //...
        //所有的stream又合成了一个大的stream，flatMap
        Stream<String> flatMap = stream.flatMap(word -> {Stream s = Stream.of(word.split(""));return s;});

        //3、终结操作
        flatMap.forEach(System.out::println);
    }
}

class Employee{
    private String name;
    private double salary;

    public Employee() {
    }

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", salary=" + salary +
                '}';
    }
}
```

#### Stream终止操作

+ Stream分为三步：
  + 创建一个Stream；
  + 各种中间操作，可以很多步；
  + 终结操作（只能一次），一旦执行终结操作，就不是Steam了；

##### 查找与匹配

###### forEach

```java
void forEach(Consumer<? super T> action)
```

###### allMatch

```java
//判断流中的数据是否每一个都满足xx条件
boolean allMatch(Predicate<? super T> predicate)
```

###### anyMatch

```java
//判断流中是否有任意一个数据满足xx条件
boolean anyMatch(Predicate<? super T> predicate)
```

###### noneMatch

```java
//判断流中是否任意一个数据都不满足xx条件
boolean noneMatch(Predicate<? super T> predicate)
```

###### findFirst

```java
//
Optional<T> findFirst();
```

###### findAny

```java
//如果是一个稳定的数据流，如果是不稳定的数据流，数据随机
Optional<T> findAny();
```

###### count

```java
//计数
long count();
```

###### max

```java
//找出最大值
Optional<T> max(Comparator<? super T> comparator)
```

###### min

```java
//找出最小值
Optional<T> min(Comparator<? super T> comparator)
```

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.Optional;
import java.util.stream.Stream;

public class TestStreamEnd {
    @Test
    public void test1(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有

        //3、终结操作
        stream.forEach(System.out::println);
    }

    @Test
    public void test2(){
        //1、创建流
        Stream<String> stream = Stream.of("hello", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        stream = stream.map(str -> str.toUpperCase());//全部转成大写
        stream = stream.map(str -> Character.toUpperCase(str.charAt(0)) + str.substring(1));//首字母转成大写

        //3、终结操作
        //Predicate<? super T> predicate
        boolean result = stream.allMatch(str -> str.toLowerCase().equals(str));//判断是否全部小写
        boolean result2 = stream.allMatch(str -> str.charAt(0)>= 65 && str.charAt(0) <= 91);

        System.out.println(result);
    }

    @Test
    public void test3(){
        //1、创建流
        Stream<String> stream = Stream.of("HELLO", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        boolean result = stream.anyMatch(str -> str.toUpperCase().equals(str));

        //3、终结操作
        System.out.println(result);
    }

    @Test
    public void test4(){
        //1、创建流
        Stream<String> stream = Stream.of("HELLO", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        boolean result = stream.noneMatch(str -> str.toUpperCase().equals(str));

        //3、终结操作
        System.out.println(result);
    }

    @Test
    public void test5(){
        //1、创建流
        Stream<String> stream = Stream.of("HELLO", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        Optional<String> first = stream.findFirst();

        //3、终结操作
        System.out.println(first.get());
    }

    @Test
    public void test6(){
        //1、创建流
        Stream<String> stream = Stream.of("HELLO", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        Optional<String> first = stream.findAny();

        //3、终结操作
        System.out.println(first.get());
    }

    @Test
    public void test7(){
        //1、创建流
        Stream<String> stream = Stream.of("HELLO", "hello","java", "hello","world","ouyang","shuangxue","middle");

        //2、中间操作，可以很多步，也可以没有
        stream = stream.filter(str -> str.toUpperCase().equals(str));

        //3、终结操作
        long count = stream.count();
        System.out.println(count);
    }

    @Test
    public void test8(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",10000));
        list.add(new Employee("安防",10000));
        list.add(new Employee("呈贡",10000));
        //1、创建流
        Stream<Employee> stream = list.stream();

        //2、中间操作，可以很多步，也可以没有
        //找出工资大于10000的员工人数
        stream= stream.filter(e -> e.getSalary() > 10000);

        //3、终结操作
        long count = stream.count();
        System.out.println(count);
    }

    @Test
    public void test9(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",12500));
        list.add(new Employee("安防",11000));
        list.add(new Employee("呈贡",15000));
        //1、创建流
        Stream<Employee> stream = list.stream();

        //2、中间操作，可以很多步，也可以没有
        //找出工资大于10000的员工人数
        Optional<Employee> max = stream.max((e1, e2) -> Double.valueOf(e1.getSalary()).compareTo(Double.valueOf(e2.getSalary())));

        //3、终结操作
        System.out.println(max);
    }
}
```

##### 规约

```java
Optional<T> reduce(BinaryOperator<T> accumulator);
```

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.Optional;
import java.util.stream.Stream;

public class TestStreamEnd2 {
    @Test
    public void test1(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",12500));
        list.add(new Employee("安防",11000));
        list.add(new Employee("呈贡",15000));
        //1、创建流
        Stream<Employee> stream = list.stream();

        Optional<Employee> reduce = stream.reduce((t1, t2) -> t1.getSalary() - t2.getSalary() > 0?t1:t2);

        System.out.println(reduce.get());//Employee{name='呈贡', salary=15000.0}
    }

    @Test
    public void test2(){
        Stream<Integer> stream = Stream.of(1,2,3,4,5);
        Optional<Integer> sum = stream.reduce((a, b) -> a + b);

        System.out.println(sum.get());//15
    }
}
```

##### 收集

```java
<R, A> R collect(Collector<? super T, A, R> collector)
```

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

    @Test
    public void test3(){
        ArrayList<Employee> list = new ArrayList<>();
        list.add(new Employee("张登",10000));
        list.add(new Employee("赵孟",12500));
        list.add(new Employee("安防",11000));
        list.add(new Employee("呈贡",15000));
        //1、创建流
        Stream<Employee> stream = list.stream();

        //2、手机工资低于10000的员工信息
        stream = stream.filter(e -> e.getSalary()<10000);//过滤只留下薪资低于10000的
        List<Employee> all = stream.collect(Collectors.toList());//把剩下的元素，收集到一个list集合中

        for (Employee employee : all) {
            System.out.println(employee);
        }
    }
}
```

### Optional类

+ 概念：

  + Optional是jdk1.8中引入的，目的是为了解决空指针问题，换一种方式处理空指针问题；Optional是一个容器；

+ 三个创建Optional的方法：

  + Optional.empty()：装的是空值；
  + Optional.of(T t)：要求t必须非空，否则报错，空指针异常；
  + Optional.ofNullable(T t)：如果t是空，不会报错；

  ```java
  import org.junit.Test;
  
  import java.util.Optional;
  
  public class TestOptional {
      @Test
      public void test1(){
          Optional<Object> opt = Optional.empty();//空容器
          Optional<String> opt2 = Optional.of("beijing");
  
          String str = null;
          Optional<String> opt3 = Optional.ofNullable(str);
      }
  }
  ```

+ 其他方法：

  + 从容器中取出被包装的对象；

    + 要求容器是非空的，如果容器中是空的，那么会报错：java.util.NoSuchElementException: No value present；

      ```java
      T get()
      ```

      ```java
      import org.junit.Test;
      
      import java.util.Optional;
      
      public class TestOptional {
          @Test
          public void test2(){
              Optional<String> opt = Optional.of("beijing");
              String string = opt.get();
              System.out.println(string);
          }
      }
      ```

  + 如果容器中是非空的，就返回被包装的对象；如果容器中是空的，用other代替；

    ```java
    T orElse()
    ```

    ```java
    import org.junit.Test;
    
    import java.util.Optional;
    
    public class TestOptional {
        @Test
        public void test4(){
            String str = "beijing";
            Optional<String> opt = Optional.ofNullable(str);
            String string = opt.orElse("shanghai");
            System.out.println(string);
        }
    }
    ```

  + 如果容器是非空的，就返回被包装的对象；如果容器中是空的，用other这个供给型接口的get()方法的返回值代替；

    ```java
    T orElseGet(Supplier<? extends T> other)
    ```

    ```java
    import org.junit.Test;
    
    import java.util.Optional;
    
    public class TestOptional {
        @Test
        public void test5(){
            String str = "beijing";
            Optional<String> opt = Optional.ofNullable(str);
            String string = opt.orElseGet(() -> new String("shanghai"));
            System.out.println(string);
        }
    }
    ```

  + 如果容器是非空的，就返回被包装的对象；如果容器中是空的，就报指定的异常；

    ```java
    <X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier)
    ```

    ```java
    import org.junit.Test;
    
    import java.util.Optional;
    
    public class TestOptional {
        @Test
        public void test6(){
            String str = null;
            Optional<String> opt = Optional.ofNullable(str);
            String string = opt.orElseThrow(() -> new RuntimeException("收获地址不存在") );
            System.out.println(string);
        }
    }
    ```

  + 判断是否存在：

    ```java
    boolean isPresent()
    ```

    ```java
    import org.junit.Test;
    
    import java.util.Optional;
    
    public class TestOptional {
        @Test
        public void test7(){
            String str = null;
            String str2 = "beijing";
            Optional<String> opt = Optional.ofNullable(str);
    
            if (opt.isPresent()){
                System.out.println(opt.get());
            } else {
                System.out.println("不存在");
            }
        }
    }
    ```

  + 如果存在，就对它包装的对象，进行消耗操作；如果不存在，什么都不做；

    ```java
    void ifPresent(Consumer<? super T> consumer)
    ```

    ```java
    import org.junit.Test;
    
    import java.util.Optional;
    
    public class TestOptional {
        @Test
        public void test8(){
            String str = null;
            String str2 = "beijing";
            Optional<String> opt = Optional.ofNullable(str);
    
            //Consumer消费型：void accept(T t)
            opt.ifPresent(t -> System.out.println(t));
        }
    }
    ```

+ Optional练习：

  ```java
  import com.sun.imageio.plugins.gif.GIFImageReader;
  import org.junit.Test;
  
  import java.util.Optional;
  
  public class TestOptionalExer {
      public static void main(String[] args) {
  //        Gril gril = new Gril("迪丽热巴");
  //        Boy boy = new Boy("张登",gril);
  //
  //        String name = getBoysGrilFriendName(boy);
  //        System.out.println(name);
  
          Boy boy = null;
          String name = getBoysGrilFriendName(boy);
          System.out.println(name);
      }
  
      public static String getBoysGrilFriendName(Boy boy){
          //return boy.getGril().getName();
  
  //        if (boy != null){
  //            if (boy.getGril()!=null){
  //                return boy.getGril().getName();
  //            }
  //        }
  //        return null;
  
          Optional<Boy> opt = Optional.ofNullable(boy);
          boy = opt.orElse(new Boy());//防止boy空
  
          Gril gril = boy.getGril();
          Optional<Gril> opt2 = Optional.ofNullable(gril);
  
          gril = opt2.orElse(new Gril());//防止Gril空
  
          String name = gril.getName();
  
          Optional<String> opt3 = Optional.ofNullable(name);
          name = opt3.orElse("cls");
  
          return name;
      }
  }
  
  class Boy{
      private String name;
      private Gril gril;
  
      public Boy() {
      }
  
      public Boy(String name, Gril gril) {
          this.name = name;
          this.gril = gril;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public Gril getGril() {
          return gril;
      }
  
      public void setGril(Gril gril) {
          this.gril = gril;
      }
  }
  
  class Gril{
      private String name;
  
      public Gril() {
      }
  
      public Gril(String name) {
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  }
  ```
