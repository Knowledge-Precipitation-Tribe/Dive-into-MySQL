# 权限

MySQL服务器通过权限表来控制用户对数据库的访问，权限表存放在mysql数据库里，由mysql\_install\_db脚本初始化。这些权限表分别user，db，table\_priv，columns\_priv和host。下面分别介绍一下这些表的结构和内容：

* user权限表：记录允许连接到服务器的用户帐号信息，里面的权限是全局级的。
* db权限表：记录各个帐号在各个数据库上的操作权限。
* table\_priv权限表：记录数据表级的操作权限。
* columns\_priv权限表：记录数据列级的操作权限。
* host权限表：配合db权限表对给定主机上数据库级操作权限作更细致的控制。这个权限表不受GRANT和REVOKE语句的影响。

