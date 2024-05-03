# 操作系统
## 四种cpu调度
- 先进先服务 FCFS
- 最短作业
- 优先级
- 时间片轮转 RR
_分为抢占性和非抢占性_ 
## 第一写者问题
### 三个条件
- 如果写者进程正在操作，读着进程必须等待
- 如果没有写者进程操作，读者进程不需要等待
- 如果读者进程操作，读者进程不需要等待，写者进程需要等待
### 两个信号量
- Readers
- writes 
## 死锁
### 死锁的必要条件
- Multal exclusion
- Hold and wait
- No preemption
- Circular wait




