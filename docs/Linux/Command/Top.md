# Top命令
概述

在linux,top主要监控系统的运行情况，是常用的性能分析工具，
能够实时显示系统中各个进程的cpu,内存等资源占用情况。

    #复制代码
    top
    # 特别的，可以通过-p参数指定一个进程进行监控
    top -p pid

# 1.top的统计信息
第一行

    top - 13:58:21 up 50 min,  1 user,  load average: 0.00, 0.01, 0.05
    up:现在运行的时间，min:已运行的时间
    user:现在登录的用户
    load average(系统负载的时间): 1分钟 5分钟 10分钟
    如果这个数字除以逻辑cpu的数量，结果高于70的时候就表明系统在超负荷运行

第二行

    Tasks: 152 total,   1 running, 151 sleeping,   0 stopped,   0 zombie
    total:总的进程，running:现在运行的进程，sleeping:沉默进程，stopped:停止数，zombie:僵尸进程

第三行

    %Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
    %cpu(s):CPU信息，s表示不止一个，us:用户空间占用cpu的百分比，sy:系统占用cpu的百分比 ni:
    id:空闲cpu百分比

第四行

    GiB Mem :      3.7 total,      3.3 free,      0.2 used,      0.1 buff/cache
    Gib Mem:内存的使用情况 ，total:总内存，free:空闲内存，used:已使用内存，buff/cache:用作内核缓存的内存量

第五行

    GiB Swap:      2.0 total,      2.0 free,      0.0 used.      3.2 avail Mem 
    Gib Swap:交换区的使用情况，total:总缓存，free:空闲，used:已使用，avail Mem:可用于进程下一次分配的内存数量

# 2.top的进程信息


    PID   进程id                                             
    USER  进程拥有者
    PR    优先级
    NI    nice负值高优先级，正值低优先级 进程使用的虚拟内存
    VIRT  进程使用的虚拟内存总量 VIRT=SWAP+RES
    RES   进程使用的未被换出的物理内存大小，RES=CODE+DATA
    SHR   共享内存的大小
    S    进程状态，D=不可中断的睡眠状态，R=运行，S=睡眠，T=跟踪，Z=僵尸进程
    %CPU  进程使用的CPU时间占用百分比
    %MEM  进程使用的物理内存百分比
    TIME+ 进程运行时间
    COMMAND  命令行

# 3.top的指令功能
    ？查看支持的功能按键
    b 粗体高亮显示
    c 显示完整的进程命令
    E 切换统计栏的内存单位 
    e 切换进程栏的内存单位
    t 切换统计栏的CPU展示方式
    m 切换统计栏的内存展示方式
    1 展开统计栏的逻辑CPU信息
    f 设置
    L 查找
    P 以CPU的使用资源排序显示
    M 以内存的使用资源排序显示
    N 以pid排序显示
    T 由进程使用的时间累计排序显示
    k 给某一个pid一个信号，杀死进程
    q或者Ctrl+C 退出top


