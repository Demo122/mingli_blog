# 明里的个人学习日志

***
# 学习记录

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

