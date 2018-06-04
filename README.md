- ### USmart函数的使用  usmart.c 三个函数 +一个串口接收函数

串口接收函数需要配合原子家自己的接收协议（回车那个）

一个函数用来初始化中断用来实现串口数据处理 。

另外两个函数一个是用来算程序运行时间的（根据所使用的MUC时钟来修改）

usmart_scan 两个参数 一个是串口数据 一个是串口接收状态  

具体修改在 usmart_config.中加头文件加按格式写好的函数名

list 打印所有函数

id  获取入口地址  

help  帮助信息

hex dec 十进制十六进制转换

runtime 1/0  开启或关闭 函数时间计时功能

带有函数参数的函数的调用  利用id获取函数参数地址   使用方法函数（地址，参数）




-  ### 高级定时器 1&8 

8个通道

16位定时器  由一个可编程预分频器驱动（16位）

脉冲宽度捕获 。产生波形 （N多功能 PWM 死区时间互补PWM 和H桥和半H桥有关  上下桥臂不是同时输出 造成差异）

周期由两个分频器控制。 高级定时器和通用定时器互相独立。




-  ### USART和UART

universal asynchronous reciver and transmitter    通用异步收发器

universal synchronous asynchronous receiver and transmitter  通用同步异步收发器

USART 支持同步模式，因此USART 需要同步始终信号USART_CK（单片机可发送），通常情况下同步信号很少使用，因此单片机的UART和

USART使用方式差不多，都是用异步模式进行收发。

通过串口向单片机发送数据。 比如说发“abcde111" 串口以字符串发送数据，首先将字符串转化为二进制,一次性接收8位，相当于第一次

接收到”a“ -0000 1010 。是一个字符是一个字节，产生一次中断。 0x01 占一个字节 0x001占两个字节。 串口中断一次一个字节八位。

//取消ARM的半主机工作模式
#pragma import(__use_no_semihosting)                             
struct __FILE { 
    int handle; 
}; 

FILE __stdout;          
_sys_exit(int x) 
{ 
    x = x; 
}

int fputc(int ch, FILE *f){      
    while((USART1->SR&0X40)==0);
    USART1->DR = (u8) ch;      
    return ch;
}

-  ### 堆 FIFO  栈 FILO

心得：对于搞嵌入式的人来所，嵌入式系统的内存是宝贵的，内存是否高效率的使用往往意味着嵌入式设备是否高质量和高性能，

所以高效的使用内存对我们来说是很重要的。



-  ###  Git

.gitignore 用于忽略你不想提交到Git上的文件
 
.gitattribute 指定非文本文件的对比合并方式 

pull是从remote repo拉取local branch的最新代码下到local repo；

fetch是从remote repo拉取other branches的最新代码下到local repo。





-  ### ESP8266 

AT指令固件包  NodeMCU固件包

芯片是乐鑫的  模组是安信可的  

ESP8266 也可以用SPI进行通信开发（未完待续）：

一共两个SPI：SPI和HSPI   其中SPI已经和内部FLASH连接 HSPI可以为我们所用（仅支持主机模式）
图:
震惊，给8266刷上nodemcu固件 竟然变成了8位MCU！ （抛弃AT，暂弃SDK！）

266如果要进行SPI与外部MCU进行通讯

https://bbs.espressif.com/viewtopic.php?t=2426

https://github.com/espressif/ESP8266_RTOS_SDK

https://www.cnblogs.com/yangfengwu/p/7524297.html

https://www.espressif.com/zh-hans/support/download/documents?keys=&field_type_tid%5B%5D=14

https://bbs.espressif.com/viewtopic.php?f=67&t=225

https://wenku.baidu.com/view/7160d1ff312b3169a551a452.html

CPOL控制空闲时的电平状态，CPHA控制数据在CLK第几个沿开始传输。

高位开始传输

-  ### FreeRTOS

利用STM32CubeMX 进行基本配置 

首先配置始终，选择外部晶振输入，然后配置两个IO口并改标签。然后使能FreeRTOS。

切换第二个表卡，点击图标。Config parameters
是配置参数，列出了FREERTOS中可配置的参数，对应FreeTTRTOSConfig.h中的参数

Include parameters 选项卡的参数是用来配置裁剪系统的。

Tasks and Queues 用于添加任务和队列

Timers and Semaphores 是添加软件定时器和信号量的选项 


-  ### JTAG JLINK SWD  下载调试

JLINK是利用STM32的JTAG口进行下载和调试的。 

使用了JLINK V7版本（利用的是之前飞思卡尔 Zigbee开发板送的） 

 用了四根线  VCC GND CLK SWDDIO 。发现下载不进去 提示尝试Reset。 因为仿真器没有这个脚。手按着开发板的复位键也不行。

MDK 设置Reset模式也没用 。网上说与一种system reset 模式和  vect reset 都没有找到。 仿真器的reset 脚接开发板的reset脚 。不就是控制开发板的reset吗

最后没有下载成功。 希望以后能用上高级版本的jink 进行测试。

-  ### STM8

Stm8cubemx 只能生成引脚分配图  不能生成代码

Stm8 AD 配置流程 
- 使能或失能AD外设
- 初始化和配置寄存器，ADC分辨率，ADC转换模式
- 配置外部触发源
- 通过软件设置触发AD转化 

typedef* structure 

structure-> =

typedef structure 

structure. =

-  ### C指针



int *p；p是一个指针变量 需要指向一个地址 （初始化） p就是一个需要被指向整形变量地址的变量。

int *p；
p=&a;
*p++;
print(a)//a=a+1;


在形参中 int *p 就是一个地址。 point( int *p){}

int* p;
p="abcd"; //可行 应为字符串传递值就是字符串的首地址
 
int a[10];
p=a; //数组a的首地址
char *arr[4] = {"hello", "world", "shannxi", "xian"};
//arr就是我定义的一个指针数组，它有四个元素，每个元素是一个char *类型的指针，这些指针存放着其对应字符串的首地址。
char (*pa)[4];
//pa是一个指针指向一个char数组，每个数组元素是一个char类型的变量

-  ### RS485 

RS485转换器SP3485。其中5脚和8脚是电源引脚；6脚和7脚就是RS485通信中的A和B两个引脚；1脚和4脚分别接到单片机的RXD和TXD引脚上，直接使用单片机UART进行数据接收和发送；2脚和3脚是方向引脚，其中2脚是低电平使能接收器，3脚是高电平使能输出驱动器，我们把这两个引脚连到一起，平时不发送数据的时候，保持这两个引脚是低电平，让MAX485处于接收状态，当需要发送数据的时候，把这个引脚拉高，发送数据，发送完毕后再拉低这个引脚就可以了。为了提高RS485的抗干扰能力，需要在靠近MAX485的A和B引脚之间并接一个电阻，这个电阻阻值从100欧到1K都是可以。

modbus 是一个应用层级的协议。 特点包括数据头的设备地址，功能码，n个数据位，CRC校验位。 另外主机发送请求后，从机会有对应的响应。

freemodbus的移植与使用

参考网址：

https://www.amobbs.com/thread-5491615-1-1.html  Freemudbus移植 

https://github.com/armink/FreeModbus_Slave-Master-RTT-STM32  主从机模式 都有




-  ### 差分信号

任何两个信号都可以分解为共模信号和差模信号。共模信号是作用在差分放大器或仪表放大器两个输入端的相同信号，通常是由于线路传导和空间磁场干扰产生的，是不希望出现的信号，差模信号是两个输入端信号的相位相差180度。如果共模信号被放大很多，会影响到真正需要放大的差模信号。设两路的输入信号分别为： A,B，分别表示为：A=m+n；B=m-n，则输入信号A,B可以看成一个共模信号 m 和差模信号 n 的合成，其中m=(A+B)/2；n=(A-B)/2。
常用共模抑制比CMRR来衡量差分放大电路抑制共模信号的能力，它是放大器对差模信号的电压放大倍数与对共模信号的电压放大倍数之比，CMRR越大，放大器的性能越好。

在差分放大电路中，无论是温度变化，还是电源电压的波动等，都会引起两管（两特性相同的三端器件所组成的差分放大电路的输入端）集电极电流以及相应的集电极电压相同的变化，其效果相当于在两个输入端加入了共模信号。温度变化、电源电压的波动等引起的信号变化当然要加以抑制，所以要抑制共模信号。
常用共模抑制比作为一项衡量差分放大电路抑制共模信号的能力的技术指标，其定义为：放大电路差模信号的电压增益与共模信号的电压增益之比的绝对值。共模抑制比愈高，抑制共模信号的能力越强。

-  ### PCB
 #### 布局
DC/DC 变换器、开关元件和整流器应尽可能靠近变压器放置，整流二极管尽可能靠近调压元件和滤波电容器。以减小其线路长度。

　　电磁干扰（EMI）滤波器要尽可能靠近 EMI 源。尽可能缩短高频元器件之间的连接，设法减少他们的分布参数及和相互间的电磁干扰。易受干扰的元器件不能相互离的太近，输入和输出应尽量远离。

　　对于电位器、可调电感线圈、可变电容器、微动开关等可调元器件的布局应考虑整块扳子的结构要求，一些经常用到的开关，在结构允许的情况下，应放置到手容易接触到的地方。元器件的布局到均衡，疏密有度。

　　发热元件应该布置在 PCB 的边缘，以利散热。如果 PCB 为垂直安装，发热元件应 该布置在 PCB 的上方。热敏元件应远离发热元件。

　　在电源布局时，尽量让器件布局方便电源线布线走向。布局时需要考虑减小输入电源回路的面积。满足流通的情况下，避免输入电源线满板跑，回路圈起来的面积过大。电源线与地线的位置良好配合，可降低电磁干扰的影响。如果电源线和地线配合不当，会出现很多环路，并可能产生噪声。

　　高、低频电路由于频率不同，其干扰以及抑制干扰的方法也不相同。所以在元件布局时，应将数字电路、模拟电路以及电源电路按模块分开布局。将高频电路与低频电路有效隔离，或者分成小的子电路模块板，之间用接插件连接。

　　此外，布局中还应特别注意强、弱信号的器件分布及信号传输方向路径等问题。 为将干扰减轻到最小程度，模拟电路部分和数字电路部分分隔开之后，保持高、中、低速逻辑电路在 PCB 上也要用不同区域，PCB 板按频率和电流开关特性分区。 噪声元件与非噪声元件要距离远一些。热敏元件与发热元件距离远一些。低电平信号通道远离高电平信号通道和无滤波的电源线。将低电平的模拟电路和数字电路分开，避免模拟电路、数字电路和电源公共回线产生公共阻抗耦合。

-  ### MQTT

 使用 Modbus 作为本地接口来管理设备，使用 MQTT 作为全局协议来扩展设备的范围，二者都起到了重要的作用.

 创建实例，创建设备，创建身份（每一台设备thing都需要绑定相应的身份principal），创建策略，得到账号密码。

 创建客户端，填入账号密码（不明）。

 S8WXST3StTeHQNTEVC4MciPoSTVEyjNji6iTcGyiR+0= 
 S8WXST3StTeHQNTEVC4MciPoSTVEyjNji6iTcGyiR+0=

 -  ### SDIO

 SIDO 第一步设置SDIO_POWER 寄存器最低2位为1 上电


  -  ### FATFS

  ①修改数据类型 integer.h
  ②配置相关功能  ffconfg.h
  ③底层驱动函数编写 一般编写6个 diskio.c 
 
  从我学习FATFS到现在已经2个月了，大概能操作TF卡后就开始往里写数据，还一直在改写写卡的逻辑，下面是我在写卡时总结的（可能并不适应与你）。 

1、硬件：lpc2132 硬件SPI操作 22M主频 
2、文件系统：FATFS R0.09 
3、卡：2G、4G、16G（有的是大陆产的，有的是台湾产的。目前2G的卡有大陆和台湾产的，发现大陆的这个没台湾的好，写卡时电流不稳定，而台湾的那个很 稳） 
4、数据：AD采样进来的音频数据，短的几秒钟，长得几个小时 
5、方式：录完一个系统进入掉电模式，有录音需要时再起来录（每次单片机起来这里就会建立一个txt文件） 
6、AD：pcm1870（谁用过这个东东呢，它老是丢数，我问ti在线支持了，他们没给我个好的解决方法，不知你们发现没有丢数这个现象） 
7、采样率：8K 


注意点：1、在TF卡中写时不要直接在根目录下写文件，最好先建立一个文件夹，在文件夹里写，这样工作电流就会小很多，而且电流也很稳定（主要原因） 
        2、一个文件夹里的txt文件数目不能太多，否则单片机从掉电模式起来到写卡时有点慢，会造成前面的数据丢失（我的2G的卡里，每个文件夹里的文件不能超过50个，超过后唤醒单片机到写卡时间过长，造成一些数据丢失） 
        3、小容量卡写电流小，大容量卡写电流大（2G:40mA，4G:50mA，16G:100mA，） 
        4、写小的文件（写几秒就要关闭的）用f_sync(&file);写大文件（就是连续写n个小时）用f_close(&file); 

还在郁闷的问题： 
1、第一次单片机从掉电模式起来的比较慢（大概2秒），但从第二次后起来就非常快了 
    注：程序到while(1)前面就进入掉电模式了，每次从掉电模式起来就到while(1)里了，执行的语句都是一模一样的啊，怎么会这样呢 

2、由于第一点的迷惑，我怀疑单片机从掉电模式起来后是不是从while(1)哪里执行呢？不是说：从哪里掉电，起来时就从那里执行的吗？？ 

3、2G的卡写电流很稳定，但4G和16G的就不怎么稳定了，尤其是16G的，写卡时电流摆动很大，即使寻址范围大也不至于电流摆动那么大吧 
   我的16G卡写电流摆动范围：50mA-100mA啊，天哪，手机里或别的电子产品里可不是这样啊，难道这是fatfs的原因，或是我写卡的逻辑不对？？？？？？？？？？？？？？？？？？？？ 

这是我写卡的程序：SD_Write_Flag是定时器里的一个变量，如果SPI数据寄存器满了（AD给的数据），他就为1，定时器每个500us去看一次, 
         if(SD_Write_Flag)   
         { 
            SD_Write_Flag=0; 
            if(buffer_number) 
            { 
              res1 = f_write(&file, buffer1, 512, &br);     //写入 
              f_sync(&file);  
              IO0SET |=1<<15;         //P0.15输出高，关闭LED 
            } 
            else 
            { 
              res1 = f_write(&file, buffer0, 512, &br);     //写入 
              f_sync(&file);  
              IO0CLR |=(1<<15);      //P0.15输出低，点亮LED 
            } 
         }

 -  ### UCosIII 
 ##### 参考的是安富莱ucosiii的教程：http://forum.armfly.com/forum.php?mod=viewthread&tid=1788&extra=page%3D1

 调度器：使用相关算法来决定当前执行任务。 就绪任务和挂起任务 。激活一个就绪态的任务。
 合作式调度器：只有一个任务可以执行，不可被抢占。直到自愿放弃、
 抢占式调度器：激活就绪任务中优先级最大的一个（ucos是数值越低越高）
 时间片调度器:Round-robin算法。适用于不要求任务实时响应的情况。给同优先级的分配一张列表。运行一段时间长度以后切换。
##### 移植
M4比M3多了一个浮点单元。
内核OS特性：
双堆栈指针 ：MSP PSP
SysTick定时器：OS时钟
SVC和PendSV：两个异常 （任务切换）
非特权级执行模式：提高系统鲁棒性
独占式访问：独占式存储和加载指令作用于信号量和互斥操作。
R0-R15寄存器  R13为堆栈指针SP
R0-R7 低位寄存器 16位指令
R8-R12 高位寄存器 32位指令和部分16位指令 
MSP 是默认堆栈指针。由OS内核，异常服务和特权访问的程序代码使用
PSP 常规程序代码使用 
![](http://ww1.sinaimg.cn/large/006Esg89gy1frry0uylk6j30fa02ydfu.jpg)

R14是连接寄存器， 保存函数返回地址 

R15是程序计数器 （PC） ，返回值是当前指令地址+4

程序状态寄存器 PSRs或xPSP

![](http://ww1.sinaimg.cn/large/006Esg89gy1frryl1hd3fj30mb091t9i.jpg)
中断屏蔽寄存器组

![](http://ww1.sinaimg.cn/large/006Esg89gy1frrylhppwfj30lv07cmy1.jpg)
如何操作

![](http://ww1.sinaimg.cn/large/006Esg89gy1frryzw4pjij30mc0bj752.jpg)
控制寄存器 ：定义特权级别和选择当前使用哪个堆栈指针。





 -  ### EMwin

 STM32 FPU 需要DSP库  在STM32Cubermx里

 STM32片内自带SRAM和FLASH，FLASH是用来存储程序的，SRAM是用来存储程序运行中的中间变量，通常不同型号的.STM32的SRAM和FLASH大小是不相同的，以我手边的STM32F103VET6来看，根据数据手册可以看到

-  ### NB-Iot
 
5.25收到NBIOT模组，模块是移远，型号BC-05 电信卡。

-  ### 荔枝pi

收到了一块5寸触摸屏（电阻） nano一块 

哇哇哇 吃灰一个礼拜 （ 答辩） 

今天晚上10点，惊觉醒。 扒开一堆“电子废品” 找到了那块闪着光的Lichee Pi  有点小激动。 

给补焊上去了，否则是分分钟要被我泰拳警告的。后来接屏+上电---果然白屏..溜回学校答辩。

打开了盒子，拿出了这块搭载全志fS100s应用级处理器的核心板（cortex A7）哇哇哇哇 高端，以前只摸过F7 （虽然树莓派已经吃灰很久了 = =）。

废话不多说，先在群里下载了各种资料，打开......MMP 没有我想要的上电就亮碉堡的镜像啊。咋办啊 ，各种资料，一度开始膨胀到linux下SDK的搭建，开始移植UBOOT。。。。

弄了半天发现我错了.. 因为我看到了这么一句话：首先进行的是安卓镜像的傻瓜是烧写，目的检测收到的荔枝皮一切都正常。烧写群主提供的镜像文件安4.1版本，启动成功！ 

惊了。 赶紧找那个就是我现在要搞的安卓镜像... 现在在下载。
30分钟过去了,发现下错了+网速卡。 好在终于百分百找到了我想要的那个，开始下载，坐骑云 美滋滋。
烧写完毕...白屏。定视一下,操。。 屏幕的排线被我弄断了  GG  界面显示不起来了。 咸鱼的那个7寸屏也点不亮。 明天找其他解决方案，暂时不排除lichee pi 本身的原因。
找到了原因了 Lichee本身是没有问题的。是我自己太菜。。。
   
-  ### STM32向量表