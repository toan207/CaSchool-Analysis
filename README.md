### Import library


```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from collections import Counter
```

### Read data from CSV file


```python
data = pd.read_csv('caschool.csv')
```

### Dataset Explaination
A data frame containing 420 observations on 14 variables.

***district:*** character. District code.  
***school:*** character. School name.  
***county:*** factor indicating county.  
***grades:*** factor indicating grade span of district.  
***students:*** Total enrollment.  
***teachers:*** Number of teachers.  
***calworks:*** Percent qualifying for CalWorks (income assistance).  
***lunch:*** Percent qualifying for reduced-price lunch.  
***computer:*** Number of computers.  
***expenditure:*** Expenditure per student.  
***income:*** District average income (in USD 1,000).  
***english:*** Percent of English learners.  
***read:*** Average reading score.  
***math:*** Average math score.  
***str:*** student teacher ratio.


```python
data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_number</th>
      <th>dist_cod</th>
      <th>county</th>
      <th>district</th>
      <th>gr_span</th>
      <th>enrl_tot</th>
      <th>teachers</th>
      <th>calw_pct</th>
      <th>meal_pct</th>
      <th>computer</th>
      <th>testscr</th>
      <th>comp_stu</th>
      <th>expn_stu</th>
      <th>str</th>
      <th>avginc</th>
      <th>el_pct</th>
      <th>read_scr</th>
      <th>math_scr</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>75119</td>
      <td>Alameda</td>
      <td>Sunol Glen Unified</td>
      <td>KK-08</td>
      <td>195</td>
      <td>10.900000</td>
      <td>0.510200</td>
      <td>2.040800</td>
      <td>67</td>
      <td>690.799988</td>
      <td>0.343590</td>
      <td>6384.911133</td>
      <td>17.889910</td>
      <td>22.690001</td>
      <td>0.000000</td>
      <td>691.599976</td>
      <td>690.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>61499</td>
      <td>Butte</td>
      <td>Manzanita Elementary</td>
      <td>KK-08</td>
      <td>240</td>
      <td>11.150000</td>
      <td>15.416700</td>
      <td>47.916698</td>
      <td>101</td>
      <td>661.200012</td>
      <td>0.420833</td>
      <td>5099.380859</td>
      <td>21.524664</td>
      <td>9.824000</td>
      <td>4.583333</td>
      <td>660.500000</td>
      <td>661.900024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>61549</td>
      <td>Butte</td>
      <td>Thermalito Union Elementary</td>
      <td>KK-08</td>
      <td>1550</td>
      <td>82.900002</td>
      <td>55.032299</td>
      <td>76.322601</td>
      <td>169</td>
      <td>643.599976</td>
      <td>0.109032</td>
      <td>5501.954590</td>
      <td>18.697226</td>
      <td>8.978000</td>
      <td>30.000002</td>
      <td>636.299988</td>
      <td>650.900024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>61457</td>
      <td>Butte</td>
      <td>Golden Feather Union Elementary</td>
      <td>KK-08</td>
      <td>243</td>
      <td>14.000000</td>
      <td>36.475399</td>
      <td>77.049202</td>
      <td>85</td>
      <td>647.700012</td>
      <td>0.349794</td>
      <td>7101.831055</td>
      <td>17.357143</td>
      <td>8.978000</td>
      <td>0.000000</td>
      <td>651.900024</td>
      <td>643.500000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>61523</td>
      <td>Butte</td>
      <td>Palermo Union Elementary</td>
      <td>KK-08</td>
      <td>1335</td>
      <td>71.500000</td>
      <td>33.108601</td>
      <td>78.427002</td>
      <td>171</td>
      <td>640.849976</td>
      <td>0.128090</td>
      <td>5235.987793</td>
      <td>18.671329</td>
      <td>9.080333</td>
      <td>13.857677</td>
      <td>641.799988</td>
      <td>639.900024</td>
    </tr>
  </tbody>
</table>
</div>
    
