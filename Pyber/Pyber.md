

```python
import numpy as np
import matplotlib.pyplot as plt
import os 
import csv
import pandas as pd
```


```python
csv_path_ride = os.path.join('./Resources/ride_data.csv') 
csv_path_city = os.path.join('./Resources/city_data.csv') 
ride_df = pd.read_csv(csv_path_ride)
city_df = pd.read_csv(csv_path_city)
#ride_df = pd.DataFrame(ride_df(index=False))
#city_df = pd.DataFrame(city_df(index=False))
ride_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_fare = ride_df['fare'].mean()
avg_fare
```




    26.80055157894731




```python
ride_df.describe()
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
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2375.000000</td>
      <td>2.375000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>26.800552</td>
      <td>4.865401e+12</td>
    </tr>
    <tr>
      <th>std</th>
      <td>12.007118</td>
      <td>2.899040e+12</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.050000</td>
      <td>2.238753e+09</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>17.235000</td>
      <td>2.360004e+12</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>26.450000</td>
      <td>4.821968e+12</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>36.635000</td>
      <td>7.366161e+12</td>
    </tr>
    <tr>
      <th>max</th>
      <td>59.650000</td>
      <td>9.997901e+12</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_rides_df = pd.DataFrame(ride_df['city'].value_counts())
```


```python
total_rides_df = total_rides_df.rename(columns = {'city' : 'Rides'})
total_rides_df = total_rides_df.sort_index()
total_rides = total_rides_df['Rides'].tolist()
len(total_rides)
```




    125




```python
driver_count_df = city_df.drop(['type'], axis=1)
driver_count_df = driver_count_df.sort_values('city')
driver_count = driver_count_df['driver_count'].tolist()
len(avg_fare)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-81-ab9ddd662ec1> in <module>()
          2 driver_count_df = driver_count_df.sort_values('city')
          3 driver_count = driver_count_df['driver_count'].tolist()
    ----> 4 len(avg_fare)
    

    TypeError: object of type 'float' has no len()



```python
new_df = ride_df.groupby(by='city')
new_df = new_df.mean()
new_df.head()

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
      <th>fare</th>
      <th>ride_id</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
      <td>5.351586e+12</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
      <td>3.536678e+12</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
      <td>4.195870e+12</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
      <td>5.086800e+12</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
      <td>4.574788e+12</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_fare = new_df['fare'].tolist()
y = new_df['city'].tolist()
len(avg_fare)
```




    125




```python
new_df['city'] = new_df.index
new_df.head()
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
      <th>fare</th>
      <th>ride_id</th>
      <th>city</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
      <td>5.351586e+12</td>
      <td>Alvarezhaven</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
      <td>3.536678e+12</td>
      <td>Alyssaberg</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
      <td>4.195870e+12</td>
      <td>Anitamouth</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
      <td>5.086800e+12</td>
      <td>Antoniomouth</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
      <td>4.574788e+12</td>
      <td>Aprilchester</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.scatter(total_rides, avg_fare, driver_count, alpha=0.5)
plt.title("Pyber Ride Sharing Data (2016)")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.show()
```


![png](Pyber_files/Pyber_10_0.png)



```python
print(len(avg_fare))
print(len(total_rides))
```

    125
    125
    


```python
city_df = city_df.sort_values('city')
city_df
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
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>65</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>94</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Arnoldview</td>
      <td>41</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Campbellport</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Carrollbury</td>
      <td>4</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Carrollfort</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Clarkstad</td>
      <td>21</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Conwaymouth</td>
      <td>18</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Davidtown</td>
      <td>73</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Davistown</td>
      <td>25</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>89</th>
      <td>East Cherylfurt</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>47</th>
      <td>East Erin</td>
      <td>43</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>71</th>
      <td>East Jenniferchester</td>
      <td>22</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>122</th>
      <td>East Leslie</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>121</th>
      <td>East Stephen</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>109</th>
      <td>East Troybury</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Edwardsbury</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Erikport</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Eriktown</td>
      <td>15</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Floresberg</td>
      <td>7</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Fosterside</td>
      <td>69</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Hernandezshire</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Horneland</td>
      <td>8</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Jacksonfort</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Jacobfort</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Jasonfort</td>
      <td>25</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>44</th>
      <td>South Roy</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>78</th>
      <td>South Shannonborough</td>
      <td>9</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Spencertown</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Stevensport</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Stewartview</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Swansonbury</td>
      <td>64</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>77</th>
      <td>Thomastown</td>
      <td>1</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Tiffanyton</td>
      <td>21</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Torresshire</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Travisville</td>
      <td>37</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Vickimouth</td>
      <td>13</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Webstertown</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>39</th>
      <td>West Alexis</td>
      <td>47</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>55</th>
      <td>West Brandy</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>31</th>
      <td>West Brittanyton</td>
      <td>9</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>69</th>
      <td>West Evan</td>
      <td>4</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>63</th>
      <td>West Jefferyfurt</td>
      <td>65</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>125</th>
      <td>West Kevintown</td>
      <td>5</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>52</th>
      <td>West Oscar</td>
      <td>11</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>81</th>
      <td>West Pamelaborough</td>
      <td>27</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>72</th>
      <td>West Paulport</td>
      <td>5</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>16</th>
      <td>West Peter</td>
      <td>61</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>West Sydneyhaven</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>99</th>
      <td>West Tony</td>
      <td>17</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Williamchester</td>
      <td>26</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Williamshire</td>
      <td>70</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Wiseborough</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Yolandafurt</td>
      <td>7</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Zimmermanmouth</td>
      <td>45</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
<p>126 rows × 3 columns</p>
</div>


