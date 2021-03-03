```python
import seaborn as sns
```


```python
sns.__version__
```




    '0.11.1'




```python
import matplotlib.pyplot as plt 
import pandas as pd 
import numpy as np 
```

# Seaborn的使用结构

- seaborn的借口都是扁平的，都通过seaborn.xx()调用
- 但是借口之间有上下级关系，存在着彼此调用
- seaborn的绘图函数主要分类三类，如下所示
![image.png](https://gitee.com/panli1998/mycloudimage/raw/master/img/%E4%B8%8B%E8%BD%BD.png)
- 在每个类别中，都存在两种函数
    1. 基于坐标轴的，axes-level,简单理解就是绘制单图的函数  
        - 绘图对象是plt中的Axes
    2. 基于图的，Figure-level,简单理解就是绘制多图的函数，通过调用单图实现  
        - 绘图对象是FacetGrid
        - 对应上图中的三个顶类函数relplot，displot,catplot

# Figure-Level 绘图 displot 
- 调用数据集出现URL故障时，请参考：[链接](https://blog.csdn.net/weixin_40815637/article/details/109311371)


```python
penguin = sns.load_dataset('penguins',cache=True,data_home='../../seaborn-data')
```


```python
penguin.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>species</th>
      <th>island</th>
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.1</td>
      <td>18.7</td>
      <td>181.0</td>
      <td>3750.0</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.5</td>
      <td>17.4</td>
      <td>186.0</td>
      <td>3800.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>40.3</td>
      <td>18.0</td>
      <td>195.0</td>
      <td>3250.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>36.7</td>
      <td>19.3</td>
      <td>193.0</td>
      <td>3450.0</td>
      <td>Female</td>
    </tr>
  </tbody>
</table>
</div>



- displot是Figure级别的绘图函数，通过kind可以调用低级的hist,kde等绘图函数
- 注意与axe级别绘图不同，它的legend在图外边


```python
sns.displot(data = penguin,x = 'flipper_length_mm',hue ='species',kind='kde')
```




    <seaborn.axisgrid.FacetGrid at 0x28ab787fca0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_9_1.png)


- 通过g.ax可以获得Figure-level对象的坐标轴，并添加其他子图


```python
tips = sns.load_dataset("tips",cache=True,data_home='../../seaborn-data/')
g = sns.relplot(data=tips, x="total_bill", y="tip")
g.ax.axhline(y = 5)
```




    <matplotlib.lines.Line2D at 0x28abd00df10>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_11_1.png)


- 修改图的属性
- Figure类型的图能智能将标签应用在子图上


```python
g = sns.relplot(data=penguin, x="flipper_length_mm", y="bill_length_mm", col="sex")
g.set_axis_labels("Flipper length (mm)", "Bill length (mm)")
```




    <seaborn.axisgrid.FacetGrid at 0x28abd0d87c0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_13_1.png)


- 使用col,row等参数，可以绘制多个子图
- 在参数中，可以直接加入axe函数的参数，比如bins


```python
sns.displot(data = penguin,x = 'flipper_length_mm',hue ='species',col='species',cumulative = True,bins = 10)
```




    <seaborn.axisgrid.FacetGrid at 0x28ab74cd790>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_15_1.png)


- 通过height,aspect可以控制子图的大小和形状
- width=height*aspect
- 默认情况下，每个子图都是正方形


```python
sns.displot(data = penguin,x = 'flipper_length_mm',hue ='species',col='species'
            ,cumulative = True,bins = 10,col_wrap=1,height=4,aspect=1.2)
```




    <seaborn.axisgrid.FacetGrid at 0x28ab9ff2820>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_17_1.png)


# Axe-Level绘图 histplot直方图 
- 默认会自动通过plt.gca获得当前正在绘制的axe


```python
sns.histplot(data = penguin,x = 'flipper_length_mm',hue ='species',multiple='stack')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x28ab704ea30>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_19_1.png)


- 可以指定ax = xx来指定绘制到那个坐标轴上


```python
f,[ax1,ax2] = plt.subplots(1,2,figsize = (8,4))
sns.scatterplot(data=penguin, x="flipper_length_mm", y="bill_length_mm", hue="species",ax = ax1)
sns.histplot(data=penguin, x="species", hue="species", shrink=.8, alpha=.8, legend=False, ax=ax2)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x28aba4c55e0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_21_1.png)


- kde分布拟合图


```python
sns.kdeplot(data = penguin,x = 'flipper_length_mm',hue ='species')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x28ab6ac77c0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_23_1.png)


# 在同一张图上绘制多个视图

## joinplot
- 在坐标轴上绘制变量的一维分布


```python
sns.jointplot(data=penguin,x = 'flipper_length_mm',y = 'bill_length_mm',
             hue = 'species')
```




    <seaborn.axisgrid.JointGrid at 0x28ab705ce20>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_26_1.png)


## pairplot()
- 会将所有数值型的列作为变量，两两组合绘制子图


```python
sns.pairplot(data=penguin,hue='species')
```




    <seaborn.axisgrid.PairGrid at 0x28abc62d520>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_28_1.png)


# seaborn接受的数据类型

## 长表long-table
- 每一列都是一个变量
- 每一行是一个样本（观察值）


```python
flight = sns.load_dataset('flights',cache=True,data_home='../../seaborn-data/')
flight.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>month</th>
      <th>passengers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1949</td>
      <td>Jan</td>
      <td>112</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>Feb</td>
      <td>118</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1949</td>
      <td>Mar</td>
      <td>132</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1949</td>
      <td>Apr</td>
      <td>129</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1949</td>
      <td>May</td>
      <td>121</td>
    </tr>
  </tbody>
</table>
</div>



- 通过指定数据源，x,y的列名来绘制图 
- style来指定线型


```python
sns.relplot(data=flight,x='year',y = 'passengers',hue='month',kind='line',style='month')
```




    <seaborn.axisgrid.FacetGrid at 0x23dbd6a18b0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_33_1.png)


## 宽表wide-table
- 每一个行列交汇的点是一个样本点，而变量则是index和columns
- seaborn不支持多级索引


```python
flight_wide = flight.pivot(index='year',columns='month',values='passengers')
flight_wide.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>month</th>
      <th>Jan</th>
      <th>Feb</th>
      <th>Mar</th>
      <th>Apr</th>
      <th>May</th>
      <th>Jun</th>
      <th>Jul</th>
      <th>Aug</th>
      <th>Sep</th>
      <th>Oct</th>
      <th>Nov</th>
      <th>Dec</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1949</th>
      <td>112</td>
      <td>118</td>
      <td>132</td>
      <td>129</td>
      <td>121</td>
      <td>135</td>
      <td>148</td>
      <td>148</td>
      <td>136</td>
      <td>119</td>
      <td>104</td>
      <td>118</td>
    </tr>
    <tr>
      <th>1950</th>
      <td>115</td>
      <td>126</td>
      <td>141</td>
      <td>135</td>
      <td>125</td>
      <td>149</td>
      <td>170</td>
      <td>170</td>
      <td>158</td>
      <td>133</td>
      <td>114</td>
      <td>140</td>
    </tr>
    <tr>
      <th>1951</th>
      <td>145</td>
      <td>150</td>
      <td>178</td>
      <td>163</td>
      <td>172</td>
      <td>178</td>
      <td>199</td>
      <td>199</td>
      <td>184</td>
      <td>162</td>
      <td>146</td>
      <td>166</td>
    </tr>
    <tr>
      <th>1952</th>
      <td>171</td>
      <td>180</td>
      <td>193</td>
      <td>181</td>
      <td>183</td>
      <td>218</td>
      <td>230</td>
      <td>242</td>
      <td>209</td>
      <td>191</td>
      <td>172</td>
      <td>194</td>
    </tr>
    <tr>
      <th>1953</th>
      <td>196</td>
      <td>196</td>
      <td>236</td>
      <td>235</td>
      <td>229</td>
      <td>243</td>
      <td>264</td>
      <td>272</td>
      <td>237</td>
      <td>211</td>
      <td>180</td>
      <td>201</td>
    </tr>
  </tbody>
</table>
</div>



- 宽表绘图时，会自动将index和columns当做x,y 
- 注意线性会不同


```python
sns.relplot(data=flight_wide,kind='line')
```




    <seaborn.axisgrid.FacetGrid at 0x23dbd7632b0>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_37_1.png)


- 在使用宽表时，有时候变量会不可预测
- 比如当绘制单变量的图时，你不能确定index和columns哪一个被分配给x


```python
sns.catplot(data=flight_wide, kind="box")
```




    <seaborn.axisgrid.FacetGrid at 0x23dbe14b760>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_39_1.png)


## 脏数据
- 既不是宽表也不是长表


```python
anagrams = sns.load_dataset("anagrams",cache=True,data_home='../../seaborn-data/')
anagrams
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>subidr</th>
      <th>attnr</th>
      <th>num1</th>
      <th>num2</th>
      <th>num3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>divided</td>
      <td>2</td>
      <td>4.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>divided</td>
      <td>3</td>
      <td>4.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>divided</td>
      <td>3</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>divided</td>
      <td>5</td>
      <td>7.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>divided</td>
      <td>4</td>
      <td>5.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>divided</td>
      <td>5</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>divided</td>
      <td>5</td>
      <td>4.5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>divided</td>
      <td>5</td>
      <td>7.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>divided</td>
      <td>2</td>
      <td>3.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>divided</td>
      <td>6</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>focused</td>
      <td>6</td>
      <td>5.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>focused</td>
      <td>8</td>
      <td>9.0</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>13</td>
      <td>focused</td>
      <td>6</td>
      <td>5.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>focused</td>
      <td>8</td>
      <td>8.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>focused</td>
      <td>8</td>
      <td>8.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>focused</td>
      <td>6</td>
      <td>8.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>focused</td>
      <td>7</td>
      <td>7.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>17</th>
      <td>18</td>
      <td>focused</td>
      <td>7</td>
      <td>8.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19</td>
      <td>focused</td>
      <td>5</td>
      <td>6.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20</td>
      <td>focused</td>
      <td>6</td>
      <td>6.0</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



- 绘图时要先将原表转换为宽表或者长表


```python
ana_long = anagrams.melt(id_vars=["subidr", "attnr"],var_name="solutions", value_name="score")
ana_long.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>subidr</th>
      <th>attnr</th>
      <th>solutions</th>
      <th>score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>divided</td>
      <td>num1</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>divided</td>
      <td>num1</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>divided</td>
      <td>num1</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>divided</td>
      <td>num1</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>divided</td>
      <td>num1</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.catplot(data=ana_long, x="solutions", y="score", hue="attnr", kind="point")
```




    <seaborn.axisgrid.FacetGrid at 0x23dbce31580>




![png](https://gitee.com/panli1998/mycloudimage/raw/master/img/output_44_1.png)

