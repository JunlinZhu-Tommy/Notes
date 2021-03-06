## 说一下你对MSS和数据传输的理解？

### 从协议角度

TCP是一个面向字节流的协议，他不限制传输消息的长度，但是在TCP之下的传输层和数据链路层所发送报文时的内存是有限的，因此会限制TCP的报文大小。

TCP会把从应用层传输的任意长度字节流，切分成许多个报文段，拆分报文段的依据就是MSS。

### 为什么要分段

应用程序很有可能是从1 ~ 发送到22个字节的，实际上TCP收到的是一个数据流，但是被拆分成很多segment段。

#### 防止 IP 层分段

如果TCP层不进行数据分段，那么就会在IP层进行分段操作。IP层基于MTU对报文进行拆分的效率是非常低的，当发生丢包时，会重传所有报文。

#### 流控：接收端的能力

服务器接收能力是动态的，如果当前特别繁忙，势必会缩减MSS的大小

![20200610160452]( https://supyyy-1259673491.cos.ap-beijing.myqcloud.com/2020/pictures20200610160452.png)

### MSS

MSS是在握手阶段就已经双方协商初始大小的，默认MSS大小：536 字节（默认 MTU576 字节，20 字节 IP 头部，20 字节 TCP 头部）

> 仅指 TCP 能够承载的最大数据，不包含 TCP 头部的大小,尽量每个 Segment 报文段携带更多的数据，以减少头部空间占用比率

#### MSS 分类

发送方最大报文段 SMSS

接收方最大报文段 RMSS