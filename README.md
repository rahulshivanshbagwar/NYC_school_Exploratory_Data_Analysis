# NYC Schools Exploratory Data Analysis


## Problem Statement

Every year, American high school students take SATs, which are standardized tests intended to measure literacy, numeracy, and writing skills. There are three sections - reading, math, and writing, each with a maximum score of 800 points. These tests are extremely important for students and colleges, as they play a pivotal role in the admissions process.

Analyzing the performance of schools is important for a variety of stakeholders, including policy and education professionals, researchers, government, and even parents considering which school their children should attend.

We have a dataset called schools.csv, which is previewed below.

Let's Analyze the schools with best Math scores,best SAT score and the borough with most deviation in the SAT score 


### Steps followed 
#### First part of the Project is to determine the most frequent duration of movies during the 1990's period using visualization.
- Step 1 : Import pandas 

          import pandas as pd

- Step 2 : Read in the schools CSV as a DataFrame.

        schools = pd.read_csv("schools.csv")
- Step 3 : Get an overview of the data .

        schools.info()
        
- Step 4 : Subset the pandas with the required parmaeters.

       math_school=schools[["school_name","average_math"]]


- Step 5 :Sort the values in Descending order. 

        sorted_math_school=math_school.sort_values("average_math",ascending=False)
        

- Step 6 :Filtering the top 10 schools with the best math scores. 

        top_math_schools=sorted_math_school[sorted_math_school["average_math"]>=800*0.8]
        best_math_schools=top_math_schools.iloc[:10].sort_values("average_math",ascending= False)
        best_math_schools
#### Second part of the project is to find the borough with the largest deviation of SAT score and find the average score and number of schools .
- Step 7 :Making a new Total Sat score column by adding math,reading and writing scores

        schools["total_SAT"]=schools ["average_math"]+schools["average_reading"]+schools["average_writing"]
        school_SAT=schools[["school_name","total_SAT"]]
        top_10_schools=school_SAT.sort_values("total_SAT",ascending=False).iloc[0:10]
        top_10_schools
- Step 8 :Filtering the borough with the most deviation of the SAT score and counting the nu ber of schools in it by first using groupby function to make a subset with the calculated parameters and then rounding it to two decimal points and selecting the borough with the largest deviation and renaming the columns .

        import numpy as np
        boroughs=schools.groupby("borough")["total_SAT"] .agg(["mean","std","count"]).round(2)
        boroughs.round(2)
        largest_borough=boroughs[boroughs["std"]==boroughs["std"].max()]
        rename_columns={"count":"num_schools","mean":"average_SAT","std":"std_SAT"}
        largest_std_dev=largest_borough.rename(columns=rename_columns)
        largest_std_dev
