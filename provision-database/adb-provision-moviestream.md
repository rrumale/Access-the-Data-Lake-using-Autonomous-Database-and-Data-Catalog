# Provision an Autonomous Database

## Introduction

This lab walks you through the steps to get started using the Oracle Autonomous Database (Autonomous Data Warehouse [ADW] and Autonomous Transaction Processing [ATP]) on Oracle Cloud Interface. In this lab, you provision a new ADW instance.

Estimated Lab Time: 5 minutes

### Objectives

In this lab, you will:

-   Create an Oracle Cloud Infrastructure compartment
-   Provision a new Autonomous Database

### Prerequisites

-   This lab requires completion of the Get Started section in the Contents menu on the left.

<if type="freetier">
## Task 1: Create a Compartment

A compartment is a collection of cloud assets, like compute instances, load balancers, databases, etc. By default, a root compartment was created for you when you created your tenancy (ie, when you registered for the trial account). It is possible to create everything in the root compartment, but Oracle recommends that you create sub-compartments to help manage your resources more efficiently.

1. Click the three-line menu, which is on the top left of the console. Scroll down till the bottom of the menu, click **Identity & Security -> Compartments**. Click the blue **Create Compartment** button to create a sub-compartment.

    ![Click Identity & Security then Compartments.](images/click-identity-and-security-then-compartments.png " ")

    ![Click the Create Compartment button.](images/click-create-compartment.png " ")

2. Give the compartment a name and description. Be sure your root compartment is shown as the parent compartment. Press the blue **Create Compartment** button.

    ![Click the Create Compartment button.](images/click-create-compartment-button.png " ")

    The compartment has been created, in which you will create an Autonomous Database instance in the next steps.

## Task 2: Choose ADW from the Services Menu
</if>
<if type="livelabs">
## Task 1: Choose ADW from the Services Menu
</if>

1. Log in to the Oracle Cloud Interface.
2. Once you are logged in, you are taken to the cloud services dashboard where you can see all the services available to you. Click the navigation menu in the upper left to show top level navigation choices.

     > **Note:** You can also directly access your Autonomous Data Warehouse service in the __Quick Actions__ section of the dashboard.

    ![Oracle home page.](./images/navigation.png " ")

3. Click **Autonomous Data Warehouse**.

    ![Click Autonomous Data Warehouse.](https://raw.githubusercontent.com/oracle/learning-library/master/common/images/console/database-adw.png " ")

4. Make sure your workload type is __Data Warehouse__ or __All__ to see your Autonomous Data Warehouse instances. <if type="freetier">Use the __List Scope__ drop-down menu to select the compartment you just created.</if><if type="livelabs">In the __List Scope__, enter the first part of the LiveLabs compartment assigned to you, then select the compartment from the list.</if>

<if type="freetier">
    ![Check the workload type on the left.](images/list-scope-freetier.png " ")

   > **Note:** Avoid the use of the `ManagedCompartmentforPaaS` compartment as this is an Oracle default used for Oracle Platform Services.

</if>
<if type="livelabs">
    ![](images/livelabs-listscope.png)
</if>


5. This console shows that no databases yet exist. If there were a long list of databases, you could filter the list by the **State** of the databases (Available, Stopped, Terminated, and so on). You can also sort by __Workload Type__. Here, the __Data Warehouse__ workload type is selected.

<if type="freetier">
    ![Autonomous Databases console.](./images/no-adb-freetier.png " ")
</if>
<if type="livelabs">
    ![](images/livelabs-nodb.png)
</if>

<if type="freetier">
6. If you are using a Free Trial or Always Free account, and you want to use Always Free Resources, you need to be in a region where Always Free Resources are available. You can see your current default **region** in the top, right hand corner of the page.

    ![Select region on the far upper-right corner of the page.](./images/Region.png " ")
</if>

<if type="freetier">
## Task 3: Create the ADB Instance
</if>
<if type="livelabs">
## Task 2: Create the ADB Instance
</if>

1. Click **Create Autonomous Database** to start the instance creation process.

    ![Click Create Autonomous Database.](./images/Picture100-23.png " ")

2.  This brings up the __Create Autonomous Database__ screen where you will specify the configuration of the instance.

<if type="freetier">
    ![](./images/create-adb-screen-freetier-default.png " ")
</if>
<if type="livelabs">
    ![](./images/livelabs-adwconfig.png)
</if>

3. Provide basic information for the autonomous database:

<if type="freetier">
    - __Choose a compartment__ - Select the compartment you just created.
    - __Display Name__ - Enter a memorable name for the database for display purposes. For this lab, use __My Quick Start ADW__.
    - __Database Name__ - Use letters and numbers only, starting with a letter. Maximum length is 14 characters. (Underscores not initially supported.) For this lab, use __MYQUICKSTART__.

    ![Enter the required details.](./images/create-adb-screen-freetier.png " ")
</if>
<if type="livelabs">
    - __Choose a compartment__ - Use the default compartment created for you.
    - __Display Name__ - Enter a memorable name for the database for display purposes. For this lab, use __My Quick Start ADW__.
    - __Database Name__ - Use letters and numbers only, starting with a letter. Maximum length is 14 characters. (Underscores not initially supported.) For this lab, use __MOVIE+your user id__, for example, __MOVIE9352__.

    ![Enter the required details.](./images/livelabs-adwname.png " ")
</if>

4. Choose a workload type. Select the workload type for your database from the choices:

    - __Data Warehouse__ - For this lab, choose __Data Warehouse__ as the workload type.
    - __Transaction Processing__ - Alternatively, you could have chosen Transaction Processing as the workload type.

    ![Choose a workload type.](./images/Picture100-26b.png " ")

5. Choose a deployment type. Select the deployment type for your database from the choices:

    - __Shared Infrastructure__ - For this lab, choose __Shared Infrastructure__ as the deployment type.
    - __Dedicated Infrastructure__ - Alternatively, you could have chosen Dedicated Infrastructure as the deployment type.

    ![Choose a deployment type.](./images/Picture100-26_deployment_type.png " ")

6. Configure the database:

    - __Always Free__ - If your Cloud Account is an Always Free account, you can select this option to create an always free autonomous database. An always free database comes with 1 CPU and 20 GB of storage. For this lab, we recommend you leave Always Free unchecked.
    - __Choose database version__ - Select 19c as the database version.
    - __OCPU count__ - Number of CPUs for your service. For this lab, specify __1 CPU__. If you choose an Always Free database, it comes with 1 CPU.
    - __Storage (TB)__ - Select your storage capacity in terabytes. For this lab, specify __1 TB__ of storage. Or, if you choose an Always Free database, it comes with 20 GB of storage.
    - __Auto Scaling__ - For this lab, keep auto scaling enabled, to allow the system to automatically use up to three times more CPU and IO resources to meet workload demand.
    - __New Database Preview__ - If a checkbox is available to preview a new database version, do NOT select it.

    > **Note:** You cannot scale up/down an Always Free autonomous database.

    ![Choose the remaining parameters.](./images/Picture100-26c.png " ")

7. Create administrator credentials:

    - __Password and Confirm Password__ - Specify the password for ADMIN user of the service instance. The password must meet the following requirements:
    - The password must be between 12 and 30 characters long and must include at least one uppercase letter, one lowercase letter, and one numeric character.
    - The password cannot contain the username.
    - The password cannot contain the double quote (") character.
    - The password must be different from the last 4 passwords used.
    - The password must not be the same password that is set less than 24 hours ago.
    - Re-enter the password to confirm it. Make a note of this password.

    ![Enter password and confirm password.](./images/Picture100-26d.png " ")

8. Choose network access:
    - For this lab, accept the default, "Allow secure access from everywhere".
    - If you want a private endpoint, to allow traffic only from the VCN you specify - where access to the database from all public IPs or VCNs is blocked, then select "Virtual cloud network" in the Choose network access area.
    - You can control and restrict access to your Autonomous Database by setting network access control lists (ACLs). You can select from 4 IP notation types: IP Address, CIDR Block, Virtual Cloud Network, Virtual Cloud Network OCID).

    ![Choose the network access.](./images/Picture100-26e.png " ")

9. Choose a license type. <if type="freetier">For this lab, choose __License Included__.</if><if type="livelabs">For this lab, choose __Bring Your Own License (BYOL)__.</if> The two license types are:
    - __Bring Your Own License (BYOL)__ - Select this type when your organization has existing database licenses.
    - __License Included__ - Select this type when you want to subscribe to new database software licenses and the database cloud service.

<if type="freetier">
    ![](./images/license.png " ")
</if>
<if type="livelabs">
    ![](images/livelabs-byol.png)
</if>

10. Click __Create Autonomous Database__.

11.  Your instance will begin provisioning. In a few minutes, the state will turn from Provisioning to Available. At this point, your Autonomous Data Warehouse database is ready to use! Have a look at your instance's details here including its name, database version, OCPU count, and storage size.

    ![Database instance homepage.](./images/Picture100-32.png " ")

Please *proceed to the next lab*.

## Learn More

Click [here](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3) for documentation on the typical workflow for using Autonomous Data Warehouse.

## Acknowledgements

- **Author** - Nilay Panchal, ADB Product Management
- **Adapted for Cloud by** - Richard Green, Principal Developer, Database User Assistance
- **Last Updated By/Date** - Rick Green, August 2021
