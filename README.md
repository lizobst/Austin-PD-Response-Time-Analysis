### Introduction  
For this project, Austin Police Department (APD) response times were analyzed to understand factors influencing emergency response efficiency. Response time is a critical factor in law enforcement, as it directly impacts the apprehension of criminals, the safety of victims, crime deterrence, and public trust in the police force. Faster response times can lead to improved crime resolution, better community relations, and increased effectiveness in handling emergencies. Conversely, delays in response time can have significant consequences such as increased crime severity, increased risk to victims, escalation of situations, and reduced public confidence.

#### Factors Affecting Response Time
Several factors influence police response times, including:

**Call Priority:** Higher-priority calls, such as violent crimes in progress, typically receive faster response times than lower-priority incidents like property damage or noise complaints.  
**Time of Day:** Response times may vary based on peak call volumes, with potential delays during high-traffic periods or late-night hours.
Location and Geography: The distribution of police units across the city, distance from the nearest patrol car, and accessibility of an area (urban vs. suburban) impact response efficiency.  
**Traffic Conditions:** Heavy congestion, road closures, and accidents can delay officers en route to a call.  
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
The datasets used in this analysis include APD response time data and APD crime data. These datasets were merged using the Incident ID field. To streamline the analysis, irrelevant columns were removed.

Data from the years 2003 and 2025 were excluded due to incompleteness, resulting in an analysis spanning 2004–2024. Rows with missing response time values were deleted. While outliers were identified, they were ultimately retained, as they may reflect significant anomalies in response time rather than data errors.

Several new variables were created to enhance the analysis. These include response time per sector, priority by sector, average response time, and the percentage of responses exceeding the goal.

### Exploratory Data Analysis

#### Summary Statistics

Response time:
The response time variable was analyzed to understand its distribution and variability. The dataset includes 14,780 observations.

- The mean response time is approximately 1,429 seconds (about 24 minutes), but the median response time is 594 seconds (about 10 minutes). The difference between the mean and median suggests a right-skewed distribution, likely influenced by extreme outliers.  
- The minimum response time recorded is 6 seconds, while the maximum is 60,689 seconds (approximately 16.9 hours), indicating potential extreme delays in some cases.  
- The 25th percentile (Q1) is 352 seconds (~6 minutes), and the 75th percentile (Q3) is 1,198 seconds (~20 minutes), meaning that 50% of calls had a response time between 6 and 20 minutes.  
- The standard deviation is 2,835 seconds (~47 minutes), highlighting a high degree of variability in response times.  
- The presence of extreme outliers suggests that while most incidents have a relatively quick response time, some cases experience significantly longer delays.  
  
These findings indicate that while typical response times are under 20 minutes, a subset of incidents experiences much longer delays, which could warrant further investigation into factors affecting response efficiency.

Response Time(s) per Sector:
Response times vary significantly across sectors:

- Fastest Response: The Airport sector has the shortest mean (349 sec, ~6 min) and median (240 sec, ~4 min) response times, likely due to its controlled environment.
- Slowest Response: The Edward sector has the longest mean (2,295 sec, ~38 min) and highest variability (std = 4,705 sec, ~78 min), with a maximum response time of ~16.9 hours, indicating potential inefficiencies.
- High Variability: Sectors like Henry and Edward show large gaps between mean and median times, suggesting outliers significantly impact average response times.
- Right-Skewed Distribution: Most sectors have higher means than medians, indicating that while typical response times are reasonable, extreme delays exist.
  
These findings highlight sector-specific response inefficiencies and areas for improvement in emergency response management.

Average Response Time(s) by Priority Level:
- Priority 0 = 427.942117
- Priority 1 = 540.269308
- Priority 2 = 1171.389359
- Priority 3 = 3597.243970
  
This trend aligns with expected emergency response protocols, where higher-priority incidents receive faster responses. The gap between Priority 2 and 3 suggests potential inefficiencies in handling lower-priority calls.


#### Statistical Analysis

##### Testing for Significant Differences 


**Response Time and Priority Levels:**

**Test for Normality and Homogeniety**

The Shapiro-Wilk test (normality) and Levene’s test (homogeneity of variance) were conducted for Response Time and Priority Level. Both tests returned p-values of 0, indicating significant violations of normality and equal variance assumptions. As a result, non-parametric methods will be used for further analysis.

**Significant Differences**

The Kruskal-Wallis test returned a p-value of 0, confirming significant differences in response times across priority levels.  
Dunn’s post hoc test further supports this, with all pairwise comparisons showing highly significant differences (p < 0.05). This indicates that response times vary substantially between each priority level, reinforcing the need for priority-based response time optimization.

**Boxplot**
![image](https://github.com/user-attachments/assets/b26dc865-1e88-4c21-a22d-c03ef0116b97)

The boxplot illustrates response times across priority levels, highlighting significant differences in both central tendency and variability.  
- The mean response time increases as the priority level decreases, with Priority 3 exhibiting the highest response times.
- Priority 3 shows the greatest variability, indicated by the wide interquartile range (IQR) and several potential outliers, reflecting more extreme response times.
- Priority 0, on the other hand, has the shortest and least variable response times, showing a more consistent pattern of rapid responses.  
This visual reinforces the findings from the Kruskal-Wallis and Dunn’s tests, with clear differences in response time distributions across priority levels.

**Correlation**  

Spearman’s correlation was used due to the non-normality of the data.  
- Priority Level had the strongest positive correlation with Response Time (ρ = 0.467), indicating that lower-priority incidents tend to have longer response times.  
- Number of Units Arrived showed a negative correlation (ρ = -0.36), suggesting that more responding units are associated with shorter response times.  
- All other variables had very weak correlations with response time, indicating minimal influence.  
These findings highlight the impact of incident priority and resource allocation on response efficiency.


**Response Time and Sectors:**

The Kruskal-Wallis test returned a p-value of 1.59e-82, indicating significant differences in response times across sectors.  
Dunn’s post-hoc test revealed significant pairwise differences in most sector comparisons. For example:  
- Adam and Airport (p < 0.05), Adam and Edward (p < 0.05), and Charlie and David (p < 0.05) show highly significant differences.
- Baker and Charlie (p ≈ 0.1) and Henry and Ida (p ≈ 0.1) showed weaker differences.  
Overall, the results indicate substantial variation in response times between sectors, with several pairwise comparisons showing strong statistical significance.



### Visualizations

#### Crime

![newplot (5)](https://github.com/user-attachments/assets/593601b1-8910-4808-829f-d73cf20eed2d)

Crime over time: The year 2005 saw the highest number of crimes, standing out as the peak year. Another significant spike occurred in 2012, reaching around 800 crimes. Since then, crime numbers have generally declined, with 2022 recording the lowest crime count of the period.

![newplot (11)](https://github.com/user-attachments/assets/9e9902f6-9025-4c9c-91da-482e0c42bdc9)
Common crimes: Family disturbances had the highest number of incidents by a wide margin. The second most frequent crime type had 826 incidents, while most other categories ranged between 660 and 462 incidents.

![newplot (10)](https://github.com/user-attachments/assets/eb319286-0a0f-4ed3-9f39-28fec58b808b)
Distribution of crime: The distribution of incidents shows that Priority Levels 0 and 3 have the fewest incidents, Priority Level 1 has a moderate number, while Priority Level 2 has the highest count of incidents.


#### Response Time

avg response time over years
![newplot (8)](https://github.com/user-attachments/assets/f04fa824-bac6-4f04-8078-1c778a556882)


percentage response time by year
![newplot (12)](https://github.com/user-attachments/assets/78943f8c-e464-4218-8a66-ec301fd5149d)

#### Sectors

![newplot](https://github.com/user-attachments/assets/20b9d843-302d-47a2-866f-671dcf1e2113)
Crime by Sector: Edward and David sectors reported the highest number of crimes, likely due to their larger populations and expansive areas. In contrast, Airport and George sectors had the lowest crime counts, correlating with their smaller populations and smaller areas.

top 3 crimes by sector
![newplot (4)](https://github.com/user-attachments/assets/e040fa35-f29d-4bf4-a48f-ed6fa32e707a)

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











