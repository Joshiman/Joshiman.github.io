---

title: "json file "
date: 2020-01-29
tags: [ data science, messy data,json,  stratigraphy, wellpath  ]
header:
  image: "/images/Ideal_gas.jpg"
excerpt: "Exploratory data analysis, Data Science, Messy Data"
mathjax: "true"
---
### The objective of this work is to creat a stratigraphy data with name, its depth and its respective measured distance (md)  and true vertical distance(tvd). To do this two json file are presented.  
              1: stratigraphy.json 
              2: wellpath.json 
      
  


```python
# import the neccsary python libraries 
import pandas as pd
import numpy as np 
import json
import pprint
pp = pprint.PrettyPrinter(indent=4)
```

####  Import the json files in to pandas dataFram


```python
df_stratigraphy = pd.read_json('stratigraphy.json')
```


```python
df_stratigraphy.head(2)
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
      <th>pickDepth</th>
      <th>pickName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10097.05</td>
      <td>A_top</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10115.92</td>
      <td>A_base</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_stratigraphy.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15 entries, 0 to 14
    Data columns (total 2 columns):
    pickDepth    15 non-null float64
    pickName     15 non-null object
    dtypes: float64(1), object(1)
    memory usage: 320.0+ bytes
    


```python
df_stratigraphy['md'] = df_stratigraphy.pickDepth*0.305800 # change the pickDepth column to meter 
```


```python
df_stratigraphy.head(2)
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
      <th>pickDepth</th>
      <th>pickName</th>
      <th>md</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10097.05</td>
      <td>A_top</td>
      <td>3087.677890</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10115.92</td>
      <td>A_base</td>
      <td>3093.448336</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_stratigraphy_2 = df_stratigraphy.round()
```


```python
df_stratigraphy_2.head(2)
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
      <th>pickDepth</th>
      <th>pickName</th>
      <th>md</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10097.0</td>
      <td>A_top</td>
      <td>3088.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10116.0</td>
      <td>A_base</td>
      <td>3093.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_stratigraphy_2.columns 
```




    Index(['pickDepth', 'pickName', 'md'], dtype='object')




```python
df_well = pd.read_json('wellpath.json') # load a json file 
```


```python
df_well_2=df_well.round(2) # round to two decimal place 
```


```python
merge_md = pd.merge(df_stratigraphy_2, df_well_2,  on='md')# merge the two dataframe in one by measured distance(md)
```


```python
merge_md.head() # 
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
      <th>pickDepth</th>
      <th>pickName</th>
      <th>md</th>
      <th>azimuth</th>
      <th>dogleg</th>
      <th>east</th>
      <th>inclination</th>
      <th>north</th>
      <th>profileType</th>
      <th>reach</th>
      <th>tvd</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10097.0</td>
      <td>A_top</td>
      <td>3088.0</td>
      <td>3.10</td>
      <td>2.17</td>
      <td>11.95</td>
      <td>43.00</td>
      <td>162.47</td>
      <td>build</td>
      <td>162.91</td>
      <td>3044.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10116.0</td>
      <td>A_base</td>
      <td>3093.0</td>
      <td>3.13</td>
      <td>2.17</td>
      <td>12.13</td>
      <td>43.36</td>
      <td>165.88</td>
      <td>build</td>
      <td>166.33</td>
      <td>3048.08</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10246.0</td>
      <td>B_top</td>
      <td>3133.0</td>
      <td>6.15</td>
      <td>6.80</td>
      <td>14.39</td>
      <td>50.86</td>
      <td>194.85</td>
      <td>build</td>
      <td>195.38</td>
      <td>3075.52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10294.0</td>
      <td>B_base</td>
      <td>3148.0</td>
      <td>6.83</td>
      <td>3.66</td>
      <td>15.80</td>
      <td>53.49</td>
      <td>206.64</td>
      <td>build</td>
      <td>207.24</td>
      <td>3084.69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10412.0</td>
      <td>C_top</td>
      <td>3184.0</td>
      <td>6.27</td>
      <td>3.97</td>
      <td>19.15</td>
      <td>57.86</td>
      <td>236.17</td>
      <td>build</td>
      <td>236.95</td>
      <td>3104.98</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge_md.info() # the merged file information
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 15 entries, 0 to 14
    Data columns (total 11 columns):
    pickDepth      15 non-null float64
    pickName       15 non-null object
    md             15 non-null float64
    azimuth        15 non-null float64
    dogleg         15 non-null float64
    east           15 non-null float64
    inclination    15 non-null float64
    north          15 non-null float64
    profileType    15 non-null object
    reach          15 non-null float64
    tvd            15 non-null float64
    dtypes: float64(9), object(2)
    memory usage: 1.4+ KB
    


```python
merge_md_sorted  = merge_md.sort_values(by='md')  # sort the date by measured distance (md)
```


```python
 print(merge_md_sorted.head())
```

       pickDepth pickName      md  azimuth  dogleg   east  inclination   north  \
    0    10097.0    A_top  3088.0     3.10    2.17  11.95        43.00  162.47   
    1    10116.0   A_base  3093.0     3.13    2.17  12.13        43.36  165.88   
    2    10246.0    B_top  3133.0     6.15    6.80  14.39        50.86  194.85   
    3    10294.0   B_base  3148.0     6.83    3.66  15.80        53.49  206.64   
    4    10412.0    C_top  3184.0     6.27    3.97  19.15        57.86  236.17   
    
      profileType   reach      tvd  
    0       build  162.91  3044.43  
    1       build  166.33  3048.08  
    2       build  195.38  3075.52  
    3       build  207.24  3084.69  
    4       build  236.95  3104.98  
    


```python
final_well = merge_md_sorted[['pickName', 'md', 'tvd']] # select the relevent columns 
```


```python
final_well['depth'] = np.where(final_well.pickName.str.contains('top'),'top','bottom')# add a new depth column 
final_well
```

    C:\Users\joshi\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




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
      <th>pickName</th>
      <th>md</th>
      <th>tvd</th>
      <th>depth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A_top</td>
      <td>3088.0</td>
      <td>3044.43</td>
      <td>top</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A_base</td>
      <td>3093.0</td>
      <td>3048.08</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>2</th>
      <td>B_top</td>
      <td>3133.0</td>
      <td>3075.52</td>
      <td>top</td>
    </tr>
    <tr>
      <th>3</th>
      <td>B_base</td>
      <td>3148.0</td>
      <td>3084.69</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C_top</td>
      <td>3184.0</td>
      <td>3104.98</td>
      <td>top</td>
    </tr>
    <tr>
      <th>6</th>
      <td>C_base</td>
      <td>3190.0</td>
      <td>3108.14</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>5</th>
      <td>D_top</td>
      <td>3197.0</td>
      <td>3111.74</td>
      <td>top</td>
    </tr>
    <tr>
      <th>7</th>
      <td>D_base</td>
      <td>3217.0</td>
      <td>3121.53</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>8</th>
      <td>E_top</td>
      <td>3239.0</td>
      <td>3131.35</td>
      <td>top</td>
    </tr>
    <tr>
      <th>9</th>
      <td>E_base</td>
      <td>3294.0</td>
      <td>3150.89</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>10</th>
      <td>H_top</td>
      <td>3389.0</td>
      <td>3168.90</td>
      <td>top</td>
    </tr>
    <tr>
      <th>11</th>
      <td>H_base_ALT</td>
      <td>3549.0</td>
      <td>3179.41</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>12</th>
      <td>H_base</td>
      <td>3580.0</td>
      <td>3180.64</td>
      <td>bottom</td>
    </tr>
    <tr>
      <th>13</th>
      <td>I_top</td>
      <td>3603.0</td>
      <td>3181.46</td>
      <td>top</td>
    </tr>
    <tr>
      <th>14</th>
      <td>I_top_ALT</td>
      <td>3659.0</td>
      <td>3182.96</td>
      <td>top</td>
    </tr>
  </tbody>
</table>
</div>




```python
final=final_well.to_dict(orient = 'records')
final
```




    [{'pickName': 'A_top', 'md': 3088.0, 'tvd': 3044.43, 'depth': 'top'},
     {'pickName': 'A_base', 'md': 3093.0, 'tvd': 3048.08, 'depth': 'bottom'},
     {'pickName': 'B_top', 'md': 3133.0, 'tvd': 3075.52, 'depth': 'top'},
     {'pickName': 'B_base', 'md': 3148.0, 'tvd': 3084.69, 'depth': 'bottom'},
     {'pickName': 'C_top', 'md': 3184.0, 'tvd': 3104.98, 'depth': 'top'},
     {'pickName': 'C_base', 'md': 3190.0, 'tvd': 3108.14, 'depth': 'bottom'},
     {'pickName': 'D_top', 'md': 3197.0, 'tvd': 3111.74, 'depth': 'top'},
     {'pickName': 'D_base', 'md': 3217.0, 'tvd': 3121.53, 'depth': 'bottom'},
     {'pickName': 'E_top', 'md': 3239.0, 'tvd': 3131.35, 'depth': 'top'},
     {'pickName': 'E_base', 'md': 3294.0, 'tvd': 3150.89, 'depth': 'bottom'},
     {'pickName': 'H_top', 'md': 3389.0, 'tvd': 3168.9, 'depth': 'top'},
     {'pickName': 'H_base_ALT', 'md': 3549.0, 'tvd': 3179.41, 'depth': 'bottom'},
     {'pickName': 'H_base', 'md': 3580.0, 'tvd': 3180.64, 'depth': 'bottom'},
     {'pickName': 'I_top', 'md': 3603.0, 'tvd': 3181.46, 'depth': 'top'},
     {'pickName': 'I_top_ALT', 'md': 3659.0, 'tvd': 3182.96, 'depth': 'top'}]




```python
#alternate depth top and bottom and later we rearrange again based on the value of tvd
keyList=kl=[i['depth'] for i in final]
for k in range(len(keyList)-1):
    if keyList[k]==keyList[k+1]:
        if keyList[k]=='top':
            keyList[k+1]='bottom'
        elif keyList[k]=='bottom':
            keyList[k+1]='top'        
keyList  
```




    ['top',
     'bottom',
     'top',
     'bottom',
     'top',
     'bottom',
     'top',
     'bottom',
     'top',
     'bottom',
     'top',
     'bottom',
     'top',
     'bottom',
     'top']




```python
final_well['depth']=keyList
print(final_well)
```

          pickName      md      tvd   depth
    0        A_top  3088.0  3044.43     top
    1       A_base  3093.0  3048.08  bottom
    2        B_top  3133.0  3075.52     top
    3       B_base  3148.0  3084.69  bottom
    4        C_top  3184.0  3104.98     top
    6       C_base  3190.0  3108.14  bottom
    5        D_top  3197.0  3111.74     top
    7       D_base  3217.0  3121.53  bottom
    8        E_top  3239.0  3131.35     top
    9       E_base  3294.0  3150.89  bottom
    10       H_top  3389.0  3168.90     top
    11  H_base_ALT  3549.0  3179.41  bottom
    12      H_base  3580.0  3180.64     top
    13       I_top  3603.0  3181.46  bottom
    14   I_top_ALT  3659.0  3182.96     top
    

    C:\Users\joshi\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    


```python
well_arr = final_well.reindex(columns= ['pickName','depth', 'md', 'tvd']) # rearrange the order of the columns 
print(well_arr)

```

          pickName   depth      md      tvd
    0        A_top     top  3088.0  3044.43
    1       A_base  bottom  3093.0  3048.08
    2        B_top     top  3133.0  3075.52
    3       B_base  bottom  3148.0  3084.69
    4        C_top     top  3184.0  3104.98
    6       C_base  bottom  3190.0  3108.14
    5        D_top     top  3197.0  3111.74
    7       D_base  bottom  3217.0  3121.53
    8        E_top     top  3239.0  3131.35
    9       E_base  bottom  3294.0  3150.89
    10       H_top     top  3389.0  3168.90
    11  H_base_ALT  bottom  3549.0  3179.41
    12      H_base     top  3580.0  3180.64
    13       I_top  bottom  3603.0  3181.46
    14   I_top_ALT     top  3659.0  3182.96
    


```python
dic=well_arr.to_dict(orient = 'records')
dic
```




    [{'pickName': 'A_top', 'depth': 'top', 'md': 3088.0, 'tvd': 3044.43},
     {'pickName': 'A_base', 'depth': 'bottom', 'md': 3093.0, 'tvd': 3048.08},
     {'pickName': 'B_top', 'depth': 'top', 'md': 3133.0, 'tvd': 3075.52},
     {'pickName': 'B_base', 'depth': 'bottom', 'md': 3148.0, 'tvd': 3084.69},
     {'pickName': 'C_top', 'depth': 'top', 'md': 3184.0, 'tvd': 3104.98},
     {'pickName': 'C_base', 'depth': 'bottom', 'md': 3190.0, 'tvd': 3108.14},
     {'pickName': 'D_top', 'depth': 'top', 'md': 3197.0, 'tvd': 3111.74},
     {'pickName': 'D_base', 'depth': 'bottom', 'md': 3217.0, 'tvd': 3121.53},
     {'pickName': 'E_top', 'depth': 'top', 'md': 3239.0, 'tvd': 3131.35},
     {'pickName': 'E_base', 'depth': 'bottom', 'md': 3294.0, 'tvd': 3150.89},
     {'pickName': 'H_top', 'depth': 'top', 'md': 3389.0, 'tvd': 3168.9},
     {'pickName': 'H_base_ALT', 'depth': 'bottom', 'md': 3549.0, 'tvd': 3179.41},
     {'pickName': 'H_base', 'depth': 'top', 'md': 3580.0, 'tvd': 3180.64},
     {'pickName': 'I_top', 'depth': 'bottom', 'md': 3603.0, 'tvd': 3181.46},
     {'pickName': 'I_top_ALT', 'depth': 'top', 'md': 3659.0, 'tvd': 3182.96}]




```python
"""create a nested dictionary"""
def func1(d):
    final=list()
    for dic in d:
        temp=dict()
        temp2=dict()
        temp['pickName']=dic['pickName']
        temp['depth']=dic['depth']
        if temp['depth']=='bottom':            
            temp2['bottom']={key:dic[key] for key in list(dic)[2:] }
            temp['depth']={'bottom':temp2['bottom']}        
        else:
            temp2['top']={key:dic[key] for key in list(dic)[2:] }
            temp['depth']={'top':temp2['top']}                
        final.append(temp)
    return final

```


```python
final=func1(dic)
pp.pprint(final)
```

    [   {'depth': {'top': {'md': 3088.0, 'tvd': 3044.43}}, 'pickName': 'A_top'},
        {'depth': {'bottom': {'md': 3093.0, 'tvd': 3048.08}}, 'pickName': 'A_base'},
        {'depth': {'top': {'md': 3133.0, 'tvd': 3075.52}}, 'pickName': 'B_top'},
        {'depth': {'bottom': {'md': 3148.0, 'tvd': 3084.69}}, 'pickName': 'B_base'},
        {'depth': {'top': {'md': 3184.0, 'tvd': 3104.98}}, 'pickName': 'C_top'},
        {'depth': {'bottom': {'md': 3190.0, 'tvd': 3108.14}}, 'pickName': 'C_base'},
        {'depth': {'top': {'md': 3197.0, 'tvd': 3111.74}}, 'pickName': 'D_top'},
        {'depth': {'bottom': {'md': 3217.0, 'tvd': 3121.53}}, 'pickName': 'D_base'},
        {'depth': {'top': {'md': 3239.0, 'tvd': 3131.35}}, 'pickName': 'E_top'},
        {'depth': {'bottom': {'md': 3294.0, 'tvd': 3150.89}}, 'pickName': 'E_base'},
        {'depth': {'top': {'md': 3389.0, 'tvd': 3168.9}}, 'pickName': 'H_top'},
        {   'depth': {'bottom': {'md': 3549.0, 'tvd': 3179.41}},
            'pickName': 'H_base_ALT'},
        {'depth': {'top': {'md': 3580.0, 'tvd': 3180.64}}, 'pickName': 'H_base'},
        {'depth': {'bottom': {'md': 3603.0, 'tvd': 3181.46}}, 'pickName': 'I_top'},
        {'depth': {'top': {'md': 3659.0, 'tvd': 3182.96}}, 'pickName': 'I_top_ALT'}]
    


```python
pd.DataFrame.from_dict(final)
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
      <th>depth</th>
      <th>pickName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>{'top': {'md': 3088.0, 'tvd': 3044.43}}</td>
      <td>A_top</td>
    </tr>
    <tr>
      <th>1</th>
      <td>{'bottom': {'md': 3093.0, 'tvd': 3048.08}}</td>
      <td>A_base</td>
    </tr>
    <tr>
      <th>2</th>
      <td>{'top': {'md': 3133.0, 'tvd': 3075.52}}</td>
      <td>B_top</td>
    </tr>
    <tr>
      <th>3</th>
      <td>{'bottom': {'md': 3148.0, 'tvd': 3084.69}}</td>
      <td>B_base</td>
    </tr>
    <tr>
      <th>4</th>
      <td>{'top': {'md': 3184.0, 'tvd': 3104.98}}</td>
      <td>C_top</td>
    </tr>
    <tr>
      <th>5</th>
      <td>{'bottom': {'md': 3190.0, 'tvd': 3108.14}}</td>
      <td>C_base</td>
    </tr>
    <tr>
      <th>6</th>
      <td>{'top': {'md': 3197.0, 'tvd': 3111.74}}</td>
      <td>D_top</td>
    </tr>
    <tr>
      <th>7</th>
      <td>{'bottom': {'md': 3217.0, 'tvd': 3121.53}}</td>
      <td>D_base</td>
    </tr>
    <tr>
      <th>8</th>
      <td>{'top': {'md': 3239.0, 'tvd': 3131.35}}</td>
      <td>E_top</td>
    </tr>
    <tr>
      <th>9</th>
      <td>{'bottom': {'md': 3294.0, 'tvd': 3150.89}}</td>
      <td>E_base</td>
    </tr>
    <tr>
      <th>10</th>
      <td>{'top': {'md': 3389.0, 'tvd': 3168.9}}</td>
      <td>H_top</td>
    </tr>
    <tr>
      <th>11</th>
      <td>{'bottom': {'md': 3549.0, 'tvd': 3179.41}}</td>
      <td>H_base_ALT</td>
    </tr>
    <tr>
      <th>12</th>
      <td>{'top': {'md': 3580.0, 'tvd': 3180.64}}</td>
      <td>H_base</td>
    </tr>
    <tr>
      <th>13</th>
      <td>{'bottom': {'md': 3603.0, 'tvd': 3181.46}}</td>
      <td>I_top</td>
    </tr>
    <tr>
      <th>14</th>
      <td>{'top': {'md': 3659.0, 'tvd': 3182.96}}</td>
      <td>I_top_ALT</td>
    </tr>
  </tbody>
</table>
</div>




```python
""" make the depth of the current marker is equal to the bottom depth of the previous marker"""
def func(final):
    cc=list()
    for i in range(len(final)-1):       
        c=dict()
        if final[i]['pickName'].endswith('top'):
            c['pickName']=final[i]['pickName']
            # Merge current dic md and tvd value to dic below it
            c['depth']={**final[i]['depth'], **final[i+1]['depth']}
            cc.append(c)
        elif final[i]['pickName'].endswith('base') or final[i]['pickName'].endswith('ALT'):
            c['pickName']=final[i]['pickName']
            c['depth']={**final[i]['depth'], **final[i+1]['depth']}
            # Interchange bottom values to top and top values to bottom 
            val=list(c['depth'].values())
            c['depth']['bottom']=val[1]
            c['depth']['top']=val[0]
            cc.append(c)      
    return cc

```


```python
resp=func(final)
pp.pprint(resp)
#print(resp)
```

    [   {   'depth': {   'bottom': {'md': 3093.0, 'tvd': 3048.08},
                         'top': {'md': 3088.0, 'tvd': 3044.43}},
            'pickName': 'A_top'},
        {   'depth': {   'bottom': {'md': 3133.0, 'tvd': 3075.52},
                         'top': {'md': 3093.0, 'tvd': 3048.08}},
            'pickName': 'A_base'},
        {   'depth': {   'bottom': {'md': 3148.0, 'tvd': 3084.69},
                         'top': {'md': 3133.0, 'tvd': 3075.52}},
            'pickName': 'B_top'},
        {   'depth': {   'bottom': {'md': 3184.0, 'tvd': 3104.98},
                         'top': {'md': 3148.0, 'tvd': 3084.69}},
            'pickName': 'B_base'},
        {   'depth': {   'bottom': {'md': 3190.0, 'tvd': 3108.14},
                         'top': {'md': 3184.0, 'tvd': 3104.98}},
            'pickName': 'C_top'},
        {   'depth': {   'bottom': {'md': 3197.0, 'tvd': 3111.74},
                         'top': {'md': 3190.0, 'tvd': 3108.14}},
            'pickName': 'C_base'},
        {   'depth': {   'bottom': {'md': 3217.0, 'tvd': 3121.53},
                         'top': {'md': 3197.0, 'tvd': 3111.74}},
            'pickName': 'D_top'},
        {   'depth': {   'bottom': {'md': 3239.0, 'tvd': 3131.35},
                         'top': {'md': 3217.0, 'tvd': 3121.53}},
            'pickName': 'D_base'},
        {   'depth': {   'bottom': {'md': 3294.0, 'tvd': 3150.89},
                         'top': {'md': 3239.0, 'tvd': 3131.35}},
            'pickName': 'E_top'},
        {   'depth': {   'bottom': {'md': 3389.0, 'tvd': 3168.9},
                         'top': {'md': 3294.0, 'tvd': 3150.89}},
            'pickName': 'E_base'},
        {   'depth': {   'bottom': {'md': 3549.0, 'tvd': 3179.41},
                         'top': {'md': 3389.0, 'tvd': 3168.9}},
            'pickName': 'H_top'},
        {   'depth': {   'bottom': {'md': 3580.0, 'tvd': 3180.64},
                         'top': {'md': 3549.0, 'tvd': 3179.41}},
            'pickName': 'H_base_ALT'},
        {   'depth': {   'bottom': {'md': 3603.0, 'tvd': 3181.46},
                         'top': {'md': 3580.0, 'tvd': 3180.64}},
            'pickName': 'H_base'},
        {   'depth': {   'bottom': {'md': 3603.0, 'tvd': 3181.46},
                         'top': {'md': 3659.0, 'tvd': 3182.96}},
            'pickName': 'I_top'}]
    


```python
"""the code arrange the top and bottom on pickName H_base, which the top is larger than the bottom """
def arrangeTopAndBottom(dic):    
    for i in range(len(dic)):
        if dic[i]['depth']['bottom']['tvd']<dic[i]['depth']['top']['tvd']:
                val=list(dic[i]['depth'].values())
                #print(val)
                dic[i]['depth']['bottom']=val[1]
                dic[i]['depth']['top']=val[0] 
    return dic
    

```


```python
diff = arrangeTopAndBottom(resp)
#pp.pprint(arr_list)
print(diff)
```

    [{'pickName': 'A_top', 'depth': {'top': {'md': 3088.0, 'tvd': 3044.43}, 'bottom': {'md': 3093.0, 'tvd': 3048.08}}}, {'pickName': 'A_base', 'depth': {'bottom': {'md': 3133.0, 'tvd': 3075.52}, 'top': {'md': 3093.0, 'tvd': 3048.08}}}, {'pickName': 'B_top', 'depth': {'top': {'md': 3133.0, 'tvd': 3075.52}, 'bottom': {'md': 3148.0, 'tvd': 3084.69}}}, {'pickName': 'B_base', 'depth': {'bottom': {'md': 3184.0, 'tvd': 3104.98}, 'top': {'md': 3148.0, 'tvd': 3084.69}}}, {'pickName': 'C_top', 'depth': {'top': {'md': 3184.0, 'tvd': 3104.98}, 'bottom': {'md': 3190.0, 'tvd': 3108.14}}}, {'pickName': 'C_base', 'depth': {'bottom': {'md': 3197.0, 'tvd': 3111.74}, 'top': {'md': 3190.0, 'tvd': 3108.14}}}, {'pickName': 'D_top', 'depth': {'top': {'md': 3197.0, 'tvd': 3111.74}, 'bottom': {'md': 3217.0, 'tvd': 3121.53}}}, {'pickName': 'D_base', 'depth': {'bottom': {'md': 3239.0, 'tvd': 3131.35}, 'top': {'md': 3217.0, 'tvd': 3121.53}}}, {'pickName': 'E_top', 'depth': {'top': {'md': 3239.0, 'tvd': 3131.35}, 'bottom': {'md': 3294.0, 'tvd': 3150.89}}}, {'pickName': 'E_base', 'depth': {'bottom': {'md': 3389.0, 'tvd': 3168.9}, 'top': {'md': 3294.0, 'tvd': 3150.89}}}, {'pickName': 'H_top', 'depth': {'top': {'md': 3389.0, 'tvd': 3168.9}, 'bottom': {'md': 3549.0, 'tvd': 3179.41}}}, {'pickName': 'H_base_ALT', 'depth': {'bottom': {'md': 3580.0, 'tvd': 3180.64}, 'top': {'md': 3549.0, 'tvd': 3179.41}}}, {'pickName': 'H_base', 'depth': {'top': {'md': 3580.0, 'tvd': 3180.64}, 'bottom': {'md': 3603.0, 'tvd': 3181.46}}}, {'pickName': 'I_top', 'depth': {'bottom': {'md': 3659.0, 'tvd': 3182.96}, 'top': {'md': 3603.0, 'tvd': 3181.46}}}]
    


```python
len(diff)
```




    14




```python
"""changing the name of the bases to undifferentiated"""
for d in range(len(diff)):
    if 'base' in diff[d]['pickName']:
        diff[d]['pickName'] = 'undifferentiated'
        #print(list(diff[d].keys()))
```


```python
diff
```




    [{'pickName': 'A_top',
      'depth': {'top': {'md': 3088.0, 'tvd': 3044.43},
       'bottom': {'md': 3093.0, 'tvd': 3048.08}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3133.0, 'tvd': 3075.52},
       'top': {'md': 3093.0, 'tvd': 3048.08}}},
     {'pickName': 'B_top',
      'depth': {'top': {'md': 3133.0, 'tvd': 3075.52},
       'bottom': {'md': 3148.0, 'tvd': 3084.69}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3184.0, 'tvd': 3104.98},
       'top': {'md': 3148.0, 'tvd': 3084.69}}},
     {'pickName': 'C_top',
      'depth': {'top': {'md': 3184.0, 'tvd': 3104.98},
       'bottom': {'md': 3190.0, 'tvd': 3108.14}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3197.0, 'tvd': 3111.74},
       'top': {'md': 3190.0, 'tvd': 3108.14}}},
     {'pickName': 'D_top',
      'depth': {'top': {'md': 3197.0, 'tvd': 3111.74},
       'bottom': {'md': 3217.0, 'tvd': 3121.53}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3239.0, 'tvd': 3131.35},
       'top': {'md': 3217.0, 'tvd': 3121.53}}},
     {'pickName': 'E_top',
      'depth': {'top': {'md': 3239.0, 'tvd': 3131.35},
       'bottom': {'md': 3294.0, 'tvd': 3150.89}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3389.0, 'tvd': 3168.9},
       'top': {'md': 3294.0, 'tvd': 3150.89}}},
     {'pickName': 'H_top',
      'depth': {'top': {'md': 3389.0, 'tvd': 3168.9},
       'bottom': {'md': 3549.0, 'tvd': 3179.41}}},
     {'pickName': 'undifferentiated',
      'depth': {'bottom': {'md': 3580.0, 'tvd': 3180.64},
       'top': {'md': 3549.0, 'tvd': 3179.41}}},
     {'pickName': 'undifferentiated',
      'depth': {'top': {'md': 3580.0, 'tvd': 3180.64},
       'bottom': {'md': 3603.0, 'tvd': 3181.46}}},
     {'pickName': 'I_top',
      'depth': {'bottom': {'md': 3659.0, 'tvd': 3182.96},
       'top': {'md': 3603.0, 'tvd': 3181.46}}}]




```python

```
