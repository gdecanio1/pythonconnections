## Install and import Vertica connector:


```python
#https://github.com/vertica/vertica-python 
```


```python
import vertica_python
import pandas as pd
```

## Connect to Vertica and create a data frame out of a SQL query:


```python
conn_info = {'host': 'vertica.gold.analytics.carezen.net',
             'port': 5433,
            #replace with your username
             'user': 'geoffrey.decanio',
            #put your password here in between the quotes
             'password': 'password',
             'database': 'carezen',
             # autogenerated session label by default,
             # 'session_label': 'some_label',
             # default throw error on invalid UTF-8 results
             'unicode_error': 'strict',
             # SSL is disabled by default
             'ssl': False,
             # autocommit is off by default
             'autocommit': True,
             # using server-side prepared statements is disabled by default
             'use_prepared_statements': False,
             # connection timeout is not enabled by default
             # 5 seconds timeout for a socket operation (Establishing a TCP connection or read/write operation)
             'connection_timeout': 10}
```


```python
with vertica_python.connect(**conn_info) as conn:
    # Open a cursor to perform database operations
    # vertica-python only support one cursor per connection
    cur = conn.cursor()
    #add a SQL query
    #triple quotation marks are helpful here
    sql = """SELECT ZIP, LATITUDE, LONGITUDE, NEAR_BY_ZIP1, NEAR_BY_ZIP2 FROM reporting.DW_D_ZIP"""
    # create a data frame from the result of that query
    df_zip = pd.read_sql(sql, conn)
```

    /Users/geoffrey.decanio/Library/Python/3.8/lib/python/site-packages/pandas/io/sql.py:761: UserWarning: pandas only support SQLAlchemy connectable(engine/connection) ordatabase string URI or sqlite3 DBAPI2 connectionother DBAPI2 objects are not tested, please consider using SQLAlchemy
      warnings.warn(



```python
# view your data frame
display(df_zip)
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
      <th>ZIP</th>
      <th>LATITUDE</th>
      <th>LONGITUDE</th>
      <th>NEAR_BY_ZIP1</th>
      <th>NEAR_BY_ZIP2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00501</td>
      <td>40.8151</td>
      <td>-73.0455</td>
      <td>00544</td>
      <td>11742</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00544</td>
      <td>40.8132</td>
      <td>-73.0476</td>
      <td>00501</td>
      <td>11742</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00601</td>
      <td>18.1642</td>
      <td>-66.7227</td>
      <td>00631</td>
      <td>00641</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00602</td>
      <td>18.3974</td>
      <td>-67.1679</td>
      <td>00605</td>
      <td>00604</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00603</td>
      <td>18.4409</td>
      <td>-67.1508</td>
      <td>00604</td>
      <td>00605</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>41620</th>
      <td>99926</td>
      <td>55.1310</td>
      <td>-131.4934</td>
      <td>99928</td>
      <td>99901</td>
    </tr>
    <tr>
      <th>41621</th>
      <td>99927</td>
      <td>56.2198</td>
      <td>-133.3295</td>
      <td>99918</td>
      <td>99950</td>
    </tr>
    <tr>
      <th>41622</th>
      <td>99928</td>
      <td>55.4104</td>
      <td>-131.7237</td>
      <td>99901</td>
      <td>99926</td>
    </tr>
    <tr>
      <th>41623</th>
      <td>99929</td>
      <td>56.3147</td>
      <td>-131.7229</td>
      <td>99903</td>
      <td>99918</td>
    </tr>
    <tr>
      <th>41624</th>
      <td>99950</td>
      <td>55.8158</td>
      <td>-132.9587</td>
      <td>99918</td>
      <td>99925</td>
    </tr>
  </tbody>
</table>
<p>41625 rows × 5 columns</p>
</div>



```python

```