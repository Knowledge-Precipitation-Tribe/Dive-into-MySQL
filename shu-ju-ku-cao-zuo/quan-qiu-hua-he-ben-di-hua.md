# 全球化和本地化

数据库表被用来存储和检索数据。不同的语言和字符集需要以不同的方式存储和检索。因此，MySQL需要适应不同的字符集（不同的字母和字符），适应不同的排序和检索数据的方法。

在讨论多种语言和字符集时，将会遇到以下重要术语：

* 字符集为字母和符号的集合；
* 编码为某个字符集成员的内部表示；
* 校对为规定字符如何比较的指令。

{% hint style="info" %}
排序英文正文很容易，对吗？或许不。考虑词APE、apex和Apple。它们处于正确的排序顺序吗？这有赖于你是否想区分大小写。使用区分大小写的校对顺序，这些词有一种排序方式，使用不区分大小写的校对顺序有另外一种排序方式。这不仅影响排序（如用ORDER BY排序数据）， 还影响搜索（例如，寻找apple的WHERE子句是否能找到APPLE）。在使用诸如法文à或德文ö这样的字符时，情况更复杂，在使用不基于拉丁文的字符集（日文、希伯来文、俄文等）时，情况更为复杂
{% endhint %}

## 使用字符集和校对顺序

MySQL支持众多的字符集。为查看所支持的字符集完整列表，使用以下语句：

```text
SHOW CHARACTER SET;
```

这条语句显示所有可用的字符集以及每个字符集的描述和默认校对。

为了查看所支持校对的完整列表，使用以下语句：

```text
SHOW COLLATION;
```

此语句显示所有可用的校对，以及它们适用的字符集。可以看到有的字符集具有不止一种校对。例如，latin1对不同的欧洲语言有几种校对，而且许多校对出现两次，一次区分大小写（由\_cs表示）， 一次不区分大小写（由\_ci表示）。

通常系统管理在安装时定义一个默认的字符集和校对。此外，也可以在创建数据库时，指定默认的字符集和校对。为了确定所用的字符集和校对，可以使用以下语句：

```text
SHOW VARIABLES LIKE 'character%;
SHOW VARIABLES LIKE 'collation%;
```

实际上，字符集很少是服务器范围（甚至数据库范围）的设置。不同的表，甚至不同的列都可能需要不同的字符集，而且两者都可以在创建表时指定。

```text
CREATE TABLE mytable(
    columns1 INT,
    columns2 VARCHAR(10)
) DEFAULT CHARACTER SET hebrew COLLATE hebrew_general_ci;
```

这个例子中指定了CHARACTER SET和COLLATE两者。一般，MySQL如下确定使用什么样的字符集和校对。

* 如果指定CHARACTER SET和COLLATE两者，则使用这些值。 
* 如果只指定CHARACTER SET，则使用此字符集及其默认的校对（如SHOW CHARACTER SET的结果中所示）。 
* 如果既不指定CHARACTER SET，也不指定COLLATE，则使用数据库默认。

除了能指定字符集和校对的表范围外，MySQL还允许对每个列设置它们，如下所示：

```text
CREATE TABLE mytable(
    columns1 INT,
    columns2 VARCHAR(10),
    columns3 VARCGAR(10) CHARACTER SET latin1 COLLATE latin1_general_ci
) DEFAULT CHARACTER SET hebrew COLLATE hebrew_general_ci;
```

如前所述，校对在对用ORDER BY子句检索出来的数据排序时起重要的作用。如果你需要用与创建表时不同的校对顺序排序特定的SELECT语句，可以在SELECT语句自身中进行：

```text
SELECT * FROM customers ORDER BY lasname, firstname COLLATE latin1_general_cs;
```

