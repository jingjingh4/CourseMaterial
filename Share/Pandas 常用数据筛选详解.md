对于 DataFrame 和 Series 是可以类比于 Excel 表格来看：对于具有多列的 Excel 表可以当作是 DataFrame 来类比，而单列的 Excel 表是可以当作一个 Series 来类比（但是这里不完全正确，例如 DataFrame 进行数据以 `[]` 的形式进行数据筛选的时候，`df[["col"]]` 这里虽然是只有一个列但是得到的数据类型是一个 DataFrame），此外 Series 可以被当作一个是一个 shape 为 `[n, :]` 的 Array 来看待——也就是说具有多行单列的数据—— n 为行数。

因为 Series 具有 Array 的数据特质，所以它完全可以进行索引操作方式来取得数据：

```python
import pandas as pd
series = pd.Series([1, 2, 3, 4, 5])

series[:2]
# ouput
0    1
1    2
dtype: int64
```

当然 Series 也具有 iloc 和 loc 属性——前者是行索引值的方式，后者是索引标签的方式，如果行索引是数值（例如上例中，就没有行字符串标签，就是说数字就是其行标签），那么 loc 也可以使用数字。

```python
series = pd.Series([1, 2, 3, 4, 5])

series.iloc[:2]
# ouput
0    1
1    2
dtype: int64

series.loc[:2]
# output
0    1
1    2
2    3
dtype: int64
```

以上需要**注意⚠️** 虽然后面方括号中数据是相同的，但是结果是不同的——这里需要记住 loc 是选择的行标签——所以是选择 0，1， 2 这三个行标签；而 iloc 是选择的索引数据值，是 0， 1。

DataFrame 的数据筛选更复杂，因为它是一个二维的数据，所以需要考虑行和列的问题。因此在这里将分别从三个角度探讨一下数据筛选：

1. 仅筛选列 

   * 单列筛选 直接筛选的话，可以使用 `[]` 来筛选，而在 `[]` 中的每一个列的 label 都需要是 DataFrame 中已有的 label，否则会提示 KeyError——不论直接筛选还是使用 loc 筛选，其中的列值都需要存在于 DataFrame

     ```python
     df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]})
     
     # 假设创建了上面一个 dataframe，需要对相应的列进行筛选
     
     # 筛选单列，如果是只有一个 []，得到的数据类型是 Series，如果是“嵌套” 的 [] 将得到一个 dataframe
     
     df["col1"]
     # Output
     0    1
     1    2
     Name: col1, dtype: int64
     
     df[["col1"]]
     # output
        col1
     0     1
     1     2
     
     ```

     DataFrame 可以使用 loc 进行列标签筛选，需要注意使用 `[]` 中需要添加一个 `,` 用于说明行和列区分，`,` 之前表示的是行，`,` 表示的是列，此外如果没有筛选行的话建议在 `,`  添加 `:` 表示选择所有的行

     ```python
     # 和第一种方式得到的结果是一样的
     df.loc[:, "col1"]
     # Output
     0    1
     1    2
     Name: col1, dtype: int64
     
     df.loc[:, ["col1"]]
     # output
        col1
     0     1
     1     2
     ```

     除了 loc 用于数据筛选，还可以使用 iloc，两者的区别在于前者需要使用行或者列的 label 名称，而后者是使用的对应的行列索引值。两者的基本结构相同，如下：

     ![image-20181018234530267](https://ws4.sinaimg.cn/large/006tNbRwgy1fwct4b7h5fj30jz06zaan.jpg)



```python
 # 两种方式得到的结果是一样的，同如果使用 loc 进行筛选列的话，存在相同的情况，但是需要注意
 df.iloc[:, 0]
 # Output
 0    1
 1    2
 Name: col1, dtype: int64
 
 df.iloc[:, [0]]
 # output
    col1
 0     1
 1     2
```

   * 多列筛选 多列的筛选的方式和前面的单列筛选没有太大的差异，主要是需要使用“嵌套”的 `[]` 将筛选列包裹——iloc 不需要进行嵌套

     ```python
     df[["col1", "col2"]]
     # Output
        col1  col2
     0     1     3
     1     2     4
     
     df.loc[:, ["col1", "col2"]]
     # output
        col1  col2
     0     1     3
     1     2     4
     
     # 注意⚠️ 使用 iloc 的时候不需要使用 [] 来嵌套
     df.iloc[:, 0:2]
     # output
        col1  col2
     0     1     3
     1     2     4
     
     # 如果需要进行不连续的筛选，可以使用 numpy 的 r_ 属性进行创建，可以进行不连续筛选
     df.iloc[:, np.r_[0:2, 2, 1]]
     # output
        col1  col2  col3  col2
     0     1     3     7     3
     1     2     4     4     4
     ```

2. 仅行筛选

   * 行的直接筛选 同样可以使用 `[]` 进行筛选，也需要使用行索引标签，需要注意⚠️即使取单行也必须使用“切片”方式——添加 `:` 的方式进行筛选，否则会被作为列名称，因此对于行列名称重复的情况谨慎使用直接筛选的方式。此外该方式得到的结果是一个 DataFrame

     ```python
     df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]})
     
     # 假设创建了上面一个 dataframe，需要对相应的列进行筛选
     
     # dataframe 的行索引标签和行索引标签值是相同的
     
     df[0:1]
     # Output
        col1  col2  col3
     0     1     3     7
     
     df[0:2]
     # output
        col1  col2  col3
     0     1     3     7
     1     2     4     4
     
     df1 = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]}, index=['a', 'b'])
     # 上面穿了一个有行标签的数据，进行行筛选同样需要 “切片” 方式
     
     df1['b':'b']
     
     # output
        col1  col2  col3
     b     2     4     4
     
     # output
        col1  col2  col3
     a     1     3     7
     b     2     4     4
     ```

   * 使用 loc 或者 iloc 的方式 两种方式都是和列筛选方式相同，只是需要控制的是行的标签名或者行索引值。推荐使用这两种方式进行筛选。得到的结果会因为筛选方式的不同，而得到 Series 或者 DataFrame——和列筛选产生 Series 和 DataFrame 的方式一样，但是需要注意行筛选时谨慎使用嵌套 `[]`

     ```python
     df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]})
     
     # 假设创建了上面一个 dataframe，需要对相应的列进行筛选
     
     # dataframe 的行索引标签和行索引标签值是相同的
     
     df.loc[0, :]
     # Output
     col1     1
     col2     3
     col3     7
     Name: 0, dtype: object
     
     df.loc[[0], :]
     # output
        col1  col2  col3
     0     1     3     7
     
     # 如果需要多行筛选，和之前多列筛选的方式一样
     df.loc[0:2, :]
     df.loc[0:4, :]
     # output
        col1  col2  col3
     0     1     3     7
     1     2     4     4
     
     # 另外需要使用 iloc 是使用的行的索引值
     df.iloc[0, :]
     # Output
     col1     1
     col2     3
     col3     7
     Name: 0, dtype: object
     
     df.iloc[[0], :]
     # output
        col1  col2  col3
     0     1     3     7
     
     # 当进行多行筛选时和 loc 方式有细微差异 如果此处使用 df.iloc[0:2, :] 行的表索引值超过范围并不会报错
     df1.iloc[[0,1], :]
     df.iloc[0:3, :]
     df.iloc[0:2, :]
     # 以上两者均不会报错，而且结果相同
        col1  col2  col3
     0     1     3     7
     1     2     4     4
     
     df1 = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]}, index=['a', 'b'])
     # 上面穿了一个有行标签的数据，
     
     df1.loc['a', :]
     # Output
     col1    1
     col2    3
     col3    7
     Name: a, dtype: int64
     
     df1.loc[['a'], :]
     # output
        col1  col2  col3
     a     1     3     7
     
     df1.loc[['a', 'b'], :]
     df1.loc["a":"b", :]
     
     # output
        col1  col2  col3
     0     1     3     7
     1     2     4     4
     
     # 使用 iloc 是筛选，和上例的方式是一样
     
     df1.iloc[0, :]
     # Output
     col1     1
     col2     3
     col3     7
     Name: a, dtype: object
     
     df1.iloc[[0], :]
     # output
        col1  col2  col3
     0     1     3     7
     
     df1.iloc[[0,1], :]
     df1.iloc[0:3, :]
     df1.iloc[0:2, :]
     # 以上两者均不会报错，而且结果相同
        col1  col2  col3
     0     1     3     7
     1     2     4     4
     ```

3. 行列混合筛选  行列混合筛选在使用 loc 和 iloc 时，和简单筛选方式是一样的，不再讲解。对直接进行行列筛选进行简单说明，行申明还是需要 `:`，列筛选需要使用根据多列还是单列判断，多列是需要使用嵌套 `[]`，且不能使用 `:`——虽然不会报错但结果不正确。单列时可以使用嵌套 `[]` 与否均可以，只是数据类型可能会存在差异

   ```python
   df1 = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4], 'col3': [7, 4]}, index=['a', 'b'])
   
   df1['a':'b'][['col1','col2']]
   
   # output
      col1  col2
   a     1     3
   b     2     4
   
   df1['a':'b']['col1':'col2']
   # output 结果不正确
   Empty DataFrame
   Columns: [col1, col2, col3]
   Index: []
   
   # 单列筛选
   
   df1['a':'b'][['col1']]
   # ouput
      col1
   a     1
   b     2
   
   df1['a':'b']['col1']
   # output
   a    1
   b    2
   Name: col1, dtype: int64
           
   df1['b':'b']['col1']
   
   # output
   b    2
   Name: col1, dtype: int64
           
   df1['b':'b'][['col1']]
   # output
      col1
   b     2
   ```

4. 条件筛选 条件筛选一般值 mask 方式筛选，它不仅可以对行条件还可以对列条件筛选。对于常用的条件筛选，例如直接对 `df[df["col1"] > 2]` ， `df.query('col1 > 2)` ，`df.select_dtypes()` 以及其他复合方法（使用 `where` 和 `drop`）不再详细讲解。这里只说明使用条件结合 `loc` 的方式进行筛选，原理上只需要得到行列位置上的 `True` 或者 `False` 的值就可以进行筛选

   ```python
   # 首选时行筛选，表现上和 df[df["col1"] > 2] 相似，只需要将条件放在行的位置即可
   df.loc[df["col1"] > 2, :]
   
   # output
     col1  col2  col3
   0     1     3     7
   1     2     4     4
   
   # 接下来是对列筛选，例如需要某些列名称的进行筛选。首先同样需要创造条件，这里需要结合使用 columns 属性以及 str.contains 方法来判断是否包含某些值
   
   df.loc[:, df.columns.str.contains("1")]
   
   # output
      col1
   0     1
   1     2
   ```


以上就是基本的信息，下面将简单说明一下在以列名称/字段名称来进行数据筛选中常犯的错误：

1. 行和列的嵌套使用 `[]` 时，直接进行了“切片”方式筛选会报错，修改方式为将“切片”改为对应的需要的值

   ```python
   df.loc[[0:2], :]
   df.loc[:, ["col1": "col2"]]
   # 报错如下
   SyntaxError: invalid syntax
   
   # 需要改为相应需要的取值，如果是数值可以使用 np.r_ 等方式进行拼接
   df.loc[np.r_[0:2], :]
   df.loc[[0, 1], :]
   ```

2. `[]` 标记使用为 `()`，同样是语法错误或者说对象不可调用。只需要将圆括号修改会方括号

   ```
   df.iloc(:,1)
   # 报错
   SyntaxError: invalid syntax
   
   df('col1')
   # 报错
   TypeError: 'DataFrame' object is not callable
   ```

3. 直接筛选的索引值超过长度，可以修改切片或者剔除不合适的值——切片方式超过长度时，不论 loc 还是 iloc 不会报错——见上面的例子

   ```python
   df1.iloc[[0, 1, 3], :]
   # 报错
   IndexError: positional indexers are out-of-bounds
   ```

4. 使用的标签值不存在，

   ```python
   df1.loc['c', :]
   
   # 报错
   KeyError: 'the label [c] is not in the [index]'
   
   df1.loc[:, 'col4']
   # 报错
   KeyError: 'the label [col4] is not in the [columns]'
   ```

5. 直接进行行筛选时，没有使用 `:`，而导致报键错误，修改需要使用 `:`，见上面的例子

   ```python
   df1['a','b']
   # 报错
   KeyError: ('a', 'b')
   
   df1['a']
   # 报错
   KeyError: 'a'
   
   ```

6. 直接行列筛选时，列不使用嵌套 `[]`，修改方案为添加 `[]`

   ```python
   df1['a':'b']['col1','col2']
   
   # 报错
   KeyError: ('col1', 'col2')
   ```