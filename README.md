### Introduction  
For this project, Austin Police Department (APD) response times were analyzed to understand factors influencing emergency response efficiency. Response time is a critical factor in law enforcement, as it directly impacts the apprehension of criminals, the safety of victims, crime deterrence, and public trust in the police force. Faster response times can lead to improved crime resolution, better community relations, and increased effectiveness in handling emergencies. Conversely, delays in response time can have significant consequences such as increased crime severity, increased risk to victims, escalation of situations, and reduced public confidence.

#### Factors Affecting Response Time
Several factors influence police response times, including:

Call Priority: Higher-priority calls, such as violent crimes in progress, typically receive faster response times than lower-priority incidents like property damage or noise complaints.  
Time of Day: Response times may vary based on peak call volumes, with potential delays during high-traffic periods or late-night hours.
Location and Geography: The distribution of police units across the city, distance from the nearest patrol car, and accessibility of an area (urban vs. suburban) impact response efficiency.  
Traffic Conditions: Heavy congestion, road closures, and accidents can delay officers en route to a call.  
Staffing and Resource Allocation: The number of available officers and dispatch efficiency influence how quickly units can be assigned and deployed.  

#### Objective
The objective of this project is to identify patterns in APD response times by analyzing historical data. Key questions explored include:

- Have response times improved or worsened over time?  
- How do response times vary across different sectors?  
- What is the relationship between priority level and response time?  
- Are there any notable trends or anomalies in response times that warrant further investigation?  

#### Data Source
The primary data source for this analysis is the [Austin Police Department (APD)](https://data.austintexas.gov/), which provides publicly available records on emergency response times, APD info, crime data, and other relevant variables. 

### Data Preparation
Datasets providing information specific to APD response time as well as APD crime data utilized for this analysis. Datasets were joined utilizing Incident ID. Irrelevant columns were removed in order to simplify the analysis. 

Years 2003 and 2025 were removed due to their incompleteness. The analysis spans years 2004-2024. Rows missing response time were deleted. Outliers were calculated but ultimately not removed due to the nature of the subject and the fact that they could highlight an issue with response time. 

New variables were calculated in order to analyze the data. Variable calculations include calculating response time per sector, priority by sector, avg response time, response percentage above goal.

### Exploratory Data Analysis

#### Summary Statistics
Response Time(s):
- count    14780.000000
- mean      1429.287957
- std       2835.410496
- min          6.000000
- 25%        351.750000
- 50%        594.000000
- 75%       1198.000000
- max      60689.000000

Response Time(s) per Sector:
	
**Sector**  **mean** **median**	 **std**	  **min** **max**  **count**						
Adam	    1426.975580	  610.5	  2602.180187	  21.0	 37331.0	 1638  
Airport	  348.816667	  240.0	  374.887479	  42.0 	 3315.0	   120  
Baker	    1245.080757	  572.0	  2146.927873	  52.0	 23297.0	 1585  
Charlie	  1390.431942	  630.0	  2351.008342	  34.0	 28937.0	 1653  
David	    1028.617898	  571.0	  1580.601944	  6.0	   23194.0	 1989  
Edward	  2295.286646	  749.0	  4704.788163	  7.0	   60689.0	 2299  
Frank	    1289.965366	  587.0	  2242.236927	  7.0	   23872.0	 1819  
George	  868.389381	  389.5	  1564.728145	  32.0	 20786.0	 678  
Henry	    1476.767908	  604.0	  2916.393306	  16.0	 47192.0	 1396  
Ida	      1343.872115	  552.0	  2533.675768	  41.0	 32996.0	 1603  

Average Response Time(s) by Priority Level:
- Priority 0 = 427.942117
- Priority 1 = 540.269308
- Priority 2 = 1171.389359
- Priority 3 = 3597.243970

Average Response Time(s) by Day of the Week:
- count       7.000000
- mean     1432.181636
- std        91.187542
- min      1319.055779
- 25%      1371.875770
- 50%      1397.910251
- 75%      1499.963659
max      1564.626566

#### Statistical Analysis

##### Testing for Significant Differences 


**Response Time and Priority Levels:**

**Test for Normality and Homogeniety**

Shapiro-Wilk test and Levene's test calculated to determine normality and homogeniety of variance for Response Time and Priority Level. Results were a p-value of 0 for all tests indicating assumptions are violated for normality and homogeneity of variance. Non-parametric testing will need to be utilized.

**Significant Differences**

Kruskal-Wallis p-value = 0.

Dunn's Test results:
               0              1              2              3  
0   1.000000e+00   1.922782e-15  1.675209e-174   0.000000e+00  
1   1.922782e-15   1.000000e+00  5.049597e-118   0.000000e+00  
2  1.675209e-174  5.049597e-118   1.000000e+00  7.503423e-243  
3   0.000000e+00   0.000000e+00  7.503423e-243   1.000000e+00  

All response times have highly significant differences between each other.

**Correlation**
Correlation was calculated using Spearman's correlation due to the non normality of the data. Priority Level had the highest positive correlation to Response Time (0.467). Number of Units Arrived had a negative correlation with Response Time (-0.36). All other correlations to Response Time were very weak.

**Boxplot**
![image](https://github.com/user-attachments/assets/b26dc865-1e88-4c21-a22d-c03ef0116b97)


**Response Time and Sectors:**

Kruskal-Wallis p-value: 1.5892233294861043e-82

Dunn's Test results:
             Adam       Airport         Baker       Charlie         David  \
Adam     1.000000e+00  4.858165e-29  1.011209e-01  9.872688e-01  9.128417e-04   
Airport  4.858165e-29  1.000000e+00  4.488067e-26  4.992431e-29  7.097834e-24   
Baker    1.011209e-01  4.488067e-26  1.000000e+00  1.036757e-01  1.162920e-01   
Charlie  9.872688e-01  4.992431e-29  1.036757e-01  1.000000e+00  9.407764e-04   
David    9.128417e-04  7.097834e-24  1.162920e-01  9.407764e-04  1.000000e+00   
Edward   2.009350e-10  1.738496e-41  7.104378e-16  1.607625e-10  5.197827e-25   
Frank    1.725362e-01  7.387383e-27  7.422799e-01  1.766965e-01  4.790183e-02   
George   8.646147e-25  2.851443e-09  2.922701e-19  8.514047e-25  7.110201e-16   
Henry    2.883812e-01  8.906900e-27  6.029737e-01  2.943630e-01  3.927506e-02   
Ida      5.540310e-03  3.436446e-24  2.625235e-01  5.706411e-03  6.943164e-01   

               Edward         Frank        George         Henry           Ida  
Adam     2.009350e-10  1.725362e-01  8.646147e-25  2.883812e-01  5.540310e-03  
Airport  1.738496e-41  7.387383e-27  2.851443e-09  8.906900e-27  3.436446e-24  
Baker    7.104378e-16  7.422799e-01  2.922701e-19  6.029737e-01  2.625235e-01  
Charlie  1.607625e-10  1.766965e-01  8.514047e-25  2.943630e-01  5.706411e-03  
David    5.197827e-25  4.790183e-02  7.110201e-16  3.927506e-02  6.943164e-01  
Edward   1.000000e+00  9.390250e-16  7.744997e-54  5.978333e-13  1.215114e-20  
Frank    9.390250e-16  1.000000e+00  5.417500e-21  8.266563e-01  1.366535e-01  
George   7.744997e-54  5.417500e-21  1.000000e+00  3.486542e-20  4.647330e-16  
Henry    5.978333e-13  8.266563e-01  3.486542e-20  1.000000e+00  1.083500e-01  
Ida      1.215114e-20  1.366535e-01  4.647330e-16  1.083500e-01  1.000000e+00  

Adam and Airport: p-value = 5.86e-29 (significant difference)
Adam and David: p-value = 8.63e-04 (significant difference)
Adam and Edward: p-value = 7.48e-11 (significant difference)
Airport and David: p-value = 8.23e-24 (significant difference)
Airport and Edward: p-value = 1.36e-41 (significant difference)
Baker and Airport: p-value = 5.27e-26 (significant difference)
Charlie and David: p-value = 3.40e-04 (significant difference)
Charlie and Edward: p-value = 2.81e-10 (significant difference)
David and Edward: p-value = 7.97e-26 (significant difference)
Frank and George: p-value = 5.96e-21 (significant difference)
George and Edward: p-value = 1.72e-54 (significant difference)
George and Henry: p-value = 1.60e-20 (significant difference)
Ida and Adam: p-value = 9.45e-03 (significant difference)
Ida and Airport: p-value = 1.87e-24 (significant difference)
Ida and Edward: p-value = 1.65e-20 (significant difference)



### Visualizations

#### Crime

change in crime over time
![newplot (5)](https://github.com/user-attachments/assets/593601b1-8910-4808-829f-d73cf20eed2d)

avg crimes by day of week
![newplot (6)](https://github.com/user-attachments/assets/9e654d43-f511-4391-ae1b-5d916339c0d0)

Crime count by sector
![newplot](https://github.com/user-attachments/assets/20b9d843-302d-47a2-866f-671dcf1e2113)

10 most common crimes
![newplot (11)](https://github.com/user-attachments/assets/9e9902f6-9025-4c9c-91da-482e0c42bdc9)

top 3 crimes by sector
![newplot (4)](https://github.com/user-attachments/assets/e040fa35-f29d-4bf4-a48f-ed6fa32e707a)

number of incidents by priority level
![newplot (10)](https://github.com/user-attachments/assets/eb319286-0a0f-4ed3-9f39-28fec58b808b)



#### Response Time

avg response time over years
![newplot (8)](https://github.com/user-attachments/assets/f04fa824-bac6-4f04-8078-1c778a556882)

avg response time per day of week
![newplot (9)](https://github.com/user-attachments/assets/d96e7268-35b5-4be7-b27e-4bfaa870d915)

percentage response time by year
![newplot (12)](https://github.com/user-attachments/assets/78943f8c-e464-4218-8a66-ec301fd5149d)

#### Sectors

Distribution of priority levels by sector
![newplot (1)](https://github.com/user-attachments/assets/e497d629-49ff-4741-8c0c-c0952c712874)

avg response time by sector and priority level
![newplot (2)](https://github.com/user-attachments/assets/08677895-695a-4051-a189-b5face32d955)

percentage of responses by sector
![newplot (3)](https://github.com/user-attachments/assets/2d27ba10-b7d6-443a-8b51-4fb31815ebb4)



### Modeling

Different models were evaluated to see how the different models would perform. Feature engineering was done to evaluate the impact of different variables in the models. The models demonstrated had the best scores.

![image](https://github.com/user-attachments/assets/8abff500-6715-4efc-9521-597388ae3574)

**K-Nearest Neighbors**
Mean Absolute Error: 1451.7088194444445

**Random Forest**
Mean Absolute Error: 1296.4532956706742
Root Mean Squared Error: 2933.692422930676
R-squared: -0.08507710699404414

**Gradient Boosting**
Gradient Boosting MAE: 1223.0624007811543
Gradient Boosting RMSE: 2801.445273365412
Gradient Boosting R²: 0.010545727262362803

**XGBoost**
XGBoost MAE: 1254.6797953845726
XGBoost RMSE: 2883.304987105955
XGBoost R²: -0.04812386288333137

**Decision Tree**
Mean Squared Error: 12889602.624263845
Root Mean Squared Error: 3590.209273045771


### Discussion











