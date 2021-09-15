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

5. Enter a name for the pre-authenticated request. Ensure their are not spaces in the name. Choose the option for Bucket.
![Click on to create new bucket](images/enter_name_click_create_pre_authenticated_reqeust_button.png =1000x500)

6. Copy the URI either by selecting it from the box or by clicking on the copy icon on the right side.
![Click on to create new bucket](images/copy_pre-authenticated_request_uri.png =1000x500)

  Note the URI would look be like
  https://objectstorage.<region>.oraclecloud.com/p/\<---token----\>/n/<--tenancy/namespace-->/b/<--Bucket Name-->/o/

  delete the section "/p/<---token---->""

  So you URI would look like

  https://objectstorage.<region>.oraclecloud.com/n/<tenancy/namespace>/b/<Bukect Name>/o/

  i.e., https://objectstorage.us-ashburn-1.oraclecloud.com/n/oraclepartnersas/b/DataStream/o/

  **Save the URI into notepad as we would be using this in the further steps.**

## Task 2: Create Data loading job using Live Data feed


## Task 3: Load July data file and run import manually
## Task 4: Load first set of data and verify the data loaded
## Task 5: Use the data for analysis
