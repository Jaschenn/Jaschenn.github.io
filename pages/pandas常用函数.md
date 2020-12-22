---
title: pandas常用函数
---

## (文章待完善)
注意1：pandas本身包含很多函数pandas.method(obj)，通常简写为pd.method(df)，df表示待处理“对象”（最常见的是Series和DataFrame对象）；而pandas产生的“对象”也包含自己的方法，通常以df.method()形式调用。部分函数和方法实现的是完全相同的功能，因此两种方法都可使用，实际上前者是“函数式编程”，后者是“面向对象编程”。例如判断一个DataFrame对象df是否含有null值，既可以用pd.isnull(df)也可以用df.isnull()。
注意2：pandas为了保护源数据，对DataFrame对象的操作一般都不会更改源数据，除非在函数中加上“inplace=True”，该语句在下面的大部分方法和函数中都有。
注意3：df.method()表示对整个DataFrame进行操作；而df[['col1','col2',…]].method()：表示对指定列进行相应的操作。通常前者返回针对整个DataFrame的结果，而后者返回指针对相应列的结果。下面都以df.method()形式描述各种方法，对应方法换成df[['col1','col2',…]].method()就是对指定列的操作。但需要注意，某些方法并不适用于Dataframe操作，而某些反复也只针对列操作，根据实际情况而定。
## 导入包

import pandas as pd

1. 创建对象

df = pd.DataFrame(data=, columns=, index=)
s = pd.Series(data=, index=)

2. 数据导入

pd.read_csv(filename)：从CSV文件导入数据
pd.read_table(filename)：从限定分隔符的文本文件导入数据
pd.read_excel(filename)：从Excel文件导入数据
pd.read_sql(query, connection_object)：从SQL表/库导入数据
pd.read_json(json_string)：从JSON格式的字符串导入数据
pd.read_html(url)：解析URL、字符串或者HTML文件
pd.read_clipboard()：从粘贴板获取内容
pd.DataFrame(dict)：从字典对象导入数据

3. 数据导出

df.to_csv(filename)：导出数据到CSV文件
df.to_excel(filename)：导出数据到Excel文件
df.to_sql(table_name, connection_object)：导出数据到SQL表
df.to_json(filename)：以Json格式导出数据到文本文件

4. 数据查看

df.head(n)：查看DataFrame对象的前n行
df.tail(n)：查看DataFrame对象的最后n行
df.shape()：查看行数和列数
df.info()：查看索引、数据类型、每列非数、内存信息
df.dtypes：返回每一列的数据类型
df.index：返回每一行的“行标签”列表
df.columns：返回每一列的“列标签”列表
df.values：返回“值”，是numpy.ndarray类型
df.count()：返回每一行或列包含的非空数据个数，不包括None, NaN, NaT等
df['col1'].unique()：查看某一列内有哪些不同的值
df.describe()：查看数据值列的汇总统计
df.max()：返回每一列的最大值
df.min()：返回每一列的最小值
df.median()：返回每一列的中位数
df.mean()：返回所有列的均值
df.corr()：返回列与列之间的相关系数
df.std()：返回每一列的标准差

s.value_counts(dropna=False)：查看Series对象的唯一值、重复值和计数
s.values: 抽取Series对象的数据
s.index: 抽取Series对象的索引
df.apply(pd.Series.value_counts)：查看DataFrame对象中每一列的唯一值和计数
说明：apply的用处很多，比如可以通过跟lambda函数联合，完成很多功能：将包含某个部分的元素挑出来等等。

5. 数据选取

一般选取
df[ ['列1' ,'列2'…]]：取单列或多列，不能用连续方式取，也不能用于取行。
df[ i:j ]：起始行下标(i)和终止行下标(j)取单行或者连续多行，不能用于列的选取。
df.列名：只用于取单列，不能用于行。
df.loc[行名,列名]：用对象的.loc[]方法实现各种取数据方式。
df.iloc[行下标,列下标]：用对象的.iloc[]方法实现各种取数据方式。**
更详细参见：https://blog.csdn.net/xtfge0915/article/details/52938740
df.values：获取所有数据
df.values[i]：获取第i行数据
df.values[i][j]：获取第i行j列数据
条件选取
df[df.a>0]：选择a列中元素>0的所有行
df[(df.a>0) & (df.b<0)]：选择a列中元素>0同时b列中元素<0的所有行
df[列list] [df.a>0]：在a列中元素>0的所有行中，抽取‘列list’指定列的数据
df[列list] [(df.a>0) & (df.b<0)]：关系同上
详见：https://www.jianshu.com/p/9e904db7a2a7

（待增加）
自带函数？？？？？？？？？？？？
df.query()：

排序

df.sort_values()：按照某列或某几列（某行或某几行）多样化排序。
df.sort_index()：默认按照index或columns排序（推荐），也可当.sort_values()使用（不推荐）。
详见：https://www.jianshu.com/p/f0ed06cd5003

数据清洗

列索引（columns）处理

df.columns = ['a','b','c']：直接重命名列标签
df.rename()：批量或者单个更改列标签

行索引（index）处理

df.set_index()：将某列作为行索引，可处理多重索引
df.reset_index()：更改行索引，可处理多重索引

判断某值是否存在

df.isin([……])：判断[……]内的元素是否在df中，返回一个与df同维的bool型DataFrame

null和na处理

pd.isnull(df)或df.isnull()：判断哪些是null，返回一个与df同维的bool型DataFrame
pd.isna(df)或df.isna()：判断哪些是null，返回一个与df同维的bool型DataFrame
pd.notnull(df)或df.notnull()：判断哪些不是null，返回一个与df同维的bool型DataFrame
pd.notna(df)或df.notna()：判断哪些不是na，返回一个与df同维的bool型DataFrame
df.fillna(value)：用value填充所有的空值

df['列名'].isna()、df['列名'].isnull()、df['列名'].notna()、df['列名'].notnull()：判断某列是否有空值，返回列同维布尔值。
df['列名'].fillna(value)：用value填充某列所有空值

df.dropna(axis=, how=)：删除所有包含空值的行（axis=0）或列（axis=1），how='any'只要出现一个空值就删，how='all'只有当所以值空才删。
df['列名'].dropna()：删除某列的空值

重复数据判断处理

df.duplicated(subset=['col1','col2',……],keep=) 等同于df[['col1','col2',……]].duplicated(keep=)：返回一个与“行数”同维的bool型Series对象，标True的行表示，这些行里面某几列（由['列名'list]指定）或所有列都相同。keep='first'/'last'/False。'first'：第一次出现的行不标注True；'表示'：最后一次出现的行不标注True；False(无引号)：所有满足要求的行都表True。
df.duplicated()：标出完全相同的行，且第一次出现那行不标注。
df.duplicated(subset=['age','id'] ,keep=False)：比较‘age’和‘id’这两列完全相同的行，并全部标注为True，比如第2行：age=5，id=123；第7行：age=5，id=123，显然第2行和第7行在age和id这两个维度上是完全相同的，那么这两行都将被标注为True。该结果同df[['city','price']].duplicated(keep=False)。

df.drop_duplicates(subset=['col1','col2',……],keep=)：参数作用完全同上，该函数是删除选定列内相同行所在的整行，返回的是一个删除了指定行后的DataFrame对象。df[['col1','col2',……]].drop_duplicates(keep=)返回的是指定列中删除了相同行的剩余结果，只有指定列。

数据替换

df.replace()：单值、多值等多种替换方式。https://blog.csdn.net/kancy110/article/details/72719340/

大小写转换

df['列名'].str.lower()：将某列中所有的大写字母改小写（只适用于单列）

数据类型转换

df.astype()：数据类型转换

数据处理(待完善)

df.groupby(col)：返回一个按列col进行分组的Groupby对象
df.groupby(col1).agg(np.mean)：返回按列col1分组的所有列的均值
df.pivot_table(index=col1, values=[col2,col3], aggfunc=max)：创建一个按列col1进行分组，并计算col2和col3的最大值的数据透视表
df.sample()：重采样
apply()
agg()
map()
mapapply()

数据合并

pd.merge()：根据一个或多个键将不同DataFrame中的行连接起来
df1.append(df2)：将df2中的行添加到df1的尾部
df.concat([df1, df2],axis=1)：将df2中的列添加到df1的尾部
df1.join(df2,on=col1,how='inner')：对df1的列和df2的列执行SQL形式的join

Pandas支持的数据类型

int 整型
float 浮点型
bool 布尔类型
object 字符串类型
category 种类
datetime 时间类型

参考文章：

参考博客：https://blog.csdn.net/brucewong0516/article/details/81782312
pandas官网：http://pandas.pydata.org/
pandas官方文档：http://pandas.pydata.org/pandas-docs/stable/index.html
pandas部分用法：https://link.zhihu.com/?target=https%3A//www.dataquest.io/blog/pandas-cheat-sheet/
