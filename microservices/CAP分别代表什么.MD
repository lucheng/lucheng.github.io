CAP分别代表什么

• Consistency 
   • (all nodes see the same data at the same time)
• Availability 
   • Reads and writes always succeed.
• Partition tolerance 
   • (the system continues to operate despite arbitrary message loss or failure of part of the system)

一致性： 更新操作成功并返回客户端完成后,分布式的所有节点在同一时间的数据完全一致

可用性:  读和写操作都能成功

分区容错性：再出现网络故障导致分布式节点间不能通信时，系统能否继续服务
