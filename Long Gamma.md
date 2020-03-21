```python
import pandas as pd
%matplotlib inline
import numpy as np
```


```python
df = pd.read_csv('/Users/JonGall45/Desktop/DIX320.csv', index_col = [0])
```


```python
df['spx50'] = df['price'].rolling(50).mean()
df['spx200']= df['price'].rolling(200).mean()
```


```python
df[['spx50', 'spx200']].plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11dd46e10>




![png](output_3_1.png)



```python
df['-GEX'] = np.where(df['gex'] < 0, 0, 1)
```


```python
df.tail()
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
      <th>price</th>
      <th>dix</th>
      <th>gex</th>
      <th>spx50</th>
      <th>spx200</th>
      <th>-GEX</th>
      <th>Long</th>
    </tr>
    <tr>
      <th>date</th>
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
      <th>3/16/20</th>
      <td>2386.13</td>
      <td>0.372537</td>
      <td>-1.758235e+09</td>
      <td>3180.4246</td>
      <td>3047.15965</td>
      <td>0</td>
      <td>-0.0</td>
    </tr>
    <tr>
      <th>3/17/20</th>
      <td>2529.09</td>
      <td>0.352458</td>
      <td>-1.153920e+09</td>
      <td>3166.3094</td>
      <td>3046.04480</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3/18/20</th>
      <td>2398.42</td>
      <td>0.354209</td>
      <td>-2.314059e+08</td>
      <td>3149.3522</td>
      <td>3044.31535</td>
      <td>0</td>
      <td>-0.0</td>
    </tr>
    <tr>
      <th>3/19/20</th>
      <td>2409.53</td>
      <td>0.353335</td>
      <td>-1.009988e+09</td>
      <td>3132.7992</td>
      <td>3042.34665</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3/20/20</th>
      <td>2304.88</td>
      <td>0.411404</td>
      <td>-6.417786e+08</td>
      <td>3113.8358</td>
      <td>3039.74030</td>
      <td>0</td>
      <td>-0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['Long'] = df['price'].pct_change(1) * df['-GEX']
```


```python
del df['StrategyPct']
```


```python
df['Long Gamma'] = (df['Long'] + 1).cumprod()
df['Buy & Hold'] = (df['price'].pct_change(1) +1).cumprod()
```


```python
df[['Long Gamma', 'Buy & Hold']].plot(figsize=(10,10))
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11e1a3650>




![png](output_9_1.png)



```python
df
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
      <th>price</th>
      <th>dix</th>
      <th>gex</th>
      <th>spx50</th>
      <th>spx200</th>
      <th>-GEX</th>
      <th>Long</th>
      <th>Long Gamma</th>
      <th>Buy &amp; Hold</th>
    </tr>
    <tr>
      <th>date</th>
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
      <th>5/2/11</th>
      <td>1361.219971</td>
      <td>0.378842</td>
      <td>1.897313e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5/3/11</th>
      <td>1356.619995</td>
      <td>0.383411</td>
      <td>1.859731e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>-0.003379</td>
      <td>0.996621</td>
      <td>0.996621</td>
    </tr>
    <tr>
      <th>5/4/11</th>
      <td>1347.319946</td>
      <td>0.392122</td>
      <td>1.717764e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>-0.006855</td>
      <td>0.989789</td>
      <td>0.989789</td>
    </tr>
    <tr>
      <th>5/5/11</th>
      <td>1335.099976</td>
      <td>0.405457</td>
      <td>1.361864e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>-0.009070</td>
      <td>0.980811</td>
      <td>0.980811</td>
    </tr>
    <tr>
      <th>5/6/11</th>
      <td>1340.199951</td>
      <td>0.418649</td>
      <td>1.490329e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>0.003820</td>
      <td>0.984558</td>
      <td>0.984558</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3/16/20</th>
      <td>2386.130000</td>
      <td>0.372537</td>
      <td>-1.758235e+09</td>
      <td>3180.4246</td>
      <td>3047.15965</td>
      <td>0</td>
      <td>-0.000000</td>
      <td>8.554854</td>
      <td>1.752935</td>
    </tr>
    <tr>
      <th>3/17/20</th>
      <td>2529.090000</td>
      <td>0.352458</td>
      <td>-1.153920e+09</td>
      <td>3166.3094</td>
      <td>3046.04480</td>
      <td>0</td>
      <td>0.000000</td>
      <td>8.554854</td>
      <td>1.857958</td>
    </tr>
    <tr>
      <th>3/18/20</th>
      <td>2398.420000</td>
      <td>0.354209</td>
      <td>-2.314059e+08</td>
      <td>3149.3522</td>
      <td>3044.31535</td>
      <td>0</td>
      <td>-0.000000</td>
      <td>8.554854</td>
      <td>1.761964</td>
    </tr>
    <tr>
      <th>3/19/20</th>
      <td>2409.530000</td>
      <td>0.353335</td>
      <td>-1.009988e+09</td>
      <td>3132.7992</td>
      <td>3042.34665</td>
      <td>0</td>
      <td>0.000000</td>
      <td>8.554854</td>
      <td>1.770125</td>
    </tr>
    <tr>
      <th>3/20/20</th>
      <td>2304.880000</td>
      <td>0.411404</td>
      <td>-6.417786e+08</td>
      <td>3113.8358</td>
      <td>3039.74030</td>
      <td>0</td>
      <td>-0.000000</td>
      <td>8.554854</td>
      <td>1.693246</td>
    </tr>
  </tbody>
</table>
<p>2236 rows × 9 columns</p>
</div>




```python
print(df)
```

                   price       dix           gex      spx50      spx200  -GEX  \
    date                                                                        
    5/2/11   1361.219971  0.378842  1.897313e+09        NaN         NaN     1   
    5/3/11   1356.619995  0.383411  1.859731e+09        NaN         NaN     1   
    5/4/11   1347.319946  0.392122  1.717764e+09        NaN         NaN     1   
    5/5/11   1335.099976  0.405457  1.361864e+09        NaN         NaN     1   
    5/6/11   1340.199951  0.418649  1.490329e+09        NaN         NaN     1   
    ...              ...       ...           ...        ...         ...   ...   
    3/16/20  2386.130000  0.372537 -1.758235e+09  3180.4246  3047.15965     0   
    3/17/20  2529.090000  0.352458 -1.153920e+09  3166.3094  3046.04480     0   
    3/18/20  2398.420000  0.354209 -2.314059e+08  3149.3522  3044.31535     0   
    3/19/20  2409.530000  0.353335 -1.009988e+09  3132.7992  3042.34665     0   
    3/20/20  2304.880000  0.411404 -6.417786e+08  3113.8358  3039.74030     0   
    
                 Long  Long Gamma  Buy & Hold  
    date                                       
    5/2/11        NaN         NaN         NaN  
    5/3/11  -0.003379    0.996621    0.996621  
    5/4/11  -0.006855    0.989789    0.989789  
    5/5/11  -0.009070    0.980811    0.980811  
    5/6/11   0.003820    0.984558    0.984558  
    ...           ...         ...         ...  
    3/16/20 -0.000000    8.554854    1.752935  
    3/17/20  0.000000    8.554854    1.857958  
    3/18/20 -0.000000    8.554854    1.761964  
    3/19/20  0.000000    8.554854    1.770125  
    3/20/20 -0.000000    8.554854    1.693246  
    
    [2236 rows x 9 columns]



```python

```
