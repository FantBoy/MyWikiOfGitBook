# db内指定字段名检索

在问题定位时，也运维中，通常需要查询某个字段来自于哪张表。

### 按字段名查

表查询哪些表有指定字段名（比如查字段名article_id）的SQL
```
SELECT * FROM information_schema.COLUMNS WHERE COLUMN_NAME='article_id';
```
或者
```
SELECT table_name, column_name FROM information_schema.columns WHERE column_name = 'article_id';
```
或者
```
SELECT column_name FROM information_schema.columns WHERE column_name LIKE '%搜索的字段%' AND table_schema = '你的数据库';
SELECT column_name FROM information_schema.columns WHERE column_name LIKE '%搜索的字段%' AND table_schema = '你的数据库' AND table_name = '你的表';
```
这个SQL能查出所有你当前打开的链接下的所有数据库中的所有含有“article_id”字段名的表。
