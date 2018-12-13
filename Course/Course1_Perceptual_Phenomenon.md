**检验心理学**

[TOC]

## $\rm I.$ 课程概览

课程项目是检验心理学，需要在回顾统计学知识的基础上完成该课程。统计学的部分，主要包括了两个部分，描述统计学、推论统计学。

注意对统计学显著性结果的解读，p值并不能衡量条件是否为真或者数据是否随机，从而它不能也不应该当作决策的因素。正确理解P值与差别有无统计学意义。P越小，不是说明实际差别越大，而是说越有理由拒绝H0 ，越有理由说明两者有差异，注意有无统计学意义和有无专业上的实际意义并不完全相同。



## $\rm II.$ 描述统计学

描述统计，使用图形、数值等形式汇总数据信息。在数据描述数据等过程，主要从两个角度 **集中趋势** 和 **离散程度** 来进行描述数据。

**集中趋势** 数值信息：

1. 均值（**Mean**）：将所有值相加，然后除以数据集中值的数量。
2. 中位数（**Median**）： 将数据集从小到大排序后，能够将数据集一分为二的值。需要注意计算会因为数据个数是奇数还是偶数个而存在差异
   - 奇数个观察值，直接使用中间的数字
   - 偶数个观测值，中位数是中间两个值的平均值。在计算的时候，使用 $\frac{x_{\frac{n}{2}}+x_{\frac{n}{2}+1}}{2}$ ，可以参考 [Median - Wikipedia](https://en.wikipedia.org/wiki/Median) 
3. 众数（**Mode**）：是一组数据中出现次数最多的数值，因此存在极端情况——可能有多个众数也可能一个也没有
   - 无众数情况：所有独特值的频数都是相同的
   - 多众数情况：某几个独特值的频数是最大且相同

**离散程度** 数值信息：

1. 五数概括：

   通过计算最小值、$Q1$、$Q2$、$Q3$ 以及最大值，概括出值域以及四分位差值。

   - **最小值**：数据中最小的值
   - $Q1$：即排序数据的第 $25\%$ 处的数据值，排序数据中中位数左侧数据的中位数。它是第一个四分位数
   - $Q2$：即中位数，排序数据 $50\%$ 处的数据
   - $Q3$：即排序数据的第 $75\%$ 处的数据值，排序数据中中位数右侧数据的中位数。它是第三个四分位数
   - **最大值**：数据中最大的值

   通过以上的数据，可以计算出相关的离散程度表示值：1）值域，$Range=max-min$；2）四分位差，$IQR=Q3-Q1$ 

2. 单一数值描述

   - 标准差：计算方式为 $Std=\sqrt{Var}$，在总体中标准差的表示符号是 $\sigma$，样本中的标识符号为 $S$——它的统计学意义是总体的无偏估计
   - 方差：每个观察值和均值之间的平均值差值平方和的平均数， 连续性数据的计算公式： $Var=\frac{1}{n}\times\displaystyle{\sum_{i=1}^n(x_i-\bar{x})^2}$ 

数据的描述还有其他相关信息，例如 异常值、杠杆值

## $\rm III.$ 推断统计学

使用样本数据对总体数据特征进行估计和假设检验的过程。推断统计的基础内容：

* 置信区间：对总体参数的一个区间估计，在一定的置信水平的可信度下该区间内参数值可以被纳入其中范围，范围的上下限由假设检验得出下

* 置信水平：与区间估计相联系的置信度。例如对数据进行区间估计得到的全部区间中，假设有 $95\%$ 的区间将包含总体参数，则这里的 $95\%$ 就是构造该区间的置信水平

* p 值：当零假设为真，真实值落在置信区间的概率

* $\alpha$ 显著水平：零假设为真时，发生拒绝零假设的概率

* 零假设/原假设（Null Hypothesis）

  表示符号是 $\rm H_0$；其提出的零假设一般是针对两个测量的现象是没有相关性的，或者是检验的样本和总体之间没有相关性。这里需要强调💰💰一点，整个假设检验中零假设才是用于描述统计学显著性检验的语句，而且显著性检验的设计也是最终是否拒绝零假设，也就是说在统计检验之前的假设中一般是默认选择零假设。

  在描述上，零假设一般常用描述“没有效果”或者“没有差异”——但是在没有进行数据验证之前，$H_0$ 是为真的，换句话来说就是按照 ”无罪推定“ 的方式来验证它。描述方式：$=$，$\le$，$\ge$

* 对立假设/备选假设（Alternative Hypothesis）

  表示符号是 $\rm H_1$ 或者 $\rm H_a$；它是和零假设的内容完全对立的假设。描述方式：$\ne$，$\lt$，$\gt$

常用的统计检验方法：

1. 单样本 Z 检验

   用于测试总体的参数是否和其他假设值有显著差异

   * 应用场景举例

     生产线上产品是否符合标示数据——$\sigma$ 可以通过通过以往的数据得到

   * 条件

     **总体属于正态分布**，$\sigma$ 已知；对小样本不适用

   * 计算公式：

     $z =\frac{\bar x - \mu}{\frac{\sigma}{\sqrt n}}$ 

2. 单样本 t 检验

   * 应用场景举例：

     地区新生儿体重是否符合全国新生儿体重要求

   * 条件：

     **总体属于正态分布**、$\sigma$ 未知；此外对小样本（样本数据小于 30 的条件下）也可以使用

   * 计算公式：

     $t = \frac{\bar x -\Delta}{\frac{s}{\sqrt n}}$ 

   注意⚠️：t 分布还依赖于自由度，自由度 $d_f$ 为样本容量减一——$d_f = n- 1$

3. 独立双样本 t 检验

   两个样本是相互独立抽取的

   * 应用场景举例

     两个学校之间学生的成绩是否有差异

   * 条件

     两个样本是相互独立的，且样本总体是正态分布的；$\sigma$ 未知

   * 计算公式

     $t=\frac{(\bar x_1 - \bar x_2) - D_0}{\sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}}}$ 

     注: $D_0$ 指的是总体之间的差异值；此外如果假设两个总体的标准差相等时，可以通过合并方差的计算方式来计算 t 值
     $$
     \begin{align}
     s_P^2=\frac{(n_1-1)*s^2+(n_2-1)*s^2}{n_1+n_2-2}\\
     d_f = n_1+n_2-2 \\
     t=\frac{(\bar x_1 - \bar x_2)-D_0}{s_p\sqrt{\frac{1}{n_1}+\frac{1}{n_2}}}\\
     \end{align}
     $$

4. 配对样本 t 检验

   配对样本的设计中，控制变量的条件下，对相同的试验对象采取两次不同的试验

   * 应用场景举例

     采取不同的方法，是否有助于提高生产线上工人的工作效率

   * 条件

     样本是配对的，服从正态分布

   * 计算公式
     $$
     \begin{align}
     \bar d =\frac{\sum{d_i}}{n}\\
     s_d=\sqrt{\frac{\sum{(d_i-\bar d)^2}}{n-1}}\\
     t=\frac{\bar d - \mu_d}{\frac{s_d}{\sqrt n}} \\
     d_f=n-1
     \end{align}
     $$







## $\rm III.$ 补充信息

1. 条件概率

    $P(A|B)=\frac{P(A\cap B)}{P(B)}=\frac{P(B|A)*P(A)}{P(B)}$，描述性表述就是 $B$ 事件发生的条件下，$A$ 事件发生的概率。

   对于条件概率的计算，可以使用 `DataFrame` 的 `groupby` 方法进行聚合即对应的分组来进行计算。因为 `groupyby` 可以创建多索引的数据，这样得到的结果就很像条件上的先决条件下第二个事件发生的概率

   ```python
   df.groupby(["has_cancer", "test_result"]).size()
   
   # 上面这中排序方式，就是确认了是否有癌症的病人的情况下被检测出了癌症的病人的统计数量
   # output
   has_cancer  test_result
   False       Negative       2077
               Positive        531
   True        Negative         29
               Positive        277
   dtype: int64
   
   # 接下来需要统计的是确认是否患癌症的病人的群组人数
   df.groupby("has_cancer").size()
   # output
   has_cancer
   False    2608
   True      306
   dtype: int64
   
   # 下面需要计算的是概率问题，所以需要通过计算比例的方式即可得到结果
   df.groupby(["has_cancer", "test_result"]).size() / df.groupby("has_cancer").size()
   
   # output
   has_cancer  test_result
   False       Negative       0.796396
               Positive       0.203604
   True        Negative       0.094771
               Positive       0.905229
   dtype: float64
   ```

2. **Bootstrap** 抽样——自学

   自助法抽样是进行的 **有放回地抽样**——自助法抽取的样本量和原样本样本量可以相同。如果我们收到的样本比较小，那么会不会因为偶然性的原因使得根据样本的统计值推算总体参数变得不准确呢。这种情况下可以使用自助法（Bootstrap）得到较好的结果。Bootstrap是现代统计学较为流行的一种统计方法，在小样本时效果很好。

   ```python
   # 一般的有放回抽样，对数据 data 进行有放回抽取 n 个样本，DataFrame 可以通过 sample 方法进行抽样
   data_sample = df.sample(n=n, replace=True)
   
   # 自助法是对抽取到的样本进行 z 次重复有放回的抽取 data_sample 中 n 个样本；下面的方法是计算了样本平均值统计量
   bootsample = []
   for _ in range(z):
   	bootsample.append(data_sample.sample(n=n, replace=True).mean())
   ```

3. Python 的计算统计检验值

   * 配对 t 检验 

     在 Scipy 中有统计学模块可以直接计算出统计检验值，例如 [ttest_rel](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_rel.html#scipy.stats.ttest_rel) 可以计算配对样本 t 检验（注意⚠️，这个是双尾检验的结果，对于单尾检验需要将结果除以 2）

   * 独立样本 t 检验

     在[statsmodels.stats.weightstats.ttest_ind ](https://www.statsmodels.org/dev/generated/statsmodels.stats.weightstats.ttest_ind.html)（可以申明单尾 t 检验还是双尾 t 检验），以及[ttest_ind](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.ttest_ind.html#scipy.stats.ttest_ind) 

   更多方法可以参考 [Statistical functions (scipy.stats) ](https://docs.scipy.org/doc/scipy/reference/stats.html)

## $\rm A$. 参考

1. 商务与经济统计
2. [One-Sample z-test](https://www.cliffsnotes.com/study-guides/statistics/univariate-inferential-tests/one-sample-z-test) 