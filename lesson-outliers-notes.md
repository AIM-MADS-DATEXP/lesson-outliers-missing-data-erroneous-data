# Lecture Outliers, Missing Data and Erroneous Data

## Lesson goals


- The student identifies outliers and differentiates between outliers and erroneous data (relates to qualifications: data understanding, data analytics).
- The student identifies missing data and interprets its meaning (relates to qualifications: data understanding, data analytics).
- The student reflects on what outliers mean in their data (relates to qualifications: data understanding, data analytics).
- The student distinguishes between "dirty data" and choosing the wrong distribution model (relates to qualifications: data understanding, data analytics).



        
## Preparation

- None

## Lesson duration

- 2:30 including two 10 min breaks

## Block 1: Outliers

- What is an outlier anyway?
- Example 1: what is an outlier anyway?
    - The fact that values get flagged as outliers is clearly related to the shape of the distribution.
    - In matplotlib boxplots, outliers are all values that match the following definition:
        1. Calculate the Interquartile Range (IQR): Q3 - Q1.
        2. Values $\lt Q_1 - 1.5 \times IQR$ and $\gt Q_3 + 1.5 \times IQR$ are outliers.
        3. In other words: the 25% lowest and 25% highest values in are regarded as outliers.
        4. But, as we have seen, there needs to be an obvious "bulge" in the distribution before outliers are flagged at all.
- Clearly what constitutes an outlier is a simply a matter of convention.
- And equally clearly the convention is that there should be a recognizable middle 50% in the distribution of the data before we talk about outliers at all.
- The so-called **Interquartile Range** (IQR) helps you find this middle 25%  (in box plots the box itself tells you where the IQR lies in your distribution and the whiskers tell you where the outliers start)
- Another often used method is to calculate the **Z-Score** for each data point. Data points with a Z-score (absolute value) larger than 3 are marked as outliers: $z = (x - \mu)/\sigma$ and $|z| > 3$ are outliers.
- Both IQR and Z-scores are only meaningful for normally distributed data.
- More generally, outlier detection is based on the following assumptions:
  - Data is normally distributed.
  - Data comes from a single population.
  - Data is continuous.
  - Observations are independent of each other.

- What could happen if one or more of these assumptions is not met?
  - Too many values are flagged as outliers.
  - Data points that are actually problematic are not recognized as outliers.

- If the data is not normally distributed:
  - Try a different method for calculating outliers, like Mean Absolute Deviation where you calculate the absolute deviation of each data point from the median and then apply a scaling factor to it. You then define outliers as all points that have $MAD_{scaled} > 2.5$ or similar.
  - Turn the distribution into a normal distribution, eg apply a log transformation to a lognormal distribution and *then* calculate the IQR.
  - Adjust the cutoff points for the IQR (if the distribution is skewed).
  - If the data is multimodal: create subgroups and apply outlier detection within each subgroup.
   
- However, **even if the data is normally distributed, the fact that a data point is an outlier does not in itself mean anything.**

- Outliers vs Erroneous data:

| Outliers                         | Erroneous data                 |
|----------------------------------|--------------------------------|
| Unusual but valid observations   | Invalid data points            |
| Can provide valuable insights    | Should be corrected or removed |
| Domain specific                  | Validation rules               |
| May indicate important phenomena | Measurement / entry errors     |

- Best practices:
  - Investigate before removing:
    - Check for data entry / coding errors.
    - Verify measurement accuracy.
    - Make sure you understand the domain.
  - Document decisions:
    - Record which values were modified and why.
    - Be transparent about criteria used.
    - Make sure your work is reproducible (always important!).
  - Sensitivity analysis:
    - Run analyses with and without outliers.
    - Report differences in results.
   
## Block 2: Missing data

- MCAR, MAR and MNAR:
  - MCAR: Missing Completely At Random
  - MAR: Missing At Random
  - MNAR: Missing Not At Random
- MCAR: Missing Completely At Random
    - Missingness is independent of any variables.
    - Least problematic: unbiased results even with deletion.
    - Causes: machine failure, spilled coffee, etc.
    - Example: during patient appointments, doctors sometimes forget to record all the required data.
- MAR: Missing At Random
  - Missingness depends on some variable that is observed.
  - Can be dealt with.
  - Causes: you know them.
  - Example: patients miss appointments if they are elderly, but you know their age so you can correct for this.
- MNAR: Missing Not At Random
  - Missingness depends on unobserved variables.
  - Most problematic: will require further work that often involves domain knowledge.
  - Causes: these are not known, which is why this is so problematic.
  - Example: patients miss appointments but it is unknown whether this simply because they are old (and you don't know their ages to begin with). 
- Example 2: Missing Values
  - Age may be Missing Completely At Random - OR it may be that poor people did not supply their age.
  - Cabin is likely Missing At Random: poor people did not have a cabin.
  - Embarked: unknown.
- How to deal with missing data:
  - DropNA : not always a good idea (for the Age column in the Titanic data set)
  - Imputation : fill the missing data with some sensible value.
- Imputation: methods
  - Simple:
    - Mean / Median / Mode substitution
    - Last observation carried forward 
  - Not so simple:
    - Simple prediction (regression)
    - k-Nearest Neighbors
    - Maximum Likelihood Esimation
    - Random Forest Imputation
    - Etc.
    - See https://scikit-learn.org/stable/modules/impute.html
- Imputation: risks
  - Reduces variance.
  - May introduce bias.
  - Distorts relationships between variables.
  - Obscures the fact that missingness is itself data.
- Example 3: Imputation 

- Imputation: Best Practices
  - Always understand WHY data is missing.
  - Choose methods appropriate to the situation:
    - Missing Completely At Random: simple methods may suffice
    - Missing Not At Random: collect additional data or use sensitivity analysis  
  - Compare the effect of different imputation methods
   
## Block 3: 

- TODO