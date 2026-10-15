

# Project Title: Healthcare Data Analysis and Insights  
 ## Problem Statement:  
<br> The healthcare industry generates vast amounts of data daily, providing valuable insights for 
healthcare providers and policymakers to improve patient care, allocate resources effectively, 
and manage healthcare costs. This project aims to analyze a comprehensive healthcare dataset 
comprising medical examinations, hospitalization, and customer profiles to extract 
insights into patient health profiles, medical histories, and healthcare costs. By exploring 
relationships between various health metrics, identifying trends, and visualizing key patterns, we 
aim to deliver actionable insights to healthcare stakeholders for informed decision-making 
through rigorous data cleaning, transformation, exploration, and analysis.  
## Project Steps and Objectives:  
### Data Cleaning: 
1) Check for the number of missing values marked with '?' in each column of the “Medical 
Examinations” Table and "Hospitalization Details" Table.
  <br>  While filtering the Smoker Column of  Medical Examination Sheet, have  ? in Id560,Id635.When Filtering Hospitalization sheet, Customer ID of 47th,296th,733th,2131th,2160th,2204 raw has ? Mark. In month column Id2322,id2318,Id3,Has ? Mark. In  Hospital Tier Customer ID Id324 and Customer ID of Id1793,Id170 has ? Symbol.

2) Fill in the missing values of ‘month’ with Sep and ‘year’ with its average rounded to the 
nearest integer.
<br>Select month Column-->Transform-->Replace Values-->? Replaced with Sep. Calculate average of year using =AVERAGE(B2:B2344)and Rounded average value using =ROUND(1982.842,0) and replace ? with 1983.
3) Determine the most frequently occurring values in the ‘smoker’, 'Hospital tier' and 'City 
tier' columns, and fill in the missing values accordingly.
<br>Calculate count of tier-1,tier-2,tier-3,Yes,No using COUNTIF().Apply greater count on missing values. Here Smoker column Missing value replaced with "No" value,'Hospital tier' and 'City missing column replaced with tier-2. 
4) If any 'State ID' values are missing, consider filling them with 'Unknown' or using another 
appropriate strategy.
Home-->Find&Select-->Find-->?-->Replace-->Unknown-->Replace-->Close.
### Data Transformation:   
1) Split the ‘names’ column in the “Customer Names” Table into 3 meaningful columns: 
‘Title’, ‘First Name’, and ‘Last Name’.
<br>Select Name column-->Transform-->ABC Format-->Trim-->clean.
<br>Select Name column-->Transform-->Split Column-->Demiliter-->Comma-->ok.
2) Convert the "NumberOfMajorSurgeries" column in the “Medical Examinations” Table to 
numerical data by replacing non-numeric characters with meaningful numerical values.
<br>Select NumberOfMajorSurgeries -->Transform-->Replace Values-->Value to find : NumberOfMajorSurgeries-->Replace with : 0 -->ok. 
3) Check for inconsistencies in the 'Heart Issues' and 'smoker' columns and propose 
corrective actions if necessary.
<br>While checking Medical Examination Sheet the 10th,19th,204th,319th,403th row has Diabetes ,HeartIssues,Cancer History,NumberOfMajorSurgeries same time. So Smoker Value changed Yes to No.
4) Create a new column named “Weight Status” that categorizes BMI into different 
categories as below:
#### BMI                    Weight Status
     Below 18.5             Underweight
    18.5 – 24.9             Normal Weight 
    25.0 – 29.9             Overweight
    30.0 and Above          Obesity

<br>Create a new column named “Weight Status”,and apply =IFS([@BMI]>=30,"Obesity",[@BMI]>=25,"Overweight",[@BMI]>=18.5,"Normal Weight",TRUE,"Underweight") this formula to categorize BMI.

5) Create a new column named “Diabetes Status” and fill it as per the information given 
below:  
   #### HbA1C       Diabetes Status 
    Below 5.7 -        Normal ,
    5.7 – 6.4 -        Prediabetes ,
    6.5 and Above-     Diabetes,

<br>Create a new column named “Diabetes Status” and apply =IFS([@HBA1C]>6.5,"Diabetes",[@HBA1C]>5.7,"Prediabetes",TRUE,"Normal") this formula to categorize HBA1C.
 
6) Merge ‘year’, ‘month’ and ‘date’ columns in the “Hospitalization Details” Table into one 
column named ‘Date of Birth’ and format it in ‘DD-MMM-YYYY’ custom format.

<br> Merge ‘year’, ‘month’ and ‘date’ columns to  ‘Date of Birth’and using =D4&C4&B4  formula and value formated to Date for a better arrangement of data.

7) Calculate the ‘Age’ of each customer based on their ‘Date of Birth’ and the date of 
collection of the dataset, which is 8thJune 2023.
<br>Create a column named Age and Find age using this formula:=DATEDIF(Hospitalization!$E2343,TODAY(),"Y").
8) Format ‘charges’ column as currency ($).
    <br>Select charges column -->Home-->Currency.
### Data Exploration, Analysis & Visualization:  
➢ Create a new sheet named “Healthcare", combine all three tables into one, using 
Customer ID as the common column, utilizing VLOOKUP.  
➢ Retain the following necessary columns: Customer ID, First Name, BMI, HBA1C, Heart 
Issues, Any Transplants, Cancer history, NumberOfMajorSurgeries, smoker, Weight 
Status, Diabetes Status, Date of Birth, charges, Hospital tier, City tier, State ID, Age.
<br>** By using this syntax  =VLOOKUP(lookup_value, table_array, col_index_num,
[range_lookup])  of VLOOKUP Specified column extracted and added to Healthcare sheet.
Select cntrl+A-->select cntrl+T-->specify location-->select my table has headers -->Pivot Table generated.
Create pivot tables if required to do the following analysis, then visualize through charts:  
#### Analysis using Pie/Donut Chart:  
➢ What is the distribution of cancer history among smokers and non-smokers?  
<br>Drag and drop Cancer History to raw column and smoker to value column-->change field value of smoker to count-->Pivot table generated.Select pivot table-->TableAnalyze-->PivotChart-->Select Pie chart-->OK.Analyze and add chart elements to you flavours. 
➢ How does the total number of major surgeries and average HbA1C differ between 
patients with and without a history of transplants? 
<br>create pivot table for total number of major surgeries with Transplants and average HbA1C by drag and drop .create pivot table only for total number of major surgeries and average HbA1C .Create 2 pie diagram by using this step: Select pivot table-->TableAnalyze-->PivotChart-->Select Pie chart-->OK.Analyze and add chart elements to you flavours. 
#### Analysis using Column/Bar Chart:  
➢ How do healthcare charges vary based on different weight statuses and diabetes 
statuses?  
<br>Drag and drop Diabetes status and Weight Status to raw column and  charges to value column-->change field value of smoker to Sum-->Pivot table generated.Select pivot table-->TableAnalyze-->Column/BarChart-->OK.Analyze and add chart elements to you flavours. 
➢ Can you compare the average charges for each hospital tier within different states?  
<br>create pivot table for StateID with Hospital tier and average of charges by drag and drop .Create Column/Bar chart by using this step: Select pivot table-->TableAnalyze-->Column/BarChart-->OK.Analyze and add chart elements to you flavours. 
#### Analysis using Line/Scatter Plot:  
➢ Is there any correlation between age and both BMI and HbA1C in the dataset?  
<br>Create pivot table using Age,BMI,HBA1C column and create Line chart by using this pivot table. We found count of BMI and HBA1C are same based on Age.
➢ Explore the relationship between age and healthcare charges. 
<br>Create pivot table using Age,charges column and create Line chart by using this Pivot table. We found No of Age Increases, the Healthcare charge decreases.
### Dashboard Creation:  
➢ Build an interactive dashboard that consolidates all key insights using the above 
visualizations. Ensure visual clarity and ease of interpretation for all chart types.

<br>Create design for dashboard and arrange all diagrams with key insights.

➢ Add slicers for the fields “Weight Status” and “Diabetes Status” to enable filtering across 
all visualizations, supporting comparison of health outcomes and charges based on body 
weight and diabetes condition.

<br>Create Slicer for “Weight Status” and “Diabetes Status” from charts.PivotAnalyzer-->InsertSlicer-->Select Fields you want.



