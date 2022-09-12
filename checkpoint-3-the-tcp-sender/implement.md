# implement

<figure><img src="../.gitbook/assets/TCPSenderclass (1).png" alt=""><figcaption></figcaption></figure>

#### fill\_window

* 若还未发送syn，则发送syn
* 若syn还未被接收到，等待
* 若\_wsize不为0，则发送segment : 1.已发送fin，则不操作；2.\_stream已空，未eof则等待，已eof则发送fin;3.尽可能多的将\_stream填充到segment中并发送，填充的多少取决于\_stream的长度、\_wsize的大小、payload能承载的最大值。
* \_wsize和\_rwsize都为0，且未发送过1字节数据大小payload的segment，若已发送fin则不操作。否则发送一个1字节大小payload的segment。

#### ack\_received

* 接收到的ackno大于next\_seqno，信息不合理，退出。
* \_rwsize设为window\_size。
* 检查已发送队列，根据返回ackno确定哪些segment被接收到了并出列。本实验只将ackno位于整个segment之后视为segment被接收，即部分被接收不视为被接收。若有segment出列\_rto置为初始值并重置重传计时。同时判断是否需要修改\_has0to1;
* 根据处理完的已发送队列计算\_wsize。
* 已发送队列为空则关闭重传计时。
* 再次调用fill\_window，根据ack到的信息发送segment。

#### tick

* 首先判断是否需要计时
* 之后增加计时，判断是否满足发送要求（计时达到，且\_wsize不为0或存在0窗口发送1字节数据的情况），满足则进行发送。

#### send\_segment

* 填充报头的seqno
* 修改\_next\_seqno
* 增加\_bytes\_in\_flight计数
* 减少\_wsize
* 发送segment，并将segment添加到已发送队列中
