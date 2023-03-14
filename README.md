# STAT1013-Final-Project
The repository for the CUHK STAT 1013 Final Project

STAT 1013: Data Science Toolbox

---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="MmmlnDheirEj">

# STAT 1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="3RSGle3hjSQl">

## **Background**

**Description**:

Dataset records the daily air quality index in Los Angeles and New York
city.

**Google Drive for Data Access**:
<https://drive.google.com/drive/folders/15MGB7gKBUkKotcZf5so7Nbm-Vk3bCtyy?usp=share_link>

Data Source: [World Air Quality Historical
Database](https://aqicn.org/historical/)

**Sample size**: ±3,000

**Feature documentation**:

| Feature  | Class  | Shape | Dtype      |
|:---------|:-------|:------|:-----------|
| LA date  | Tensor |       | datetime64 |
| LA pm25  | Tensor |       | float64    |
| LA o3    | Tensor |       | float64    |
| LA no2   | Tensor |       | float64    |
| LA co    | Tensor |       | float64    |
| NY date  | Tensor |       | datetime64 |
| NY pm 25 | Tensor |       | float64    |
| NY o3    | Tensor |       | float64    |
| NY no2   | Tensor |       | float64    |
| NY co    | Tensor |       | float64    |

</div>

<div class="cell markdown" id="zwm_DQtv0kcU">

## **Hypothesis**

-   Idea and Reasoning
    -   Analyze and compare the daily Air Quality Index (AQI) of Los
        Angeles and New York City from 2020-2022
    -   Find out which large city in the United States overall air
        pollution level fluctuated more during and after the pandemic.
        Also whether there are other factors & variables that affect the
        air quality in the 2 cities (wildfire, urban activities, etc)
-   Two groups to be compared:
    -   **G1**: air quality index in Los Angeles; **G2**: air quality
        index in New York city
-   Response variable to be measured:
    -   `AQI`
-   Is your response variable quantitative rather than categorical?
    -   `AQI` is quantitative data ranging from 0-500
-   Prediction on differences expected between the samples:
    -   We expect that AQI in Los Angeles will fluctuate more than New
        York City since the [California wildfires highly impacts the air
        quality](https://csl.noaa.gov/factsheets/csdWildfiresFIREX.pdf)
        and there were [multiple wildfires in
        2021](https://www.fire.ca.gov/incidents/2021/)
-   Data Collection Method:
    -   From [World Air Quality Historical
        Database](https://aqicn.org/historical/)
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) Collect data from a larger timeline or compare multiple
        cities
    -   \(ii\) Investigate other indicators of air quality
    -   \(iii\) Analyze more variables for comparison (specific time of
        national pandemic lockdowns or wildfires to analyze the before
        and after result)

</div>

<div class="cell markdown" id="eT1NGrFe_Ilk">

## **Dataset Preparation**

</div>

<div class="cell code" execution_count="13" id="6XlILPYr_L5G">

``` python
import pandas as pd
```

</div>

<div class="cell code" execution_count="14"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:73}"
id="Yf94ydaz8rH9" outputId="35f350d1-667b-4564-edcb-f0009a8a3d3b">

``` python
## Upload files
from google.colab import files
upload = files.upload()
```

<div class="output display_data">

    <IPython.core.display.HTML object>

</div>

<div class="output stream stdout">

    Saving AQI Dataset.csv to AQI Dataset.csv

</div>

</div>

<div class="cell code" execution_count="15"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="mTAwvvWPtliS" outputId="0af3c001-917f-450b-fb6c-cb5744122c61">

``` python
df= pd.read_csv('/content/sample_data/AQI Dataset.csv')
df.head(5)
```

<div class="output execute_result" execution_count="15">

          LA date  LA pm25  LA o3  LA no2  LA co     NY date  NY pm25  NY o3  \
    0  12/31/2022     16.0   27.0     3.0    1.0  12/31/2022     65.0   21.0   
    1  12/30/2022     40.0   15.0     7.0    2.0  12/30/2022     85.0    7.0   
    2  12/29/2022     37.0   13.0    19.0    3.0  12/29/2022     70.0    8.0   
    3  12/28/2022     31.0   18.0    14.0    3.0  12/28/2022     58.0    5.0   
    4  12/27/2022     53.0   21.0    13.0    3.0  12/27/2022     53.0   13.0   

       NY no2  NY co  
    0    15.0    2.0  
    1    33.0    8.0  
    2    43.0    7.0  
    3    40.0    4.0  
    4    30.0    3.0  

</div>

</div>

<div class="cell code" execution_count="16"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="KScQZYrSzEXn" outputId="14050038-5005-4aae-e0b4-c021d7fe5c51">

``` python
## Data Basic Information
df['LA date'] = pd.to_datetime(df['LA date'])
df['NY date'] = pd.to_datetime(df['NY date'])
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1458 entries, 0 to 1457
    Data columns (total 10 columns):
     #   Column   Non-Null Count  Dtype         
    ---  ------   --------------  -----         
     0   LA date  1458 non-null   datetime64[ns]
     1   LA pm25  1443 non-null   float64       
     2   LA o3    1453 non-null   float64       
     3   LA no2   1456 non-null   float64       
     4   LA co    1450 non-null   float64       
     5   NY date  1431 non-null   datetime64[ns]
     6   NY pm25  1419 non-null   float64       
     7   NY o3    906 non-null    float64       
     8   NY no2   886 non-null    float64       
     9   NY co    753 non-null    float64       
    dtypes: datetime64[ns](2), float64(8)
    memory usage: 114.0 KB

</div>

</div>

<div class="cell markdown" id="w5Fn6dZcvB-J">

### Groups to compare in the dataset

-   G1 (LA pm25)
-   G2 (NY pm25)

### First 5 records of both groups

</div>

<div class="cell code" execution_count="17"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="IttHvxNiv4a-" outputId="5f46a5ba-7253-44b4-b34c-e9dbe0862e73">

``` python
## G1 first 5 data
df[['LA date', 'LA pm25']].head(5)
```

<div class="output execute_result" execution_count="17">

         LA date  LA pm25
    0 2022-12-31     16.0
    1 2022-12-30     40.0
    2 2022-12-29     37.0
    3 2022-12-28     31.0
    4 2022-12-27     53.0

</div>

</div>

<div class="cell code" execution_count="18"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="yGwX0yAvwuGR" outputId="81d886d0-14a9-4ca7-f1cd-9ce02b7b32bf">

``` python
## G2 first 5 data
df[['NY date', 'NY pm25']].head(5)
```

<div class="output execute_result" execution_count="18">

         NY date  NY pm25
    0 2022-12-31     65.0
    1 2022-12-30     85.0
    2 2022-12-29     70.0
    3 2022-12-28     58.0
    4 2022-12-27     53.0

</div>

</div>

<div class="cell markdown" id="lmjg0UoU2fKM">

### Data Visualization

</div>

<div class="cell code" execution_count="19" id="ROZpjgHGxX4T">

``` python
import seaborn as sns
import matplotlib.pyplot as plt
```

</div>

<div class="cell code" execution_count="20"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:511}"
id="eiyJ9H3I_V7d" outputId="c7d8695d-cc83-4dae-a984-fa9d878b443a">

``` python
df.describe(include='all')
```

<div class="output stream stderr">

    <ipython-input-20-174ba9bf1a5c>:1: FutureWarning: Treating datetime data as categorical rather than numeric in `.describe` is deprecated and will be removed in a future version of pandas. Specify `datetime_is_numeric=True` to silence this warning and adopt the future behavior now.
      df.describe(include='all')

</div>

<div class="output execute_result" execution_count="20">

                        LA date      LA pm25        LA o3       LA no2  \
    count                  1458  1443.000000  1453.000000  1456.000000   
    unique                 1458          NaN          NaN          NaN   
    top     2022-12-31 00:00:00          NaN          NaN          NaN   
    freq                      1          NaN          NaN          NaN   
    first   2019-01-01 00:00:00          NaN          NaN          NaN   
    last    2022-12-31 00:00:00          NaN          NaN          NaN   
    mean                    NaN    50.325017    33.477632    15.877060   
    std                     NaN    18.180147    11.170187     8.218703   
    min                     NaN    11.000000     2.000000     1.000000   
    25%                     NaN    38.000000    27.000000     9.000000   
    50%                     NaN    50.000000    33.000000    15.000000   
    75%                     NaN    61.000000    39.000000    22.000000   
    max                     NaN   183.000000    95.000000    77.000000   

                  LA co              NY date      NY pm25       NY o3     NY no2  \
    count   1450.000000                 1431  1419.000000  906.000000  886.00000   
    unique          NaN                 1431          NaN         NaN        NaN   
    top             NaN  2022-12-31 00:00:00          NaN         NaN        NaN   
    freq            NaN                    1          NaN         NaN        NaN   
    first           NaN  2019-01-01 00:00:00          NaN         NaN        NaN   
    last            NaN  2022-12-31 00:00:00          NaN         NaN        NaN   
    mean       3.634483                  NaN    43.852713  109.575055   12.70316   
    std        2.131345                  NaN    27.435425  175.028937    7.22589   
    min        1.000000                  NaN     5.000000    1.000000    1.00000   
    25%        2.000000                  NaN    25.000000   23.000000    7.00000   
    50%        3.000000                  NaN    37.000000   32.000000   11.00000   
    75%        5.000000                  NaN    49.000000   46.000000   16.00000   
    max       14.000000                  NaN   141.000000  500.000000   43.00000   

                 NY co  
    count   753.000000  
    unique         NaN  
    top            NaN  
    freq           NaN  
    first          NaN  
    last           NaN  
    mean      1.990704  
    std       1.029443  
    min       1.000000  
    25%       1.000000  
    50%       2.000000  
    75%       2.000000  
    max       8.000000  

</div>

</div>

<div class="cell code" execution_count="21"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:541}"
id="YQF90HeZzLxJ" outputId="a227f161-ec25-4453-b768-e569b9e0da7a">

``` python
## Scatterplot of both LA pm25 & NY pm25 over time
sns.scatterplot(data=df, x='LA date', y='LA pm25')
plt.show()
sns.scatterplot(data=df, x='NY date', y='NY pm25')
plt.show()
```

<div class="output display_data">

![](209fdc415090b4bd2f756edd742f6f3bd3f0597b.png)

</div>

<div class="output display_data">

![](bca58c2253ec44fa6378881831accab07675f9d8.png)

</div>

</div>

<div class="cell code" execution_count="22"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:541}"
id="Md5NNwO_3_tT" outputId="2088e227-bed2-4abf-c82f-8560e24e80f9">

``` python
## Histogram
sns.histplot(df, x='LA pm25')
plt.show()
sns.histplot(df, x='NY pm25')
plt.show()
```

<div class="output display_data">

![](94c09c7513af6dee37d44f5c94abfd2c593b7591.png)

</div>

<div class="output display_data">

![](c52f53f3833d718077845cecce6815f6bd85de5d.png)

</div>

</div>

<div class="cell code" execution_count="23"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:541}"
id="BvFnhSWu9lMD" outputId="f2d8bb82-28ae-447f-a019-62a6f91a0ded">

``` python
## Boxplot
sns.boxplot(data=df, x='LA pm25')
plt.show()
sns.boxplot(data=df, x='NY pm25')
plt.show()
```

<div class="output display_data">

![](1e958b07e717fa2188e76fa309a2cd7001b74baa.png)

</div>

<div class="output display_data">

![](b9274c81d2b35b376765dd126e6dd4c44441b919.png)

</div>

</div>

<div class="cell markdown" id="q7VGlNAZ9xyf">

### Data Visualization Description

-   From the initial assessment, on average New York has lower levels of
    PM25 compared to Los Angeles
-   However New York has a higher frequency of high-levels PM25 in the
    period of end 2021 - beginning 2022, as seen in the scatterplot and
    the outliers in the boxplot. Where Los Angeles has relatively stable
    levels of PM25 over time.

</div>
