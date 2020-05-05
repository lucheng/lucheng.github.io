Redis作为缓存（六种淘汰策略）
达到最大内存限制时(maxmemory), Redis 根据 maxmemory-policy 配置的策略, 来决定具体的行为。

当前版本,Redis 3.0 支持的策略包括:

noeviction: 不删除策略, 达到最大内存限制时, 如果需要更多内存, 直接返回错误信息。 大多数写命令都会导致占用更多的内存(有极少数会例外, 如 DEL )。

allkeys-lru: 所有key通用; 优先删除最近最少使用(less recently used ,LRU) 的 key。

volatile-lru: 只限于设置了 expire 的部分; 优先删除最近最少使用(less recently used ,LRU) 的 key。

allkeys-random: 所有key通用; 随机删除一部分 key。

volatile-random: 只限于设置了 expire 的部分; 随机删除一部分 key。

volatile-ttl: 只限于设置了 expire 的部分; 优先删除剩余时间(time to live,TTL) 短的key。