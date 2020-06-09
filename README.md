用法：一个数据库sql回滚解析工具

 /usr/bin/bingo2sql 
参数是：[/usr/bin/bingo2sql] ,个数: 1Usage of bingo2sql:
-h, --host string 数据库地址
-P, --port int 端口号 (default 3306)
-u, --user string 用户名
-p, --password string 密码
--start-file string 起始binlog文件
--stop-file string 结束binlog文件
--start-pos int 起始位置
--stop-pos int 结束位置
--start-time string 开始时间
--stop-time string 结束时间
-d, --databases string 数据库列表,多个时以逗号分隔
-t, --tables string 表名或表结构文件.远程解析时指定表名(可多个,以逗号分隔),本地解析时指定表结构文件
-C, --connection-id uint 指定线程ID
-B, --flashback 逆向语句 (default false)
--ddl 解析DDL语句(仅正向SQL) (default false)
--sql-type string 解析的语句类型 (default "insert,delete,update")
--max int 解析的最大行数,设置为0则不限制 (default 100000)
-o, --output string 输出到指定文件
-g, --gtid string GTID范围.格式为uuid:编号[-编号],多个时以逗号分隔
-K, --no-primary-key 对INSERT语句去除主键. 可选. (default false)
-M, --minimal-update 最小化update语句. 可选. (default true)
-I, --minimal-insert 使用包含多个VALUES列表的多行语法编写INSERT语句. (default true)
-N, --stop-never 持续解析binlog (default false)
--show-gtid 显示gtid (default true)
--show-time 显示执行时间,同一时间仅显示首次 (default true)
--show-all-time 显示每条SQL的执行时间 (default false)
--show-thread 显示线程号,便于区别同一进程操作 (default false)


具体例子
基于位点：

./bin/bingo2sql -h ip -uwork -p'xx' -P 3306 -d db_admin -tzx_scores --start-file" mysql-bin.000002"--start-pos 7047 --stop-pos 7667 

/bin/bingo2sql -h ip -uwork -p'xx' -P 3306 -d db_admin -tzx_scores --start-file" mysql-bin.000002"--start-pos 7047 --stop-pos 7667 -B

基于gtid形式：
./bingo2sql -h 10.104.113.41 -uwork -p'xx' -P 3306 -d db_admin -tzx_scores --start-file "mysql-bin.000002" -g 1bb1b861-f776-11e6-3306-010104113041:32
./bingo2sql -h 10.104.113.41 -uwork -p'xx' -P 3306 -d db_admin -tzx_scores --start-file "mysql-bin.000002" -g 1bb1b861-f776-11e6-3306-010104113041:32-33

回滚sql生成：
./bingo2sql -h 10.104.113.41 -uwork -p'xx' -P 3306 -d db_admin -tzx_scores --start-file "mysql-bin.000002" -g 1bb1b861-f776-11e6-3306-010104113041:32-33 -B