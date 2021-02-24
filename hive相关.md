- 连接不成功
  
  ```
  Error: Could not open client transport with JDBC Uri: jdbc:hive2://node3:10000: java.net.ConnectException: Connection refused (Connection refused) (state=08S01,code=0)
  ```
  - 1.集群没有全部健康的情况导致，我的问题是由两个namenode同时standby无法切换一个新的active
    - 解决方案，检查各个node是否正常，输出日志
  ```
  User: root is not allowed to impersonate root
  ```
  - core-site.xml配置以下，并发送到其他机子
  ```
  <property> 
  <name>hadoop.proxyuser.root.hosts</name>
  <value>*</value> 
  </property> 
  <property> 
  <name>hadoop.proxyuser.root.groups</name> 
  <value>*</value> 
  </property>
  ```
- 配置项修改
  - 内部表改为外部表
  ```
  ('EXTERNAL'='TRUE');必须大写
  ```
- 分区表处理
  ```
  1.一张分区表插入到另一张分区表的时候不要带上分区字段
  2.有分区字段的表在插入的时候要加入partition字段
  ```
- hivesql
  - 当存在多个分区时distribute by 与order by 不能同用，order by需要更换为sort by；
  - 子表查询需要

```
javax.jdo.JDOFatalInternalException: Error creating transactional connection factory
```
- mysql connector没有或者hive-site.xml配置有缺陷
```
OutOfMemoryError: Java heap space
Mapreduce时直接Error
```
- 1.将系统设置的set mapred.max.split.size = 300000000;我们原先的最大分片设置成200000000.降低切片大小，这样的坏处是会产生更多的map去执行。
- 2.将上面集群的heap.size设置的更大些，比如2048（2g）

```
Error while processing statement: FAILED: Execution Error, return code 137 from org.apache.hadoop.hive.ql.exec.mr.MapredLocalTask
```
- 错误的原因 :  在执行 多表join的操作, HIVE会优化尝试 mapjoin, 将小表的数据放置在内存中, 但是内存不足无法放置, 导致运行失败
- 解决方案: 
  - 关闭掉mapjoin
  - set hive.auto.convert.join= false;
```
Could not connect to hadoop02:10000 (code THRIFTTRANSPORT): TTransportException('Could not connect to hadoop02:10000',)
```
- jvm堆栈不足在cm中的hive配置项搜索Java 堆栈调整到2GB内存
