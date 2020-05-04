Mysql优化 show profile
1. 先观察，开启慢查询日志，设置相应的阈值（比如超过3秒就是慢SQL），在生产环境跑上个一天过后，看看哪些SQL比较慢。
2. Explain和慢SQL分析。比如SQL语句写的烂，索引没有或失效，关联查询太多（有时候是设计缺陷或者不得以的需求）等等。
3. Show Profile是比Explain更近一步的执行细节，可以查询到执行每一个SQL都干了什么事，这些事分别花了多少秒。
4. 找DBA或者运维对MySQL进行服务器的参数调优。
https://www.cnblogs.com/dwlovelife/p/11110561.html