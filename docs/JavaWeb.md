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


***
## javaweb
123