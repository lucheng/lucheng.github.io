   1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。 
   2.对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。 
   3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。

   ArrayList 初始化容量为10 ，超过的话为1.5倍扩容，每次扩容会重新生成数组，频繁插入的操作中，建议指定容量大小。
