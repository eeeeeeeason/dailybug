## Mkdirs failed to create /user/hadoop/hbase-staging
- new Path("hdfs://")不能识别导致
- 解决：配置Configuration , conf.set("fs.defaultFS","hdfs://node1:8020");
