# STAT1013-Final-Project
The repository for the CUHK STAT 1013 Final Project


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

