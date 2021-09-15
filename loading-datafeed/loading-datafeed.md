# Loading data from Data Feed

## About this lab

In this lab we would look at example to load data using the **Live Data Stream** feature that allows us to load the latest data from the OCI Bucket,  this bucket act as Data Lake for receiving and collecting the stream data received from application.  We would use the sample data coming in form from CSV files for month of July and August 2020.  The data used in this in CSV format and we would upload the file in the bucket to simulate data received in the bucket.  

Estimated Time: 15 minutes

### Objectives
In this lab, you will:

- Create a Bucket and pre-authenticated request
- Setup Live feed tables
- Schedule job to load the recently uploaded data.
- Verify the data being uploaded and use it for analysis

### Prerequisites

To complete this lab, you need to have the following:

- All previous labs successfully completed
- Sample data files used in exercise

## Task 1: Create a new bucket and pre-authenticated request URI

1. To crates a new bucket. Login to the Oracle cloud. From the main menu select storage and then Bucket.
![Click the Open Bucket Admin Page](images/go_to_storage_and_bucket.png =1000x500)

2. Click on to create new bucket.
![Click on to create new bucket](images/click_on_create_bucket_button.png =1000x500)

3. In the Create Bucket dialog box give appropirate name for the bucket. Leave all other options as default.
  ![Click on to create new bucket](images/enter_name_for_bucket_and_click_create.png =1000x500)

  On completion you will see the new bucket name in the list of buckets

4. Click on the vertical 3 dots icon on the right end of the bucket name and select the create pre-authenticated request option.
![Click on to create new bucket](images/click_the3dots_and_select_create_pre_authenticated_request.png =1000x500)

  Note: By default the visibility is set a private.  Its standard practice to keep bucket visibility private and create pre-authenticated request URI on which we can set permission and a expiry date.

5. Enter a name for the pre-authenticated request. Ensure their are not spaces in the name. Choose the option for Bucket and check the Enable Object Listing option.
![Click on to create new bucket](images/enter_name_click_create_pre_authenticated_reqeust_button.png =1000x500)

6. Copy the URI either by selecting it from the box or by clicking on the copy icon on the right side.
![Click on to create new bucket](images/copy_pre-authenticated_request_uri.png =1000x500)

  Your URI would look like

  https://objectstorage.us-ashburn-1.oraclecloud.com/p/YvB1YSywPUMK7PxLxa4i5ciUW-cmlOcOGMLc_ZA0EAcMWc1xEMVJMtQLApFdKCSo/n/oraclepartnersas/b/DataStream/o/

  **Save the URI into notepad as we would be using this in the further steps.**

  **Note:** the URI would look be like
  **https://objectstorage.<region>.oraclecloud.com/p/<--token-->/n/<--tenancy or namespace-->/b/<--Bucket Name-->/o/**

  Incase we have set the visibility of the bucket to public we can delete the section **"/p/<--token-->""**
  So your URI would look like
  **https://objectstorage.<region>.oraclecloud.com/n/<--tenancy or namespace-->/b/<--Bucket Name-->/o/**
  i.e., https://objectstorage.us-ashburn-1.oraclecloud.com/n/oraclepartnersas/b/DataStream/o/

## Task 2: Create Data loading job using Live Data feed

1. Go to ADW home page and click on service console button.
![Click on to create new bucket](images/go_to_adw_console.png =1000x500)

2. One the service console page select Development on the left hand menu and select Database Actions tile.
![Click on to create new bucket](images/under_development_menu_select_database_action.png =1000x500)

3. This would open a new tab with login page,  use the default user ADMIN and the password you assigned during database creation.
![Click on to create new bucket](images/login_to_database_actions_homepage.png =500x500)

4. Click on the Data Load tile to create a new data load job.
![Click on to create new bucket](images/in_database_actions_select_dataload_under_datatools.png =1000x500)

5. In the database actions page click on the Manage Cloud Store button
![Click on to create new bucket](images/click_on_manage_cloud_store_button.png =1000x500)

6. Click on the +Add Cloud Storage button
![Click on to create new bucket](images/click_on_add_cloud_storage_button.png =1000x500)

7. Enter name for the cloud storage and copy the pre-authenticated URI that we created earlier in the box labeled URI+bucket.
![Click on to create new bucket](images/enter_name_and_pre-authenticated_URI_and_click_test_button.png =1000x500)
    1. Click on the Test Button at bottom to test the connection.
    2. If the connection is successfully we see the message. "Cloud Storage URI is valid for the credentials provided"
    3. Click on Create button to create the
8. step 8
9. step 9
10. step 10


## Task 3: Load July data file and run import manually

1. step 1
2. step 2
3. step 3
4. step 4
5. step 5
6. step 6
7. step 7
8. step 8
9. step 9
10. step 10

## Task 4: Load first set of data and verify the data loaded

1. step 1
2. step 2
3. step 3
4. step 4
5. step 5
6. step 6
7. step 7
8. step 8
9. step 9
10. step 10

## Task 5: Use the data for analysis

1. step 1
2. step 2
3. step 3
4. step 4
5. step 5
6. step 6
7. step 7
8. step 8
9. step 9
10. step 10
