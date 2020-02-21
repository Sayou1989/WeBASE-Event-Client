# 附录

## 1. 安装示例

### 1.1 Java部署

此处给出OpenJDK安装简单步骤，供快速查阅。更详细的步骤，请参考[官网](https://openjdk.java.net/install/index.html)。

#### ① 安装包下载

从[官网](https://jdk.java.net/java-se-ri/11)下载对应版本的java安装包，并解压到服务器相关目录

```shell
mkdir /software
tar -zxvf openjdkXXX.tar.gz /software/
```

#### ② 配置环境变量

- 修改/etc/profile

```
sudo vi /etc/profile
```

- 在/etc/profile末尾添加以下信息

```shell
JAVA_HOME=/software/jdk-11
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH==.:$JAVA_HOME/lib
export JAVA_HOME CLASSPATH PATH
```

- 重载/etc/profile

```
source /etc/profile
```

#### ③ 查看版本

```
java -version
```

## 2. 常见问题

### 2.1 脚本没权限

- 执行shell脚本报错误"permission denied"或格式错误

```
赋权限：chmod + *.sh
转格式：dos2unix *.sh
```

### 2.2 构建失败

- 执行构建命令`gradle build -x test`抛出异常：

```
A problem occurred evaluating root project 'WeBASE-Event-Client'.
Could not find method compileOnly() for arguments [[org.projectlombok:lombok:1.18.2]] on root project 'WeBASE-Event-Client'.
```

  答：

方法1、已安装的Gradle版本过低，升级Gradle版本到4.10以上即可
方法2、直接使用命令：`./gradlew build -x test`

## 3. application.yml配置项说明

| 参数                                             | 默认值               | 描述             |
| ------------------------------------------------ | -------------------- | ---------------- |
| server.port                                      | 5006                 | 当前服务端口     |
| server.servlet.context-path                      | /WeBASE-Event-Client | 当前服务访问路径 |
| spring.rabbitmq.host                             | 127.0.0.1            | rabbitmq主机地址 |
| spring.rabbitmq.port                             | 5672                 | rabbitmq端口     |
| spring.rabbitmq.username                         | defaultAccount       | rabbitmq账号     |
| spring.rabbitmq.password                         | defaultPassword      | rabbitmq密码     |
| spring.rabbitmq.virtual-host                     |                      | rabbitmq虚拟地址 |
| spring.rabbitmq.listener.simple.acknowledge-mode | manual               | 手动确认消息消费 |
| spring.rabbitmq.ssl.enabled                      | false                | 是否启用SSL支持  |
| logging.config                                   | classpath:log4j2.xml | 日志配置文件目录 |
| constant.frontIpPort                             | 127.0.0.1:5002       | 前置服务IP端口   |