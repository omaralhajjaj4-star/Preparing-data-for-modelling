# Preparing-data-for-modelling
Data Transformation and Filtering
This script processes the customer_train.csv dataset to prepare it for analysis. The primary goals are to optimize data types for memory efficiency and logical consistency, and then to filter the dataset based on specific criteria.

1. Data Loading and Preparation
First, the script loads the customer_train.csv dataset into a pandas DataFrame and creates a working copy named ds_jobs_transformed to preserve the original data.

2. Data Type Optimization
To ensure the data is represented appropriately and to reduce memory usage, several columns are converted to more suitable data types.

Ordinal Categories: Columns with an inherent order are converted to ordered categorical types. This allows for logical comparisons (e.g., 'Graduate' is higher than 'High School'). The columns and their specified orders are:

enrolled_university: no_enrollment < Part time course < Full time course

education_level: Primary School < High School < Graduate < Masters < Phd

experience: <1 < 1 < ... < 20 < >20

company_size: <10 < 10-49 < ... < 10000+

last_new_job: never < 1 < 2 < 3 < 4 < >4

Boolean (Two-Factor) Categories: Columns with only two distinct values are mapped to boolean (True/False) types for simplicity.

relevant_experience: Mapped to True for 'Has relevant experience' and False otherwise.

job_change: Mapped to True for 1.0 and False for 0.0.

Numeric Types: Numerical columns are downcast to more memory-efficient types.

student_id and training_hours: Converted to int32.

city_development_index: Converted to float16.

Nominal Categories: Any remaining columns with object data types (i.e., text-based features without a natural order) are converted to the standard category type.

3. Data Filtering
After the data types have been optimized, the script filters the DataFrame to create a specific subset of the data. The final dataset, ds_jobs_transformed, contains only individuals who meet the following two conditions:

Have 10 or more years of experience (experience >= '10').

Work at companies with 1,000 or more employees (company_size >= '1000-4999').
