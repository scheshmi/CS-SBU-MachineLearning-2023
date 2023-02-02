---
layout: default
title: Lectures 1
parent: Lectures
nav_order: 1
has_children: false
permalink: /lectures/lecture1
---

> The purpose of visualization is insight, not pictures. - Ben A. Shneiderman

Before starting visualisation, you should ask yourself for whom you're visualising the data"? 
- yourself to explore the data
- or declaring a point to someone else

> Visualization gives you answers to questions you didn’t know you had. - Ben Schneiderman

Either way, it helps:
- Analysing the data in a better way
- Simplifying complicated data to make sense of them
- And eventually accelerating the process of decision making. (persuading someone else)

> Data visualization is an aid from the beginning to the end of the typical data science pipeline. It improves the understanding and communication of the data for both data experts and end users. - Samara Vazquez Perez

But visualisation tools for exploration may vary from representation ones.

Some of useful tools are :
- [Matplotlib](https://matplotlib.org/)
- [Seaborn](https://seaborn.pydata.org/)
- [Geoplotlib](https://github.com/andrea-cuttone/geoplotlib)
- [GeoPandas](https://geopandas.org/)
- [Cartopy](https://scitools.org.uk/cartopy/docs/latest/)
- [Bokeh](http://bokeh.org/)
- [Altair](https://altair-viz.github.io/)
- [Plotnine](https://github.com/has2k1/plotnine)
- [Pygal](http://pygal.org/)
- [Plotly](https://plotly.com)
- [Missingno](https://github.com/ResidentMario/missingno)
- [Gleam](https://github.com/dgrtwo/gleam)
- [Leather](https://leather.readthedocs.io/en/0.3.3/)
- [Folium](https://python-visualization.github.io/folium/)

In this notebook we'll use `Matplotlib` and `Seaborn`.  

## First Plot with Matplotlib  


```python
import numpy as np
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
sns.set_style("dark")
sns.set(rc={'figure.figsize':(12,8)})
```


```python
x = np.linspace(0, 2, 100)
plt.figure(figsize=(10, 8), dpi=80)
plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
```




    <matplotlib.legend.Legend at 0x7f75c30e46d0>




    
![png](05-1/05-1_3_1.png)
    


For every single ['Figure'](https://matplotlib.org/stable/api/figure_api.html), always label each [`axis`](https://matplotlib.org/stable/api/axis_api.html). use title for [`axes`](https://matplotlib.org/stable/api/axes_api.html#matplotlib.axes.Axes). when there's more than one data type to draw, use legend.

## Matplotlib Object-Oriented

First, make we should make a [`Figure`](https://matplotlib.org/stable/api/figure_api.html). then we add [`axes`](https://matplotlib.org/stable/api/figure_api.html#matplotlib.figure.Figure.add_axes) to it.


```python
x = np.linspace(0, 2, 100)

fig = plt.figure(figsize=(10, 8))
fig.suptitle('A figure with subplots', fontsize=16)

ax_1 = fig.add_axes([0, 0, 1, 0.4])
ax_2 = fig.add_axes([0, 0.5, 0.4, 0.4])
ax_3 = fig.add_axes([0.5, 0.5, 0.5, 0.4])

ax_1.plot(x, x, label='linear')
ax_2.plot(x, x**2, label='quadratic')
ax_3.plot(x, x**3, label='cubic')

ax_1.set_xlabel('x')
ax_2.set_ylabel('y')
ax_3.set_title('Comparison')

ax_2.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x7f75bd73d3a0>




    
![png](05-1/05-1_7_1.png)
    


Also, we can draw a plot within another plot.


```python
x = np.linspace(0, 2, 100)

fig = plt.figure(figsize=(10, 8))

ax_1 = fig.add_axes([0, 0, 1, 1])
ax_2 = fig.add_axes([0.1, 0.5, 0.4, 0.4])

ax_1.plot(x, x**2, label='quadratic', color='orange', linestyle='dashed')
ax_1.text(1.3, 1.5, r"$y=x^2$", fontsize=20, color="orange")
ax_1.grid(True)

ax_2.plot(x, x, label='linear')
ax_2.plot(x, x**2, label='quadratic')
ax_2.plot(x, x**3, label='cubic')

ax_1.set_xlabel('x')
ax_1.set_ylabel('y')

ax_1.legend(loc='best')
ax_2.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x7f75bd60dc40>




    
![png](05-1/05-1_9_1.png)
    


For separate axes, we can easily use [`subplots()`](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.subplots.html).


```python
fig, axes = plt.subplots(nrows=1,ncols=3, figsize=(10,8))

for i in range(3):
    axes[i].plot(x, x**(i+1))
```


    
![png](05-1/05-1_11_0.png)
    


It's clear that the above figure is not intuitive. axes all sit side by side with a different scale on the y-axis. and there's no point in that figure besides didactic reason.

## Bad Visualisation

### 1. inconsistent scale


```python
x_1 = np.linspace(0, 1, 80, endpoint=False)
x_2 = np.linspace(1, 2, 20)
x = np.concatenate((x_1, x_2))
plt.figure(figsize=(10, 8), dpi=80)
plt.plot(x, label='linear')
plt.plot(x**2, label='quadratic')
plt.plot(x**3, label='cubic')
plt.xlabel('x label')
plt.xticks([0, 20, 40, 60, 80, 90, 100], [0, 0.25, 0.5, 0.75, 1, 1.5, 2])
plt.ylabel('y label')
plt.title("Simple Plot")
plt.grid(True)
plt.legend()
```




    <matplotlib.legend.Legend at 0x7f75bd3b3be0>




    
![png](05-1/05-1_15_1.png)
    


**This is broken.** in this plot the range from 1 to 2 on the x-axis is denser than the same range from 0 to 1. this easily leads you to misinterpretation. 

Don't get it wrong, it is advised to use other scales rather than linear space when it's beneficial. just be consistent and declare that the plot isn't drawn on linear space. 


```python
x = np.linspace(0, 5, 100)
fig, axes = plt.subplots(1, 2, figsize=(10,5))
      
axes[0].plot(x, x, label='linear')
axes[0].plot(x, x**2, label='quadratic')
axes[0].plot(x, x**3, label='cubic')
axes[0].plot(x, np.exp(x), label='cubic')
axes[0].set_title("Normal scale")
axes[0].grid(True)

axes[1].plot(x, x, label='linear')
axes[1].plot(x, x**2, label='quadratic')
axes[1].plot(x, x**3, label='cubic')
axes[1].plot(x, np.exp(x), label='cubic')
axes[1].set_yscale("log")
axes[1].set_title("Logarithmic scale")
axes[1].grid(True)

axes[1].legend(loc='best')
```




    <matplotlib.legend.Legend at 0x7f75bd2f1f10>




    
![png](05-1/05-1_17_1.png)
    


### 2. Wrong type of chart

- is data quantitative or qualitative?
- is quantitative continuous or discrete?


```python
flights = sns.load_dataset("flights")
flights_1957 = flights[flights.year == 1957]
flights_1957.head(12)
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
      <th>96</th>
      <td>1957</td>
      <td>Jan</td>
      <td>315</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1957</td>
      <td>Feb</td>
      <td>301</td>
    </tr>
    <tr>
      <th>98</th>
      <td>1957</td>
      <td>Mar</td>
      <td>356</td>
    </tr>
    <tr>
      <th>99</th>
      <td>1957</td>
      <td>Apr</td>
      <td>348</td>
    </tr>
    <tr>
      <th>100</th>
      <td>1957</td>
      <td>May</td>
      <td>355</td>
    </tr>
    <tr>
      <th>101</th>
      <td>1957</td>
      <td>Jun</td>
      <td>422</td>
    </tr>
    <tr>
      <th>102</th>
      <td>1957</td>
      <td>Jul</td>
      <td>465</td>
    </tr>
    <tr>
      <th>103</th>
      <td>1957</td>
      <td>Aug</td>
      <td>467</td>
    </tr>
    <tr>
      <th>104</th>
      <td>1957</td>
      <td>Sep</td>
      <td>404</td>
    </tr>
    <tr>
      <th>105</th>
      <td>1957</td>
      <td>Oct</td>
      <td>347</td>
    </tr>
    <tr>
      <th>106</th>
      <td>1957</td>
      <td>Nov</td>
      <td>305</td>
    </tr>
    <tr>
      <th>107</th>
      <td>1957</td>
      <td>Dec</td>
      <td>336</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig, axe = plt.subplots(1, figsize=(10,5))
axe.scatter(list(flights_1957.month), list(flights_1957.passengers), color='orange')
axe.plot(list(flights_1957.month), list(flights_1957.passengers), linestyle='dashed')
```




    [<matplotlib.lines.Line2D at 0x7f75bd605130>]




    
![png](05-1/05-1_20_1.png)
    


Data is not continuous. so we're not allowed to draw a line between two consecutive months.

### 3. Too many variables


```python
diamonds = sns.load_dataset("diamonds")
```


```python
fig = plt.figure(figsize=(10,8))
ax = diamonds.color.value_counts().plot(kind='pie')
```


    
![png](05-1/05-1_24_0.png)
    


Too many variables, especially in the pie chart make it useless. use other categories or bar charts.

### 4. readability


<iframe id="reddit-embed" src="https://www.redditmedia.com/r/dataisbeautiful/comments/ml9pyw/oc_dataviz_rule_0_illustrated_text_in_plots/?ref_source=embed&amp;ref=share&amp;embed=true" sandbox="allow-scripts allow-same-origin allow-popups" style="border: none;" scrolling="no" width="640" height="525"></iframe>

## Seaborn and Which Type for What Reason?
- Trends:
    - Line charts: [`seaborn.lineplot`](https://seaborn.pydata.org/generated/seaborn.lineplot.html)
- Relationship:
    - Bar charts: [`seaborn.barplot`](https://seaborn.pydata.org/generated/seaborn.barplot.html)
    - Heatmaps: [`seaborn.heatmap`](https://seaborn.pydata.org/generated/seaborn.heatmap.html)
    - Scatter plots: [`seaborn.scatterplot`](https://seaborn.pydata.org/generated/seaborn.scatterplot.html) and [`seaborn.swarmplot`](https://seaborn.pydata.org/generated/seaborn.swarmplot.html)
    - regression line: [`seaborn.regplot`](https://seaborn.pydata.org/generated/seaborn.regplot.html) and [seaborn.lmplot](https://seaborn.pydata.org/generated/seaborn.lmplot.html)
- Distribution
    - Histograms: [seaborn.displot](https://seaborn.pydata.org/generated/seaborn.displot.html) and [`seaborn.histplot`](https://seaborn.pydata.org/generated/seaborn.histplot.html)
    - KDE plots: [`seaborn.kdeplot`](https://seaborn.pydata.org/generated/seaborn.kdeplot.html) and [`seaborn.jointplot`](https://seaborn.pydata.org/generated/seaborn.jointplot.html)



```python
tips = sns.load_dataset('tips')
```

### Trends


```python
sns.lineplot(data=flights, x="year", y="passengers", hue="month")
```




    <AxesSubplot:xlabel='year', ylabel='passengers'>




    
![png](05-1/05-1_31_1.png)
    


### Relationship


```python
sns.barplot(x='sex', y='total_bill', data=tips)
```




    <AxesSubplot:xlabel='sex', ylabel='total_bill'>




    
![png](05-1/05-1_33_1.png)
    



```python
sns.boxplot(x='time', y='total_bill', data=tips)
```




    <AxesSubplot:xlabel='time', ylabel='total_bill'>




    
![png](05-1/05-1_34_1.png)
    



```python
sns.violinplot(x='time', y='total_bill', data=tips, hue='sex', split=True)
```




    <AxesSubplot:xlabel='time', ylabel='total_bill'>




    
![png](05-1/05-1_35_1.png)
    



```python
sns.lmplot(x='total_bill', y='tip', data=tips, hue='sex', height=8, aspect=1)
```




    <seaborn.axisgrid.FacetGrid at 0x7f75b970b970>




    
![png](05-1/05-1_36_1.png)
    



```python
sns.relplot(data=tips, x="total_bill", y="tip", hue="day", col="time", row="sex")
```




    <seaborn.axisgrid.FacetGrid at 0x7f75b97121f0>




    
![png](05-1/05-1_37_1.png)
    



```python
flights = sns.load_dataset('flights')
```


```python
flights_pv = flights.pivot_table(index='month', columns='year', values='passengers')
sns.heatmap(flights_pv)
```




    <AxesSubplot:xlabel='year', ylabel='month'>




    
![png](05-1/05-1_39_1.png)
    


### Distributions


```python
tips = sns.load_dataset('tips')
```


```python
tips_mean = tips.total_bill.mean()
tips_sd = tips.total_bill.std()

ax = sns.displot(data=tips, x="total_bill", kde=True, height=8)

plt.axvline(x=tips_mean, color='black', linestyle='dashed')

plt.axvline(x=tips_mean + tips_sd, color='red', linestyle='dotted')
plt.axvline(x=tips_mean - tips_sd, color='red', linestyle='dotted')

plt.title('$\mu = {}$ | $\sigma = {}$'.format(round(tips_mean, 2), round(tips_sd, 2)))
```




    Text(0.5, 1.0, '$\\mu = 19.79$ | $\\sigma = 8.9$')




    
![png](05-1/05-1_42_1.png)
    



```python
sns.jointplot(x=tips['total_bill'], y=tips['tip'], height=10)
```




    <seaborn.axisgrid.JointGrid at 0x7f75b93f5ca0>




    
![png](05-1/05-1_43_1.png)
    



```python
sns.pairplot(tips, hue='sex', height=3)
```




    <seaborn.axisgrid.PairGrid at 0x7f75b9415b50>




    
![png](05-1/05-1_44_1.png)
    


## Further readings
The first two are strongly recommended, trust me you won't regret it! :)
1. [Python Graph Gallery](https://www.python-graph-gallery.com/), A general guide for visualizing every type of data in python
1. [Data-to-Viz](https://www.data-to-viz.com)
1. [Fundamentals of Data Visualization](https://clauswilke.com/dataviz/) by Claus O. Wilke
1. [Storytelling with Data](https://www.storytellingwithdata.com/) by Cole Nussbaumer Knaflic
1. [Matplotlib Cheatsheets](https://github.com/matplotlib/cheatsheets)
