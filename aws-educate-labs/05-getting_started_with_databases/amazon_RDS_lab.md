# Task1: Creating an Amazon RDS database

This task involves the creation of MYSQL database in Virtual Private CLoud VPC

## Steps:
1. On the Services  menu, choose **RDS**.

2. Choose **Create Database**
![Create Database](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/02-create_database.JPG)

![Choose Standard Create option](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/02-stancard_create.JPG)

### The lab Uses the Standard Create Method

3. Under **Engine options**, select  **MySQL**.

![Choose MySQL](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/03-choose_MySQL.JPG)

   - For Version, keep MySQL 8.0.28. 
 4. In the **Templates** section, select  **Dev/Test**

 ![Choose Dev/Test](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/04-Dev_Test.JPG)


 5. In the **Availability and durability** section, choose **Single DB instance**

 ![Select Siingle Database Instance](/aws/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/05-single_database.JPG)

6. In the **Settings** section next, configure the following options :

   - **DB instance identifier:** inventory-db
**Master username:** admin

- **Master password:** lab-password
- **Confirm password:** lab-password

7. In the **Instance configuration** section, configure the following options for DB instance class:

   - Choose  **Burstable classes (includes t classes).**
    - Choose **db.t3.micro**.

8. In the **Storage** section next,

    - For **Storage type** choose **General Purpose SSD (gp2)** from the Dropdown menu.
    - For **Allocated storage** keep 20.
    - Clear or Deselect **Enable storage autoscaling.**
9.  In the **Connectivity** section, configure the following options: 

    - For **Compute resource**

        - keep default  **Don’t connect to an EC2 compute resource**,  you will establish this manually later.

        ![Don't Connect to EC2](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/09-connectivity_section_1.JPG)
    
    - For **Virtual private cloud (VPC)** Choose **Lab VPC** from the Dropdown menu

    - For **DB Subnet group**, keep default value **rds-lab-db-subnet-group**
    - For **Public access** Keep default value **(No)**

    ![Choose no For Public Access](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/09-connectivity_section_2.JPG)

    - For **VPC security group (firewall)** 

        - Choose the **X** on **default** to remove this security group. 

        
        - Choose **DB-SG** from the dropdown list to add it.

        ![Choose DB-SG](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/09-connectivity_section_3.JPG)

        - For **Availability Zone**, Keep default **No preference**  
    - For **Database authentication** keep default value **Password authentication**
![Choose PAssword Authentication](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/09-connectivity_section_4.JPG)


10. In the Monitoring section

Clear/DeSelect the **Enable Enhanced monitoring** option.

![Clear Enhanced Monitoring](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/10-enhanced_monitoring.JPG)

11. Expand the following **Additional configuration** section by choosing
- Under **Database options**, for **Initial database name**, enter `inventory`

![Type Inventory](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/11-database_options.JPG)

- Leave other options at their defaults.

12. At the bottom of the page, choose **Create database**

![Click Create Database](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/12-create_database.JPG)

You should receive this message: **Creating database inventory-db.**

If you receive an error message that mentions **rds-monitoring-role**, confirm that you have cleared the **Enable Enhanced monitoring option** in the previous step, and then try again.

Make sure the database instance status shows available before moving on tho the next task

# Task 2: Configuring web application communication with the database instance

We will use the application already deployed automatically by the lab in an Amazon EC2 instance to configure connection settings which will be stored in ****AWS Secrets Manager** for further use.. Ensure that you use the IP address of the instance to connect to the application.

## Steps: 

13. On the **Services**  menu, choose ****EC2**.
14. In the left navigation pane, choose **Instances**.

In the center pane, there should be a running instance that is named **App Server**

15. Select the check box for the **App Server** instance.

16. In the **Details** tab, copy the **Public IPv4 address** to your clipboard.
Tip: You can choose copy   to copy the displayed value the displayed value.

17. Open a new web browser tab, paste the IP address into the address bar, and then press Enter.

![Web Application in primitive form](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/17-the_primitive_web_application_page.JPG)

The web application should appear. It does not display much information because the application is not yet connected to the database.

18. Choose  **Settings.**

![Choose Settings](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/18-choose_settings.JPG)

You can now configure the application to use the Amazon RDS database instance that you created earlier. You first retrieve the database endpoint so that the application knows how to connect to a database.

19. Return to the AWS Management Console, but do not close the application tab.

20. On the **Services**  menu, choose **RDS**.
21. In the left navigation pane, choose **Databases**.
22. Under **DB identifier**, Choose 'inventory-db'.

23. From the **Connectivity & security** section, copy the Endpoint to your clipboard.

It should look similar to this example: inventory-db.crwxbgqad61a.rds.amazonaws.com

24. Return to the browser tab with the inventory application, and enter the following values:

     - For **Endpoint**, paste the endpoint you copied earlier.
    - For **Database**, enter inventory
    - For **Username**, enter admin
    - For Password, enter lab-password

    ![Endppoint parameters](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/copy_endpoint.JPG)
Choose **Save**.

The application will now Save this information into **AWS Secrets Manager**  and connect to the database, load some initial data, and display information.

25. You can use the web application to   **Add inventory**,  edit, and  delete inventory information.

![Add Inventory](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/25-insert_new_records.JPG)

The inventory information is stored in the Amazon RDS MySQL database that you created earlier in the lab. This means that any failure in the application server will not lead to loss of any data. It also means that multiple application servers can access the same data.

26. Insert new records into the table. Ensure that the table has **5** or more inventory records.

27. Optional: To access the saved parameters, go to the **AWS Management console**. On the **Services  menu**, choose **Secrets Manager** , choose **Secrets**.

# Task 3: Monitoring the Database Instance

Monitoring is used to maintain the reliability, availability, and performance of any database.

This task involves exploring the many useful metrics for monitoring the health of you database instances provided by Amazon RDS.

28. Return to the **AWS Management Console**.

29. On the **Services**  menu , choose **RDS**.

30. Choose Databases.

31. Choose 'inventory-db'.

32. In the pane below, choose Monitoring tab.

![Monitoring tab](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/32-choose_monitoring_tab.JPG)

![CloudWatch Metrics](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/32-Cloud_watch_metrics.JPG)

Observe the CloudWatch metrics indicating respective database Instance parameters as shown in example below.

33. Perform various operations on the web application like add, update or remove records from inventory database and observe the changes in the values mentioned above.

34. Scroll down further to observe other  available metrics.

# Task 4: Task 4: Performing operations on Database.

This task show us some admin tasks that can be performed on the database in amazon RDS

35. Return to the **RDS Management Console** 
36. Choose **Databases**.

37. **Choose 'inventory-db'**.

38. Under **Actions** menu, there are various operations to perform e.g. **Stop** **temporarily, Reboot**, etc.


![Actions Menu](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/38-actions_menu.JPG)

39. Choose **Stop temporarily**, to stop the instance temporarily. (Database automatically restarts after 7 days)

    - Select checkbox under 'Acknolwedgement'
    - Choose  **Stop Temporarily**

    ![Stop temporarily](/AWS/aws-educate-labs/assets/screenshots/005-amazon_RDS_lab/39-automatinc_restart.JPG)

    **Note**: Stopping the instance also stops the billing charges associated with the running instance. Database(s) continues to occupy storage space and incur billing charges.

40. Refresh the browser after few minutes to verify that the instance is stopped. (Status = Stopped) 

Optional - You can **Start** the instance, re-connect it to the  web application and continue to use.

# Summary

In this lab I launched MYSQL RDS database instance, configured an existing web application to interact with the database instance. Then I performed basic tasks such as querying, updating records and monitored the various metrics to gain insights  into the health of the database and finally performed basic database administrative operations