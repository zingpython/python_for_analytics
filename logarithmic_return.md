
# logarithmic return


```python
import pandas as pd
import numpy as np
import datetime
import matplotlib.pyplot as plt
from datetime import date
import pandas_datareader.data as web
```


```python
start = date(2015, 1, 1)

end = date.today()
```


```python
stock = web.DataReader("TWTR", 'yahoo', start, end)
stock.info()
stock.tail()

```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 538 entries, 2015-01-02 to 2017-02-21
    Data columns (total 6 columns):
    Open         538 non-null float64
    High         538 non-null float64
    Low          538 non-null float64
    Close        538 non-null float64
    Volume       538 non-null int64
    Adj Close    538 non-null float64
    dtypes: float64(5), int64(1)
    memory usage: 29.4 KB





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>2017-02-14</th>
      <td>15.920000</td>
      <td>16.600000</td>
      <td>15.850000</td>
      <td>16.520000</td>
      <td>34709300</td>
      <td>16.520000</td>
    </tr>
    <tr>
      <th>2017-02-15</th>
      <td>16.850000</td>
      <td>16.889999</td>
      <td>16.299999</td>
      <td>16.740000</td>
      <td>35072600</td>
      <td>16.740000</td>
    </tr>
    <tr>
      <th>2017-02-16</th>
      <td>16.690001</td>
      <td>16.790001</td>
      <td>16.320000</td>
      <td>16.350000</td>
      <td>21465000</td>
      <td>16.350000</td>
    </tr>
    <tr>
      <th>2017-02-17</th>
      <td>16.360001</td>
      <td>16.629999</td>
      <td>16.360001</td>
      <td>16.620001</td>
      <td>14346600</td>
      <td>16.620001</td>
    </tr>
    <tr>
      <th>2017-02-21</th>
      <td>16.639999</td>
      <td>16.690001</td>
      <td>16.299999</td>
      <td>16.420000</td>
      <td>15931900</td>
      <td>16.420000</td>
    </tr>
  </tbody>
</table>
</div>




```python
stock["Return"] = 0.0

```


```python
stock.tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>Return</th>
    </tr>
    <tr>
      <th>Date</th>
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
      <th>2017-02-14</th>
      <td>15.920000</td>
      <td>16.600000</td>
      <td>15.850000</td>
      <td>16.520000</td>
      <td>34709300</td>
      <td>16.520000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2017-02-15</th>
      <td>16.850000</td>
      <td>16.889999</td>
      <td>16.299999</td>
      <td>16.740000</td>
      <td>35072600</td>
      <td>16.740000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2017-02-16</th>
      <td>16.690001</td>
      <td>16.790001</td>
      <td>16.320000</td>
      <td>16.350000</td>
      <td>21465000</td>
      <td>16.350000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2017-02-17</th>
      <td>16.360001</td>
      <td>16.629999</td>
      <td>16.360001</td>
      <td>16.620001</td>
      <td>14346600</td>
      <td>16.620001</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2017-02-21</th>
      <td>16.639999</td>
      <td>16.690001</td>
      <td>16.299999</td>
      <td>16.420000</td>
      <td>15931900</td>
      <td>16.420000</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
stock['Return'] = np.log(stock['Adj Close']/stock['Adj Close'].shift(1))
```


```python
stock[["Adj Close", "Return"]].tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Adj Close</th>
      <th>Return</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-02-14</th>
      <td>16.520000</td>
      <td>0.043929</td>
    </tr>
    <tr>
      <th>2017-02-15</th>
      <td>16.740000</td>
      <td>0.013229</td>
    </tr>
    <tr>
      <th>2017-02-16</th>
      <td>16.350000</td>
      <td>-0.023573</td>
    </tr>
    <tr>
      <th>2017-02-17</th>
      <td>16.620001</td>
      <td>0.016379</td>
    </tr>
    <tr>
      <th>2017-02-21</th>
      <td>16.420000</td>
      <td>-0.012107</td>
    </tr>
  </tbody>
</table>
</div>




```python
stock["Adj Close"].plot(grid=True, figsize=(8,5))
plt.show()
```


```python

```
