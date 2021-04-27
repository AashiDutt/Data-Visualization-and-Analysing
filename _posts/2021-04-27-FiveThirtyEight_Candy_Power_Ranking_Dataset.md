
**Performing Data Visulaization** usig different tools like histogram, scatterplot, linecharts etc..

**Candy Power Ranking**: Dataset Description

This folder contains the data behind the story The Ultimate Halloween Candy Power Ranking.

candy-data.csv includes attributes for each candy along with its ranking.

 For binary variables, **1 means yes, 0 means no.**

The data contains the following fields:

chocolate

fruity

caramel	

peanutalmondy	

nougat	

crispedricewafer	

hard	

bar	

pluribus	

sugarpercent	

pricepercent	

winpercent	

Find Dataset [Here](https://www.kaggle.com/fivethirtyeight/fivethirtyeight-candy-power-ranking-dataset)


```python
# imports
import pandas as pd
```


```python
my_data = pd.read_csv('candy-data.csv', index_col = 'competitorname')
```


```python
my_data.head()
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
      <th>chocolate</th>
      <th>fruity</th>
      <th>caramel</th>
      <th>peanutyalmondy</th>
      <th>nougat</th>
      <th>crispedricewafer</th>
      <th>hard</th>
      <th>bar</th>
      <th>pluribus</th>
      <th>sugarpercent</th>
      <th>pricepercent</th>
      <th>winpercent</th>
    </tr>
    <tr>
      <th>competitorname</th>
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
      <th>100 Grand</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.732</td>
      <td>0.860</td>
      <td>66.971725</td>
    </tr>
    <tr>
      <th>3 Musketeers</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.604</td>
      <td>0.511</td>
      <td>67.602936</td>
    </tr>
    <tr>
      <th>One dime</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.011</td>
      <td>0.116</td>
      <td>32.261086</td>
    </tr>
    <tr>
      <th>One quarter</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.011</td>
      <td>0.511</td>
      <td>46.116505</td>
    </tr>
    <tr>
      <th>Air Heads</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.906</td>
      <td>0.511</td>
      <td>52.341465</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline

```

# Line Chart


```python
plt.figure(figsize = (14,7))

plt.title("Candy Ranking")

sns.lineplot(data = my_data)


```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ec9cb5950>




![png](output_7_1.png)


From the above Lineplot its hard to find out the accurate win percent for any of the competitor. 

Let's try out some other plot.

# BarPlot


```python
plt.figure(figsize = (10,6))
plt.title("Bar plot for candy data")

sns.barplot(x = my_data.index, y = my_data['winpercent'])

plt.ylabel("winpercent")
```




    Text(0, 0.5, 'winpercent')




![png](output_10_1.png)


This representation is much better as you can clearly see the winpercent for each competitorname.

Let's try out plotting Heatmap for candy data.

# Heatmap


```python
plt.figure(figsize = (14,7))
plt.title("Heatmap for candy data")

sns.heatmap(data = my_data, annot= True)

plt.ylabel("competitorname")
plt.xlabel("Data")
```




    Text(0.5, 42.0, 'Data')




![png](output_13_1.png)


Heatmap doesn't seem to give some suitable outcome.

Let's try scatterplot. it depicts the winpercent vs sugarpercent.

## **Scatterplot**


```python
sns.scatterplot(x = my_data['winpercent'], y= my_data['sugarpercent'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebebbed90>




![png](output_16_1.png)



```python
# Let's distinguish based on whether candy has chocolate or not.
sns.scatterplot(x = my_data['winpercent'], y= my_data['sugarpercent'], hue = my_data['chocolate'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebeaa4b50>




![png](output_17_1.png)


Scatterplot shows that the winpercent is more if candy contains chocolate.


```python
# Let's add regression line to scatterplot
sns.regplot(x = my_data['winpercent'], y= my_data['sugarpercent'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebe9f40d0>




![png](output_19_1.png)



```python
# We can also add 2 regression lines too
sns.lmplot(x = "winpercent", y= "sugarpercent", hue = "chocolate", data = my_data)
```




    <seaborn.axisgrid.FacetGrid at 0x7f4ebe99e910>




![png](output_20_1.png)


Since, both lines have positive slope means candy having chocolate and no chocolate both have sales. Since chocolate plot overlaps no chocolate plot thus, candy having chocolate have high winpercent.

Categorical Scatter Plot

This depicts a much easier representation of candy data that has chocolate or not.


```python
sns.swarmplot(x = my_data['chocolate'], y = my_data['winpercent'])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebe8d2ed0>




![png](output_22_1.png)


We, can conclude that candy containing chocolate has higher win percent than candy that does not contain chocolate.

## **Distributions - Histograms and Density Plots**


```python
sns.distplot(a = my_data['winpercent'], kde = False)
```

    /usr/local/lib/python3.7/dist-packages/seaborn/distributions.py:2557: FutureWarning: `distplot` is a deprecated function and will be removed in a future version. Please adapt your code to use either `displot` (a figure-level function with similar flexibility) or `histplot` (an axes-level function for histograms).
      warnings.warn(msg, FutureWarning)
    




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebe8f6850>




![png](output_25_2.png)



```python
# Let's try Kernel Density estimator (KDE)
sns.kdeplot(data = my_data['winpercent'], shade = True)

# Shade colors the area under curve
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f4ebe811fd0>




![png](output_26_1.png)



```python
# we can even plot a 2D KDE plot with dark background color
sns.set_style("dark")  #darkgrid, whitegrid, dark, white, ticks
sns.jointplot(x = my_data['winpercent'], y = my_data['chocolate'], kind = "kde")
```




    <seaborn.axisgrid.JointGrid at 0x7f4ebfcdb310>




![png](output_27_1.png)



```python
# Let's add color coded plots

sns.distplot(a = my_data['sugarpercent'], label = "sugarpercent", kde = False)
sns.distplot(a = my_data['pricepercent'], label = "pricepercent", kde = False)

plt.title("color coded plot for candy data")
plt.legend()

```

    /usr/local/lib/python3.7/dist-packages/seaborn/distributions.py:2557: FutureWarning: `distplot` is a deprecated function and will be removed in a future version. Please adapt your code to use either `displot` (a figure-level function with similar flexibility) or `histplot` (an axes-level function for histograms).
      warnings.warn(msg, FutureWarning)
    




    <matplotlib.legend.Legend at 0x7f4ebbe4c810>




![png](output_28_2.png)

