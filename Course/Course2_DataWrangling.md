**目录：**

[TOC]

# $\rm I$. 课程概览

本次课程内容将进入数据清理部分的课程，数据清理（Data Wrangling）包括三个方面的内容：1）数据收集（Gather Data）；2）数据评估（Access Data）；3）数据清洗（Clean Data）。接下来将从这几个方面来讲解相关内容。

**数据清理**：是一种数据转换的过程，即从原始数据转换为可分析的数据的过程。在这个过程中需要处理的主要问题是“脏”数据的**质量问题**以及数据结构方面的 **整洁度** 问题。[^1] 

**提醒⏰：1）养成好的习惯，对于在数据每一步的处理尽量做好记录，以方便复盘以及技术信息分享；2）做好数据备份工作，对处理前和处理后的数据都分别做好备份**

# $\rm II$. 数据收集

## 2.1不同方式收集数据

数据收集的方式可以通过 API、网页爬取、网页文件下载以及公司内部等形式。例如课程中的 `Kaggle` 数据内容下载可以通过通过 API[^2] 的方式进行下载：

```bash
# 第一步安装 API 
pip install kaggle

# 在 Mac/Linux 系统中安装 API
pip install --user kaggle

# 第二步配置文件——需要到 Kaggle 的个人账户下下载 API 配置文件

# 第三步修改 API 配置文件的文件属性，注意文件保存位置——下面的命令为 Linux 和 Mac 下命令
chmod 600 ~/.kaggle/kaggle.json

# 第四步下载文件，直接下载完整数据集
kaggle datasets download -d udacity/armenian-online-job-postings

# 可以使用相应的参数来下载特定的文件，下面下载了 features.txt 文件
kaggle datasets download -d udacity/armenian-online-job-postings -f features.txt
```

Kaggle 的个人账户（`https://www.kaggle.com/<username>/account`）下载 API 配置文件

<img src=https://ws1.sinaimg.cn/large/006tNbRwgy1fxtxonsgahj30uq0ewmyx.jpg width=50%/>

## 2.2 处理压缩文件

在数据收集的过程中，压缩或者打包格式文件(`rar`, `zip`, `tar` 等)有多种处理方式，例如 `zip` 文件可以通过 `unzip` 将文件进行解压缩[^3]（`rar` 文件需要安装相应的程序文件处理），`tar` 文件可以通过`tar` 命令进行还原文件。[^4] 在 Python 中，可以使用标准库 zipfile[^5] 来完成解压缩，或者仅读取压缩文件。

```python
# 从压缩文件中解压缩
with zipfile.ZipFile('armenian-online-job-postings.zip', 'r') as myzip:
    myzip.extractall()
    
# 从压缩文件中读取文件信息，而不解压缩
with zipfile.ZipFile("./ncis-and-census-data.zip") as zfile:
    for filename in zfile.namelist():
        with zfile.open(filename, 'r') as data:
            if filename.endswith("xlsx"):
                    df_gun = pd.read_excel(data)
            else:
                df_census = pd.read_csv(data, sep=",", thousands=',')
```

## 2.3 文件导入

在进行数据处理之前，需要将文件内容通过相应方法将数据内容读取到相应的对象中以完成后续的工作。例如可以使用 pandas 来读取文件[^6]，标准库中 csv, JSON 等可以读取特定文件的内容[^7]



# $\rm III$. 数据评估

数据评估，常见的方法上可以从视觉观察、编程审核等方式评估数据。从需要评估的内容来看，主要包括以下内容 **数据质量** 和 **数据整洁度** 两个方面。

## 3.1 评估角度

### 3.1.1 数据质量

**数据质量**指查看或评估数据在特定情境下是否能准确表示其目的。常见的数据质量问题：

- 数据缺失，需要注意数据的缺失包括有意义的缺失
- 数据无效，单元格中的值不符合常规，数据类型不合适
- 数据不准确，数据值不准确
- 数据不一致，主要指数据值信息不一致，比如，使用不同的长度单位（英寸和厘米）

### 3.1.2 数据整洁度

数据整洁度，主要是从数据结构方面来判断数据存在的问题。其主要的评判标准：

- 每个变量构成一列
- 每个观察结果构成一行
- 每种类型的观察单位构成一个表格

>In summary, tidy data is a useful conceptual idea and is often the right way to go for general, small data sets, but may not be appropriate for all problems[^8]

## 3.2 评估方法

基于对以上评估数据的角度，可以采用多种方式进行数据评估，例如直接通过视觉观察数据、编程的方法——例如数据信息确认的方法以及可视化的方法都可以对数据进行评估。

视觉评估数据的角度，可以通过直接观察数据内容就可以确认数据存在的问题。例如，可以通过直接观察到方式缺失数据、数据值不一致以及数据正确性的问题。

编程评估数据的角度，主要是使用代码来处理难以观察到的数据问题。该方法主要是依据数据类型的不同方法来进行不同的处理。例如 DataFrame 的数据类型有自己方法来确认数据信息，Numpy 提供的 ndarray 的数据类型及该类型下的方法外还提供了其他方法。

# $\rm IV$. 数据清洗

清洗是对数据质量和整洁度进行处理的行动过程，一般处理的是数据错误或者不相关数据。而处理方法方面，可以采用替换、填充、合并以及拆分等方式，通过数据转换的方式来提高数据整洁度。我们在数据分析的过程中主要是采用编码的方式来进行数据清洗，其主要的流程过程为：

编程数据清洗过程：

1. **定义** 

   指以书面形式定义数据清洗计划，其中我们需将评估转变为定义的清洗任务。这个计划也可作为一个指导清单，所以其他人（或我们自己将来）也可以回顾和重现自己的工作

2. **编码**

   将这些定义转换为代码并执行该代码

3. **测试**

   一般使用代码对数据内容进行测试检验，以确保有效完成我们的清洗工作

# $\rm V$. 数据处理后工作

当完成一定的数据处理工作之后，我们可以继续数据分析的后续工作——分析、可视化等。但是需要注意⚠️数据分析是一个迭代的过程，在后面的分析过程中还是可能需要继续数据清洗的工作。



# $\rm A$. 参考

[^1]: [Data wrangling](https://en.wikipedia.org/wiki/Data_wrangling) 
[^2]: [kaggle-api: Official Kaggle API](https://github.com/ZenRay/kaggle-api) 
[^3]: [Linux unzip命令](http://www.runoob.com/linux/linux-comm-unzip.html)

```bash
# zip 压缩，压缩指定目录下所有文件和文件夹打包为当前目录下，不使用 -q 参数可以显示相关压缩信息
zip -q -r file.zip /home/users/file

# unzip 解压缩，-n 参数可以不覆盖原文件，需要解压到指定的文件位置，可以通过 -d 参数及其跟随值来指定
unzip -n test.zip -d /tmp 
```

[^4]: [Linux tar命令](http://www.runoob.com/linux/linux-comm-tar.html) 

```bash
# 打包
tar -cvf name.tar name.txt    # 仅打包，不压缩！ 
tar -zcvf name.tar.gz name.txt   # 打包后，以 gzip 压缩 
tar -jcvf name.tar.bz2 name.txt  # 打包后，以 bzip2 压缩 

# 解包
tar -zxvf name.tar.gz
```

[^5]: [zipfile 官方文档](https://docs.python.org/3/library/zipfile.html#zipfile-objects) 
[^6]: [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html) 
[^7]: [python3-cookbook 3.0.0 文档](https://python3-cookbook.readthedocs.io/zh_CN/latest/c06/p01_read_write_csv_data.html) 
[^8]: [Non-tidy data · Simply Statistics](https://simplystatistics.org/2016/02/17/non-tidy-data/) 