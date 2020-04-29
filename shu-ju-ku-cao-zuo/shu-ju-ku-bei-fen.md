# 数据库备份

MySQL 数据库管理系统通常会采用有效的措施来维护数据库的可靠性和完整性。但是在数据库的实际使用过程当中，仍存在着一些不可预估的因素，会造成数据库运行事务的异常中断，从而影响数据的正确性，甚至会破坏数据库，导致数据库中的数据部分或全部丢失。

 数据库系统提供了备份和恢复策略来保证数据库中数据的可靠性和完整性。

##  数据库备份

数据库备份是指通过导出数据或者复制表文件的方式来制作数据库的副本。当数据库出现故障或遭到破坏时，将备份的数据库加载到系统，从而使数据库从错误状态恢复到备份时的正确状态。

 可以使用SELECT INTO OUTFILE语句把表数据导出到一个文本文件中进行备份。

{% hint style="info" %}
注意：这种方法只能导出或导入数据的内容，而不包括表的结构。若表的结构文件损坏，则必须先设法恢复原来表的结构。
{% endhint %}

【实例】将数据库 test\_db 的表 tb\_students\_info 的全部数据备份到 C 盘的数据备份目录下文件名为 file.txt 的文件中，要求每个字段用逗号分开，并且字符用双引号标注，每行以问号结束。

 输入的SQL语句和执行结果如下所示。

```text
mysql> SELECT * FROM test_db.tb_students_info
    -> INTO OUTFILE 'C:/ProgramData/MySQL/MySQL Server 5.7/Uploads/file.txt'
    -> FIELDS TERMINATED BY '"'
    -> LINES TERMINATED BY '?';
Query OK, 10 rows affected (0.06 sec)
```

 用记事本查看 MySQL 备份文件夹下的 file.txt 文件，内容如下图所示。

![](../.gitbook/assets/image%20%28115%29.png)

