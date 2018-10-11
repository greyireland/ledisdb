源码目录结构

store底层存储接口
DB 统一实现，统一使用下面具体实现
Driver接口，goleveldb，leveldb,rocksdb各个具体实现（键按照字符串排序）
rpl 复制相关


ledis核心实现
KV实现用基础接口
Hash实现：
* 保存hash长度
* 保存结构hash_field1:value

List实现：
* 保存开始和结尾序列号
* 保存格式 list_01:value1，前面插入list_00:value0 后面插入list_02:value2，取长度，直接用结尾减开始，取所有通过range取

Set实现：
* 保存set的长度
* 保存格式 set_val1，重复可以通过key排重，取所有通过range取（开始set_xx，结束set_xx:1 ???怎么确定一段，前缀匹配？），diff通过取所有和后面的所有值比较就行

Zset实现：
* 保存zset长度
* 保存分值，zset_member1:score1 ，保存zset_score1_member1键 用于排序获取


