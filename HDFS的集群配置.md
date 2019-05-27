### HDFS的集群配置

1.添加用户： 
         
```
  useradd 用户名
  passwd 用户名
```
     

然后输入密码。


2.查看虚拟机用户名：

```
hostname 
```


3.永久修改主机名：

```
vi /etc/hostname
```

按下我，进入VI的编辑模式，编辑完后按下ESC键，然后输入：WQ退出，然后重启重启（更新数据）


4.配置映射文件：

```
vi /etc/hosts
进入编辑模式，输入ip用户名值，然后保存并退出。
  使用scp -r / etc / hosts ip地址：/ etc /发送到相应的IP地址的etc / hosts中。
```


5.安装JDK 

```
上传使用sftp协议，alt + p 
解压：tar -zxvf包名-C路径
```


6.jdk的环境变量的配置

```
vi /etc/profile

按ģ快速到配置文件的最低，然后按我进入编辑模式，在最后添加环境变量

export java_home=/root/hd/jdk1.8.0_191
export path=$path:$java_home/bin
注意java_home的路径是安装jdk的绝对路径地址
 退出并保存  
 然后（加载环境变量）

source etc/profile
```

 6.ssh免密登录

```
 ssh-keygen
直接三次回车，然后


ssh-copy-id hadoop01
先自己后其他
```

 7.重命名文件：

```
mv a b 
 mv /a/b/c

（将/一个文件下文件移动到/ B下并命名为c）中
```

8.hdfs的环境配置

```
    1.修改hadoop-env.sh
       

 export JAVA_HOME=/root/apps/jdk1.8.0_60
```

```
     2.修改core-site.xml（核心配置）
         

<configuration>
               //配置
                 <property>
                         <name>fs.defaultFS</name>
                         <value>hdfs://hadoop01:9000</value>
                </property>
        </configuration>
修改HDFS-site.xml中

<configuration>
     <property>
        <name>dfs.namenode.http-address</name>
        <value>hadoop04:50070</value>
     </property>

     <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>hadoop05:50090</value>
     </property>

      <property>
        <name>dfs.namenode.name.dir</name>
        <value>/root/hd/dfs/name</value>
      </property>

      <property>
        <name>dfs.replication</name>
        <value>3</value>
      </property>

       <property>
        <name>dfs.datanode.data.dir</name>
        <value>/root/hd/dfs/data</value>
       </property>
</configuration>
```


2.启动HDFS集群
1.格式化的NameNode：
    

```
hadoop namemode -format
```

    
   2.配置hadoop的环境变量

```
export JAVA_HOME=/root/hd/jdk1.8.0_141
export HADOOP_HOME=/root/hd/hadoop-2.8.4
export PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
3.分发Hadoop的环境变量

scp -r /etc/profile hd09-02:/etc

注意：加载环境变量source / etc / profile 
```
    
4.启动namenode
  

```
 hadoop-daemon.sh start namenode
```
    
  启动数据管理部


```
   hadoop-daemon.sh start datanode
```

    
   访问namenode提供的web端口：50070 
4. 
自动批量的启动脚本

    1）修改配置文件从站
   

```
hadoop02
    hadoop03
```

    
    2）执行启动命令
  

```
 start-dfs.sh
```

3.停止集群命令

```
stop-dfs.sh
```


