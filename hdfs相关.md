- 在迁移datanode过程中，发现jps进程存在datanode但实际是dead状态。
  - 由于同一个版本的namenode和datanode有clusterid来识别彼此，需要先删除对应在hdfs-site.xml底下配置的name.dir和data.dir目录的current
