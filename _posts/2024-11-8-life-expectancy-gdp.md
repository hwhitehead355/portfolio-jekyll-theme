---
layout: post
title: "Life Expectancy and GDP Codecademy Project"
---

## Project Brief
This notebook was created for a Codecademy project, and the data was provided by Codecademy. The project brief was:</br>
"Try and identify the relationship between the GDP and life expectancy of six countries in the given csv."


```python
import pandas as pd
import numpy as np
import seaborn as sns
import itertools
import matplotlib.pyplot as plt
```


```python
## Read in csv and convert to DataFrame, the inspect first 5 lines and nature of data
df = pd.read_csv("all_data.csv")
print(df.head())
print(df.info())
```

      Country  Year  Life expectancy at birth (years)           GDP
    0   Chile  2000                              77.3  7.786093e+10
    1   Chile  2001                              77.3  7.097992e+10
    2   Chile  2002                              77.8  6.973681e+10
    3   Chile  2003                              77.9  7.564346e+10
    4   Chile  2004                              78.0  9.921039e+10
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 96 entries, 0 to 95
    Data columns (total 4 columns):
     #   Column                            Non-Null Count  Dtype  
    ---  ------                            --------------  -----  
     0   Country                           96 non-null     object 
     1   Year                              96 non-null     int64  
     2   Life expectancy at birth (years)  96 non-null     float64
     3   GDP                               96 non-null     float64
    dtypes: float64(2), int64(1), object(1)
    memory usage: 3.1+ KB
    None
    

All of the data seems good so far!  No missing data.  No unhelpful types.
Just need to change the column headings so that I can use them more easily.


```python
print(list(df.columns))
df.rename(columns={'Country': 'country', 'Year': 'year', 'Life expectancy at birth (years)': 'life_expectancy' ,'GDP': 'gdp' }, inplace=True)
print(list(df.columns))
```

    ['Country', 'Year', 'Life expectancy at birth (years)', 'GDP']
    ['country', 'year', 'life_expectancy', 'gdp']
    


```python
#first test a single scatter as I want it, ready to put into function

china = df[df.country == "China"]

sns.scatterplot(x = china.life_expectancy, y = china.gdp)
plt.xlabel("Life Expectancy at Birth in Years")
plt.ylabel("GDP in Trillions USD")
plt.title("China Life Expectancy vs GDP")
plt.show()
plt.close()
```


    
![png](life_expectancy_gdp_files/life_expectancy_gdp_5_0.png)
    



```python
# Dind min and max for setting unified axes to ensure like-for-like comparison

print("min life: " + str(df.life_expectancy.min()))
print("max life: " + str(df.life_expectancy.max()))
print("min gdp: " + str(df.gdp.min()))
print("max gdp: " + str(df.gdp.max()))

# Ended up not using these anyway
```

    min life: 44.3
    max life: 81.0
    min gdp: 4415702800.0
    max gdp: 18100000000000.0
    


```python
def scatter_six(df):
    country_list = df.country.unique()
    index = 1
    plt.figure(figsize = (12, 10))
    palette = itertools.cycle(sns.color_palette()) # Iterate through a cycle of colours
    for thiscountry in country_list:
        tempdf = df[df.country == thiscountry]
        plt.subplot(2,3,index)
        ax = sns.scatterplot(x = tempdf.life_expectancy, y = tempdf.gdp, color=next(palette))
        #ax.set(xlim=(44, 82))
        #ax.set(ylim=(4000000000.0, 20000000000000.0))
        plt.xlabel("Life Expectancy at Birth in Years")
        plt.ylabel("GDP in Trillions USD")
        plt.title(str(thiscountry) + " Life Expectancy vs GDP")
        index += 1
    plt.subplots_adjust(left = 0.1, bottom = 0.1, right = 0.9, top = 0.9, wspace = 0.4, hspace = 0.4)
    plt.show()
    plt.close()

scatter_six(df)

```


    
![png](life_expectancy_gdp_files/life_expectancy_gdp_7_0.png)
    


Setting the axes to be the same, to compare like with like, was a good idea and the code worked, but they're too different, hence commented out

I'm pleased with cycling through the colours.


```python

```
