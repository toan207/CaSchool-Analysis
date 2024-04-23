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



### Clean data
We have a number of teachers that cannot be in decimal form, so we need to convert all values in the teacher variable into integers.


```python
data = data.astype({'teachers':'int'})
data.head()
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
      <td>10</td>
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
      <td>11</td>
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
      <td>82</td>
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
      <td>14</td>
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
      <td>71</td>
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



# Test Score Column

### Descriptive Statistics


```python
data['testscr'].describe()
```




    count    420.000000
    mean     654.156548
    std       19.053348
    min      605.550049
    25%      640.049988
    50%      654.449982
    75%      666.662506
    max      706.750000
    Name: testscr, dtype: float64



So we have:
- Mean of test scores is `653.16`
- Median of test scores is `654.449982`
- Standard Deviation of test scores is `19.053348`
- The quartiles are `640.049988`, `654.449982`, `666.662506` respectively


```python
idxMinTestScore = data['testscr'].idxmin()
idxMaxTestScore = data['testscr'].idxmax()
print(data['county'][idxMinTestScore])
print(data['county'][idxMaxTestScore])
```

    Fresno
    Santa Clara
    

So we have county with the lowest average test score, ***Fresno*** is `605.550049`  
And the highest average test score, ***Santa Clara*** is `706.750000`


```python
data['testscr'].var()
```




    363.0300564285934



We have variance of test scores is `363.0300564285934`

### Chart


```python
x = np.array(data['testscr'])
plt.hist(x)
plt.show()
```


    
![png](Untitled_files/Untitled_16_0.png)
    


***Comment:*** The shape of the data set from Caschool's test score column is most concentrated in the middle and the remaining values range symmetrically towards the extreme points -> Caschool's test score column is normally distributed


```python
sortedTestscr = sorted(data['testscr'])
cutTestscr = pd.cut(sortedTestscr,[0,621,638,655,672,689,np.inf],labels=['(604-621]','(621-638]','(638-655]','(655-672]','(672-689]','(689-706]'])
count = []
labl = []
counter = Counter(cutTestscr)

for i in counter:
    count.append(counter[i])
    labl.append(i)
    
y = np.array(count)

plt.pie(y, labels=labl)
plt.show()
```


    
![png](Untitled_files/Untitled_18_0.png)
    



```python
x = np.array(data.testscr)
y = np.array(data.str)

plt.scatter(x,y)
plt.show()
```


    
![png](Untitled_files/Untitled_19_0.png)
    



```python
data.testscr.corr(data.str)
```




    -0.2263627510868672



Then we have the correlation is `-0.2263627510868672` < 0, it means that the fewer students a teacher manages (student/teacher ratio), the higher the student's average score.  
But the correlation coefficient is only meaningful when less than -0.8 or greater than 0.8, so the correlation coefficient between these two variables is not meaningful.

# Enrollment Total Column

### Descriptive Statistics


```python
data['enrl_tot'].describe()
```




    count      420.000000
    mean      2628.792857
    std       3913.104985
    min         81.000000
    25%        379.000000
    50%        950.500000
    75%       3008.000000
    max      27176.000000
    Name: enrl_tot, dtype: float64



So we have:
- Mean of enrollment total is `2628.792857`
- Median of enrollment total is `950.500000`
- Standard Deviation of enrollment total is `3913.104985`
- The quartiles are `379.000000`, `950.500000`, `3008.000000` respectively


```python
idxMinEnrollmentTotal = data['enrl_tot'].idxmin()
idxMaxEnrollmentTotal = data['enrl_tot'].idxmax()
print(data['county'][idxMinEnrollmentTotal])
print(data['county'][idxMaxEnrollmentTotal])
```

    Sonoma
    Kern
    

So we have the county with the lowest average enrollment total is ***Sonoma***, `81.000000`
And the highest average erollment total is ***Kern***, `27176.000000`


```python
data['enrl_tot'].var()
```




    15312390.622860553



We have variance of enrollment total is `15312390.622860553`

### Chart


```python
x = np.array(data['enrl_tot'])
plt.hist(x)
plt.show()
```


    
![png](Untitled_files/Untitled_30_0.png)
    


***Comment***: The shape of data set from Caschool's enrollment total column is highest at the beginning and the remaining values decrease towards the end -> Caschool's enrollment total column is non-normal distribution.


```python
sortedEnrltot = sorted(data['enrl_tot'])
cutEnrltot = pd.cut(sortedEnrltot,[0,5499,10918,16337,21756,np.inf],labels=['(80-5499]','(5499-10918]','(10918-16337]','(16337-21756]','(21756-27175]'])
count = []
labl = []
counter = Counter(cutEnrltot)

for i in counter:
    count.append(counter[i])
    labl.append(i)
    
y = np.array(count)

plt.pie(y, labels=labl)
plt.show()
```


    
![png](Untitled_files/Untitled_32_0.png)
    



```python
x = np.array(data.enrl_tot)
y = np.array(data.computer)

plt.scatter(x,y)
plt.show()
```


    
![png](Untitled_files/Untitled_33_0.png)
    



```python
data.enrl_tot.corr(data.computer)
```




    0.9288820929667774



We have correlation is  `0.9288820929667774` > 0, it means that the higher the total enrollment, the more computers the school has.
The correlation coefficient is meaningful when less than -0.8 or greater than 0.8, so the correlation between these two variables is meaningful.

# Math Score Column

### Descriptive Statistics


```python
data['math_scr'].describe()
```




    count    420.000000
    mean     653.342619
    std       18.754202
    min      605.400024
    25%      639.375015
    50%      652.449982
    75%      665.849991
    max      709.500000
    Name: math_scr, dtype: float64



So we have:
- Mean of math score is `653.342619`
- Median of math score is `652.449982`
- Standard Deviation of math score is `18.754202`
- The quartiles are `639.375015`, `652.449982`, `665.849991` respectively


```python
idxMinMathScore = data['math_scr'].idxmin()
idxMaxMathScore = data['math_scr'].idxmax()
print(data['county'][idxMinMathScore])
print(data['county'][idxMaxMathScore])
```

    Fresno
    Santa Clara
    

So we have the county with the lowest average math score is ***Fresno***, `605.400024`
And the highest average math score is ***Sata Clara***, `709.500000`


```python
data['math_scr'].var()
```




    351.72009914605263



We have variance of math score is `351.72009914605263`

### Chart


```python
x = np.array(data['math_scr'])
plt.hist(x)
plt.show()
```


    
![png](Untitled_files/Untitled_44_0.png)
    


***Comment***: The shape of the data set is most concentrated in the middle and the remaining values range symmetrically towards the extreme points -> Caschool's math score column is normally distributed.


```python
sortedMathscr = sorted(data['math_scr'])
cutTestscr = pd.cut(sortedMathscr,[0,620,650,670,690,700,np.inf],labels=['(0-620]','(620-650]','(650-670]','(670-690]','(690-700]','(700-710]'])
count = []
labl = []
counter = Counter(cutTestscr)

for i in counter:
    count.append(counter[i])
    labl.append(i)
    
y = np.array(count)

plt.pie(y, labels=labl)
plt.show()
```


    
![png](Untitled_files/Untitled_46_0.png)
    



```python
x = np.array(data.math_scr)
y = np.array(data.meal_pct)

plt.scatter(x,y)
plt.show()
```


    
![png](Untitled_files/Untitled_47_0.png)
    



```python
data.math_scr.corr(data.meal_pct)
```




    -0.8230145180649385



We have the correlation is `-0.8230145180649385` < 0, it means that the higher the student's average math score, the fewer students are eligible for a free lunch.
The correlation coefficient is meaningful when less than -0.8 or greater than 0.8, so the correlation coefficient between these two variables is meaningful.
