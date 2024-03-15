### 3_8

描述：

```
梯形累加积分计算面积 列出各组耗时
```

输出：

```
took :3.29
area2:0.589049
took :3.087
area3:0.589049
took :3.165
area4:0.589049
res:0.589049
```

### 3_11

描述：

```
//计算pi值，并探讨多线程分块对不同i（随i的大小耗时变化）的方法的影响
```

输出：

```
pi :3.14159
3.1415926436
took :0.085
2  --pi :3.14159
3.1415926436
took :0.0320001
3  --sum :596.903
596.9026022820
took :2.682
4  --sum :596.903
596.9026022820
took :6.035
```



### 3_12

描述：

```
    1. 16个线程， 共同维护一块共享内存
    2. 当启动时，每个线程生产一个消息，并在休息5ms后进入读取阶段
    3. 读取阶段时，直到该线程已读取过一个消息，否则循环访问获取消息。
    4. 对读取到的消息打印输出本线程的id；
```

输出：

```
9 get message: 0 
14 get message: 6 
13 get message: 1 
10 get message: 4 
7 get message: 5 
12 get message: 3 
8 get message: 7 
6 get message: 13 
0 get message: 8 
5 get message: 9 
3 get message: 14 
1 get message: 10 
4 get message: 11 
2 get message: 10 
11 get message: 12 
15 get message: 2 
```

