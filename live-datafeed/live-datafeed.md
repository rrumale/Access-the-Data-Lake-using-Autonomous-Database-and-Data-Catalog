# Loading data from Data Feed

## About this lab

In this lab we would look at example to load data using the **Live Data Stream** feature that allows us to load the latest data from the OCI Bucket,  this bucket act as Data Lake for receiving and collecting the stream data received from application.  We would use the sample data coming in form from CSV files for month of July and August 2020.  The data used in this in CSV format and we would upload the file in the bucket to simulate data received in the bucket.  The live feed job would create a table MOVIESTREAM_DATAFEED based on the columns defined in the CSV file and load any data that is already present in the during the first run.  Based on schedule set job would get executed, however in the subsequent runs it would look for new data loaded in the bucket and would load the rows into the existing table.  Use sqldeveloper tool to check table creation and loading of row from the live feed.

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


## Task 1: Create a new bucket, add initial data and create pre-authenticated request URI

1. To crates a new bucket. Login to the Oracle cloud. From the main menu select storage and then Bucket.
![Click the Open Bucket Admin Page](images/go_to_storage_and_bucket.png =1000x500)

2. Click on to create new bucket.
![Click on to create new bucket](images/click_on_create_bucket_button.png =1000x500)

3. In the Create Bucket dialog box give appropriate name for the bucket. Leave all other options as default.
  ![Click on to create new bucket](images/enter_name_for_bucket_and_click_create.png =1000x500)

  On completion you will see the new bucket name in the list of buckets

4. To Upload the datafile for the initial load. Got to the Bucket Details page and Click on the bucket name to open the bucket.
![Click on to create new bucket](images/click_on_upload_button_to_upload_initial_dataload_file.png =1000x500)

5. Enter object name and select the file to be uploaded, wait for few seconds for the file details to be accepted. Once the file name appears in the window click on upload button to upload the file.
![Click on to create new bucket](images/enter_object_name_and_select_file_tobe_uploaded.png =1000x500)

  Once the upload start we can see the progress and finish message. Click close button to close the upload dialog box and go to the bucket details page.
  ![Upload finished message](images/upload_finished_message.png =250x500)

  You should be able to see the name of recently updated file in the objects listing in bucket details page.
  ![Upload finished message](images/bucket_object_list_showing_uploaded_file.png =500x500)  

  Note: In current example we are using small data set from the July 2020 data. This file could be file with single empty records.  Live feed would pickup the file and load the data based on the format it recognizes. OCI support several file formats of which JSON and CSV formats are more commonly used.

6. To create pre-authenticated request on the bucket. Click on the vertical 3 dots icon on the right end of the bucket name and select the create pre-authenticated request option.  
![Click on to create new bucket](images/click_the3dots_and_select_create_pre_authenticated_request.png =1000x500)

  You also create new or view existing pre-authenticated request on the bucket from pre-authenticated request link under Resources menu in the Bucket Details page.
  ![Click on to create new bucket](images/pre-authenticated_requests_options_in_bucket_details_page.png =1000x500)
  ![Click on to create new bucket](images/listing_pre-authenticated_requests_on_bucket.png =1000x500)

  Note: (a) By default the visibility is set a private.  Its standard practice to keep bucket visibility private and create pre-authenticated request URI on which we can set permission and a expiry date.  

7. Enter a name for the pre-authenticated request. Ensure their are not spaces in the name. Choose the option for Bucket and check the Enable Object Listing option.
![Click on to create new bucket](images/enter_name_click_create_pre_authenticated_reqeust_button.png =1000x500)

8. Copy the URI either by selecting it from the box or by clicking on the copy icon on the right side.
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

## Task 2: Create loading job using Live Data feed

1. Go to ADW home page and click on service console button.
![Click on to create new bucket](images/go_to_adw_console.png =1000x500)

2. One the service console page select Development on the left hand menu and select Database Actions tile.
![Click on to create new bucket](images/under_development_menu_select_database_action.png =1000x500)

3. This would open a new tab with login page,  use the default user ADMIN and the password you assigned during database creation.
![Click on to create new bucket](images/login_to_database_actions_homepage.png =500x500)

4. Click on the Data Load tile to create a new data load job.
![Click on the Data Load tile to create a new data load job](images/in_database_actions_select_dataload_under_datatools.png =1000x500)

5. Select the Data feed tile.
![Click on the Feed Data option and click next](images/select_feed_data_option_and_click_next.png =1000x500)
  Note: On selecting live feed option, you would notice the source would is automatically selected as Cloud storage. This is because that is the only option available for Live Feed.

6. In the database actions page click on the Manage Cloud Store button
![click on the Manage Cloud Store button](images/click_on_manage_cloud_store_button.png =1000x500)

7. Click on the +Add Cloud Storage button
![Click on Add Could Storage button](images/click_on_add_cloud_storage_button.png =1000x500)

8. Enter name for the cloud storage and copy the pre-authenticated URI that we created earlier in the box labeled URI+bucket.
![Enter cloud storage name and URI](images/enter_name_and_pre-authenticated_URI_and_click_test_button.png =750x500)
    1. Click on the Test Button at bottom to test the connection.
    2. If the connection is successfully we see the message. "Cloud Storage URI is valid for the credentials provided"
    3. Click on Create button to create the
9. You would see the new tile getting created with the cloud storage name, we would also get a confirmation message on top right corner(which goes away in few seconds).
![Confirmation message of Cloud storage creation](images/confirmation_message_of_new_cloud_storage.png =1200x1000)

10. Next we would create the Live feed job using the cloud store we just created.  For this click on browser back button to go back to Live data feed home Page. Then click on the Create Live Table Feed button on the top right corner.
![Click on create live table feed button](images/click_on_create_live_table_feed_button.png =1200x1000)

11. In the Live table feed creation window fill in the details as need.
![Fill in the details for the live table feed and click create button](images/fill_in_details_for_live_table_feed_and_click_create.png =500x500)
    1. In this example we would give live feed name & live feed table name as MOVIESTREAM_DATAFEED.
    2. Since we are using CSV files in this example we would use string *.csv.
    3. Check Enable Schedule to set a schedule. For this example the schedule is set for 1 day as we would execute the job manually with immediate option to save time. In practice you can set the interval based on your application requirement and volume of data received.
    4. Check the Start Date, default value is current date and time.  End date can be specified if we are expecting data feed to stop after a period.


    Note: The Object filter can be added to filter files using sub folder, file name pattern & file extension types. This is useful when we have lot of streams coming into Data lake or Bucket we created.  It allows us to create Multiple live feed jobs to load data specific files mapped to specific live feed tables in ADW.  

12. Confirmation of new live feed schedule created. A message appears on the top right corner and a new tile get created in the search area.
![Confirmation message of successful creation of new live feed job](images/confirmation_message_of_new_live_feed_schedule.png =1200x1000)

13. Manually execute the data load immediately. OR alternatively can wait for the job to run as per the schedule you have set while creating data feed.
![Confirmation message of successful creation of new live feed job](images/run_live_table_feed_immediately_once.png =1200x1000)

14. Login via sqldeveloper to check the creation of new Live feed table by name "MOVIESTREAM_DATAFEED".  You might have to refresh the schema to for new table and structure to get listed. Run a select statement so view the data from table.  Note It takes seconds to after the data load is completed to show the columns list under the table.
![Verify the Live feed table and data loaded in the initial load](images/check_table_and_data_loaded_from_sqldeveloper.png =1000x1000)

## Task 3: Load the next data set

To simulate a stream of data being collected, we would upload a new file in the bucket we created and test the loading of data.  The Live feed object would be running based on the schedule we have defined. It would check for any new objects being added.  When it finds a new object it would pickup and load the data in the existing live feed table "MOVIESTREAM_DATAFEED".  We can take record count to see the number of records loaded in the second run.

1. Check the record count in the table before the next load.
![Get record count before next load](images/record_count_before_next_load.png =1000x500)

2. Go to the bucket and load the August data set.  Follow the same step for loading data file in bucket we did earlier.
![Upload the next data set](images/upload_august2020_data_file.png =1000x500)
  The file would listed in the object list of bucket.
![New file will show in the object list](images/upload_august2020_data_file_2.png =1000x500)

3. Run the Live Feed job immediately.  Alternatively you can wait for the job to run as per schedule.  
![Confirmation message of successful creation of new live feed job](images/run_live_table_feed_immediately_once.png =1000x1000)

4. Check row count to verify the number of records loaded in table.  Go to sqldeveloper and check the row count.
![Confirmation message of successful creation of new live feed job](images/record_count_before_after_next_load.png =1000x1000)

Since the both the files have same number of records, and we have all the records loaded we would see double the number of row that existed earlier.

**We can continue to load more set of file or create an OCI logging job to write to the data lake based on the application requirement.**

## Task 4: Verify the Live Data feed job logs.

We can check the execution history of Live feed jobs and any errors received from the logs. The logs can we viewed from the log history from the "Live Table Feed Run Details" on the Live feed job we created. We can also query the table CLOUD\_INGEST\_LOG where errors encountered are during data load are logged.

1.  Checking job history from "Live Table Feed Run Details" option on Live feed job. Go to the live feed page, on the MOVIESTREAM_DATAFEED tile click on the vertical 3 dots icon to open the menu. click on "Live Table Feed Run Details"
    ![Check Live Feed Run Details from live feed schedule ](images/check_live_feed_run_details_from_live_feed_schedule.png =1000x1000)

    This would open Live Table Feed Run Details dialog box. The dialog box has tow tabs "Loaded files" & "Log".

    The default selected is "Loaded files" which shows the files that were loaded and number of records loaded in each run.

    ![Check Live Feed Run Details from live feed schedule ](images/live_table_feed_run_details_loaded_files.png =1000x1000)

    Click on the "Log" tab to see the log history of action it is doing to load the data.  This show the sub task, time, status and message related to sub tasks.

    ![Check Live Feed Run Details from live feed schedule ](images/live_table_feed_run_details_log.png =1000x1000)

2. CLOUD\_INGEST\_LOG table in the schema. This table gets created along with the Live feed table. Any errors encountered during the Live feed load job runs are logged into this tables.  Its easier to manually check the details from sqldeveloper or we can supply the data to application can handle them.
![Check Live Feed Run Details from live feed schedule ](images/cloud_ingest_log_table_in_schema.png =1000x1000)

3. Live feed logs.  On the live feed page you click on the settings icon on the bottom left corner of the window.  This would open up a Database Action Processes dialog box showing the history of the live feed job runs.
![Check Live Feed Run Details from live feed schedule ](images/check_logs_from_settings_icon_on_live_feed_page.png =1000x1000)
