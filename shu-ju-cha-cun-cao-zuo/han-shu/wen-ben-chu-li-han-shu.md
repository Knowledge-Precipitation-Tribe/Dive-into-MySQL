# 文本处理函数

之前我们已经看过一个文本处理函数的例子，其中使用RTrim\(\) 函数来去除列值右边的空格。下面是另一个例子，这次使用Upper\(\)函数：

```text
SELECT vend_name, Upper(vend_name) AS vend_name_upcase
FROM vendors
ORDER BY vend_name;
```

![](../../.gitbook/assets/image%20%2835%29.png)

正如所见，Upper\(\)将文本转换为大写，因此本例子中每个供 应商都列出两次，第一次为vendors表中存储的值，第二次作 为列vend\_name\_upcase转换为大写。

## 常用的文本处理函数

![](../../.gitbook/assets/image%20%2833%29.png)

![](../../.gitbook/assets/image%20%28104%29.png)

SOUNDEX是一个将任何文 本串转换为描述其语音表示的字母数字模式的算法。SOUNDEX考虑了类似 的发音字符和音节， 使得能对串进行发音比较而不是字母比较。 虽然 SOUNDEX 不是SQL概念， 但MySQL（就像多数DBMS一样）都提供对 SOUNDEX的支持。

下面给出一个使用Soundex\(\)函数的例子。customers表中有一个顾客Coyote Inc.，其联系名为Y.Lee。但如果这是输入错误，此联系名实际应该是Y.Lie，怎么办？显然，按正确的联系名搜索不会返回数据，如 下所示：

```text
SELECT cust_name, cust_contact
FROM customers
WHERE cust_contact = 'Y.Lie';
```

![](../../.gitbook/assets/image%20%2814%29.png)

现在试一下使用Soundex\(\)函数进行搜索，它匹配所有发音类似于 Y.Lie的联系名：

```text
SELECT cust_name, cust_contact
FROM customers
WHERE Soundex(cust_contact) = Soundex('Y.Lie');
```

![](../../.gitbook/assets/image%20%2858%29.png)

