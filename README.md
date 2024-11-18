java c
FIT5196-S2-2024 Assessment 2
This is a group assessment and is worth 40% of your total mark for FIT5196.
Due date: Friday 18 October 2024, 11:55pm
Task 1. Data Cleansing (50%)
For this assessment, you are required to write Python code to analyse your dataset, find and fix the problems in the data. The input and output of this task are shown below:
Table 1. The input and output of task 1

Input files
Submission
Output files
Other Deliverables
Group_dirty_data
Group_dirty_data_sol
Group_ass2_task
.csv
ution.csv
1.ipynb
Group_outlier_da
Group_outlier_data_s
Group_ass2_task
ta.csv
olution.csv
1.py
Group_missing_d
Group_missing_data_

ata.csv
solution.csv

warehouse.csv


Note1: All files must be zipped into a file named Group_ass2.zip (please use zip not rar, 7z, tar, etc.)
Note2: Replace  with your group id (do not include <>)
Note3: You can find your three input files from the folder with your group numberhere. Using the wrong files will result in zero marks.
Note4:  Please strictly follow the instructions in the appendix to generate the .ipynb and .py files.Exploring and understanding the data is one of the most important parts of the data wrangling process. You are required to perform. graphical and/or non-graphical EDA methods to understand the data first and then find the data problems. In this assessment, you have been provided with three  data  inputs  along  with  the  additional  file:  warehouse.csv  here.  Due  to  an  unexpected scenario, a portion of the data is missing or contains anomalous values. Thus, before moving to the nextstep in data analysis, you are required to perform. the following tasks:


1.   Detect and fix errors in _dirty_data.csv
2.   Impute the missing values in _missing_data.csv
3.   Detect and remove outlier rows in _outlier_data.csv
○    (w.r.t. the  delivery_charges attribute only)
Project Background
As a starting point, here is what we know about the dataset in hand:The dataset contains transactional retail data from an online electronics store (DigiCO) located in Melbourne, Australia. The store operation  is exclusively online, and it has three warehouses around Melbourne from which goods are delivered to customers.
Each instance of the data represents a single order from DigiCO store. The description of each data column is shown in Table 2.
Table 2. Description of the columns
COLUMN
DESCRIPTION
order_id
A unique id for each order
customer_id
A unique id for each customer
date
The date the order was made, given in YYYY-MM-DD format
nearest_warehouse
A string denoting the name of the nearest warehouse to the customer
shopping_cart
A list of tuples representing the order items: first element of the tuple is the item ordered, and the second element is the quantity ordered for     that item
order_price
A float denoting the order price in AUD. The order price is the price of items before any discounts and/or delivery charges are applied.
customer_lat
Latitude of the customer’s location
customer_long
Longitude of the customer’s location
coupon_discount
An integer denoting the percentage discount to be applied to the order_price.
distance_to_nearest_wa rehouse
A float representing the arc distance, in kilometres, between the customer and the nearest warehouse to him/her.
(radius of earth: 6378 KM)
delivery_charges
A float representing the delivery charges of the order
Notes:
1.   The output csv files must have the exact same columns as the respective input files. Any misspelling or mismatch will lead to a malfunction of the auto-marker which will in turn lead to losing marks.
2.   In the file  Group_dirty_data.csv, any  row can carry no more than one anomaly. (i.e. there can only be up to one issue in a single row.)
3.  All anomalies in dirty data have one and only one possible fix.
4.   There are no data anomalies in the file Group_outlier_data.csv except for outliers. Similarly,   there  are  only  coverage  data  anomalies  (i.e.  no  other  data  anomalies)  in Group_missing_data.csv.
5.   The  retail  store  has three different warehouses in Melbourne (see warehouse.csv for their locations)
6.   The retail store focuses only on 10 branded items and sells them at competitive prices7.   In order to get the item unit price, a useful python package to solve multivariable equations is
numpy.linalg
8.   The distance is calculated as Haversine Distance (with radius of earth = 6378 KM) like here  .
9.   The  store  has  different  business  rules  depending  on  the  seasons  to  match  the  different demands of each season. For example, delivery charge is calculated using a linear model which differs depending on the season. The model depends linearly (but in different ways for each season) on:
○    Distance between customer and nearest warehouse
○   Whether the customer wants an expedited delivery
○   Whether the customer was happy with his/her last purchase (if no previous purchase, it is assumed that the customer is happy)
10. It is recommended to use sklearn.linear_model.LinearRegression for solving the linear model as demonstrated in the tutorials.
11.  Using proper data for model training is crucial to have a good linear model (i.e. R2  score over 0.97 and very close to 1) to validate the delivery charges. The better your model is, the more   accurate your result will be.
12. To check whether a customer is happy with their last order, the customer's latest review is classified    using    a    sentiment    analysis    classifier.    SentimentIntensityAnalyzer   from nltk.sentiment.vader is used to obtain the polarity score. A sentiment is considered positive if it has a 'compound' polarity score of 0.05 or higher and is considered negative otherwise.Refer to thi代 写FIT5196-S2-2024 Assessment 2Python
代做程序编程语言s link for more details on how to use this module.
13. If the customer provided a coupon during purchase, the coupon discount percentage will be applied to the order price before adding the delivery charges (i.e. the delivery charges will    never be discounted).
14. The below columns are error-free (i.e. don’t look for any errors in dirty data for them):
○    coupon_discount
○    delivery_charges
○    The ordered quantity values in the shopping_cart attribute
○    order_id
○    customer_id
○    latest_customer_review
15. For missing data imputation, you are recommended to try all possible methods to impute
missing values and keep the most appropriate one that could provide the best performance.
16. As EDA is part of this assessment, no further information will be given publicly regarding the    data. However, you can brainstorm with the teaching team during tutorials or on the Ed forum.
17. No libraries/packages restriction.
Methodology (10%)
The report _ass2_task1.ipynb should demonstrate the methodology (including all steps) to achieve the correct results.
You need to demonstrate your solution using correct steps.
●    Your solution should be presented in a proper way including all required steps.
●    You need to select and use the appropriate Python functions for input, process and output.
●    Your   solution   should   be   an   efficient   one   without   redundant   operations   and unnecessary reading and writing the data.
Task 2: Data Reshaping (15%)You need to complete task 2 with the suburb_info.xlsx file ONLY. With the given property and suburb related data, you need to study the effect of different normalisation/transformation (e.g. standardisation, min-max normalisation, log, power, box-cox transformation) methods on these columns:        number_of_houses,       number_of_units,        population,        aus_born_perc, median_income, median_house_price. You need to observe and explain their effect assuming we want to develop a linear model to predict the “median_house_price” using the 5 attributes mentioned above.
When reshaping the data, we normally have two main criteria.
●    Second, we want our features to  have as much linear relationship as possible with the target variable (i.e., median_house_price).You need to first explore the data to see if any scaling or transformation is necessary (if yes why? and  if not, also why?) and then  perform. appropriate actions and document your  results and observations.  Please  note  that the aim for this task  is to  prepare the  data for   a  linear regression model, it’s not building the linear model. That is, you need to record all your steps from load the raw data to complete all the required transformations if any.
Input files
Submission
suburb_info.xlsx
Group_ass2_task2.ipynbYou could consider the scenario of task 2 to be an open exploratory project: Jackie and Kiara have got some funding to do an exploratory consulting project on the property market. We wish to understand any interesting insights from the relevant features in different suburbs of Melbourne. Before we step into the final linear regression modelling stage, we wish to hire you to prepare the data for us and tell us if any transformation/normalisation is required? Will those data satisfy the assumptions of linear regression?  How  could we  make  our data  more suitable for the  latter modelling stage.As  an  exploratory  task,  you  only  need  to  put  your  journey   of  exploration  in  proper documentation in your .ipynb file, no other output file to be submitted for task 2. We will mark based on the .ipynb content for task 2.
Table3. Description of the suburb_info.xlsx file.
suburb
The suburb name, which serves as the index of the data
number_of_houses
The number of houses in the property suburb
number_of_units
The number of units in the property suburb
municipality
The municipality of the property suburb
aus_born_perc
The percentage of the Australian-born population in the property suburb
median_income
The median income of the population in the property suburb
median_house_price
The median ‘house’ price in the property suburb
population
The population in the property suburb


Task 3: Project Reflective Report (15%)
Input files
Submission
N/A
Group_report.pdf
3.1 Feedback Session During Week 10 Applied Session
Tasks :Please attend the week 10 applied session and present your working progress to your TA for some feedback. You need to:
1.   Present your current progress
2.  Any future planning you wish to undertake
3.   Record/Noted the TA’s suggestions
4.   Continue your work with tailored solution/follow-ups based on the suggestions
Details:
●   Time/Date: Week 10, during your allocated Applied sessions
●    Duration: Approximate 5-8 minutes per group
●    Location: Normal location of allocated applied sessions in your Allocate+ records
●   Criterion: Please refer to A2 marking rubrics
3.2 Group Reflection Presentation (Hurdle)
There will be a reflective presentation for your A2. The aim for the presentation is to check    your understanding of your A2 project and make sure all submissions are compliant with the academic integrity requirements of Monash.
Details:
●   Time/Date: Week 12, during your allocated Applied sessions
●    Duration: Approximate 5-10 minutes per group
●    Location: Normal location of allocated applied sessions in your Allocate+ records
●   Arrangement: We will provide a time schedule for every group during their
allocated session, please arrive at your allocated time slot. If you arrive earlier, please wait patiently outside the room.
●   Content: Please briefly describe your methodology/ logic of A2 (at least for 80% of A2, detailed subtasks please refer to A2 marking rubrics) and answer questions if any
●   Criterion: Please refer to A2 marking rubrics





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
