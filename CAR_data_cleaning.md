
_By: Tarique Hasheem_

__Programmatically Manipulating Data__

I will demonstrate how to programmatically manipulate data with the Python Programming Language.  This demonstration will include the use of:

* Functions
* Pandas
* String manipulations
* Slicing

__The Data__

I have imported the data from the [California Association of Realtors website](https://www.car.org/marketdata/data/housingdata/).  The dataset contains median sales prices (in percentages) beginning from Jan-1990 until Dec-2017.

__The Challenge__

Without manipulating and cleaning the data we cannot perform any statistical analysis on the dataset.  The cells are strings, and these strings have a trailing '%' character denoting a percentage.  

__Importing The Data__

We will begin with importing the Pandas Library and reading the csv file into a new data frame.  To make sure the import was successful lets print a few lines from the head of the data frame.


```python
import pandas as pd

df = pd.read_csv('housing/CA_Association_Realtor.csv', index_col=0,
                na_values=['#DIV/0!'])

df.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CA*</th>
      <th>Alameda</th>
      <th>Amador</th>
      <th>Butte</th>
      <th>Calaveras</th>
      <th>Contra-Costa</th>
      <th>Del Norte</th>
      <th>El Dorado</th>
      <th>Fresno</th>
      <th>Glenn</th>
      <th>...</th>
      <th>Tehama</th>
      <th>Tulare</th>
      <th>Tuolumne</th>
      <th>Ventura</th>
      <th>Yolo</th>
      <th>Yuba</th>
      <th>Unnamed: 53</th>
      <th>Los Angeles Metropolitan Area</th>
      <th>Inland Empire</th>
      <th>S.F. Bay Area</th>
    </tr>
    <tr>
      <th>Mon-Yr</th>
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
      <th>Jan-90</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Feb-90</th>
      <td>-1.8%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-67.8%</td>
      <td>NaN</td>
      <td>-6.6%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.3%</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>11.8%</td>
      <td>NaN</td>
      <td>-4.7%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-4.0%</td>
      <td>1.8%</td>
      <td>-14.8%</td>
    </tr>
    <tr>
      <th>Mar-90</th>
      <td>-11.0%</td>
      <td>58.0%</td>
      <td>NaN</td>
      <td>26.3%</td>
      <td>NaN</td>
      <td>78.1%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.4%</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>78.9%</td>
      <td>NaN</td>
      <td>28.7%</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>23.2%</td>
      <td>32.1%</td>
      <td>32.2%</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 56 columns</p>
</div>



Now lets print the data types of these columns.


```python
df.dtypes.head()
```




    CA*          object
    Alameda      object
    Amador       object
    Butte        object
    Calaveras    object
    dtype: object



__Manipulations__

We immediately notice the columns are ```objects``` (strings).  Lets do the following:  

* Replace white space between with underscores ```_```. ex: 'San Francisco' transformed to 'San_Francisco'
* Replace dashes ```-``` with underscores ```_```.
* Replace the '```*```' character with an empty space.
* Delete the entire ```unnamed:_53``` column.

The code below will take care of these for us.


```python
df.columns = df.columns.str.lower()
df.columns = df.columns.str.replace(' ', '_')
df.columns = df.columns.str.replace('*', '')
df.columns = df.columns.str.replace('-', '_')
del df['unnamed:_53']
```

__Functions__

Here our function will replace all ```%``` characters with blank spaces and convert the cell into a float.  We will run the function on each cell individually.


```python
def ss(a):
    # a = define dataframe and column name in dot notation. ex: df.ca
    # strips '%' from strings in cells
    df[a] = df[a].str.replace('%', '').astype(float)
    
    return #df[a]
ss('ca')
ss('alameda')
ss('butte')
ss('calaveras')
ss('contra_costa')
ss('del_norte')
ss('el_dorado')
ss('fresno')
ss('glenn')
ss('humboldt')
ss('kern')
ss('lake')
ss('kings')
ss('lassen')
ss('los_angeles')
ss('madera')
ss('marin')
ss('mariposa')
ss('mendocino')
ss('merced')
ss('mono')
ss('monterey')
ss('napa')
ss('nevada')
ss('orange')
ss('placer')
ss('plumas')
ss('riverside')
ss('sacramento')
ss('san_benito')
ss('san_bernardino')
ss('san_diego')
ss('san_francisco')
ss('san_joaquin')
ss('san_luis_obispo')
ss('san_mateo')
ss('santa_barbara')
ss('santa_clara')
ss('santa_cruz')
ss('siskiyou')
ss('solano')
ss('sonoma')
ss('stanislaus')
ss('sutter')
ss('tehama')
ss('tulare')
ss('tuolumne')
ss('ventura')
ss('yolo')
ss('yuba')
# deleted column ss('unnamed:_53')
ss('los_angeles_metropolitan_area')
ss('inland_empire')
ss('s.f._bay_area')
```


```python
ss('amador')
ss('shasta')
```


```python
df.dtypes.head()

```




    ca           float64
    alameda      float64
    amador       float64
    butte        float64
    calaveras    float64
    dtype: object



We can see our data type have successfully converted into floats.  Now when we run ```describe()``` we have statistical information as output.


```python
df.describe()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ca</th>
      <th>alameda</th>
      <th>amador</th>
      <th>butte</th>
      <th>calaveras</th>
      <th>contra_costa</th>
      <th>del_norte</th>
      <th>el_dorado</th>
      <th>fresno</th>
      <th>glenn</th>
      <th>...</th>
      <th>sutter</th>
      <th>tehama</th>
      <th>tulare</th>
      <th>tuolumne</th>
      <th>ventura</th>
      <th>yolo</th>
      <th>yuba</th>
      <th>los_angeles_metropolitan_area</th>
      <th>inland_empire</th>
      <th>s.f._bay_area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>335.000000</td>
      <td>334.000000</td>
      <td>165.000000</td>
      <td>335.000000</td>
      <td>203.000000</td>
      <td>335.000000</td>
      <td>107.000000</td>
      <td>107.000000</td>
      <td>335.000000</td>
      <td>143.000000</td>
      <td>...</td>
      <td>140.000000</td>
      <td>122.000000</td>
      <td>255.000000</td>
      <td>179.000000</td>
      <td>335.000000</td>
      <td>107.000000</td>
      <td>140.000000</td>
      <td>335.000000</td>
      <td>335.000000</td>
      <td>335.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.133731</td>
      <td>2.288623</td>
      <td>3.063636</td>
      <td>3.548358</td>
      <td>3.735468</td>
      <td>2.468657</td>
      <td>8.785047</td>
      <td>2.591589</td>
      <td>1.928657</td>
      <td>9.466434</td>
      <td>...</td>
      <td>2.240000</td>
      <td>6.294262</td>
      <td>2.459608</td>
      <td>4.101676</td>
      <td>1.885970</td>
      <td>2.856075</td>
      <td>2.893571</td>
      <td>1.298209</td>
      <td>1.570746</td>
      <td>1.765373</td>
    </tr>
    <tr>
      <th>std</th>
      <td>4.581089</td>
      <td>20.874287</td>
      <td>26.011079</td>
      <td>28.485937</td>
      <td>24.960841</td>
      <td>21.984690</td>
      <td>41.637064</td>
      <td>18.557677</td>
      <td>17.979147</td>
      <td>57.124011</td>
      <td>...</td>
      <td>20.848321</td>
      <td>37.933891</td>
      <td>21.858144</td>
      <td>29.209610</td>
      <td>20.020144</td>
      <td>24.618072</td>
      <td>24.127766</td>
      <td>15.531970</td>
      <td>16.366428</td>
      <td>18.877861</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-16.000000</td>
      <td>-52.600000</td>
      <td>-43.600000</td>
      <td>-67.800000</td>
      <td>-47.500000</td>
      <td>-46.600000</td>
      <td>-76.900000</td>
      <td>-35.800000</td>
      <td>-54.000000</td>
      <td>-63.600000</td>
      <td>...</td>
      <td>-35.500000</td>
      <td>-61.200000</td>
      <td>-43.800000</td>
      <td>-70.500000</td>
      <td>-46.900000</td>
      <td>-42.500000</td>
      <td>-51.000000</td>
      <td>-32.100000</td>
      <td>-36.500000</td>
      <td>-42.300000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-2.700000</td>
      <td>-10.575000</td>
      <td>-15.400000</td>
      <td>-14.300000</td>
      <td>-15.100000</td>
      <td>-11.800000</td>
      <td>-19.400000</td>
      <td>-11.950000</td>
      <td>-9.250000</td>
      <td>-21.800000</td>
      <td>...</td>
      <td>-13.500000</td>
      <td>-21.600000</td>
      <td>-10.650000</td>
      <td>-15.050000</td>
      <td>-10.150000</td>
      <td>-11.750000</td>
      <td>-12.525000</td>
      <td>-8.500000</td>
      <td>-8.100000</td>
      <td>-8.350000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.100000</td>
      <td>-0.550000</td>
      <td>0.000000</td>
      <td>0.600000</td>
      <td>3.100000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>2.900000</td>
      <td>0.700000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>1.800000</td>
      <td>0.000000</td>
      <td>0.400000</td>
      <td>0.000000</td>
      <td>-0.700000</td>
      <td>-3.500000</td>
      <td>0.000000</td>
      <td>-0.100000</td>
      <td>0.100000</td>
      <td>-0.600000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.600000</td>
      <td>13.375000</td>
      <td>17.100000</td>
      <td>16.100000</td>
      <td>21.000000</td>
      <td>11.700000</td>
      <td>36.800000</td>
      <td>13.450000</td>
      <td>12.550000</td>
      <td>26.700000</td>
      <td>...</td>
      <td>14.725000</td>
      <td>26.600000</td>
      <td>13.900000</td>
      <td>20.750000</td>
      <td>11.800000</td>
      <td>14.000000</td>
      <td>15.825000</td>
      <td>8.800000</td>
      <td>9.200000</td>
      <td>10.550000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15.600000</td>
      <td>67.400000</td>
      <td>113.000000</td>
      <td>167.400000</td>
      <td>76.000000</td>
      <td>95.900000</td>
      <td>160.000000</td>
      <td>57.200000</td>
      <td>73.500000</td>
      <td>475.000000</td>
      <td>...</td>
      <td>73.200000</td>
      <td>160.000000</td>
      <td>78.900000</td>
      <td>150.000000</td>
      <td>68.000000</td>
      <td>90.200000</td>
      <td>121.900000</td>
      <td>56.600000</td>
      <td>60.300000</td>
      <td>62.700000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 55 columns</p>
</div>



__Slicing__

Lets slice some data.


```python
df[df.alameda >= 60].alameda
```




    Mon-Yr
    Mar-92    67.4
    Mar-15    63.0
    Mar-16    61.5
    Mar-17    66.4
    Name: alameda, dtype: float64




```python
df['Jan-17': 'Dec-17']['alameda']
```




    Mon-Yr
    Jan-17   -32.9
    Feb-17    -7.1
    Mar-17    66.4
    Apr-17     0.5
    May-17    23.9
    Jun-17    11.9
    Jul-17   -16.0
    Aug-17    12.9
    Sep-17   -20.5
    Oct-17    22.5
    Nov-17   -12.7
    Dec-17   -11.6
    Name: alameda, dtype: float64




```python
df['alameda'].tail(12)
```




    Mon-Yr
    Jan-17   -32.9
    Feb-17    -7.1
    Mar-17    66.4
    Apr-17     0.5
    May-17    23.9
    Jun-17    11.9
    Jul-17   -16.0
    Aug-17    12.9
    Sep-17   -20.5
    Oct-17    22.5
    Nov-17   -12.7
    Dec-17   -11.6
    Name: alameda, dtype: float64



__Conclusion__

Python allows us to manipulate data with ease when using the Pandas Library.  It's fun, challenging, and most importantly rewarding when it all comes together.  Thanks for viewing.

The end.
