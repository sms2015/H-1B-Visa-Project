# H-1B-Visa-Project
Analysis of 2014 H-1B visa data

H-1B Visa Applications 2014
Stacey Schwarcz

Section 1: 

Question 1
Which companies applied for the largest number of H­1B visas where the job opening was located in NYC? Please describe any issues you may encounter summarizing the data by employer name.

Several issues were encountered in this analysis:

The first is that while the state name is the standard two letter state code, the city names used for work locations do not appear to be standardized (i.e. selected from a drop down menu).  Rather, there are many ways in which New York City is referred to by various employers including “NYC”, “New York City”, “Brooklyn”, “Manhattan”, etc.  In addition in some cases there are misspellings of these names.  

The next issue encountered is with the employer name. The same employer name can be spelled in a number of ways:
  	Some companies had names with punctuation for one application and none in their name for another: INFOCEPTS LLC vs INFOCEPTS, LLC vs INFOCEPTS. Punctuation and suffixes (LLC, INC, etc) could be removed to resolve this issue
  	Some companies have multiple divisions: GOLDMAN SACHS EXECUTION & CLEARING L.P., GOLDMAN SACHS SERVICES LLC , GOLDMAN, SACHS & CO.  This issue is more difficult to resolve as there would need to be an automated way to identify that these are all variations of “GOLDMAN SACHS”. Even referring to the official SEC company name list (https://www.sec.gov/rules/other/4-460list.htm ) wouldn’t immediately resolve the issue as the official name there is: Goldman Sachs Group Inc.   This problem would require a normalizing algorithm (as described here https://www.addaptive.com/blog/using-algorithms-normalize-company-names/) or Name Entity Recognition (as described here: https://nlp.stanford.edu/software/CRF-NER.shtml).

Simplifications: 

In the interest of time, this analysis only looked at applications where work location 1 or 2 was “NYC” or “New York City”, and employer names were not adjusted before consolidation. 
The result was that The NYC/New York City employer applying for the greatest number of visas was 'MPHASIS CORPORATION' with 30 total workers.

Question 2
Calculate the mean and standard deviation of wages proposed for workers located in New York City and Mountain View. Are the average wages in these two locations statistically different? What factors could explain the results?
Wage rates can be annual, hourly, weekly, bi-weekly, and monthly.  However, greater than 90% of the applications by total workers are annual. To simplify for the purpose of this exercise, only applications where the proposed wage unit was annual were considered.
The distribution of wages for New York City did not resemble a normal distribution so a non-parametric test was used to test whether the average wages of Mountain View are different from NYC. The result is statistically significant so the means are different: the mean for Mountain View, $112,574 is higher than the mean for NYC, $82,195.
The following factors could explain the results:
  	This analysis was simplified to only include companies where location 1 or location 2 is "NYC" or "New York City", however there are many variations on these names so not all of NYC is being captured in this data such that it might not be representative of New York City wages for H-1B visas.
  	The cost of living may be higher in Mountain View than in NYC, leading to higher salaries. This would require an additional data source to verify
  	The number and/or types of jobs for which visas are being requested in Mountain View may be higher paying or have lower supply or higher demand, than those in NYC.

Question 3
For NYC, what is the relationship between the total number of H­1B visas requested by an employer and the average wages proposed? Visually represent this relationship if appropriate. Is the relationship statistically significant? What might explain this relationship?

The scatter plot shows the relationship between the total number of H-1B visas requested and the average wages proposed. The correlation is very weak at 0.065, and the p-value of 0.318 is greater than 0.05 so this correlation is not significant, so there is no statistically significant relationship between the number of workers and average proposed wage rates.
Based on the scatter plot, only a small percentage of companies have applications with more than 5 jobs and there is no obvious pattern between average wages and the number of positions.
 
Section 2: Brainstorming
What interesting questions might this dataset address? Brainstorm a handful of interesting questions, and scope them. Describe steps, methodology, and level of effort that would be required to answer each question. Additional, enriching, datasets are allowed, but not required.

1.	How do proposed wage rates compare to the prevailing wage rates? Are they higher or lower than the prevailing wage rates? Are there differences by location, industry, or occupation? 
  	Steps: data exploration to visually identify differences, consider applications which have proposed wages that are (10%) higher/lower than prevailing, or (25%) higher/lower than the prevailing. Identify which states have the largest percentage of cases with 10%/25% higher/lower proposed wages.  Drill down by employer, occupation, or industry to determine what might be driving these differences.
  	For each state compute the % of applications where the wages are higher than the prevailing wage

2.	What features are predictive of whether an application will be certified or not?
  	Steps: data exploration to visually look at features, and for a moderate effort a logistic regression to determine the predictive value of these features.  For a high level of effort a machine learning model using holdout sets to compare model.

3.	For those that are certified, what features are predictive of how long an application takes to be certified. Steps are similar to question 2

Section 3: Exploration
Choose a question to answer from your brainstorming section. 

How do proposed wage rates compare to the prevailing wage rates? Are they typically higher or lower than the prevailing wage rates? Are there differences by location, industry, or occupation? 

The following features were explored by generating new variables and exploring the distribution by status: month (does season or time of year make a difference), length of employment, Full Time vs Part Time, number of workers, Location (group by region to simplify), Proposed wage rate.

Based on data exploration only 3 features were worth testing with logistic regression: employment length, full time vs part time, proposed wage rate.  Based on the data exploration it seemed unlikely that these would have much if any predictive value and the result of the logistic regression was that the accuracy was no better than the null rate, so these features do not provide any additional information or form a useful model for predicting whether an application will be denied.

There may be other factors that were not considered that may have predictive value, or it may just not be possible to predict the status based on this data set

