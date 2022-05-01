# MySQL原理学习

- MySQL体系结构
- InnoDB存储引擎
- InnoDB的存储结构
```sql
create table t1( 
    col1 int not null auto_increment, 
    col2 varchar(7000), primary key(col1)
) engine=InnoDB;
```

查看初始化的信息：<br/>
t1.frm: 表定义<br/>
t1.ibd: innodb数据，初始大小是96K<br/>

通过py_innodb_page_info.py工具查看page信息：
```py
python py/py_innodb_page_info.py -v /data/mysql56/mysql_study/t1.ibd 
page offset 00000000, page type <File Space Header>
page offset 00000001, page type <Insert Buffer Bitmap>
page offset 00000002, page type <File Segment inode>
page offset 00000003, page type <B-tree Node>, page level <0000>
page offset 00000000, page type <Freshly Allocated Page>
page offset 00000000, page type <Freshly Allocated Page>
Total number of page: 6:
Freshly Allocated Page: 2
Insert Buffer Bitmap: 1
File Space Header: 1
B-tree Node: 1
File Segment inode: 1
```

行信息：
```shell
show table status like 't1'\G;
********[ 1. row ]*******
Name            | t1
Engine          | InnoDB
Version         | 10
Row_format      | Compact
Rows            | 31
Avg_row_length  | 51266
Data_length     | 1589248
Max_data_length | 0
Index_length    | 0
Data_free       | 0
Auto_increment  | 65
Create_time     | 2022-04-30 14:54:23
Update_time     | <null>
Check_time      | <null>
Collation       | latin1_swedish_ci
Checksum        | <null>
Create_options  | 
Comment         | 

```
可以看到Row_format为Compact，这是行的压缩格式。





- 索引与算法
- 锁与事务
- 性能优化

## 参考资料
- MySQL技术内幕 InnoDB存储引擎.pdf
- [Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/)
