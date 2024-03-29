---
title: 暂时正在写的
date: 2019/2/10
categories: bigData
tags:
- 暂时
---

这是个暂时的文章，写完之后我就把这个移植到该移植到的地方，所以你在这看到啥也不奇怪  
## temp
## Pandas
**`import pandas as pd`**
numpy pandas和Scipy+matplotlib无缝贴合，而且和后面的机器学习库也是配合精妙。  
pandas主要使用Series，DataFrame,Panel三种数据结构，分别适用于一维，二维，高维的情况。基于numpy数组，速度有保障。
### 属性和类型
- pandas支持的类型:
    - float 默认
    - int 默认
    - bool
    - datetime64 
    - datetime64 
    - timedelta 
    - category 
    - object 包括字符串  

默认的数据类型是int64,float64  
如果一列中含有多个类型,则该列的类型会是object,同样字符串类型的列也会被当成object类型.
不同的数据类型也会被当成object, 比如int32, float32
### Series
- 由`pandas.Series( data, index=None, dtype, name ,copy)`创建。
    - data是`一维`的类数组对象，数组字符串
    - index默认会用自然数来标记，你也可以自己传入一个和data长度相同的数组作为下标
    - dtype仍然是用来规定数据类型的
    - copy默认为False，是否复制数组  

用一个`常数`和`字符串`创建的时候所有的值都是该常数。  
字典默认会把键作为index值放到data    
:::warning
字典无序但是索引有序，自己再指定一次index=[自己想要的顺序的k]就可以了
:::
- index和values属性可以获得当前的键和值的集合,直接用下标也可以取出来。
- Series.name属性也就是上面的name参数会添加一些说明
- Series.index.name=""会对列上面有一个属性说明。  

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```
l=[1,2,3,4,5,6,7,8]
x=pd.Series(l,index=["a","b","c","d","e","h","i","j"],name="xxx")
x.index.name="sdfyu"
``` 

```json
sdfyu
a    1
b    2
c    3
d    4
e    5
h    6
i    7
j    8
Name: xxx, dtype: int64
```

</details>

### DataFrame
使用`pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=False)`实例化创建。
- data 嵌套列表，二维数组，字典，DF
- colunms 索引对象or类数组对象，可以创建后动态修改df.columns=["xx","yy"]，设置列的名称，使用df.index.name="xx"设置列标题
- index 性质同colunms，设置行的名称，df.columns.name="xx"
- dtype 控制类型

<br/>

可以使用字典创建，字典的K会作为行标题，V(是数组的情况下)作为每一行的数据  
可以使用自定义对象类型的数组创建。

```py
pd.DataFrame([("a",100,"1"),("b",1798,"1"),("e",122,"1"),("ee",312435465,"1")],
             index=["b","a","e","ee"])# 元组数组创建
pd.DataFrame(np.arange(0,16).reshape((4,4)))# 二维数组创建
pd.DataFrame({'a':[1,2,3,4,5],
              'b':[6,7,8,9,10],
              'c':[11,12,34,54,56]},
             index=["A","B","C","D","E"])# 字典创建
```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json
元组数组创建
 	0 	1 	      2
b 	a 	100 	  1
a 	b 	1798 	  1
e 	e 	122 	  1
ee 	ee 	312435465 1

二维数组创建


	0 	1 	2 	3
0 	0 	1 	2 	3
1 	4 	5 	6 	7
2 	8 	9 	10 	11
3 	12 	13 	14 	15


字典创建
 	a 	b 	c
A 	1 	6 	11
B 	2 	7 	12
C 	3 	8 	34
D 	4 	9 	54
E 	5 	10 	56
```

</details>

**基本属性**:
- T 转置，参考numpy的转置
- at 切片的(×)
- axes 返回行和列的label，[0]是行[1]是列
- blocks 各种数据类型分块输出
- dtypes 返回各列类型
- ftypes 返回各列类型，以及数据稀疏or密集
- empty 是不是空
- iat 切片的后面讲
- iloc 切片的，后面讲
- is_copy 是不是复制？警告:已经快不用了!(×)
- ix 切片的，后面讲 警告:已经快不用了!(×)
- loc 切片的，后面讲(×)
- ndim 数据维度，DF一定是2
- shape 数据形状
- size 数据总量，shape的乘积
- style 看不懂了咋还有样式?(×)
- values 嵌套的二维数组全是值
- head() 返回前n行。
- tail() 返回最后n行。



<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>


```py
print(verifyData)
print(verifyData.T) 
print(verifyData.axes) 
print(verifyData.blocks) 
print(verifyData.dtypes) 
print(verifyData.ftypes) 
print(verifyData.empty) 
print(verifyData.is_copy) 
print(verifyData.ndim) 
print(verifyData.shape)
print(verifyData.size) 
print(verifyData.style) 
print(verifyData.values) 
print(verifyData.head(5)) 
print(verifyData.tail(2)) 
```


```json
verifyData:
    Enterprise Destination    Price Origin Custom
0   1301930930        D110   4.6000  OR028    C18
1   1301965881        D125  10.7274  OR028    C16
2   3104915030        D137   1.8462  OR049    C16
3   3104915030        D140  28.6700  OR081    C16
4   3107965839        D043   2.1850  OR101    C16
5   3109965344        D056   5.1700  OR034    C16
6   3109965344        D082  26.0500  OR049    C16
7   3109965531        D137   1.9355  OR094    C16
8   3111966828        D074   7.6250  OR091    C16
9   3116961332        D012   5.0300  OR057    C16
10  3117940415        D094   3.7697  OR093    C16
11  3117940415        D094   3.4276  OR093    C16
12  3117960753        D113   2.2414  OR091    C16
13  3122262938        D007  30.8000  OR001    C01
14  3122266784        D092   4.3400  OR100    C16
15  3122268341        D021   1.9741  OR100    C15
16  3122268341        D004   4.5300  OR100    C16
17  3122268643        D015   1.9862  OR093    C16
18  3201912922        D033   3.5156  OR049    C16
19  3201919012        D044   2.3370  OR033    C16

verifyData.T:
                     0           1           2           3           4   \
Enterprise   1301930930  1301965881  3104915030  3104915030  3107965839   
Destination        D110        D125        D137        D140        D043   
Price               4.6     10.7274      1.8462       28.67       2.185   
Origin            OR028       OR028       OR049       OR081       OR101   
Custom              C18         C16         C16         C16         C16   

                     5           6           7           8           9   \
Enterprise   3109965344  3109965344  3109965531  3111966828  3116961332   
Destination        D056        D082        D137        D074        D012   
Price              5.17       26.05      1.9355       7.625        5.03   
Origin            OR034       OR049       OR094       OR091       OR057   
Custom              C16         C16         C16         C16         C16   

                     10          11          12          13          14  \
Enterprise   3117940415  3117940415  3117960753  3122262938  3122266784   
Destination        D094        D094        D113        D007        D092   
Price            3.7697      3.4276      2.2414        30.8        4.34   
Origin            OR093       OR093       OR091       OR001       OR100   
Custom              C16         C16         C16         C01         C16   

                     15          16          17          18          19  
Enterprise   3122268341  3122268341  3122268643  3201912922  3201919012  
Destination        D021        D004        D015        D033        D044  
Price            1.9741        4.53      1.9862      3.5156       2.337  
Origin            OR100       OR100       OR093       OR049       OR033  
Custom              C15         C16         C16         C16         C16  

verifyData.axes:
[RangeIndex(start=0, stop=20, step=1), Index(['Enterprise', 'Destination', 'Price', 'Origin', 'Custom'], dtype='object')]

verifyData.blocks:
{'float64':       Price
0    4.6000
1   10.7274
2    1.8462
3   28.6700
4    2.1850
5    5.1700
6   26.0500
7    1.9355
8    7.6250
9    5.0300
10   3.7697
11   3.4276
12   2.2414
13  30.8000
14   4.3400
15   1.9741
16   4.5300
17   1.9862
18   3.5156
19   2.3370,
 'int64':     Enterprise
0   1301930930
1   1301965881
2   3104915030
3   3104915030
4   3107965839
5   3109965344
6   3109965344
7   3109965531
8   3111966828
9   3116961332
10  3117940415
11  3117940415
12  3117960753
13  3122262938
14  3122266784
15  3122268341
16  3122268341
17  3122268643
18  3201912922
19  3201919012, 
'object':    Destination Origin Custom
0         D110  OR028    C18
1         D125  OR028    C16
2         D137  OR049    C16
3         D140  OR081    C16
4         D043  OR101    C16
5         D056  OR034    C16
6         D082  OR049    C16
7         D137  OR094    C16
8         D074  OR091    C16
9         D012  OR057    C16
10        D094  OR093    C16
11        D094  OR093    C16
12        D113  OR091    C16
13        D007  OR001    C01
14        D092  OR100    C16
15        D021  OR100    C15
16        D004  OR100    C16
17        D015  OR093    C16
18        D033  OR049    C16
19        D044  OR033    C16}

verifyData.dtypes:
Enterprise       int64
Destination     object
Price          float64
Origin          object
Custom          object
dtype: object

verifyData.ftypes:：
Enterprise       int64:dense
Destination     object:dense
Price          float64:dense
Origin          object:dense
Custom          object:dense
dtype: object

verifyData.empty：False

verifyData.is_copy：None

verifyData.ndim:2

verifyData.shape:(20, 5)

verifyData.size：100


verifyData.style:<pandas.io.formats.style.Styler object at 0x0000020A062C9D30>


verifyData.values：:
[[1301930930 'D110' 4.6 'OR028' 'C18']
 [1301965881 'D125' 10.7274 'OR028' 'C16']
 [3104915030 'D137' 1.8462 'OR049' 'C16']
 [3104915030 'D140' 28.67 'OR081' 'C16']
 [3107965839 'D043' 2.185 'OR101' 'C16']
 [3109965344 'D056' 5.17 'OR034' 'C16']
 [3109965344 'D082' 26.05 'OR049' 'C16']
 [3109965531 'D137' 1.9355 'OR094' 'C16']
 [3111966828 'D074' 7.625 'OR091' 'C16']
 [3116961332 'D012' 5.03 'OR057' 'C16']
 [3117940415 'D094' 3.7697 'OR093' 'C16']
 [3117940415 'D094' 3.4276 'OR093' 'C16']
 [3117960753 'D113' 2.2414 'OR091' 'C16']
 [3122262938 'D007' 30.8 'OR001' 'C01']
 [3122266784 'D092' 4.34 'OR100' 'C16']
 [3122268341 'D021' 1.9741 'OR100' 'C15']
 [3122268341 'D004' 4.53 'OR100' 'C16']
 [3122268643 'D015' 1.9862 'OR093' 'C16']
 [3201912922 'D033' 3.5156 'OR049' 'C16']
 [3201919012 'D044' 2.337 'OR033' 'C16']]
 
verifyData.head(5)：
   Enterprise Destination    Price Origin Custom
0  1301930930        D110   4.6000  OR028    C18
1  1301965881        D125  10.7274  OR028    C16
2  3104915030        D137   1.8462  OR049    C16
3  3104915030        D140  28.6700  OR081    C16
4  3107965839        D043   2.1850  OR101    C16

verifyData.tail(2) :
    Enterprise Destination   Price Origin Custom
18  3201912922        D033  3.5156  OR049    C16
19  3201919012        D044  2.3370  OR033    C16

```
    
</details>

<br/> 

### Panel
因为MutiIndex存在，所以更高维的Panel用的很少。不过书上说了去了解一下万一用到也不至于无从下手。  
**pd.Panel(data=None, items=None, major_axis=None, minor_axis=None, copy=False, dtype=None)**
- data=None 数据源
- items=None axis=0 每个item对应于内部包含的数据帧(DataFrame)
- major_axis=None axis=1它是每个数据帧(DataFrame)的索引(行)。
- minor_axis=None axis=2它是每个数据帧(DataFrame)的列。
- copy=False 依旧不知道是干嘛的
- dtype=None 控制数据类型


```py

```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>



## DF的文件IO
### 从其他文件读取
<h3>pd.DataFrame.from_csv()</h3><br/>

<h3>pd.DataFrame.from_dict()</h3><br/>
      
<h3>pd.DataFrame.from_items()</h3><br/>
     
<h3>pd.DataFrame.from_records()</h3><br/>
  

### 存储为其他文件

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More </I></B></summary>

```java
pd.DataFrame.to_clipboard() 
pd.DataFrame.to_gbq()       
pd.DataFrame.to_panel()     
pd.DataFrame.to_sql() √
pd.DataFrame.to_csv() √       
pd.DataFrame.to_hdf() √       
pd.DataFrame.to_parquet()   
pd.DataFrame.to_stata()
pd.DataFrame.to_dense()      
pd.DataFrame.to_html()       
pd.DataFrame.to_period()    
pd.DataFrame.to_string() √
pd.DataFrame.to_dict() √      
pd.DataFrame.to_json() √      
pd.DataFrame.to_pickle() √    
pd.DataFrame.to_timestamp()
pd.DataFrame.to_excel() √     
pd.DataFrame.to_latex()     
pd.DataFrame.to_records() √   
pd.DataFrame.to_xarray()
pd.DataFrame.to_feather()   
pd.DataFrame.to_msgpack()   
pd.DataFrame.to_sparse()
```

</details>

重点讲讲画勾几个
<h3>pd.DataFrame.to_excel()</h3>    
<h3>pd.DataFrame.to_dict()</h3>       
<h3>pd.DataFrame.to_string()</h3>   
<h3>pd.DataFrame.to_json()</h3>       
<h3>pd.DataFrame.to_sql()</h3>   
<h3>pd.DataFrame.to_csv()</h3>        
<h3>pd.DataFrame.to_pickle()</h3>     
<h3>pd.DataFrame.to_hdf()</h3>

关于hdf5看这里，他和hdfs没有一点关系。
<h3>pd.DataFrame.to_records()</h3>      



## 索引对象
### index对象
在Pandas中索引是对象，可以有多级，轻松就可以转为一维二维很好操作。  
pd生成的对象的index属性拿到的就是index对象。也可以通过pd.index()实例化，像一个一维数组一样,是一个**不可变**对象。

```py
x=pd.Series(np.arange(1,10))
x.index,x.index[0:4],x.index[x.index>3]
----------------------------------------
(RangeIndex(start=0, stop=9, step=1),
 RangeIndex(start=0, stop=4, step=1),
 Int64Index([4, 5, 6, 7, 8], dtype='int64'))
```
`pd.Index(data=None, dtype=None, copy=False, name=None, fastpath=False, tupleize_cols=True, **kwargs)`  
参数不多说，当成支持集合运算的一维数组用就行了。这东西可以充当Series和DataFrame初始化的index参数。
### MultiIndex对象
这个对象用来充当索引，多级索引相当于数据增加了一个维度  
有很多创建方法，`pd.MultiIndex()`是最基本的  
- levels=None 二(n)维数组，里面有不同的元素 [[a,b,c],[d,e,f]]
- labels=None 二(n)维数字数组[[0,2,1,1],[0,1,1,2]]组合levels成为一个多级索引
- sortorder=None or int默认就行
- names=None ["行名字","列名字"]
- dtype=None 
- copy=False 不要管这个
- name=None 
- verify_integrity=True 不要管这个
- _set_identity=True 不要管这个

- from_arrays()  
    - pd.MultiIndex.from_arrays([[a,b,c,d],[1,2,3,4]])
    - 生成a1,b2,c3,d4的索引
- from_tuples()  
    - pd.MultiIndex.from_tuples([(a,1),(a,2),(b,1),(b2)])
    - 生成了a1，a2,b1,b2的索引
- from_product()  
    - 根据<a href='https://zh.wikipedia.org/zh-hans/%E7%AC%9B%E5%8D%A1%E5%84%BF%E7%A7%AF'>笛卡儿积</a>生成多级索引
    - pd.MultiIndex.from_product([[a,b],[1,2]])
    - 生成了a1，a2,b1,b2的索引
    
<br/>

使用的时候直接传入index参数中。    
两级索引的`Series`可以使用`unstack`转为`DataFrame`，反之可以用`stack`，不需要参数默认保留最后一轴
在字典中也可以隐式的创建MultiIndex，index用嵌套列表表示多级索引时，pandas会进行自动处理，直接使用MultiIndex也是可以的，下例:


<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```py
multiIndex代码
```

</details>

## 索引和切片
### Series切片
pd底层时numpy的，所以很多东西是通用的。支持像数组和字典一样的切片，`S[1]`或者`S["x"]`你的索引设置的是整数你下标就得是整数，字符串亦然。  
Series是map映射对象，支持一些map的操作 `x in keys``items()` `keys()` `values`。也可以直接用点`.`但不推荐。  
下标同样和numpy一样是增强版`S([["x","y","z"]])`就可以取出三个值来，支持bool操作`S[S>200]`也可以切片`S['x':'z']`
:::danger
直接字符串接切片前后都包括，不会有头没尾  
仍然同时支持整数切片，此时会有头没尾  
pandas不再使用视图，全都是副本，每次切出来都生成一个新对象
:::
```py

```

注意一个特殊的情况，当你自己指定了和原始数组不一样的整数索引，取一个数字的时候是你定义的索引，而且片的时候使用的是数组原来的索引
```py

```
为了避免混乱，两个函数  
- S.iloc[]使用原始数组的下标作为索引
- S.loc[]使用你自己的索引  

<br/>

同时适用于DataFrame  
多级索引MultiIndex也支持切片用逗号`,`隔开每个索引，不能直接取二级索引  
`S.[:,5]` 取第一级索引的所有取第二级索引5。
```py

```

### DataFrame切片
在使用`iloc[]`的时候DF已经相当于一个没什么索引的二维数组了，用整数操作即可。  
loc也适用于DF。一般来说全选切片只能使用一次，但是DF中使用了`idx`可以让我们使用多次,就是把要索引的项先用idx进行一次索引  
```py

```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>
<br/>
  
  
  
  
  
:::danger
作为索引的MultiIndex,要进行从小到大排序，不然切片的时候会错误
:::
### 处理缺失数据
如果数据中有缺失，表示为None，np.nan，NAN,null等，或该列的数据类型不一致，dtype会被判定为Object，直接进行加和等运算会报错。
:::danger
np.nan会被判定为一个浮点数，该数值参与任何运算都会得到nan，一般用来标记缺失数据  
pandas中使用NAN来标记缺失数据
:::
numpy处理nan有特定的函数
- np.nansum(),np.nanmean。。。  
这些函数在计算的时候会直接忽略掉`这一项`。例如计算平均的时候除数会少1    
<br/>

pandas在把np转为pd的数据结构的时候，自动把np.nan，None转换为NaN，在计算得时候会自动忽略NaN的存在，也有专门对NaN的处理函数
- df.isnull()
    - 返回同规模的Bool矩阵，True代表的项就是NaN
- df.notnull()
    - 返回同规模的Bool矩阵，False代表的项就是NaN
- df.dropnull()
    - 删除NaN数据，返回不包含NaN的新对象
    - 默认axis=0，行全删除
    - 指定axis=1/'columns'，列全删除
    - inplace=False，为True会对原df产生影响
- df.fillna(x)
    - 用x填充NaN
    - inplace=False，为True会对原df产生影响
    - limit=n 限制最多填充个数
    - axis= 0/1 修改填充方向
    - method='ffill'前值填充后值，若前面没值仍然是NaN(从上往下看)，bfill是后值填充前值，若后面没值仍然是NaN(从下往上看)  
    
前面的操作如果不指明都会生成一个新对象，注意替换要指明方向保险一些


```py
鸽了
```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>

## DataFrame连接
pandas提供了numpy风格的连接和数据库风格的连接。  
### 轴向连接
- pd.concat()
    - objs  需要连接的对象，用数组盛着
    - axis=0 0 or 1默认0 指定轴连接
    - join='outer' 其他轴是按照并集还是交集连接   
    - join_axes=None 指定其他n-1条轴的索引，不执行并/交操作队医DF当axis=0若该项为列表，则该列表的值就是DF的列标签  
    - ignore_index=False 若为True，放弃列标签，代替为自然数
    - keys=None 设置多级索引
    - levels=None 指定多级索引标签  
    - names=None 多级索引名称
    - verify_integrity=False 若为True，当连接轴有重复就报错
    - sort=None 不知道，应该是用来排序的    
    - copy=True 是否为复制  

```py
p122-123
```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>    

注意s1只有一列，而s3有三列，这时候s1会自动对齐NaN，而所有的数字类型都自动类型转换成了浮点数  
当制定轴向的索引不相同时会按照最大规模补全NaN（取了并集），如果`join="inner"`则会把不全的所有列删掉(交集)  
按1轴连接也能设置多级索引
```py
p124-125
```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>    
  
`df1.append(df2)`等同于`axis=0`的concat，其中`ignore_index=True`的话会忽略原有的行索引重新设置为自然数。注意这个方法不会改变fd1
的值只会新返回一个


### 数据库风格连接 
- pd.merge针对DF对象使用的数据库风格连接函数  
    - left,right 要连接的两表
    - how='inner' 四个选项'inner'/'outer'/'left'/'right'。默认为inner。
        - left/right：仅以left/right的DataFrame对象中所指定的列为键、以并集（outer）的方式合并数据。
        - outer：两个DataFrame对象指定键的并集。
        - inner：两个DataFrame对象指定键的交集
    - on=None 默认为None。用于合并的字段名称（列标签）。一般是两个DataFrame所共有的列。如果on=None，且未指定合并的键，则以两个DataFrame对象列标签的交集为合并的键
    - left_on/right_on=None 默认为None。从left/right所引用的DataFrame对象中选择记录（列标签）作为数据合并的键
    - left_index/right_index=False 默认为False。如果为True，则以left/right所引用对象的索引为键合并数据
    - sort=False 也没讲，也没用到
    - suffixes=('_x','_y') 默认为("_x","_y")。左右两侧相同列名称的后缀
    - copy=True 不说
    - indicator=False 默认为False。如果为True，在返回的DataFrame对象中会增加列标签"merge"的列,给出是怎么合并的信息，注明每行数据的来源。如果是字符串，则此列标签为该字符串
    - validate=None 


```py
128-131
```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>

- DF.join()参数基本与merge一致，可以直接由DF调用，同样不改变原数组值
    - on=None  
    - how='left'  
    - lsuffix=''  
    - rsuffix=''  
    - sort=False 

```py

```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>

### 组合数据
填充数据，转置和试图，在数据处理中经常需要的操作。  
- df.combine_first(df2)
    - 填充。当df2列和行都比df多，df中有缺失数据而df2中没有，此时会把df1中缺少的数据不上并且缺少的列也会添加进去。
    - 返回一个新对象
- stack()/unstack()
    - 转置，可以理解为np.T
    - 注意参数和一维数组(Series)的转置,dropnan=True,这个参数会自动删除转换后NaN的列  
    

透视表，相当于数据库中的视图(view),先解释一下逻辑：指定某一列数据作为一个轴，然后抽取指定列数据形成一个二维视图  
#{此处图1,2 p139}  

- df.pivot(index=None,coumns=None,values=None)  
当数据对应2个及以上的多值，pivot会报错，此时需要pivot_table
- df.pivot_table  
    - #{参数}  
    
    
pivot_table可以指定冲突的处理函数，内置的函数有#{内置函数}    

<br/>
三个函数示例:

```py

```

<details>
  <summary><B><I style="cursor:pointer; color: #0e5870">Click to See More Results</I></B></summary>

```json

```

</details>

## 分组运算

想一下SQL的groupby操作，pandas也有对应的实现分组运算的函数。    
### 统计运算函数

对于pandas.DF中的数字类型列，np的所有统计函数仍然适用，不过要注意大部分的统计函数在DF里是实例方法而不是类方法。例如求和(sum)求平均数(mean)，求中位数(median)
指定axis=0 or 1 可以指定对行或者列进行操作  

:::tip
若进行统计操作的某一列全为NaN，则该列会自动不计入总数中，例如平均`Σ/n`的时候该列不计入n中  
pandas中所有带有参数inplace=False的函数都是不改变原数组，返回一个新的，指定一下为True就会直接改变原数组。
:::

常用函数:
- describe()可以直接给出大多数需要统计的项目（超好用
- head/tail(n)查看头/尾n条记录，默认5
- isnull.any()数据是否完整，返回同规模的DF，和np里面一样
- nuique()去重  



#{一行统计重复的列
统计字符串出现的次数
映射函数
reduce实现
字符串&数字排序
抽样
类型转换
离散化
}
### 矢量化字符串
### 离散化数据
### 分组处理

## 时间序列

### Numpy的日期类型
### pandas



## Scipy

### Scipy
数学基础有点跟不上，数据挖掘也没怎么敲。   
先去学高数，考完研这些都会还的🧐