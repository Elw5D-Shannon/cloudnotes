
- 除了传统的数据库管理系统（DBMS）外，还有其他方式可以用来管理数据，比如简单的文件存储、数据仓库、NoSQL 数据库等。
- 在大多数数据库管理系统中，分号是 SQL 语句的标准终止符，用于分隔多条语句。
- SQL 关键字（如 `SELECT`、`FROM`、`WHERE`）本身不区分大小写。`
- SQL 是一种自由格式语言，对换行和缩进没有语法要求。将语句分多行书写（尤其是复杂查询）可以提高可读性。
- SQL（Structured Query Language，结构化查询语言）是一种**通用的、标准化的**数据库查询和管理语言，并非 MySQL 专用。绝大多数关系型数据库（如 **Oracle、SQL Server、PostgreSQL、SQLite、DB2** 等）都支持 SQL 标准

### 基础知识
E-R，实体-联系模型 P220
  
在数据库中，产生数据不一致性的根本原因是*数据冗余*

关系数据模型（用二维表来表示实体集及实体集之间联系的数据模型）
能表示实体间的1:1联系
能表示实体间的1:n联系
能表示实体间的m:n联系

在关系模型中，如果把关系简单看作一张表，则“元组”对应表里面的（行）

数据模型通常由（ 数据结构）、数据操作和完整性约束条件组成

数据完整性约束是指**对数据的有效性和一致性进行限制和检查的规则**。它确保数据在数据库中的**准确性和可靠性**。“性别的取值只能是'男'或'女'”是一种**数据完整性约束**，具体来说是一个**值域约束（Domain Constraint）**，它**限制了性别字段的取值范围**，确保性别字段只能接受特定的值（'男'或'女'），从而保证了数据的有效性和一致性。

- **主键（PRIMARY KEY）**  
    主关键字是用来唯一标识关系中每一条记录的属性。
    用来保证表中**实体完整性**（唯一且非空），用于唯一标识每一行。
- **外键（FOREIGN KEY）**  
    用来建立两个表之间的引用关系，从而实现**参照完整性**。  
    外键指向另一个表（或同一表）的主键或唯一键。

```python
#连接数据库的代码
conn = pymysql.connect(host='localhost',user='root',passwd='123123',charset='utf8')
#获取游标
cursor = conn.cursor()
#MySQL中可能同时存在多个数据库，为了对指定的数据库进行操作，可使用：
dbName = 你的数据库名称
conn.select_db(dbName)
#当然，如果在创建数据库连接对象时指定了连接的数据库时，就不需要再指定数据库对象：
dbName = 你的数据库名称
conn = pymysql.connect(host='localhost',user='root',passwd='123456',charset='utf8',db=dbName)
# 创建enroll数据库
    cursor.execute('create database enroll')
    conn.select_db('enroll')
    # 创建nudt数据表
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS nudt (
            year INT,
            province VARCHAR(100),
            firstBatch INT,
            gcMax INT,
            gcMin INT,
            gcMean INT,
            xlMax INT,
            xlMin INT,
            xlMean INT
        )
    """)
```

MySQL支持的字段属性包括：
- 日期和时间数据类型。
data：3字节，日期，格式：2014-09-18
time：3字节，时间，格式：08:42:30
datetime：8字节，日期时间，格式：2014-09-18 08:42:30
timestamp：4字节，自动存储记录修改的时间
year：1字节，年份
- 数值数据类型。
tinyint：1字节，范围（-128~127）
smallint：2字节，范围（-32768~32767）
mediumint：3字节，范围（-8388608~8388607）
int： 4字节，范围（-2147483648~2147483647）
bigint：8字节，范围（+-9.22*10的18次方）
- 浮点型
float(m, d)：4字节，单精度浮点型，m总个数，d小数位
double(m, d)：8字节，双精度浮点型，m总个数，d小数位
decimal(m, d)：decimal是存储为字符串的浮点数
- 字符串数据类型。
char(n)：固定长度，最多255个字符
varchar(n)：可变长度，最多65535个字符
tinytext：可变长度，最多255个字符
text：可变长度，最多65535个字符
mediumtext：可变长度，最多2的24次方-1个字符
longtext：可变长度，最多2的32次方-1个字符

```python
import pymysql
def insert(year,province,firstBatch,gcMax,gcMin,gcMean,xlMax,xlMin,xlMean):
    conn = pymysql.connect(host='localhost', user='root', passwd='123123', charset='utf8')
    cursor = conn.cursor()
    conn.select_db('enroll')
    # -----------Begin----------
    # 请在下面输入插入数据的语句，完成相应功能
    sql = 'insert into nudt(year,province,firstBatch,gcMax,gcMin,gcMean,xlMax,xlMin,xlMean)    values (%s,"%s",%s,%s,%s,%s,%s,%s,%s)' % (year,province,firstBatch,gcMax,gcMin,gcMean,xlMax,xlMin,xlMean)
    cursor.execute(sql)
    # ------------End-----------
    # 提交数据到数据库
    conn.commit()
    # 关闭数据库连接
    cursor.close()
    conn.close()
def select():
    conn = pymysql.connect(host='localhost', user='root', passwd='123123', charset='utf8')
    cursor = conn.cursor()
    conn.select_db('enroll')
    # -----------Begin----------
    # 请在下面输入查询数据的语句，完成相应功能
    sql = "SELECT year, province, firstBatch, gcMax, gcMin, gcMean, xlMax, xlMin, xlMean FROM nudt WHERE year = 2014"
    cursor.execute(sql)
    # 请在下面输入获取数据的语句，完成相应功能
    records = cursor.fetchall()
    # ------------End-----------
    for record in records:
        print(record)
    # 关闭数据库连接
    cursor.close()
    conn.close()
```


在存储信息时可能出现不能将所有信息存入同一张表中的情况，如汽车购入记录和汽车出售记录，为了查询汽车剩余数量，就需要同时获取汽车购入记录及对应的出售记录。汽车购入记录中有一个字段为brand，汽车销售记录中同样有一个brand字段，则可通过该字段将两表关联起来，获取汽车剩余数量：

select A.brand, A.inNum - B.outNum from ininfo A, outinfo B where A.brand = B.brand
这种查询方式即为关联查询，brand为两表的共有字段。



多表直接汇总
在多表查询时，可直接将每张表中的数据全部取出汇总：
select * from ininfo, outinfo
这种查询会使得表中的一条记录出现多次，如ininfo表中有两条记录a、b，outinfo表中有两条记录c、d，则查询结果为：
a c
a d
b c
b d
另外，这种查询方式会将ininfo，outinfo两张表中的全部字段取出汇总，上述查询语句得到的结果为：`indata`，`inNum`，`brand`，`outdata`，`outNum`，`brand`
当两张表没有共有字段时这种操作方式没问题，但是如果表与表之间有共有字段，如ininfo，outinfo表中的brand字段，这种查询方式会使结果中出现重复字段。

等值连接
- 这种查询方式会将两张表中共有字段相同的记录连接前来输出，这种查询方式只适合于表与表之间有共有字段，即表与表之间存在关联。查询方式为：
  select * from ininfo A, outinfo B where A.brand = B.brand
- 如ininfo中a的brand为Chevrolet，outinfo中b的brand为Chevrolet，则等值连接的结果为：a.indata，a.inNum，a.brand，b.indata，b.outNum，b.brand
  这种查询方式同样存在共有字段多次输出的问题。

自然连接
- 自然连接查询保证多表之间的共有字段只输出一次，如：
  select A.brand, A.indata, A.inNum, B.outdata, B.outNum from ininfo A, outinfo B
- 查询结果如下
  a.brand， a.indata， a.inNum， b.outdata， b.outNum

## 代码如下：
创建provincialEntryScore、nudtTechScore、nudtMilScore表
往三张表中插入数据
以直接汇总、等值连接及自然连接三种方式汇总三张表中的数据

provincialEntryScore表中包含的字段及对应的属性为：
year：int
province：varchar(100)
entryScore：int

nudtTechScore表中包含的字段及对应的属性为：
year：int
province：varchar(100)
techMax：int
techMin：int
techMean：int

nudtMilScore表中包含的字段及对应的属性为：
year：int
province：varchar(100)
milMax：int
milMin：int
milMean：int

```python
import pymysql
def create(cursor):
    # 创建provincialEntryScore表
    sql =  'create table provincialEntryScore(year int, province varchar(100), entryScore int)'
    cursor.execute(sql)
    # 创建nudtTechScore表
    sql = 'create table nudtTechScore(year int, province varchar(100), techMax int, techMin int, techMean int)'
    cursor.execute(sql)
    # 创建nudtMilScore表
    sql = 'create table nudtMilScore(year int, province varchar(100), milMax int, milMin int, milMean int)'
    cursor.execute(sql)

def insert(cursor,year,province,entryScore,techMax,techMin,techMean,milMax,milMin,milMean):
    # 请在下面输入将数据插入provincialEntryScore表中的语句
    sql = 'insert into provincialEntryScore(year, province, entryScore) values (%s, "%s", %s)' % (year, province, entryScore)
    cursor.execute(sql)
    # 请在下面输入将数据插入nudtTechScore表中的语句
    sql = 'insert into nudtTechScore(year, province, techMax, techMin, techMean) values (%s, "%s", %s, %s, %s)' % (year, province, techMax, techMin, techMean)
    cursor.execute(sql)
    # 请在下面输入将数据插入nudtMilScore表中的语句
    sql = 'insert into nudtMilScore(year, province, milMax, milMin, milMean) values (%s, "%s", %s, %s, %s)' % (year, province, milMax, milMin, milMean)
    cursor.execute(sql)

def selectAll(cursor):
    # 请在下面输入多表直接汇总的语句
    sql =  'select * from provincialEntryScore, nudtTechScore, nudtMilScore'
    cursor.execute(sql)
    records = cursor.fetchall()
    return records

def selectEqual(cursor):
    # 请在下面输入等值连接的语句
    sql = 'select * from provincialEntryScore A,nudtTechScore B,nudtMilScore C where A.year = B.year and A.year = C.year and A.province = B.province and A.province = C.province'
    cursor.execute(sql)
    records = cursor.fetchall()
    return records

def selectNatural(cursor):
    # 请在下面输入自然连接的语句
    sql ='select A.year, A.province, A.entryScore, B.techMax, B.techMin, B.techMean, C.milMax, C.milMin, C.milMean from provincialEntryScore A, nudtTechScore B, nudtMilScore C where A.year = B.year and A.year = C.year and A.province = B.province and A.province = C.province'
    cursor.execute(sql)
    records = cursor.fetchall()
    return records
    # ------------End-----------
```

