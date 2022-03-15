# 明里的个人学习日志

***
# 学习记录

## 3.15 数据结构
**数据结构**
- 栈：后进先出，先进后出
- 队列：先进先出，后进后出
- 数组：数组是一种查询快，增删慢的模型
    1. 查询速度快：查询数据通过地址值和索引定位，查询任意数据耗时相同。（元素在内存中是连续存储的）
    2. 删除效率低：要将原始数据删除，同时后面每个数据前移。
    3. 添加效率极低：添加位置后的每个数据后移，再添加元素
- 链表： 链表中的元素是在内存中不连续存储的，每个元素节点包含数据值和下一个元素的地址
    1. 链表查询慢。无论查询哪个数据都要从头开始找
    2. 链表增删相对快
- 二叉树
    1. 只能有一个根节点，每个节点最多支持2个直接子节点
    2. 节点的度： 节点拥有的子树的个数，二叉树的度不大于2 叶子节点 度为0的节点，也称之为终端结点
    3. 高度：叶子结点的高度为1，叶子结点的父节点高度为2，以此类推，根节点的高度最高。
    4. 层：根节点在第一层，以此类推
    5. 兄弟节点 ：拥有共同父节点的节点互称为兄弟节点
- 平衡二叉树：平衡二叉树是在满足查找二叉树的大小规则下，让树尽可能矮小，以此提高查数据的性能
- **红黑树**
![红黑树](note_img\学习记录\3.15\红黑树.png)
![总结](note_img\学习记录\3.15\总结.png)

**List系列集合**
- 特点：
    1. ArrayList、LinekdList ：有序，可重复，有索引。
    2. 有序：存储和取出的元素顺序一致
    3. 有索引：可以通过索引操作元素
    4. 可重复：存储的元素可以重复
- List的实现类的底层原理
    1. ArrayList底层是基于数组实现的，根据查询元素快，增删相对慢。
    2. LinkedList底层基于双链表实现的，查询元素慢，增删首尾元素是非常快的。
- List集合的遍历方式有几种: **迭代器**(推荐，更安全) 、增强for循环、Lambda表达式、for循环（因为List集合存在索引）
- LinkedList的特点：底层数据结构是双链表，查询慢，首尾操作的速度是极快的，所以多了很多首尾操作的特有API。
![LinkedList特点](note_img\学习记录\3.15\linkedlist.png)

```
//linkedlist可以完成队列、栈结构，因为它是双链表结构
//栈
LinkedList<String> stack=new LinkedList<>();
    //入栈
//  stack.addFirst("1");
//  stack.addFirst("2");
//  stack.addFirst("3");
stack.push("1"); //push就是addFirst

System.out.println(stack);  //[3, 2, 1]
    //出栈
//  System.out.println(stack.removeFirst()); //3
//  System.out.println(stack.removeFirst()); //2
//  System.out.println(stack.removeFirst()); //1
System.out.println(stack.pop()); //pop就是removeFirst()

//队列
LinkedList<String> queue=new LinkedList<>();
    //入队
queue.addLast("A");
queue.addLast("B");
queue.addLast("C");
System.out.println(queue); //[A, B, C]
    //出队
System.out.println(queue.removeFirst());
System.out.println(queue.removeFirst());
System.out.println(queue.removeFirst());
```

**集合的并发修改异常问题**
![集合的并发修改异常](note_img\学习记录\3.15\集合的并发修改异常.png)
**Iterator迭代器中的remove的方法需要在next()方法调用后才能调用，且只能使用一次**


**泛型**
1. 泛型概述
    - 泛型：是JDK5中引入的特性，可以在编译阶段约束操作的数据类型，并进行检查
    - **泛型类的原理：把出现泛型变量的地方全部替换成传输的真实数据类型**
    - 泛型的格式：<数据类型>; 注意：泛型只能支持引用数据类型
    - 泛型类的格式：修饰符 class 类名<泛型变量>{  }
    - 泛型方法的格式：修饰符 <泛型变量> 方法返回值 方法名称(形参列表){}
    - 泛型接口的格式：修饰符 interface 接口名称<泛型变量>{}
    - 集合体系的全部接口和实现类都是支持泛型的使用的
2. 泛型的好处
    - 统一数据类型
    - 把运行时期的问题提前到了编译期间，避免了强制类型转换可能出现的异常，因为编译阶段类型就能确定下来
3. 通配符:?
    - ? 可以在“使用泛型”的时候代表一切类型。
    - E T K V 是在定义泛型的时候使用的
    - 泛型的上下限：
        - ? extends Car: ?必须是Car或者其子类   泛型上限
        - ? super Car ： ?必须是Car或者其父类   泛型下限


**Set系列集合**
- Set系列集合特点
    1. 无序：存取顺序不一致
    2. 不重复：可以去除重复
    3. 无索引：没有带索引的方法，所以不能使用普通for循环遍历，也不能通过索引来获取元素
- Set集合实现类特点
    1. HashSet : **无序**、不重复、无索引
    2. LinkedHashSet：**有序**、不重复、无索引
    3. TreeSet：**排序**、不重复、无索引
- **HashSet底层原理**
    HashSet集合底层采取哈希表存储的数据,哈希表是一种对于增删改查数据性能都较好的结构。
    1. **哈希表的组成**
        * JDK8之前的，底层使用**数组+链表**组成
        * JDK8开始后，底层采用**数组+链表+红黑树**组成。
    2. jdk8的hashset原理
        * 哈希表（数组、链表、红黑树的结合体）
        * 当挂在元素下面的数据过多时，查询性能降低，**从JDK8开始后，当链表长度超过8的时候，自动转换为红黑树**
        * HashSet去重复原理解析
        ![HashSet去重复](note_img\学习记录\3.15\Hashset去重复.png)
- **LinkedHashSet**
    * 有序、不重复、无索引。
    * 这里的有序指的是保证存储和取出的元素顺序一致
    * 原理：底层数据结构是依然哈希表，只是每个元素又额外的多了一个双链表的机制记录存储的顺序。
- **TreeSet**
    1. 不重复、无索引、可排序
    2. 可排序：按照元素的大小默认升序（有小到大）排序。
    3. TreeSet集合底层是基于**红黑树的数据结构实现排序**的，增删改查性能都较好。
    4. **注意：TreeSet集合是一定要排序的，可以将元素按照指定的规则进行排序。**
    **想要使用TreeSet存储自定义类型，需要制定排序规则**
    自定义排序规则,TreeSet集合存储对象的的时候有2种方式可以设计自定义比较规则
    -  让自定义的类（如学生类）实现Comparable接口重写里面的compareTo方法来定制比较规则。
    - **TreeSet集合有参数构造器，可以设置Comparator接口对应的比较器对象，来定制比较规则。**
    ```
     public TreeSet(Comparator<? super E> comparator) {
        this(new TreeMap<>(comparator));
    }
    ```
![集合使用场景](note_img\学习记录\3.15\集合使用场景.png)


可变参数
* 可变参数用在形参中可以接收多个数据。可变参数的格式：数据类型...参数名称
* 传输参数非常灵活，方便。可以不传输参数，可以传输1个或者多个，也可以传输一个数组
* **可变参数在方法内部本质上就是一个数组**
* 可变参数的注意事项
    1. 一个形参列表中可变参数只能有一个
    2. 可变参数必须放在形参列表的最后面
    
**Collections集合工具类**
    java.utils.Collections:是集合工具类
    **作用：Collections并不属于集合，是用来操作集合的工具类。**





























## 3.14 Arrays、二分查找、lambda表达式

**Arrays**
![arrays1](note_img\学习记录\3.14\arrays1.png)
![arrays2](note_img\学习记录\3.14\arrays2.png)
![comparatoe](note_img\学习记录\3.14\Arrays_comparator.png)

**二分查找**
```
/**
 * 二分查找法
 */
public class BinarySearch {
    // 二分查找法,在有序数组arr中,查找target
    // 如果找到target,返回相应的索引index
    // 如果没有找到target,返回-1
    public static int find(Comparable[] arr, Comparable target) {

        // 在arr[l...r]之中查找target
        int l = 0, r = arr.length-1;
        while( l <= r ){

            //int mid = (l + r)/2;
            // 防止极端情况下的整形溢出，使用下面的逻辑求出mid
            int mid = l + (r-l)/2;

            if( arr[mid].compareTo(target) == 0 )
                return mid;

            if( arr[mid].compareTo(target) > 0 )
                r = mid - 1;
            else
                l = mid + 1;
        }

        return -1;
    }
}
```
![binarySearch](note_img\学习记录\3.14\二分查找.png)

**Lambda表达式**
![lambda](note_img\学习记录\3.14\lambda表达式.png)
![lambda2](note_img\学习记录\3.14\lambda2.png)
[附录](https://www.runoob.com/java/java8-lambda-expressions.html)

**集合**
![collection体系](note_img\学习记录\3.14\collection集合体系.png)
```
ArrayList<String > arrayList=new ArrayList<>();
    arrayList.add("google");
    arrayList.add("baidu");
    arrayList.add("tencent");
    arrayList.add("bytedance");
    arrayList.add("jd");
    
    //forEach
    arrayList.forEach(new Consumer<String>() {
        @Override
        public void accept(String s) {
            System.out.println(s);
        }
    });
```


***
## 3.13 内部类
![内部类](note_img\学习记录\3.13\内部类.png)
![静态内部类](note_img\学习记录\3.13\静态内部类.png)
静态内部类中可以直接访问外部类的静态成员
![成员内部类](note_img\学习记录\3.13\成员内部类.png)

**匿名内部类**
![匿名内部类](note_img\学习记录\3.13\匿名内部类.png)

**常用API**
* Object类
![object_equals](note_img\学习记录\3.13\object_equals.png)
* Objects类，jdk1.7后才有
![objects概述](note_img\学习记录\3.13\objects.png)
**在比较前会做一个是否为null的判断，避免空指针异常，更加安全**

**StringBuilder**
当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。
和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

在使用 StringBuffer 类时，每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象，所以如果需要对字符串进行修改推荐使用 StringBuffer。

StringBuilder 类在 Java 5 中被提出，**它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。**

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。
![StringBuilder](note_img\学习记录\3.13\StringBuilder.png)

**Math**
![math](note_img\学习记录\3.13\math.png)

**System**
![system](note_img\学习记录\3.13\system.jpg)

**BigDecimal**
![bigdecimal](note_img\学习记录\3.13\BigDecimal_1.jpg)
![bigdecimal](note_img\学习记录\3.13\BigDecimal_2.jpg)
![bigdecimal](note_img\学习记录\3.13\bigdecimal_3.jpg)
```
System.out.println(0.09+0.01);
double a=0.09,b=0.01;
System.out.println(a+b);
BigDecimal ba=BigDecimal.valueOf(a);
BigDecimal bb=BigDecimal.valueOf(b);
System.out.println(ba.add(bb));

//输出
0.09999999999999999
0.09999999999999999
0.10
```
**注意：BigDecimal是一定要做精度运算的**
```
BigDecimal a = BigDecimal.valueOf(10.0);
BigDecimal b = BigDecimal.valueOf(3.0);
//BigDecimal c=a.divide(b); //报错，因为10/3是无限循环，得不到精确值
BigDecimal c = a.divide(b, 2, RoundingMode.HALF_UP); //四舍五入，精确2位
System.out.println(c);
```
* 日期格式化和解析
![日期格式化和解析](note_img\学习记录\3.13\日期格式化和解析.jpg)
![日历对象](note_img\学习记录\3.13\日历对象.png)

**包装类**
![包装类](note_img\学习记录\3.13\包装类.png)
![自动装箱——拆箱](note_img\学习记录\3.13\自动拆箱装箱.png)

**正则表达式**
![正则表达式](note_img\学习记录\3.13\正则表达式.png)

***
## 三月十一
***多态***
![多态](note_img\学习记录\3.11\多态.png)
![多态中的成员访问](note_img\学习记录\3.11\多态中的成员访问.png)
![注意事项](note_img\学习记录\3.11\注意事项.png)
![总结](note_img\学习记录\3.11\总结.png)

***
## 三月十
- 包：package,相同包下的口语直接访问，否则需要import导入，加入一个类中需要用到不同类，这两个类名又是一样的，那么默认只能导入一个类，另一个需要通过带包名访问
![权限修饰符](note_img\学习记录\3.10\20220310权限修饰符.png)

- **final关键字**
![final关键字](note_img\学习记录\3.10\20220310final.png)

- **常量**
![常量](note_img\学习记录\3.10\20220310常量.png)

- **枚举**
![枚举特点](note_img\学习记录\3.10\20220310枚举特点.png)

- **抽象类和抽象方法**
![抽象类和抽象方法](note_img\学习记录\3.10\20220310抽象类和抽象方法.png)
    1. 抽象类是用来被继承的，抽象方法是交给子类重写实现的
    2. 一个类如果继承了抽象类，那么这个类必须重写抽象类的全部抽象方法，除非这个类也定义为抽象类
![抽象类特点](note_img\学习记录\3.10\20220310抽象类特点.png)

- **面试题**
![final和abstract](note_img\学习记录\3.10\20220310final和abstract.png)


- ***接口***
![接口](note_img\学习记录\3.10\接口.png)
![接口的多实现](note_img\学习记录\3.10\接口的多实现.png)
![接口多继承](note_img\学习记录\3.10\接口多继承.png)

**JDK8接口新增方法**
![JDK8接口1](note_img\学习记录\3.10\jdk8接口.png)
![JDK8接口2](note_img\学习记录\3.10\jdk8接口2.png)
**JDK9接口新增方法**
![JDK9接口](note_img\学习记录\3.10\jdk9接口.png)
**![总结](note_img\学习记录\3.10\20220310接口新增方法总结.png)**

***注意事项***
1. 接口不能创建对象
2. 一个类实现多个接口，多个接口中有同样的静态方法不冲突，**因为接口的静态方法只能通过接口名来调用，子类无法调用**
3. 一个类继承了父类，同时又实现了接口，父类中和接口中有同名方法，默认用父类的
```
public class Test {
    public static void main(String[] args) {
        ErHa er = new ErHa();
        er.eat();
    }
}
interface Animal {
    default void eat() {
        System.out.println("接口eat");
    }
}
class Dog {
    public void eat() {
        System.out.println("class eat");
    }
}
class ErHa extends Dog implements Animal {
}
```
4. 一个类实现了多个接口，多个接口中存在同名的默认方法，不冲突，整个类重写该方法即可
5. 一个接口继承多个接口是可以的，如果多个接口存在规范冲突则不能多继承。 

***
## 三月九
***java进阶***

**static关键字使用**
- 静态成员变量，有static修饰,属于类，只在类第一次加载时创建，可以被共享访问，通过```类名.变量名``` 或者```对象名.变量名```
- 静态成员方法，有static修饰，归属类，用类名访问
- static 访问注意事项：
    1. 静态方法只能访问静态的成员，不可以直接访问实列成员
    2. 实例方法可以访问静态的成员，也可以访问实列成员
    3. 静态方法中是不可以出现this关键字的
- **工具类不用创建对象，都是静态成员方法，可以写一个private的构造函数**
**代码块**
![代码块](note_img\学习记录\3.9\20220309staticCode.png)
```
public class StaticCode {
    /**
     * 静态代码块，static修饰,与类一起加载，自动触发执行
     * 作用：可以用于初始化静态资源
     */
    public static int num;

    static {
        System.out.println("这是静态代码块");
        num = 0;
    }

    public static void main(String[] args) {

    }
}
```

**单例模式**
- 可以保证系统中，应用该模式的这个类永远只有一个实例，即一个类永远只能创建一个对象
- 例如任务管理器对象哦我们只需要一个就可以解决问题了，这样口语节省内存空间
- 实现方式很多：
    1. 饿汉单例：在用类获取对象的时候，对象以及提前为你创建好了
    ```
    public class SingleInstance {
        //饿汉单例设计模式
        /**
        * 饿汉单例设计模式：在用类获取对象的时候，对象以及提前为你创建好了
        * 2.这个对象只能是一个，所以定义为静态成员变量！
        */
        public static SingleInstance instance=new SingleInstance();

        /**
        * 1.必须把构造器私有化
        */
        private SingleInstance(){
        }
    }
    ```
    2. 懒汉单例：真正需要该对象的是，才去创建一个对象（延迟加载对象）
    ```
    public class LanSingleInstance {
        //设置成私有的，防止通过类名直接取null的对象
        private static LanSingleInstance instance; //null

        //提供静态成员方法返回对象
        public static LanSingleInstance getInstance() {
            //只需第一次创建
            if (instance == null) {
                instance = new LanSingleInstance();
            }
            return instance;
        }

        //构造函数私有
        private LanSingleInstance() {
        }
    }
    ```

**继承**
继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
```
class 父类 {
}
 
class 子类 extends 父类 {
}
```
![继承特点](note_img\学习记录\3.9\20220309继承.png)
![继承特点](note_img\学习记录\3.9\20220309继承特点2.png)
![继承特点](note_img\学习记录\3.9\20220309继承特点3.png)

- 重写 

![方法重写](note_img\学习记录\3.9\20220309重写.png)

- 构造器：子类构造器一定要调用父类构造器，无论是有参还是无参构造器，一定要调用
**super(),this()构造器必须在构造器的第一行**
![this,super](note_img\学习记录\3.9\20220309this-super.png)



***
## 三月八
String类，java.lang.String ,对象不可更改类型，创建的对象不可更改，String变量每次的修改其实都是产生并指向了新的字符串对象，原来的字符串对象都市没有改变的，所以称不可变字符串
```
//创建字符串，
//方式一
String str1 = "方式一 this is a string";
System.out.println(str1);

//方式二
//1.public String() :创建一个空白字符串，不含任何内容，几乎不用
String str2=new String();
System.out.println(str2);

//2.public string(string) 根据传入的字符串内容来创建字符串对象，几乎不用
String str3=new String("i am chinese");
System.out.println(str3);

//3.public string (char [] c) : 根据字符数组的内容来创建字符串对象
char c[]={'a','b','v','i','中','国'};
String str4=new String(c);
System.out.println(str4);

//4. public string(byte []):根据字节数组的内容来创建字符串对象
byte [] b={97,98,99,100,101,102,103};
String str5=new String(b);
System.out.println(str5);
```
***面试题***

**Q** 
有什么区别
**A**
- 以""方式给出的字符串对象，在字符串常量池中存储 ，而且相同内容只会在其中存储一份
- 通过构造器的new对象，每new一次都会产生一个新的对象，放在堆内存中

**Q**
```
//这行代码创建了两个对象，new一个，常量"abc"一个
String s2 = new String("abc"); 
//这行代码创建了0个对象
String s1 = "abc";
//地址不同，false
System.out.println(s1 == s2);

String str1="abc";
string str2="ab";
String str3=s2+"c"; //只要没明确写出是字符串，都会new新对象放在堆内存中
```
![string面试题](note_img\学习记录\3.8\20220308String面试题.png)

***ArrayList集合***
![ArrayList](note_img\学习记录\3.8\20220308Arraylist.png)
```
//泛型
//jdk17开始，泛型后面的类型声明可以不写
ArrayList<String> list=new ArrayList<>(); 
```
```
ArrayList<String> list=new ArrayList<String >();
    list.add("java");
    list.add("c");
    list.add("c++");
    list.add("python");
    list.add("js");
    list.add("html");

    //1.public E get(int index)：获取某个位置出的元素值
    System.out.println(list.get(0));

    //2.public int size() 获取集合的大小
    System.out.println(list.size());

    //3.集合遍历
    for (String s :
            list) {
        System.out.println(s);
    }

    //4.public E remove(int index) :删除某个索引，并返回被删除的元素值
    String str2=list.remove(0);
    System.out.println(str2);
    System.out.println(list);
    list.remove("java");
    // remove(object o )只会删除第一次出现的元素，后面出现的不会删除

    //5. public E set(int index,E element): 修改某个索引位置的元素值
    list.set(0,"c++");
    System.out.println(list);
```
![ArrayListAPI](note_img\学习记录\3.8\20220308ArraylistAPI.png)

## 三月七
摸鱼

## 三月六
摸鱼

***
## 三月五
方法
```
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}
```
**递归求1-n的和**
```
//求1-n的值
public static int nSum(int n){
    if(n!=0){
        return n+nSum(n-1);
    }else {
        return n;
    }
}
```
java中的参数传递机制：
* 基本类型的参数传递，是值传递，传的是数据值，并不是传地址
* **引用类型的参数传递，传的是地址**

**方法重载**：同一个类中，出现多个方法名称相同，但是**形参列表不同**，那么这些方法就是重载方法
形参列表不同是指，**形参个数、类型、顺序不同**

return可以单独使用，立即跳出，结束当前方法

***面向对象*** 三大特征：**封装、继承、多态**
* 构造器 
    - 无参数构造器（默认存在的），写不写都有，**一旦定义了有参构造器，那么无参构造器就没有了，还想用无参构造器就必须自己写一个**
    - 有参数构造器
* this关键字
    - 可以出现再构造器和方法中、代表当前对象的地址
    - 用于指定访问当前对象的成员变量、成员方法


***
## 三月四
三种控制结构，顺序、分支、循环
switch注意事项：
* 表达式类型只能是byte、short、int、char，jdk5开始支持枚举，jkd7支持String,不支持double、float，因为double、float底层计算不精确，不支持long,因为太大了
* case给出得值不允许重复，且只能是字面量，不能是变量
* 不要忘记写break，否则会出现穿透现象

**for循环** 
```
for (初始化; 循环语句; 迭代语句){
}
for (int i = 0; i++ < 10; System.out.println(i)){
    //输出1-10
}
```
**冒泡排序**
* 比较轮数为 数组长度-1
* 每轮次数为 数组长度-i-1
```
int [] arr={6,5,4,3,2,1};
for (int i = 0; i < arr.length-1; i++) {
    for (int j = 0; j < arr.length-i-1 ; j++) {
        if(arr[j]>arr[j+1]){
            int temp=arr[j+1];
            arr[j+1]=arr[j];
            arr[j]=temp;
        }
        System.out.println("第"+i+"轮"+Arrays.toString(arr));
    }
}
System.out.println("排序完成："+Arrays.toString(arr));
```



***
## 三月三

JAVA中的数据类型，引用数据类型（除基本数据类型外都是,例如`String`）和基本数据类型

**基本数据类型：四大类8种**
1. 整数
    * `byte`   1字节
    * `short`  2字节
    * `int`    4字节
    * `long`   8字节  `long l=1234165464L` *不加L默认是int*
2. 浮点数
    * `float`  4字节  `float score=98.5F`  *不加F默认是double*
    * `double` 8字节
3. 字符
    * `char`   2字节
4. 布尔
    * `boolean`1字节

**自动类型转换**
*类型范围小的变量，考研直接赋值给类型范围大的变量*
```
byte a=12;    原理:   a 00001100 （8位）     
int b=a;              b 00000000 00000000 00000000 00001100 (32位)
System.out.println(b); // b=12 
```
**byte short char 是直接转换成int类型参与运算的**
类型转换面试题，byte i=10; byte j=120; byte k=i+j;(*不行，byte在运算中当做int,所有k要声明为int*)  **因为byte太小，运算容易越界，所有干脆直接当作int运算**

*&& 短路与，左边为false，右边不执行
*|| 短路或，左边为true,右边不执行
*三元运行符 ```条件？a:b  int max=a>b ？ a:b ```
三元运算符嵌套，```int max = i>j? (i>k? i: k) : (j>k? j: K) ```


## 三月二
学习了git使用，搭建了docsify个人博客，主要用于记录学习过程，Java笔记
其中git使用常用命令为：
```
git init  初始化仓库 
git add xxx.xx 添加文件
git add -A 添加所有修改的文件
git commit -m "xxxx"
git reset --hard HEAD^ 返回上一版本，HEAD时当前版本 
git branch xxx 创建分支
git cheackout xx 切换分支
git merge xx 合并分支
git push origin xx 更新到github
git status 查看当前状态
....
```
附上参考资料，[不会再查](https://mp.weixin.qq.com/s/swnwBiuyVmhs5iPqv3H6BQ)

***

