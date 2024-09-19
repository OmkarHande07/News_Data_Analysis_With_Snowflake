# News_Data_Analysis_With_Snowflake
Developed an Event Driven Pipeline for Increamental Load in Snowflake Table

Extracting news data from an open-source endpoint using API and used Airflow Dag to perform tasks using python scripts to ingest the data into target Snowflake table.

**Tech Stack:**
1. Airflow
2. Google Cloud Storage
3. Python
4. SnowFlake

**Steps to create pipeline:**

1. Search newsapi.org in google -> click on get API key -> fill all the details -> API key will be generated (Copy it and store it somewhere)
2. Now we need to create destination table where files should be written
3. Login to GCP console -> search for Bucket -> create new bucket -> create a folder inside that bucket -> create 1 more folder inside the folder for (parquet_files)
4. Now from console search for Composer -> create environment(this will take time to get created & also need to add required roles and permission which will be asked)
5. After it the environment will be up and running -> open the environment -> open pypi packages option which will be displayed in right side -> edit -> add apache_airflow_providers_snowflake -> save
6. Now open Airflow UI -> Admin -> connection -> fill all details -> in condition type select Snowflake
   
   ![Screenshot 2024-09-19 094808](https://github.com/user-attachments/assets/8474d6a9-3ff2-4952-bc8a-9f97520ec25c)
   
7. Now open worksheet in Snowflake -> write and execute the sql commands from (snowflake_commands input file)
8. While creating external integration in worksheet execute the desc command for integration -> from O/P copy service account - property value
9. Now open the bucket location of parquet_files folder -> permission ->Grant Access -> paste the copied text in principle -> role -> select custome role -> save (Using this the snowflake query will get data from bucket)
10. Now go to Composer -> open DAG'S folder -> upload the python scripts from input files folder (update the bucket_name and start_date as per your's ) -> in Airflow UI new DAG will be created -> open the DAG & manually trigger it
    
    ![Screenshot 2024-09-19 132950](https://github.com/user-attachments/assets/3afbc305-20e7-42e6-b726-94d39b0ccb70)

11. after it run seccessfully -> open GCP bucket -> new files will be created -> also in Snowflake UI table will be created
12. We can check the records by executing select command from worksheet
 [Data will be extracted using API]
