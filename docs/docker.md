## docker安装
### ubuntu中安装docker
1. 卸载旧版本
    ``` 
     sudo apt-get remove docker docker-engine docker.io containerd runc
    ```
2. 安装依赖
    ```
    sudo apt-get update
    sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    ```
3. 添加docker官方gpg密钥，这里改成中科大镜像的
    ```
     curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

    ```
4. 设置稳定版本库，也换成中科大的
    ```
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/ \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
5. 安装docker,默认是安装最新版
    ```
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```
    ***你可以使用如下命令查看当前存储库中可用的版本，自己指定版本号***
    **查看**
    ```
     apt-cache madison docker-ce
    ```
    **安装**
    ```
     sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin

    ```
6. 测试是否安装成功
    ```
     sudo docker run hello-world
    ```
    **如下，则成功**
    ```
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    2db29710123e: Pull complete 
    Digest: sha256:10d7d58d5ebd2a652f4d93fdd86da8f265f5318c6a73cc5b6a9798ff6d2b2e67
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
    3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
    $ docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    ```
7. 卸载
    ```
    sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin

    sudo rm -rf /var/lib/docker
    sudo rm -rf /var/lib/containerd
    ```

## 编写dockerfile制作深度学习镜像
### dockerfile指令
    ```
    FROM   		#基础镜像  一切从这里开始构建
    MAINTAINER  #镜像是谁写的  名字+邮箱
    RUN  		#镜像构建的时候需要运行的命令
    ADD			#步骤，tomcat镜像，加一个tomcat压缩包！添加内容
    WORKDIR 	#镜像的工作目录
    VOLUME		#挂载的目录
    EXPOSE		#指定暴露端口
    CMD			#指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代
    ENTRYPOINT	#指定这个容器启动的时候要运行的命令，可以追加命令
    ONBUILD		#当构建一个被继承DockerFile，这个时候就会运行ONBUILD的指令
    COPY		#类似ADD，将我们的文件拷贝到镜像中
    ENV			#构建的时候设置环境变量
    ```
    