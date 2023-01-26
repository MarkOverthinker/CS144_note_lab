# 整体大致总结

ByteStream:实现一个基础字节流。

StreamReassembler:以一个ByteStream作为输出缓冲区，接收并组织乱序数据报，形成基础的滑动窗口。有数据情况下，找到合适位置插入，并合并重复数据。无数据情况下，判断是否为eof，可能为syn\ack之类，无影响。

StreamReceiver、
