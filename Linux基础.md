# `Linux`基础

## 第一章：`Linux`基础知识：

#### 1.常用的`linux`发行版：

`debian`，`ubuntu`，`centos`，`redhat`，`openeular`，`archlinux`等

#### 2.`GNU`与常见的`GNU`软件，`GPL`：

`GNU`致力于开发自由的类`UNIX`系统，是`Linux`能够迅速发展的重要原因

常见的`GNU`软件有：`gcc`，`gdb`等

`GPL`是一种许可证，意味着可以免费得到源代码并任意修改，有义务公开修改后的源代码

#### 3.`Linux`系统组成：

内核，shell，文件系统，应用程序

#### 4.`MBR`分区命名：

主分区占4个，逻辑分区从5开始编号，如`dev/sda`的第一个逻辑分区为`dev/sda5`

#### 5.安装软件的方法：

1.源码编译安装

2.`rpm`，`dpkg`

3.`yum`，`dnf`，`apt`，apt`-`get等

#### 6.`Linux`目录结构：

单一目录树结构，最上层是根目录， 所有目录都是从根目录出发而生成的

根目录底下常见的目录有`bin`，`boot`，`dev`，`etc`，`root`，`sbin`，`usr`，`lib`，`home`，`mnt`等

知道如何表示绝对路径和相对路径（`/root/`和`./abc/`）

#### 7.文件类型和文件权限：

**文件类型**分为：普通文件（-），目录文件（d），链接文件（l），设备文件（c，b），其他（管道，socket等）

**权限修改**：`chmod`。使用方法如`chmod a+x 1.txt`,`chmod 657 1.txt`

#### 8.文件的标识——`inode`：

唯一标识文件的是`inode`而非文件名

可以通过`stat`或者`ls -i`查看

#### 9.软链接和硬链接：

**建立命令**：`ln`，软链接需要加`-s`选项

**区别和联系**：

**硬链接**：不能对目录创建，多个文件名指向同一个`inode`，只有删除所有硬链接才会释放数据块，不能跨文件系统

**软链接**：可交叉文件系统，可对目录创建，可对不存在的文件创建，删除软链接不影响被指向的文件，删除被指向的文件会让软链接成为一个死链接

#### 10.`Linux`常用命令及相关命令参数：

**帮助命令**：`man`

**文件操作**：`ls`,`cd`,`mkdir`,`rmdir`,`pwd`,`rm`,`ln`,`grep`,`more`,`less`,`chmod`,`touch`

**网络命令**：`ifconfig`,`ping`,`route`

**其他命令**：`su`,`tar`

## 第二章：`Linux`编程基础：

#### 1.`vi`的使用：

**三种模式**：命令模式（进入默认），编辑模式，底行模式

**复制**：`yy`（行），`yw`（单词），`3yy`，`3yw`         **粘贴**：`p`，`P`

**查找**：**命令模式**：`/str`（下一个）  `?str`（上一个）  `/`（下继续）  `?`（上继续）

**替换**：**底行模式**：`:s/str1/str2`（行首次）`:s/str1/str2/g`（行所有）`:a,b s/str1/str2/g`（a到b行的所有，当前行为`.` ，末行为`$`

#### 2.`gcc`的使用：

**编译流程**：源代码→预处理→编译→汇编→链接

**文件名变化**：`.c`→`.i`→`.s`→`.o`→`a.out`

​				`-c`：只是编译不链接（生成.o)

​				`-S`：只是编译不汇编（生成.s）

​				`-E`：只进行预编译（生成.i）

​				`-o file`：把输出文件输出到file里

**调试**：`-g`

**出错警告**：`-Wall`

**库依赖使用**：

​				`-I dir`：在**头**文件的搜索路径列表中添加`dir`目录

​				`-L dir`：在库文件的搜索路径列表中添加`dir`目录

​				`-lpthread`：链接名为`libpthread.so`的库文件

#### 3.`makefile`的使用：

```makefile
program: main.o add.o dec.o mul.o div.o
	gcc main.o add.o dec.o mul.o div.o -o program
main.o:main.c main.h#main.h可省略
	gcc -c main.c -o main.o
add.o:add.c
	gcc -c add.c -o add.o
dec.o:dec.c
	gcc -c dec.c -o dec.o
mul.o:mul.c
	gcc -c mul.c -o mul.o
div.o:div.c
	gcc -c div.c -o div.o
clean:#伪目标
	rm *.o program
```

```makefile
objects = main.o add.o dec.o mul.o div.o
CC=gcc #若系统的CC指向gcc，可省略
CPPFLAGS=-I /tmp #若预处理无要求，可省略
CFLAGS=-Wall -O -g #若没有编译选项，可省略
LDFLAGS=-L /tmp –lpthread #若链接时无库依赖，可省略
program: $(objects)
	$(CC) $(LDFLAGS) $^ -o $@
clean:
	rm *.o program
```

#### 4.`gdb`的使用：

**调试过程**：

​			编译程序`（-g）`→启动调试`（gcc file）`→查看代码`（l）`→设置断点`（b）`→查看断点`（info b）`→运行程序`（r）`→单步调试`（n或s）`→查看变量`（p）`→继续运行`（c）`→退出`（q）`

​			此外还有：

​			`delete [断点号]`：删除指定断点，

​			`clear [行号或函数名]`：删除指定断点，

​			`ignore [断点号] [次数]`：忽略某个断点多少次

## 第三章：内核与启动管理：

#### 1.`Linux`系统管理常见命令：

`fdisk`：创建和维护分区表，

`df`：显示目前在 Linux 系统上的文件系统磁盘使用情况统计，

`du`：显示目录或文件的大小

#### 2.`Linux`启动过程（系统引导过程）：

上电→`BIOS`自检→`MBR/GPT`→`GRUB`→加载内核→`INIT`→登录

#### 3.`Linux`内核：

**五个重要子系统**：进程调度，进程间通信，内存管理，虚拟文件系统，网络接口

**裁剪编译安装命令**：

​			裁剪：`make config`（字符界面）`make menuconfig`（文本图形） `make xconfig`（图形界面）

​			编译安装：`make clean`（清理环境），`make dep`（编译依赖），`make bzImage`（编译），`make modules`（编译模块驱动），上述两步可以直接`make`，`make install`（安装）

## 第四章：文件系统：

#### 1.文件的物理结构，逻辑结构：

**物理结构**：文件在设备上的存储组织形式，即存储结构、文件分配方式

​					分为连续文件，链式文件，索引文件

**逻辑结构**：应用程序（用户）所看 到的文件结构

#### 2.描述空闲块：

**空闲区表法**：记录连续空闲区域的表格，表格的每一项记录 一个空闲区域的起始块号和块数，适用于连续文件

**空闲块链表法**：将所有的空闲块的块号用链表链在一起，适用于链式文件

**位视图法**：每一位对应一个物理块，0、1分别表示对应物 理块为空闲或占用。适合于索引文件

#### 3.`Linux`文件系统：

**块和块组的概念**：文件系统中存储的最小单位是**块**，包含一定数量的连续存储块组成**块组**

**块位图、`inode`位图、`inode`表的作用和大小**：

​			**块位图**用来描述整个块组 中哪些块已用

​			**`inode`位图**和块位图类似，本身占一个块，其中每个`bit`表 示一个`inode`是否空闲可用

​			**`inode`表**：每个文件都有一个`inode`，一个块组中的所有 `inode`组成了`inode`表

#### 4.定位一个文件的过程：

1.确定`inode`号

2.寻找`inode`号在磁盘上的位置

3.计算`inode`所在的块组：`inode`所在块组=(`inode`号-1)/每块组`inode`个数 取整

4.计算`inode`在该块组`inode`表中的序号：`inode`序号=(`inode`号-1)%每块组`inode`个数

5.确定`inode`在文件系统中的起始字节：某`inode`表项起始字节=`inode`起始块号每块所占字节数+该节点在块组内的序号*每个节点表 项所占字节数

#### 5.`ext3`多重索引原理：

0-11为直接指针，表示数据块的编号，12、13、14为一、二、三级间接指针

#### 6.`ext4`相对于`ext3`的改进：

块号从32位扩展到48位，`inode`占用字节数扩展为256， 引入Flexible 块组和元块组（二选一），每个块组的结构不是完全固定的,索引变为了区段索引

#### 7.`ext4`区段索引的基本原理：

将一个文件存储到多个连续的磁盘区域中，然后使用一个目录项来指向这些磁盘区间的起始位置和大小等信息

#### 8.文件相关命令：

`du`,`df`,`fdisk`,`dd`,`find`,`locate`,`whereis`,`which`,`mount`,`tar`	

#### 9.重定向：

`ls -l 1>log`, `ls -l 2>log`, `ls -l >log 2>&1`

## 第五章：进程与线程编程：

#### 1.程序，进程的概念：

**程序**：一组指令的有序集合

**进程**：具有独立功能的程序的一次运行过程

#### 2.进程的标识、特点：

程序名不能唯一标识进程，进程ID可唯一标识进程

具有独立性，动态性，并发性

#### 3.进程相关命令：

`ps –aux`、`kill`、`killall`、`top`

#### 4.进程的状态与转换：

**5态模型**：创建，就绪，执行，阻塞，僵死/终止

#### 5.常用的进程调度算法（非抢占与抢占）：

先进先出`（FIFO）`，最短进程优先`（SJF）`，轮转调度`（RR）`， 优先级调度，完全公平调度法`（CFS）`

`Linux`中**实时进程**严格按优先级调度，同优先级采用FIFO或者RR，**普通进程**采用完全公平调度法`（CFS）`

#### 6.死锁，互斥与同步：

**死锁**：指系统中若干进程相互 “无知地”等待对方所占有地资源而无限地处于等待状态地一种僵持局

**产生死锁必要条件**：资源的独占使用 ▪ 资源的非抢占式分配 ▪ 对资源的保持和请求 ▪ 对资源的循环等待

**互斥**：进程的互斥就是禁止多个进程同时进入各自访问同一临界资源的临界区，以保证对临界资源的排他性使用

**同步**：进程的同步是指进程间为了合作完成一个 任务而相互等待、协调步调

#### 7.僵尸进程和防范：

**为什么**：子进程比父进程先结束就会产生僵尸进程

**解决**：使用`wait`或者`waitpid`监控子进程状态

#### 8.多进程编程：

```c
/*****waitpid.c********/
int main(void)
{
	pid_t pid,pid_w;
	pid=fork();
	if(pid<0)
	{
   		exit(1);
  	}
	if(pid==0)  
	{
    		int i;
    		for(i=3;i>0;i--)
    		{
     			printf("This is the child\n");
     			sleep(2);
     		}
    		exit(0);
 	}
	else
 	{
 		do{
      			pid_w=waitpid(pid,NULL,WNOHANG); 
      			if(pid_w==0)
      			{
        			printf("The child process is running...\n");
        			sleep(1);
       			}
     		}while(pid_w==0);
   		if(pid_w==pid)
   		{
     			printf("Child Process %d End!\n",pid_w);
    	}
    	else
     		printf("some error occured.\n");
   	}
}
```

#### 9.进程间通信：

管道及有名管道，共享内存，套接字，信号量，信号，报文队列

其中共享内存最快，套接字可以跨机器通信

资源分配方面，进程是操作系统资源分配的基本单位

CPU调度方面，线程是调度执行的基本单位

#### 10.信号量与互斥锁：

用于解决线程间数据的共享和通信问题

## 第六章：`Linux`网络编程：

#### 1.网络相关命令：

`ifconfig`,`ping`,`route`

#### 2.什么是socket：

实质上是一种文件描述符

常见的有流式socket，数据包socket，原始socket

#### 3.通信五元组：

通信协议、本地主机地址、本地端口、远端主机地址、远端端口

五元组能唯一确定某次网络通信，socket包含这五种信息

#### 4.`TCP`通信实现：

```c
/* client */
int main(int argc,char *argv[])
{
        int sockfd;	
        char buffer[1024];
        struct sockaddr_in server_addr;
        struct hostent *host;
        int nbytes;
		short portnumber;
        if(3!=argc){ //命令行参数不为3
                fprintf(stderr,"Usage:%s hostname portnumber\a\n",argv[0]);
                exit(1);
        }
        portnumber=atoi(argv[2]);
        printf("server %s:%d\n",argv[1],portnumber);
        if(1==(sockfd=socket(AF_INET,SOCK_STREAM,0))){
                fprintf(stderr,"Socket error:%s\a\n",strerror(errno));
                exit(1);
        }
        printf("Socket id is %d\n",sockfd);
        bzero(&server_addr,sizeof(struct sockaddr_in));
        server_addr.sin_family=AF_INET;
        server_addr.sin_port=htons(portnumber);
		server_addr.sin_addr.s_addr=inet_addr(argv[1]);
        if(-1==connect(sockfd,(struct sockaddr *)(&server_addr),sizeof(struct sockaddr))){
                fprintf(stderr,"Connect Error:%s\n\a",strerror(errno));
                exit(1);
        }
        printf("Connect\n");
        if(-1==(nbytes=recv(sockfd,buffer,1024,0))){
                fprintf(stderr,"Read Error:%s\n\a",strerror(errno));
                exit(1);
        }
        buffer[nbytes]='\0';
        printf("I have received:%s\n",buffer);
        close(sockfd);
        exit(0);
}
```

```c
/* server */
int main(int argc,char *argv[])
{
        int sockfd,new_fd;
        struct sockaddr_in server_addr;
        struct sockaddr_in client_addr;
        int sin_size,portnumber;
        char input[1024];
        sin_size=sizeof(client_addr);
        if(2!=argc){
                fprintf(stderr,"Usage:%s portnumber\a\n",argv[0]);
                exit(1);
        }
        if((portnumber=atoi(argv[1]))<0){
                fprintf(stderr,"Usage:%s portnumber\a\n",argv[0]);
                exit(1);
        }
        //server creating
        if(1==(sockfd=socket(AF_INET,SOCK_STREAM,0))){
                fprintf(stderr,"Socket error:%s portnumber\a\n",strerror(errno));
                exit(1);
        }
        printf("Socket id is %d\n",sockfd);
        bzero(&server_addr,sizeof(struct sockaddr_in));
        server_addr.sin_family=AF_INET;
        server_addr.sin_addr.s_addr=htonl(INADDR_ANY);
        server_addr.sin_port=htons(portnumber);
		printf("port :%d, network port:%d\n",portnumber,server_addr.sin_port);
        //bind sockfd
        if(-1==bind(sockfd,(struct sockaddr *)(&server_addr),sizeof(struct sockaddr))){
                fprintf(stderr,"Bind error:%s\n\a",strerror(errno));
                exit(1);
        } 
        printf("Bind\n");
        //listen sockfd
        if(-1==(listen(sockfd,5))){
                fprintf(stderr,"Listen error:%s\n\a",strerror(errno));
                exit(1);
        }
        printf("Listen\n");
        while(1){
                //try until connect
                bzero(&client_addr,sizeof(struct sockaddr_in));
                if(-1==(new_fd=accept(sockfd,(struct sockaddr *)(&client_addr),&sin_size))){
                        fprintf(stderr,"Accept error:%s\n\a",strerror(errno));
                        exit(1);
                }
                printf("Accept! sin_size=%d\n",sin_size);
                printf("Server get connection from %s\nPlease input:",inet_ntoa(client_addr.sin_addr));
				fgets(input,1000, stdin);
                if(-1==send(new_fd,input,strlen(input),0)){
                        fprintf(stderr,"Send Error:%s\n",strerror(errno));
                        exit(1);
                }
               	close(new_fd);
        }
        close(sockfd);
        exit(0);
}
```

#### 5.`UDP`通信实现

```c
/* server */
void msg_chat(int sockfd,struct sockaddr *pcliaddr,socklen_t clilen)
{
        int n;
        socklen_t len;
        char mesg[80];
        for(;;)
        {
                len=clilen;
                n=recvfrom(sockfd,mesg,80,0,pcliaddr,&len);
                mesg[n]=0;
                printf("\nClient Says:%s\n",mesg);
                printf("Server says:");
                fgets(mesg,80,stdin);
                sendto(sockfd,mesg,strlen(mesg),0,pcliaddr,len);
        }
}

int main(int argc, char* argv[])
{
        int sockfd;
        struct sockaddr_in servaddr,cliaddr;
        if (argc != 2)
        {
                printf("Usage: %s port\n",argv[0]);
                return 0;
        }
        sockfd=socket(AF_INET,SOCK_DGRAM,0);
        bzero(&servaddr,sizeof(servaddr));
        servaddr.sin_family=AF_INET;
        servaddr.sin_addr.s_addr=htonl(INADDR_ANY);
        servaddr.sin_port=htons(atoi(argv[1]));
        if(-1==bind(sockfd,(struct sockaddr *)&servaddr,sizeof(servaddr))){
                perror("bind error");
                exit(1);
        }
        msg_chat(sockfd,(struct sockaddr *)&cliaddr,sizeof(cliaddr));
        return 0;
}
```

```c
/* client */
void msg_chat(int sockfd,struct sockaddr *pservaddr,socklen_t servlen)
{
        int n;
        socklen_t len;
        char mesg[80];
        while(1)
        {
                printf("Client Says:");
                fgets(mesg,80,stdin);
                sendto(sockfd,mesg,strlen(mesg),0,pservaddr,servlen);
                n=recvfrom(sockfd,mesg,80,0,pservaddr,&len);
                mesg[n]=0;
                printf("Server Reply:%s\n",mesg);
        }
 
}

int main(int argc,char **argv)
{
        int sockfd;
        struct sockaddr_in servaddr;
        if(argc!=3){
                printf("Usage:%s IPaddress Port\n",argv[0]);
                exit(1);
        }
        bzero(&servaddr,sizeof(servaddr));
        servaddr.sin_family=AF_INET;
        servaddr.sin_port=htons(atoi(argv[2]));
        if(inet_aton(argv[1],&servaddr.sin_addr)<=0){
                printf("[%s] is not a valid IPaddress\n",argv[1]);
                exit(1);
        }
        sockfd=socket(AF_INET,SOCK_DGRAM,0);
        msg_chat(sockfd,(struct sockaddr *)&servaddr, sizeof(servaddr));
        return 0;
}
```



## 第八章：`Shell`编程：

#### 1.几种运行方式：

`.`或者`source`：在当前shell下运行

`sh`：新建一个shell，继承父环境但不改变父环境

`./filename`：新建一个shell运行，必须有可执行权限

#### 2.`Shell`变量：

▪ 用户自定义变量 

▪ 环境变量：使用`export`引用或者修改，常用有 `HOME`,`PATH`,`PWD`

 ▪ 位置参数变量 ：`$num`或者`${num}`

▪ 专用参数变量：`$*`，`$@`，`$0`，`$#`，`$?`，`$$`，`$!`

#### 3.通配符：

*：匹配不限长度的多个字符

? ：匹配任意一个字符

[] ：匹配字符组所限定的任何一个字符 

! ：表示不在方括号中所列出的字符

#### 4.三种引号：

**双引号**：双引号内的字符，除`$`、 `和 \仍保留其特殊功能 外，其余字符均作为普通字符对待

**单引号**：由单引号括起来的字符都作为普通字符出现

**倒引号**：倒引号括起来的字符串被shell解释为命令行

#### 5.括号：

()——命令组、结合$进行命令替换、初始化数组`array=(a b c d)` 

[]——字符范围、数组编号、算术运算、条 件判断 

{}——变量引用等

(())——算术运算、for循环中的算术运算比较`for((i=0;i<5;i++))` 

[[]]——条件判断等

#### 6.数字运算：

**`let`**：`let num=1+1`  或者`let "num=1+1"`

**`expr`**：`expr 5 % 3`      `expr \( 2 + 5 \) \* 2 – 3 # 括号必须被转义`

#### 7.条件测试：

**文件测试**：`[ -f name ]`      `[ -e name ]`

**字符串测试**：`[ -z str ]`    `[ str1 = str2 ]`   `[[ str1 == str2 ]]`

​						字符串按从左到右对应字符的ASCII码进行比较

**整数测试**：`[ int1 -eq int2 ]`   `[ in1 -gt int2 ]`   双[]也可以

​					`((int1 == int2))`

**逻辑测试**：`[ x -a y ]`   `[ x -o y ]`  `[ ! x]`

​				`[[ pattern1 && pattern2 ]]` `[[ pattern1 || pattern2 ]] `  `[[ ! pattern ]]`

​				`(( expr1 && expr2 )) `  `(( expr1 || expr2 ))`  `(( ! expr )) `

#### 8.流程控制：

```shell
myhost=centos1.ls-al.me
if ping -c1 -w2 $myhost &>/dev/null
then
echo "$myhost is UP."
else
echo "$myhost is DOWN." 
fi
```

```shell
case x in
	p1)
		command1
		;;
	p2)
		command2
		;;
	*)
		command3
		;;
esac
```

```shell
for variable in list
do 
	commands
done
```

```shell
for ((expr1;expr2;expr3)) # 执行 expr1
do # 若 expr2的值为真时进入循环，否则退出 for循环
	commands # 执行循环体，之后执行 expr3
done # 循环结束的标志，返回循环顶部
```

```shell
while expr # 执行 expr
do # 若expr的退出状态为0，进入循环，否则退出while
	commands # 循环体
done # 循环结束标志，返回循环顶部
```

```shell
until expr # 执行 expr
do # 若expr的退出状态非0，进入循环，否则退出until
	commands # 循环体
done # 循环结束标志，返回循环顶部
```

