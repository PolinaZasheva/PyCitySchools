
# PyCity Schools Analysis

* As a whole, schools with higher budgets, did not yield better test results. By contrast, schools with higher spending per student actually (\$645-675) underperformed compared to schools with smaller budgets (<\$585 per student).

* As a whole, smaller and medium sized schools dramatically out-performed large sized schools on passing math performances (89-91% passing vs 67%).

* As a whole, charter schools out-performed the public district schools across all metrics. However, more analysis will be required to glean if the effect is due to school practices or the fact that charter schools tend to serve smaller student populations per school. 
---

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
school_data_to_load = "Resources/schools_complete.csv"
student_data_to_load = "Resources/students_complete.csv"

# Read School and Student Data File and store into Pandas Data Frames
school_data = pd.read_csv(school_data_to_load)
student_data = pd.read_csv(student_data_to_load)

# Combine the data into a single dataset
school_data_complete = pd.merge(student_data, school_data, how="left", on=["school_name", "school_name"])

# Creating data farmes
school_df=school_data
student_df=student_data
combined_df=school_data_complete

combined_df.head()
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
      <th>Student ID</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school_name</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
  </tbody>
</table>
</div>



## District Summary

* Calculate the total number of schools


* Calculate the total number of students

* Calculate the total budget

* Calculate the average math score 

* Calculate the average reading score

* Calculate the overall passing rate (overall average score), i.e. (avg. math score + avg. reading score)/2

* Calculate the percentage of students with a passing math score (70 or greater)

* Calculate the percentage of students with a passing reading score (70 or greater)

* Create a dataframe to hold the above results

* Optional: give the displayed data cleaner formatting


```python
#create a DataFrame for 
District={}

District=pd.DataFrame()
```


```python
# Calculare the total number of schools
District["Total Schools"] =[school_df.school_name.value_counts().sum()]
print(District)
```

       Total Schools
    0             15



```python
# Calculate the total number of students
District["Total Students"] = [school_df["size"].sum()]
print(District)
```

       Total Schools  Total Students
    0             15           39170



```python
# Calculate the total budget
District["Total Budget"]=[school_df["budget"].sum()]
print(District)
```

       Total Schools  Total Students  Total Budget
    0             15           39170      24649428



```python
#Calculate the average math score
District["Average Math Score"]=[student_df["math_score"].mean()]
print(District)
```

       Total Schools  Total Students  Total Budget  Average Math Score
    0             15           39170      24649428           78.985371



```python
#Calculate the average reading score
District["Average Reading Score"]=[student_df["reading_score"].mean()]
print(District)
```

       Total Schools  Total Students  Total Budget  Average Math Score  \
    0             15           39170      24649428           78.985371   
    
       Average Reading Score  
    0               81.87784  



```python
#Calculate the overall passing rate (overall average score), i.e. (avg. math score + avg. reading score)/2
#passing grade is 70%
Total_Students=len(student_df["Student ID"])
avg_math_score=len(student_df[student_df["math_score"] >= 70])/ Total_Students
avg_reading_score=len(student_df[student_df["reading_score"] >= 70])/ Total_Students

overall_passing_rate=(avg_math_score+avg_reading_score)/2
print(overall_passing_rate)
```

    0.8039315802910391



```python
# Calculate the percentage of students with a passing math score (70 or greater)
District["%Passing Math"]=len(student_df[student_df["math_score"] >= 70])/ Total_Students
```


```python
#Calculate the percentage of students with a passing reading score (70 or greater)
District["%Passing Reading"]=len(student_df[student_df["reading_score"] >= 70])/ Total_Students
```


```python
#overall
District["%Overall Passing Rate"]=[overall_passing_rate]
```


```python
#Create a dataframe to hold the above results
Districts=pd.DataFrame(District)
print(Districts)
```

       Total Schools  Total Students  Total Budget  Average Math Score  \
    0             15           39170      24649428           78.985371   
    
       Average Reading Score  %Passing Math  %Passing Reading  \
    0               81.87784       0.749809          0.858055   
    
       %Overall Passing Rate  
    0               0.803932  



```python
#Optional: give the displayed data cleaner formatting
Districts.style.format({"Total Budget": "${:,.2f}",
                      "%Passing Math": "{:.1%}","%Passing Reading": "{:.1%}", "Overall Passing Rate": "{:.1%}"})

Districts
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
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>%Passing Math</th>
      <th>%Passing Reading</th>
      <th>%Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>0.749809</td>
      <td>0.858055</td>
      <td>0.803932</td>
    </tr>
  </tbody>
</table>
</div>



## School Summary

* Create an overview table that summarizes key metrics about each school, including:
  * School Name
  * School Type
  * Total Students
  * Total School Budget
  * Per Student Budget
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)
  
* Create a dataframe to hold the above results


```python
#Create an overview table that summarizes key metrics about each school, including:

#School Name Grouping
School_Name = combined_df.set_index('school_name').groupby(['school_name'])

#School Type Grouping
School_Type = school_df.set_index('school_name')['type']

#Calculating Total Students
Total_Students = combined_df.groupby("school_name")['Student ID'].count()

#Calculating Total School Budget
School_Budget = school_df.set_index('school_name')['budget']

#Calculating Per Student Budget
Student_Budget = school_df.set_index('school_name')['budget']/school_df.set_index('school_name')['size']

#Average Math Score
avg_math_score = School_Name['math_score'].mean()

#Average Reading Score
avg_reading_score=School_Name['reading_score'].mean()

#%Passing Math
passing_math_score = combined_df[combined_df['math_score']>=70].groupby('school_name')['Student ID'].count()/Total_Students

#%Passing Reading
passing_reading_score = combined_df[combined_df['reading_score']>=70].groupby('school_name')['Student ID'].count()/Total_Students

#Overall Passing Rate (Average of the above two)
overall_passing_rate = (passing_math_score+passing_reading_score)/2
```


```python
#Create a dataframe to hold the above results
school_summary = pd.DataFrame({
    "School Type": School_Type,
    "Total Students": Total_Students,
    "Per Student Budget": Student_Budget,
    "Total School Budget": School_Budget,
    "Average Math Score": avg_math_score,
    "Average Reading Score": avg_reading_score,
    '% Passing Math': passing_math_score,
    '% Passing Reading': passing_reading_score,
    "Overall Passing Rate": overall_passing_rate
})
```


```python
#styling and formatting School Summary Output
school_summary = school_summary[['School Type', 
                          'Total Students', 
                          'Total School Budget', 
                          'Per Student Budget', 
                          'Average Math Score', 
                          'Average Reading Score',
                          '% Passing Math',
                          '% Passing Reading',
                          'Overall Passing Rate']]

school_summary.style.format({'Total Students': '{:,}', 
                          "Total School Budget": "${:,}", 
                          "Per Student Budget": "${:.0f}",
                          'Average Math Score': "{:.1f}", 
                          'Average Reading Score': "{:.1f}", 
                          "% Passing Math": "{:.1%}", 
                          "% Passing Reading": "{:.1%}", 
                          "Overall Passing Rate": "{:.1%}"})
```




<style  type="text/css" >
</style>  
<table id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >School Type</th> 
        <th class="col_heading level0 col1" >Total Students</th> 
        <th class="col_heading level0 col2" >Total School Budget</th> 
        <th class="col_heading level0 col3" >Per Student Budget</th> 
        <th class="col_heading level0 col4" >Average Math Score</th> 
        <th class="col_heading level0 col5" >Average Reading Score</th> 
        <th class="col_heading level0 col6" >% Passing Math</th> 
        <th class="col_heading level0 col7" >% Passing Reading</th> 
        <th class="col_heading level0 col8" >Overall Passing Rate</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col0" class="data row0 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col1" class="data row0 col1" >4,976</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col2" class="data row0 col2" >$3,124,928</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col3" class="data row0 col3" >$628</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col4" class="data row0 col4" >77.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col5" class="data row0 col5" >81.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col6" class="data row0 col6" >66.7%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col7" class="data row0 col7" >81.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow0_col8" class="data row0 col8" >74.3%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col0" class="data row1 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col1" class="data row1 col1" >1,858</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col2" class="data row1 col2" >$1,081,356</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col3" class="data row1 col3" >$582</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col4" class="data row1 col4" >83.1</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col5" class="data row1 col5" >84.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col6" class="data row1 col6" >94.1%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col7" class="data row1 col7" >97.0%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow1_col8" class="data row1 col8" >95.6%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row2" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col0" class="data row2 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col1" class="data row2 col1" >2,949</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col2" class="data row2 col2" >$1,884,411</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col3" class="data row2 col3" >$639</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col4" class="data row2 col4" >76.7</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col5" class="data row2 col5" >81.2</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col6" class="data row2 col6" >66.0%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col7" class="data row2 col7" >80.7%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow2_col8" class="data row2 col8" >73.4%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row3" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col0" class="data row3 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col1" class="data row3 col1" >2,739</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col2" class="data row3 col2" >$1,763,916</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col3" class="data row3 col3" >$644</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col4" class="data row3 col4" >77.1</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col5" class="data row3 col5" >80.7</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col6" class="data row3 col6" >68.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col7" class="data row3 col7" >79.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow3_col8" class="data row3 col8" >73.8%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row4" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col0" class="data row4 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col1" class="data row4 col1" >1,468</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col2" class="data row4 col2" >$917,500</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col3" class="data row4 col3" >$625</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col4" class="data row4 col4" >83.4</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col5" class="data row4 col5" >83.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col6" class="data row4 col6" >93.4%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col7" class="data row4 col7" >97.1%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow4_col8" class="data row4 col8" >95.3%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row5" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col0" class="data row5 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col1" class="data row5 col1" >4,635</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col2" class="data row5 col2" >$3,022,020</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col3" class="data row5 col3" >$652</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col4" class="data row5 col4" >77.3</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col5" class="data row5 col5" >80.9</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col6" class="data row5 col6" >66.8%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col7" class="data row5 col7" >80.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow5_col8" class="data row5 col8" >73.8%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row6" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col0" class="data row6 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col1" class="data row6 col1" >427</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col2" class="data row6 col2" >$248,087</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col3" class="data row6 col3" >$581</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col4" class="data row6 col4" >83.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col5" class="data row6 col5" >83.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col6" class="data row6 col6" >92.5%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col7" class="data row6 col7" >96.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow6_col8" class="data row6 col8" >94.4%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row7" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col0" class="data row7 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col1" class="data row7 col1" >2,917</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col2" class="data row7 col2" >$1,910,635</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col3" class="data row7 col3" >$655</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col4" class="data row7 col4" >76.6</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col5" class="data row7 col5" >81.2</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col6" class="data row7 col6" >65.7%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col7" class="data row7 col7" >81.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow7_col8" class="data row7 col8" >73.5%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row8" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col0" class="data row8 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col1" class="data row8 col1" >4,761</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col2" class="data row8 col2" >$3,094,650</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col3" class="data row8 col3" >$650</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col4" class="data row8 col4" >77.1</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col5" class="data row8 col5" >81.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col6" class="data row8 col6" >66.1%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col7" class="data row8 col7" >81.2%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow8_col8" class="data row8 col8" >73.6%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row9" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col0" class="data row9 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col1" class="data row9 col1" >962</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col2" class="data row9 col2" >$585,858</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col3" class="data row9 col3" >$609</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col4" class="data row9 col4" >83.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col5" class="data row9 col5" >84.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col6" class="data row9 col6" >94.6%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col7" class="data row9 col7" >95.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow9_col8" class="data row9 col8" >95.3%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row10" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col0" class="data row10 col0" >District</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col1" class="data row10 col1" >3,999</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col2" class="data row10 col2" >$2,547,363</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col3" class="data row10 col3" >$637</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col4" class="data row10 col4" >76.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col5" class="data row10 col5" >80.7</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col6" class="data row10 col6" >66.4%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col7" class="data row10 col7" >80.2%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow10_col8" class="data row10 col8" >73.3%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row11" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col0" class="data row11 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col1" class="data row11 col1" >1,761</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col2" class="data row11 col2" >$1,056,600</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col3" class="data row11 col3" >$600</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col4" class="data row11 col4" >83.4</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col5" class="data row11 col5" >83.7</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col6" class="data row11 col6" >93.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col7" class="data row11 col7" >95.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow11_col8" class="data row11 col8" >94.9%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row12" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col0" class="data row12 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col1" class="data row12 col1" >1,635</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col2" class="data row12 col2" >$1,043,130</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col3" class="data row12 col3" >$638</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col4" class="data row12 col4" >83.4</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col5" class="data row12 col5" >83.8</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col6" class="data row12 col6" >93.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col7" class="data row12 col7" >97.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow12_col8" class="data row12 col8" >95.3%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row13" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col0" class="data row13 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col1" class="data row13 col1" >2,283</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col2" class="data row13 col2" >$1,319,574</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col3" class="data row13 col3" >$578</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col4" class="data row13 col4" >83.3</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col5" class="data row13 col5" >84.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col6" class="data row13 col6" >93.9%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col7" class="data row13 col7" >96.5%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow13_col8" class="data row13 col8" >95.2%</td> 
    </tr>    <tr> 
        <th id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdlevel0_row14" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col0" class="data row14 col0" >Charter</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col1" class="data row14 col1" >1,800</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col2" class="data row14 col2" >$1,049,400</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col3" class="data row14 col3" >$583</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col4" class="data row14 col4" >83.7</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col5" class="data row14 col5" >84.0</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col6" class="data row14 col6" >93.3%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col7" class="data row14 col7" >96.6%</td> 
        <td id="T_0a113ddc_452c_11e9_b8ec_8c85902c29bdrow14_col8" class="data row14 col8" >95.0%</td> 
    </tr></tbody> 
</table> 



## Top Performing Schools (By Passing Rate)

* Sort and display the top five schools in overall passing rate


```python
top_five_schools=school_summary.sort_values("Overall Passing Rate", ascending = False)

top_five_schools.style.format({'Total Students': '{:,}', 
                          "Total School Budget": "${:,}", 
                          "Per Student Budget": "${:.0f}",
                          'Average Math Score': "{:.1f}", 
                          'Average Reading Score': "{:.1f}", 
                          "% Passing Math": "{:.1%}", 
                          "% Passing Reading": "{:.1%}", 
                          "Overall Passing Rate": "{:.1%}"})

top_five_schools.head()
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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>0.941335</td>
      <td>0.970398</td>
      <td>0.955867</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>0.932722</td>
      <td>0.973089</td>
      <td>0.952905</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>0.945946</td>
      <td>0.959459</td>
      <td>0.952703</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>0.933924</td>
      <td>0.971390</td>
      <td>0.952657</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>0.938677</td>
      <td>0.965396</td>
      <td>0.952037</td>
    </tr>
  </tbody>
</table>
</div>



## Bottom Performing Schools (By Passing Rate)

* Sort and display the five worst-performing schools


```python
#Select the bottom 5 schools
bottom_five_schools=school_summary.sort_values("Overall Passing Rate", ascending = True)
```


```python
#Sort from worst to better amont the bottom 5
bottom_five_schools = bottom_five_schools.sort_values('Overall Passing Rate')
```


```python
bottom_five_schools.style.format({'Total Students': '{:,}', 
                          "Total School Budget": "${:,}", 
                          "Per Student Budget": "${:.0f}",
                          'Average Math Score': "{:.1f}", 
                          'Average Reading Score': "{:.1f}", 
                          "% Passing Math": "{:.1%}", 
                          "% Passing Reading": "{:.1%}", 
                          "Overall Passing Rate": "{:.1%}"})

bottom_five_schools.head()
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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>0.663666</td>
      <td>0.802201</td>
      <td>0.732933</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>0.659885</td>
      <td>0.807392</td>
      <td>0.733639</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>0.656839</td>
      <td>0.813164</td>
      <td>0.735002</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>0.660576</td>
      <td>0.812224</td>
      <td>0.736400</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>0.683096</td>
      <td>0.792990</td>
      <td>0.738043</td>
    </tr>
  </tbody>
</table>
</div>



## Math Scores by Grade

* Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.

  * Create a pandas series for each grade. Hint: use a conditional statement.
  
  * Group each series by school
  
  * Combine the series into a dataframe
  
  * Optional: give the displayed data cleaner formatting


```python
#Create a table that lists the average Math Score = Grade 9 and group by school
ninth_math_scores = student_df.loc[student_df['grade']=='9th'].groupby('school_name')["math_score"].mean()
```


```python
#Create a table that lists the average Math Score = Grade 10 and group by school
tenth_math_scores = student_df.loc[student_df['grade']=='10th'].groupby('school_name')["math_score"].mean()
```


```python
#Create a table that lists the average Math Score = Grade 11 and group by school
eleventh_math_scores = student_df.loc[student_df['grade']=='11th'].groupby('school_name')["math_score"].mean()
```


```python
#Create a table that lists the average Math Score = Grade 12 and group by school
twelveth_math_scores = student_df.loc[student_df['grade']=='12th'].groupby('school_name')["math_score"].mean()
```


```python
#Combine the series into a dataframe
math_scores = pd.DataFrame({
        "9th": ninth_math_scores,
        "10th": tenth_math_scores,
        "11th": eleventh_math_scores,
        "12th": twelveth_math_scores
})
math_scores = math_scores[['9th', '10th', '11th', '12th']]
math_scores.index.name = "School"
```


```python
#Optional: give the displayed data cleaner formatting
math_scores.style.format({'9th': '{:.1f}', 
                          "10th": '{:.1f}', 
                          "11th": "{:.1f}", 
                          "12th": "{:.1f}"})
```




<style  type="text/css" >
</style>  
<table id="T_2274e3c6_452c_11e9_abbd_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >9th</th> 
        <th class="col_heading level0 col1" >10th</th> 
        <th class="col_heading level0 col2" >11th</th> 
        <th class="col_heading level0 col3" >12th</th> 
    </tr>    <tr> 
        <th class="index_name level0" >School</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow0_col0" class="data row0 col0" >77.1</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow0_col1" class="data row0 col1" >77.0</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow0_col2" class="data row0 col2" >77.5</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow0_col3" class="data row0 col3" >76.5</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow1_col0" class="data row1 col0" >83.1</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow1_col1" class="data row1 col1" >83.2</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow1_col2" class="data row1 col2" >82.8</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow1_col3" class="data row1 col3" >83.3</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row2" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow2_col0" class="data row2 col0" >76.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow2_col1" class="data row2 col1" >76.5</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow2_col2" class="data row2 col2" >76.9</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow2_col3" class="data row2 col3" >77.2</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row3" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow3_col0" class="data row3 col0" >77.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow3_col1" class="data row3 col1" >77.7</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow3_col2" class="data row3 col2" >76.9</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow3_col3" class="data row3 col3" >76.2</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row4" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow4_col0" class="data row4 col0" >82.0</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow4_col1" class="data row4 col1" >84.2</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow4_col2" class="data row4 col2" >83.8</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow4_col3" class="data row4 col3" >83.4</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row5" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow5_col0" class="data row5 col0" >77.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow5_col1" class="data row5 col1" >77.3</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow5_col2" class="data row5 col2" >77.1</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow5_col3" class="data row5 col3" >77.2</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row6" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow6_col0" class="data row6 col0" >83.8</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow6_col1" class="data row6 col1" >83.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow6_col2" class="data row6 col2" >85.0</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow6_col3" class="data row6 col3" >82.9</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row7" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow7_col0" class="data row7 col0" >77.0</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow7_col1" class="data row7 col1" >75.9</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow7_col2" class="data row7 col2" >76.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow7_col3" class="data row7 col3" >77.2</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row8" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow8_col0" class="data row8 col0" >77.2</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow8_col1" class="data row8 col1" >76.7</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow8_col2" class="data row8 col2" >77.5</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow8_col3" class="data row8 col3" >76.9</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row9" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow9_col0" class="data row9 col0" >83.6</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow9_col1" class="data row9 col1" >83.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow9_col2" class="data row9 col2" >84.3</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow9_col3" class="data row9 col3" >84.1</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row10" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow10_col0" class="data row10 col0" >76.9</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow10_col1" class="data row10 col1" >76.6</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow10_col2" class="data row10 col2" >76.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow10_col3" class="data row10 col3" >77.7</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row11" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow11_col0" class="data row11 col0" >83.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow11_col1" class="data row11 col1" >82.9</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow11_col2" class="data row11 col2" >83.4</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow11_col3" class="data row11 col3" >83.8</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row12" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow12_col0" class="data row12 col0" >83.6</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow12_col1" class="data row12 col1" >83.1</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow12_col2" class="data row12 col2" >83.5</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow12_col3" class="data row12 col3" >83.5</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row13" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow13_col0" class="data row13 col0" >83.1</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow13_col1" class="data row13 col1" >83.7</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow13_col2" class="data row13 col2" >83.2</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow13_col3" class="data row13 col3" >83.0</td> 
    </tr>    <tr> 
        <th id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdlevel0_row14" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow14_col0" class="data row14 col0" >83.3</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow14_col1" class="data row14 col1" >84.0</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow14_col2" class="data row14 col2" >83.8</td> 
        <td id="T_2274e3c6_452c_11e9_abbd_8c85902c29bdrow14_col3" class="data row14 col3" >83.6</td> 
    </tr></tbody> 
</table> 



## Reading Score by Grade 

* Perform the same operations as above for reading scores


```python
#Create a table that lists the average Reading Score = Grade 9 and group by school
ninth_reading_scores = student_df.loc[student_df['grade']=='9th'].groupby('school_name')["reading_score"].mean()
```


```python
#Create a table that lists the average Reading Score = Grade 10 and group by school
tenth_reading_scores = student_df.loc[student_df['grade']=='10th'].groupby('school_name')["reading_score"].mean()
```


```python
#Create a table that lists the average Reading Score = Grade 11 and group by school
eleventh_reading_scores = student_df.loc[student_df['grade']=='11th'].groupby('school_name')["reading_score"].mean()
```


```python
#Create a table that lists the average Reading Score = Grade 12 and group by school
tweleveth_reading_scores = student_df.loc[student_df['grade']=='12th'].groupby('school_name')["reading_score"].mean()
```


```python
#Combine the series into a dataframe
reading_scores = pd.DataFrame({
        "9th": ninth_reading_scores,
        "10th": tenth_reading_scores,
        "11th": eleventh_reading_scores,
        "12th": tweleveth_reading_scores
})
reading_scores = reading_scores[['9th', '10th', '11th', '12th']]
reading_scores.index.name = "School"
```


```python
#Optional: give the displayed data cleaner formatting
reading_scores.style.format({'9th': '{:.1f}', 
                          "10th": '{:.1f}', 
                          "11th": "{:.1f}", 
                          "12th": "{:.1f}"})
```




<style  type="text/css" >
</style>  
<table id="T_3694796e_452c_11e9_aa05_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >9th</th> 
        <th class="col_heading level0 col1" >10th</th> 
        <th class="col_heading level0 col2" >11th</th> 
        <th class="col_heading level0 col3" >12th</th> 
    </tr>    <tr> 
        <th class="index_name level0" >School</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row0" class="row_heading level0 row0" >Bailey High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow0_col0" class="data row0 col0" >81.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow0_col1" class="data row0 col1" >80.9</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow0_col2" class="data row0 col2" >80.9</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow0_col3" class="data row0 col3" >80.9</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >Cabrera High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow1_col0" class="data row1 col0" >83.7</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow1_col1" class="data row1 col1" >84.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow1_col2" class="data row1 col2" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow1_col3" class="data row1 col3" >84.3</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row2" class="row_heading level0 row2" >Figueroa High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow2_col0" class="data row2 col0" >81.2</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow2_col1" class="data row2 col1" >81.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow2_col2" class="data row2 col2" >80.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow2_col3" class="data row2 col3" >81.4</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row3" class="row_heading level0 row3" >Ford High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow3_col0" class="data row3 col0" >80.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow3_col1" class="data row3 col1" >81.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow3_col2" class="data row3 col2" >80.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow3_col3" class="data row3 col3" >80.7</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row4" class="row_heading level0 row4" >Griffin High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow4_col0" class="data row4 col0" >83.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow4_col1" class="data row4 col1" >83.7</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow4_col2" class="data row4 col2" >84.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow4_col3" class="data row4 col3" >84.0</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row5" class="row_heading level0 row5" >Hernandez High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow5_col0" class="data row5 col0" >80.9</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow5_col1" class="data row5 col1" >80.7</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow5_col2" class="data row5 col2" >81.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow5_col3" class="data row5 col3" >80.9</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row6" class="row_heading level0 row6" >Holden High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow6_col0" class="data row6 col0" >83.7</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow6_col1" class="data row6 col1" >83.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow6_col2" class="data row6 col2" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow6_col3" class="data row6 col3" >84.7</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row7" class="row_heading level0 row7" >Huang High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow7_col0" class="data row7 col0" >81.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow7_col1" class="data row7 col1" >81.5</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow7_col2" class="data row7 col2" >81.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow7_col3" class="data row7 col3" >80.3</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row8" class="row_heading level0 row8" >Johnson High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow8_col0" class="data row8 col0" >81.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow8_col1" class="data row8 col1" >80.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow8_col2" class="data row8 col2" >80.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow8_col3" class="data row8 col3" >81.2</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row9" class="row_heading level0 row9" >Pena High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow9_col0" class="data row9 col0" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow9_col1" class="data row9 col1" >83.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow9_col2" class="data row9 col2" >84.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow9_col3" class="data row9 col3" >84.6</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row10" class="row_heading level0 row10" >Rodriguez High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow10_col0" class="data row10 col0" >81.0</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow10_col1" class="data row10 col1" >80.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow10_col2" class="data row10 col2" >80.9</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow10_col3" class="data row10 col3" >80.4</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row11" class="row_heading level0 row11" >Shelton High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow11_col0" class="data row11 col0" >84.1</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow11_col1" class="data row11 col1" >83.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow11_col2" class="data row11 col2" >84.4</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow11_col3" class="data row11 col3" >82.8</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row12" class="row_heading level0 row12" >Thomas High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow12_col0" class="data row12 col0" >83.7</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow12_col1" class="data row12 col1" >84.3</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow12_col2" class="data row12 col2" >83.6</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow12_col3" class="data row12 col3" >83.8</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row13" class="row_heading level0 row13" >Wilson High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow13_col0" class="data row13 col0" >83.9</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow13_col1" class="data row13 col1" >84.0</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow13_col2" class="data row13 col2" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow13_col3" class="data row13 col3" >84.3</td> 
    </tr>    <tr> 
        <th id="T_3694796e_452c_11e9_aa05_8c85902c29bdlevel0_row14" class="row_heading level0 row14" >Wright High School</th> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow14_col0" class="data row14 col0" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow14_col1" class="data row14 col1" >83.8</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow14_col2" class="data row14 col2" >84.2</td> 
        <td id="T_3694796e_452c_11e9_aa05_8c85902c29bdrow14_col3" class="data row14 col3" >84.1</td> 
    </tr></tbody> 
</table> 



## Scores by School Spending

* Create a table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:
  * Average Math Score
  * Average Reading Score
  * % Passing Math
  * % Passing Reading
  * Overall Passing Rate (Average of the above two)


```python
# Sample bins. Feel free to create your own bins.
spending_bins = [0, 585, 615, 645, 675]
group_names = ["<$585", "$585-615", "$615-645", "$645-675"]
```


```python
combined_df['spending_bins'] = pd.cut(combined_df['budget']/combined_df['size'], spending_bins, labels = group_names)
```


```python
#group by spending
group_by_spending = combined_df.groupby('spending_bins')
```


```python
#Average Math Score
avg_math = group_by_spending['math_score'].mean()
```


```python
#Average Reading Score
avg_read = group_by_spending['reading_score'].mean()
```


```python
#% Passing Math
pass_math = combined_df[combined_df['math_score']>=70].groupby('spending_bins')['Student ID'].count()/group_by_spending['Student ID'].count()
```


```python
#% Passing Reading
pass_reading = combined_df[combined_df['reading_score']>=70].groupby('spending_bins')['Student ID'].count()/group_by_spending['Student ID'].count()
```


```python
#Overall Passing Rate (Average of the above two)
overall =(pass_math+pass_reading)/2
```


```python
#Create Dara Frame           
scores_by_school_spend = pd.DataFrame({
    "Average Math Score": avg_math,
    "Average Reading Score": avg_read,
    '% Passing Math': pass_math,
    '% Passing Reading': pass_reading,
    "Overall Passing Rate": overall
    })
```


```python
scores_by_school_spend.index.name = "Spending Ranges(Per Student)"

#formating
scores_by_school_spend.style.format({'Average Math Score': '{:.1f}', 
                              'Average Reading Score': '{:.1f}', 
                              '% Passing Math': '{:.1%}', 
                              '% Passing Reading':'{:.1%}', 
                              'Overall Passing Rate': '{:.1%}'})
```




<style  type="text/css" >
</style>  
<table id="T_7bff4da8_452c_11e9_885c_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Math Score</th> 
        <th class="col_heading level0 col1" >Average Reading Score</th> 
        <th class="col_heading level0 col2" >% Passing Math</th> 
        <th class="col_heading level0 col3" >% Passing Reading</th> 
        <th class="col_heading level0 col4" >Overall Passing Rate</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Spending Ranges(Per Student)</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_7bff4da8_452c_11e9_885c_8c85902c29bdlevel0_row0" class="row_heading level0 row0" ><$585</th> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow0_col0" class="data row0 col0" >83.4</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow0_col1" class="data row0 col1" >84.0</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow0_col2" class="data row0 col2" >93.7%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow0_col3" class="data row0 col3" >96.7%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow0_col4" class="data row0 col4" >95.2%</td> 
    </tr>    <tr> 
        <th id="T_7bff4da8_452c_11e9_885c_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >$585-615</th> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow1_col0" class="data row1 col0" >83.5</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow1_col1" class="data row1 col1" >83.8</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow1_col2" class="data row1 col2" >94.1%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow1_col3" class="data row1 col3" >95.9%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow1_col4" class="data row1 col4" >95.0%</td> 
    </tr>    <tr> 
        <th id="T_7bff4da8_452c_11e9_885c_8c85902c29bdlevel0_row2" class="row_heading level0 row2" >$615-645</th> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow2_col0" class="data row2 col0" >78.1</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow2_col1" class="data row2 col1" >81.4</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow2_col2" class="data row2 col2" >71.4%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow2_col3" class="data row2 col3" >83.6%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow2_col4" class="data row2 col4" >77.5%</td> 
    </tr>    <tr> 
        <th id="T_7bff4da8_452c_11e9_885c_8c85902c29bdlevel0_row3" class="row_heading level0 row3" >$645-675</th> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow3_col0" class="data row3 col0" >77.0</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow3_col1" class="data row3 col1" >81.0</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow3_col2" class="data row3 col2" >66.2%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow3_col3" class="data row3 col3" >81.1%</td> 
        <td id="T_7bff4da8_452c_11e9_885c_8c85902c29bdrow3_col4" class="data row3 col4" >73.7%</td> 
    </tr></tbody> 
</table> 



## Scores by School Size

* Perform the same operations as above, based on school size.


```python
# Sample bins. Feel free to create your own bins.
size_bins = [0, 1000, 2000, 5000]
group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]
```


```python
combined_df['size_bins'] = pd.cut(combined_df['size'], size_bins, labels = group_names)
```


```python
#group by spending: 
group_by_size = combined_df.groupby('size_bins')
```


```python
#Average Math Score
avg_math = group_by_size['math_score'].mean()
```


```python
#Average Reading Score
avg_read = group_by_size['reading_score'].mean()
```


```python
#% Passing Math
pass_math = combined_df[combined_df['math_score']>=70].groupby('size_bins')['Student ID'].count()/group_by_size['Student ID'].count()
```


```python
#% Passing Reading
pass_reading = combined_df[combined_df['reading_score']>=70].groupby('size_bins')['Student ID'].count()/group_by_size['Student ID'].count()
```


```python
#Overall Passing Rate (Average of the above two)
overall = (pass_math + pass_reading)/2
```


```python
#Create Dara Frame           
scores_by_school_size = pd.DataFrame({
    "Average Math Score": avg_math,
    "Average Reading Score": avg_read,
    '% Passing Math': pass_math,
    '% Passing Reading': pass_reading,
    "Overall Passing Rate": overall
    })
```


```python
scores_by_school_size.index.name = "School Size"

#formating
scores_by_school_size.style.format({'Average Math Score': '{:.1f}', 
                              'Average Reading Score': '{:.1f}', 
                              '% Passing Math': '{:.1%}', 
                              '% Passing Reading':'{:.1%}', 
                              'Overall Passing Rate': '{:.1%}'})
```




<style  type="text/css" >
</style>  
<table id="T_c8b5292e_452c_11e9_80bd_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Math Score</th> 
        <th class="col_heading level0 col1" >Average Reading Score</th> 
        <th class="col_heading level0 col2" >% Passing Math</th> 
        <th class="col_heading level0 col3" >% Passing Reading</th> 
        <th class="col_heading level0 col4" >Overall Passing Rate</th> 
    </tr>    <tr> 
        <th class="index_name level0" >School Size</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdlevel0_row0" class="row_heading level0 row0" >Small (<1000)</th> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow0_col0" class="data row0 col0" >83.8</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow0_col1" class="data row0 col1" >84.0</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow0_col2" class="data row0 col2" >94.0%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow0_col3" class="data row0 col3" >96.0%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow0_col4" class="data row0 col4" >95.0%</td> 
    </tr>    <tr> 
        <th id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >Medium (1000-2000)</th> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow1_col0" class="data row1 col0" >83.4</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow1_col1" class="data row1 col1" >83.9</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow1_col2" class="data row1 col2" >93.6%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow1_col3" class="data row1 col3" >96.8%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow1_col4" class="data row1 col4" >95.2%</td> 
    </tr>    <tr> 
        <th id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdlevel0_row2" class="row_heading level0 row2" >Large (2000-5000)</th> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow2_col0" class="data row2 col0" >77.5</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow2_col1" class="data row2 col1" >81.2</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow2_col2" class="data row2 col2" >68.7%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow2_col3" class="data row2 col3" >82.1%</td> 
        <td id="T_c8b5292e_452c_11e9_80bd_8c85902c29bdrow2_col4" class="data row2 col4" >75.4%</td> 
    </tr></tbody> 
</table> 



## Scores by School Type

* Perform the same operations as above, based on school type.


```python
#group by type
scores_by_type = combined_df.groupby("type")
```


```python
#Average Math Score
avg_math = scores_by_type['math_score'].mean()
```


```python
#Average Reading Score
avg_read = scores_by_type['reading_score'].mean()
```


```python
#% Passing Math
pass_math = combined_df[combined_df['math_score']>=70].groupby('type')['Student ID'].count()/scores_by_type['Student ID'].count()
```


```python
#% Passing Reading
pass_reading = combined_df[combined_df['reading_score']>=70].groupby('type')['Student ID'].count()/scores_by_type['Student ID'].count()
```


```python
#Overall Passing Rate (Average of the above two)
overall = (pass_math + pass_reading)/2
```


```python
#Create Dara Frame           
scores_by_school_type = pd.DataFrame({
    "Average Math Score": avg_math,
    "Average Reading Score": avg_read,
    '% Passing Math': pass_math,
    '% Passing Reading': pass_reading,
    "Overall Passing Rate": overall
    })
```


```python
scores_by_school_type.index.name = "School Type"

#formating
scores_by_school_type.style.format({'Average Math Score': '{:.1f}', 
                              'Average Reading Score': '{:.1f}', 
                              '% Passing Math': '{:.1%}', 
                              '% Passing Reading':'{:.1%}', 
                              'Overall Passing Rate': '{:.1%}'})
```




<style  type="text/css" >
</style>  
<table id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bd" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Math Score</th> 
        <th class="col_heading level0 col1" >Average Reading Score</th> 
        <th class="col_heading level0 col2" >% Passing Math</th> 
        <th class="col_heading level0 col3" >% Passing Reading</th> 
        <th class="col_heading level0 col4" >Overall Passing Rate</th> 
    </tr>    <tr> 
        <th class="index_name level0" >School Type</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdlevel0_row0" class="row_heading level0 row0" >Charter</th> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow0_col0" class="data row0 col0" >83.4</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow0_col1" class="data row0 col1" >83.9</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow0_col2" class="data row0 col2" >93.7%</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow0_col3" class="data row0 col3" >96.6%</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow0_col4" class="data row0 col4" >95.2%</td> 
    </tr>    <tr> 
        <th id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdlevel0_row1" class="row_heading level0 row1" >District</th> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow1_col0" class="data row1 col0" >77.0</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow1_col1" class="data row1 col1" >81.0</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow1_col2" class="data row1 col2" >66.5%</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow1_col3" class="data row1 col3" >80.9%</td> 
        <td id="T_f92bcb6c_452c_11e9_b85e_8c85902c29bdrow1_col4" class="data row1 col4" >73.7%</td> 
    </tr></tbody> 
</table> 




```python
#Analysis: 
# 1)Schools larger than 2000 students have a lower overall scores than smaller schools
# 2)Charter School have higher math scores compared to District Shools
# 3)Higher rates of spending are not necesseraly associated with higher overall rates of passint standarized tests
```
