## mysql

### mysql安装和配置
- **MySQL 5.7.24 解压版,解压安装**
- **配置**
    1. 添加环境变量
    2. 新建配置文件
         新建一个文本文件，内容如下：
        ```properties
        [mysql]
        default-character-set=utf8

        [mysqld]
        character-set-server=utf8
        default-storage-engine=INNODB
        sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
        ```
        把上面的文本文件另存为，在保存类型里选`所有文件 (*.*)`，文件名叫`my.ini`，存放的路径为MySQL的`根目录`(例如我的是`D:\software\mysql-5.7.24-winx64`,根据自己的MySQL目录位置修改)。
        **上面代码意思就是配置数据库的默认编码集为utf-8和默认存储引擎为INNODB。**
- **初始化MySQL**
    ```sql
    mysqld --initialize-insecure
    ```
    **需要管理员权限**
- **注册MySQL服务**
    ```sql
    mysqld -install
    ```
- **启动MySQL服务**
    ```java
    net start mysql  // 启动mysql服务
        
    net stop mysql  // 停止mysql服务
    ```
- **修改默认账户密码**
    在黑框里敲入`mysqladmin -u root password 1234`，这里的`1234`就是指默认管理员(即root账户)的密码，可以自行修改成你喜欢的。

    ```
    mysqladmin -u root password 1234
    ```
- **登录MySQL**
    ```sql
    mysql -uroot -p1234
    ```
    **登陆参数**：

    ```
    mysql -u用户名 -p密码 -h要连接的mysql服务器的ip地址(默认127.0.0.1) -P端口号(默认3306)
    ```

- **退出**
    退出mysql：

    ```
    exit
    quit
    ```

- **卸载MySQL**
    1. 敲入`net stop mysql`，回车。
        ```
        net stop mysql
        ```
    2. 再敲入`mysqld -remove mysql`，回车。
        ```
        mysqld -remove mysql
        ```
    3. 最后删除MySQL目录及相关的环境变量。
**至此，MySQL卸载完成！**

- **MySql数据模型**

**关系型数据库：**
> 关系型数据库是建立在关系模型基础上的数据库，简单说，关系型数据库是由多张能互相连接的 二维表 组成的数据库

关系型数据库的**优点**：

* 都是使用表结构，格式一致，易于维护。
* 使用通用的 SQL 语言操作，使用方便，可用于复杂查询。
  * 关系型数据库都可以通过SQL进行操作，所以使用方便。
  * 复杂查询。现在需要查询001号订单数据，我们可以看到该订单是1号客户的订单，而1号订单是李聪这个客户。以后也可以在一张表中进行统计分析等操作。
* 数据存储在磁盘中，安全。

### SQL基础
#### SQL概述
* 英文：Structured Query Language，简称 SQL
* SQL 语句可以单行或多行书写，以分号结尾。
* **MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写。**
* 注释
    * 单行注释: -- 注释内容 或 #注释内容(MySQL 特有) 
     > 注意：使用-- 添加单行注释时，--后面一定要加空格，而#没有要求。
    * 多行注释: /* 注释 */
#### SQL分类
* DDL(Data Definition Language) ： 数据定义语言，用来定义数据库对象：数据库，表，列等
DDL简单理解就是用来操作数据库，表等
* DML(Data Manipulation Language) 数据操作语言，用来对数据库中表的数据进行增删改
DML简单理解就对表中数据进行增删改
* **DQL(Data Query Language) 数据查询语言，用来查询数据库中表的记录(数据)**
DQL简单理解就是对数据进行查询操作。从数据库表中查询到我们想要的数据。
* DCL(Data Control Language) 数据控制语言，用来定义数据库的访问权限和安全级别，及创建用户
DML简单理解就是对数据库进行权限控制。比如我让某一个数据库表只能让某一个用户进行操作等。
> 注意： 以后我们最常操作的是 `DML` 和 `DQL`  ，因为我们开发中最常操作的就是数据。


***
## javaweb
123