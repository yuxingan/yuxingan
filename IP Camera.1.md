
# 关于NALU使用RTP包进行发送可能的类型有：

## 单一 NAL 单元模式
即一个 RTP 包仅由一个完整的 NALU 组成。这种情况下 RTP NAL 头类型字段和原始的H.264的NALU 头类型字段是一样的。

对于 NALU的长度小于 MTU [^1]大小的包，一般采用单一 NAL 单元模式。

对于一个原始的H.264 NALU 单元常由 `[StartCode] [NALU Header] [NALU Payload]` 三部分组成，其中 Start Code 用于标示这是一个NALU 单元的开始，必须是"00 00 00 01" 或"00 00 01"，

NALU 头仅一个字节，其后都是 NALU 单元内容。打包时去除 "00 00 01" 或"00 00 00 01" 的开始码，把其他数据封包的 RTP 包即可，有如下例子：

```
[00 0000 01 67 42 A0 1E 23 56 0E 2F ... ] 

封装成 RTP 包将如下：

[ RTPHeader ] [ 67 42 A0 1E 23 56 0E 2F… ]
```

代码：

[基于RTP的H264视频数据打包解包类](https://blog.csdn.net/gokartscomeon/article/details/44408295)

[从零开始写一个RTSP服务器](https://blog.csdn.net/weixin_42462202/article/details/98986535)

 [^1]:**MTU（Maximum Transmission Unit，MTU）**：最大传输单元，是指一种通信协议的某一层上面所能通过的最大数据报大小（以字节为单位）。最大传输单元这个参数通常与通信接口有关（网络接口卡、串口等）。
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MTA5MDkyNThdfQ==
-->