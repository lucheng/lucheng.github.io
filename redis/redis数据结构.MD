Redis哪几种数据结构


string、hash、list、set、sorted set
这里的数据结构指的是key-value中value的数据结构，分别为string、hash、list、set、sorted set。每种数据结构都有相关的命令，比如set命令表示使用string来存储value，get命令的参数只能为对应value值存储为string的key，操作其他数据结构需要相应的命令，这些命令可以从redis官方站点查询。

string

使用string时，redis**大多数情况下**并不会理解或者解析其含义，无论使用json、xml还是纯文本在redis看来都是一样的，只是一个字符串，只能进行strlen、append等对字符串通用的操作，无法针对其内容进一步操作。其基本操作命令有set、get、strlen、getrange、append：

SET key value
GET key
STRLEN key
GETRANGE  key start end
APPEND key value

在大多数情况之外，就是string中存储的为纯数字的情况，redis可以将字符串当做数字进行进一步操作，这些操作包括decr、decrby、incr、incrby和incrbyfloat。

hash

使用hash时，在我看来，就是value本身就是一组key-value对，不过redis将这里的key称为field（但是hkeys命令为什么不叫hfields命令呢哈哈），也就是value是一组field-value对。其基本操作命令有hset、hget、hmset、hmget、hgetall、hkeys和hdel：

HSET key field value
HGET key field
HMSET key field value [field value ...]
HMGET key field [field ...]
HGETALL key
HKEYS key
HDEL key field [field ...]


list

使用list时，value就是一个string数组，操作这组string时，可以像对待栈一样使用pop和push操作，但是这个栈两端都能进行操作；也可以像对待数组一样使用一个index参数来操作。list的操作命令略杂，主要分为两类：L开头的和R开头的，L代表LEFT或者LIST，进行一些从列表左端进行的操作，或者一些与端无关的操作；R代表RIGHT，进行一些从列表右端进行的操作。

set

set用于存储一组不重复的值，也可以进行一些集合的操作，就像数学上的集合，它是无序的。基本操作有sadd和sismember：

SADD key member [member ...]
SISMEMBER key member

集合操作有：求交sinter、求并sunion和求差sdiff：

SINTER key [key ...]
SUNION key [key ...]
SDIFF key [key ...]

sorted set

sorted set类似set，但是sorted set里每个元素都有一个score，这个score可用于排序和排名。基本操作有zadd、zcount、zrank：

ZADD key score member [score member ...]
ZCOUNT key min max
ZRANK key member
