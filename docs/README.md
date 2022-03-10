# 明里的个人学习日志

***
# 学习记录

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

