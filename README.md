# Pyspark-X-DBT-End-To-End-Data-Engineering-Project
This project is about combining  pyspark and DBT to make sense out of the data.
Key concepts tackled:
  - Pyspark Streaming
  - Dynamic Ingestion
  - Incremental Loading
  - Upsert
  - SCD - 2 in Snapshots(DBT)
  - Data Transformations

## Project Architecture
The following is an overview of the entire project. Come aloooong!

<img width="1015" height="510" alt="Screenshot (118)" src="https://github.com/user-attachments/assets/61b51e75-bd0e-46c1-ad55-8b24ee888a04" />

### Source and Bronze Layer
Logged in to Databricks and created catalog, schema and bronze.
Also created a volume and respective folders for the various tables in the volume to act as storage and source.
In the bronze layer created a volume to store the checkpoints to be used in the pyspark streaming

<img width="1368" height="764" alt="Screenshot (97)" src="https://github.com/user-attachments/assets/51115043-3d39-4872-bff0-754e6146db69" />

#### Spark Streaming
- Managed to ingest the data dynamically and also ensuring pyspark streaming as observed in the codes below.
<img width="1284" height="740" alt="Screenshot (99)" src="https://github.com/user-attachments/assets/0d723781-9577-45a3-b6ce-1da53cf6d97a" />

<img width="1289" height="746" alt="Screenshot (100)" src="https://github.com/user-attachments/assets/6e592fc4-b215-420c-9447-47a68f8e4258" />

<img width="1333" height="768" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/167d6e1d-00ac-4024-a317-d3f7d83c37d0" />

### Silver - Transformations
In this transformations phase managed to create Class in python to help remove duplicates, generate current timestamp and upsert. This helps to manage repetition hence minimizing time wastage in the transformations.
Other transformations included:
  - Split
  - Concatenation
  - Dropping columns

<img width="1302" height="733" alt="Screenshot (105)" src="https://github.com/user-attachments/assets/9257e11d-7e9f-4166-8416-d6285a7a88da" />

<img width="1320" height="719" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/72fb3fd2-26f1-4c9b-92e0-17a8216aba6e" />


### Data Build Tool - DBT
My adapter is Databricks, hence connected DBT with it using, host, tokens so as to access the data in the databricks.

<img width="1403" height="768" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/f031b433-c9e8-4651-ae6d-d54a8709037f" />

Successfully managed to configure everything and initiated the DBT.

<img width="1377" height="768" alt="Screenshot (107)" src="https://github.com/user-attachments/assets/881098f6-8ccb-4a7b-b77c-895b2c4312b4" />

Ensured the project name in the dbt_project.yml is different from the one defined earlier in the DBT. Also configured the materialization to tables.

Did sample exploration in the analysis folder to confirm that everything was good.

<img width="1381" height="768" alt="Screenshot (108)" src="https://github.com/user-attachments/assets/28679330-0718-4174-85b8-83ed86a7f2a0" />

Basically models is the backbone of DBT. I created folders in this region that is source, silver and gold.
In the sources I created source.yml to help us see the lineage.

<img width="1377" height="768" alt="Screenshot (109)" src="https://github.com/user-attachments/assets/b6e3f972-94ef-4695-91f8-161bc3a03c33" />

<img width="1364" height="768" alt="Screenshot (110)" src="https://github.com/user-attachments/assets/7455685e-7dec-479a-9d8a-0b175cf0fb06" />

#### Incremental Loading in DBT

<img width="1373" height="768" alt="Screenshot (111)" src="https://github.com/user-attachments/assets/f484d1e2-4135-4d58-942e-42246cdef946" />

#### Custom Schema Configuration
DBT creates its own default schemas, I needed to customize it to match the desired requirement as below.

<img width="1377" height="768" alt="Screenshot (112)" src="https://github.com/user-attachments/assets/49f8c6da-ac1b-433c-9675-9d5f241b4712" />

Defining macro for the schema customization.

<img width="1390" height="746" alt="Screenshot (113)" src="https://github.com/user-attachments/assets/bbb40e2a-193f-48be-bd60-8549fe76cd99" />

#### SCD - 2 Using Snapshots
Used Slowly Changing Dimensions Type 2 to track the history of various products. Changed the database name from analytics to datamodeling which was used in Databricks

<img width="1386" height="768" alt="Screenshot (115)" src="https://github.com/user-attachments/assets/97e901ec-90ee-4155-81da-c69b848fc8ae" />

- Finally published everything using dbt run and explored our catalog if everything was effective and ready to serve our data.

<img width="1364" height="768" alt="Screenshot (116)" src="https://github.com/user-attachments/assets/09e69bf5-a390-4128-9d11-a44d76be3f29" />

Confirming the SCD -2

<img width="1342" height="768" alt="Screenshot (117)" src="https://github.com/user-attachments/assets/7bc0854e-016d-49f5-b541-8eb3e74c6aa7" />

