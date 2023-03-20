# AKY-DB
一个简易版java数据库
MYDB 是一个 Java 实现的简单的数据库，部分原理参照自 MySQL、PostgreSQL 和 SQLite。实现了以下功能：

数据的可靠性和数据恢复
两段锁协议（2PL）实现可串行化调度
MVCC
两种事务隔离级别（读提交和可重复读）
死锁处理
简单的表和字段管理
简陋的 SQL 解析（因为懒得写词法分析和自动机，就弄得比较简陋）
基于 socket 的 server 和 client

# 开发环境
Window 11 + IDEA 2021 + JDK 8

# 运行方式
首先执行以下命令编译源码：
mvn compile
接着执行以下命令以 /tmp/mydb 作为路径创建数据库：
mvn exec:java -Dexec.mainClass="top.guoziyang.mydb.backend.Launcher" -Dexec.args="-create E:/tmp/mydb"
随后通过以下命令以默认参数启动数据库服务：
mvn exec:java -Dexec.mainClass="top.guoziyang.mydb.backend.Launcher" -Dexec.args="-open E:/tmp/mydb"
这时数据库服务就已经启动在本机的 9999 端口。重新启动一个终端，执行以下命令启动客户端连接数据库：
mvn exec:java -Dexec.mainClass="top.guoziyang.mydb.client.Launcher"
会启动一个交互式命令行，就可以在这里输入类 SQL 语法，回车会发送语句到服务，并输出执行的结果。

# 测试样例
create table test_table id int32, value int32 (index id)
insert into test_table values 10 33
select from test_table where id = 10
begin
insert into test_table values 20 34
commit
select from test_table where id > 0
