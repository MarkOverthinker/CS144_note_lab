# 重发机制

每隔一段时间，TCPSender会调用tick,tick会传入自上次调用tick后经过的时间，在时间到达重传时间后，重新发送最老的还未被TCPReceiver接收的TCPSegment。

<figure><img src="../.gitbook/assets/QQ截图20220912143349.png" alt=""><figcaption></figcaption></figure>
