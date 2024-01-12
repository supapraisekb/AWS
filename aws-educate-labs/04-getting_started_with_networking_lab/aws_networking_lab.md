Part 1: Exploring the Default VPC

# Task 1: Exploring the Example of VPC Configuration

In this section, i explored the example VPC provided by AWS. It is a model of the default VPC created with every AWS account.

VPCs are logically isolated from other Virtual networks in the AWS cloud. 

Below is an Architectural model of a VPC

![Default VPC architecture in an AWS Account](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/01-Default_VPC_architecture.JPG)

From the lab environment:

1. I acessed the **services** menu the AWS managemnet console and typed **VPC**. I chose ***VPC*** from the search results. 

2. Too see the available VPCs, in the left navigation pane i chose **Your VPCs**

There are two existing VPCs created for the lab namely: default VPC and Ecample VPC.

![Default and Example VPC]()

3. I noticed that the Example VPC has a CIDR block of 

```
172.31.0.0/16
```

This CIDR range includes all addresses from 172.31.0.0 through 172.31.255.255

4. I took note of the VPC ID of the Example VPC for later use

#Task 2: Exploring a Subnet

The goal of this task is to take a deeper look into the subnet address.

A subnet is a subrange of IP addresses in the VPC. AWS resources can be launched into specified subnets. It is a good practice to use a bpublic subnet for the resources you want to make available to users access over the internet. Resources such as applications data and databases that you want to be obscured from the public should be on the private subnet.

The image below is an example of a VPC with 4 subnets

![Sample VPC with 4 Subnets](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/task2-Sample-vpc-with-4-subnets.JPG)

5. Choose **Subnets** from the navigation pane.

I noticed that all the subnets that begin with the name **Public Subnets** are associated with the Example VPC.

![choose subnets]()

Each of the subnets has it's own different IPV4 CIDR range.  Always ensure that CIDR ranges do not overlap when planning your design

6. FFrom the list of Subnets iI chose the subnet named **Public Subnet 1**

The subnet has a CIDR block of 172.31.0.0/20

``The VPC has a CIDR block of 172.31.0.0/16``  

This subnet under review has a CIDR block of 172.31.0.0/20

Adress ranges from 
``172.31.0.0 - 172.3115.255``

a total of 4,096 address. 

i noticed that the console display only 4,091 addresses as being available because AWS reserves 5 address in each subnet.

7. The **Auto-assign public IPV4 address** is set to **Yes** 

For this reason, the subnet automatically assigns a public IP address for all instances that are launched into it.

# Task 3: Exploring the Internet Gateway

The goal of this task is to give insignt into the VPC's internet gateway (IGW).

Internet gateway is the mechanism that permits the flow of traffic from resource in a the VPC to the internet. IGW is highly available and horisontally scalable. 

![internet gateway architecture](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/07-IGW_architecture.JPG)

**The two subnets have access to the internet through the internet gateway*


Two main functions of the IGW are:

- To designnate a target in the route tables that connects to the internet
- To perform network address translation (NAT) for the instances that have a public IP address.

8. I chose **Internet Gateways** from the navigation pane

![Select internet gateways from nav pane]()

9. I selected the row containing the internet gateway named **Example Internet Gateway**

I observed that the **State** of the internet gateway is **Attached**.

To see what VPC the internet gateways is attached to, check the **VPC ID** . It corresponds to the example VPC's id.


# Task 4: Exploring a Route Table 

In this task, I explored the route table  used by the Ezample VPC.

Before subnets can have access to the internet gateway, the **route table** associated with the subnets must be configured to use the internet gateway.

Route tables consist of a set of rules known as **Routes** which are used to specify where network traffic should go to. 
- Each subnet in a VPC must be associated with a single route table
- You can associate several subnets with  with the same route table


![VPC arcitecture showing a route table](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/Task4-subnets-with-route-table.JPG)

**The route table contains:**

a. A route that directs internet-bound traffic to the IGW. Any subnet that is associated route table that contains a route to an IGW is known as a **Public subnet**

b. and a local ip of the VPC 


10. In the left navigation pane I chose **Route Tables**

11. I located and selected the route table named **Public Route Table** 

12. Choose the routes at the lower half of the page.

I observed two routes:

a. a local route 

b.  apublic route

All route target at ``172.31.0.0/16`` which is the range of the example VPC are routed Locally and allows all subnets in this vp communicate with each other

All internet bound traffic destined for ``0.0.0.0/0`` are routed to the internet gateway

13. I chose **Subnet associations**

tab

14. In the **Explicit subnet associations** section, I saw that that the subnet with the IPV4 CIDR ``172.31.0.0/20`` is included in the ist. 
This is a different subnet from what i reviewed earlier.

All of the subnets in the lsit are public subnets because they have a route table entry that sends traffic to the internet through the internet gateway

# Task 5: Exploring the Security Groups

The aim of this task is to look deeper into the Secutiry group already setup for use in the Example VPC. I will create a custom vps and create and inbound rule for HTTP.

A **security group** acts as a virtual firewall for the instances provisioned in the VPC.

It controls the inbound and outbound traffic to the instance. 

![VPC architecture showing Security Grouo table](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/task5-security-groups.JPG)

15. I selected **Security groups** from the left navigation pane
16. Find and select the row which containsthe **default** securty group of the Example VPC 

N/B: I located the Examole VPC using the ID i saved earlier in the task

17. from the lower half of the page I chose the **Outbound Rules** tab 

The rule allows **all** protocols and **all** port ranges to send traffic to any IP address  ``0.0.0.0/0``

18. Chose the **Inbound Rules** tab


This rule allows all incoming traffic to **All** Protocols and **All** ports from resources that use the default  SG.

It is against good practices to make changes to the default security group rather I will need to create a new one and then add a rule to the new security group according to the specified needs

18. Locate a row containing the **Web-Server-SG** security group for the Example VPC and select it

19. In the lower half of the page, I chose **Inbound Rules** tab
20. **Edit Inbound rules**
21. **Add rule**
22. I made the following configurations:

- For **Type** I chose **HTTP**
- From **Source type** dropdown, I chose **Anywhere IPV4**
- For the **Description**, enter 

```
Allow web access
```
23. **Save Rules**

# Task 6: Identify an EC2 Instance's VPC and subnet

The purpose of this task is to enable me find the VPC and subnet for an EC2 instance.  I also need to test the **Web-Server_SG** security group configuration by confirming that I have acess to the EC2 instance.

![SG of an EC2 instance in a VPC and subnet](/AWS/aws-educate-labs/assets/screenshots/004-amazon_networking_lab/task6-EC2-instance.JPG)

24. On the **Services** menu, I chose intsances
25. I selected the **Instances (Running)** option

26. I selected **Web-server**
27. In the details tab, the value for the **VPC ID** was located. It is verified that there is an EC2 instance deployed into the **Example VPC**. The VPC and subnet specified when reating a subnet cannot be changed.

## I Tested the connectivity by Verifying that I can reach the website

28. From the details tab, I copied the **Public IPV4 address** 
29. On a new browser tab, I pated the IP copies and pressed Enter key and go a **Hello from your webserver!** mesage

# Part 2: Creating a VPC

Being able to use the default VPC during learning about and working with AWS cloud is very convenient. However, in the real world, you often need to create custom VPCs to meet a customer's requirements. For example, a customer might have already used the CIDR range of the default VPC in their on-premises network configuration. A customer might also want to vary how many addresses are included in each subnet. Because it is not possible to change the CIDR ranges assigned to the VPC or its subnets, you need to create a new VPC for your customer.


In this part of the lab I will create a VOC witht the following requirements given by a hypothetical customer


Top-level VPC

- **VPC IPv4 CIDR** - ```10.0.0.0/16```

Availability Zones:

- They need to deploy their resources to two Availability Zones.

Two public subnets:

- **Public Subnet 1** - ```10.0.0.0/24```

- **Public Subnet 2** - ```10.0.1.0/24```

Two private subnets:

- **Private Subnet 1** - ```10.0.2.0/24```

- **Private Subnet 2** - ```10.0.3.0/24```


# TASK 7: Create a Custom VPC

A VPC is configured by defining its IP address range and creating subnets. You can also configure route tables, network gateways, and security settings.

The VPC console provides a wizard that can automatically create several VPC architectures. this this wizard is used to create a new VPC.

30. Return to the browser tab with the AWS console.

31. In the AWS Management Console on the **Services menu**, enter VPC. From the search results, choose **VPC**.

Any value not provided by the lab instructions was left as a default value.

32. In the left navigation pane, choose **Your VPCs**.

33. Choose **Create VPC** and configure the following settings:

- For **Resources to create**, choose **VPC and more**

- For **Name tag auto-generation**, enter ```Lab```.

- For **IPv4 CIDR block**, ensure that the value is ```10.0.0.0/16```.

For **Availability Zones (AZs)**, choose **2**.

- For **Number of public subnets**, choose **2**.

- For **Number of private subnets**, choose **2**.

- Expand **Customize subnets CIDR blocks**.

- Update the subnet CIDR block values using the ranges provided by your customer.

34. Take a moment to review the **Preview** diagram provided in the wizard.

Choose **Create VPC**.

The wizard immediately starts creating your VPC. After it finishes, you have a VPC that has all of the components that you explored earlier: subnets, route tables, an internet gateway, and a default security group. The VPC wizard also automatically configures the routes in the route tables for both the public subnets and the private subnets.


 Thhe default security group explored earlier, shows that the default security group created by the wizard blocks incoming traffic from the internet. To reach a web server in the new VPC, you need to add a rule to this default security group.

35. Choose **View VPC**.

A VPC's default security group does not allow traffic from outside the VPC. 

 I added a new security group to my custom VPC because changing a VPC's default settings is wrong.

36. In the left navigation pane, **choose Security** Groups.

37. Choose **Create security group**.

38. For **Security group name**, enter 

```
Web-Server2-SG
```

39. For **Description**, enter 
```
Allows HTTP access
```

40. For **VPC**, clear the selection and then choose **Lab-vpc**.

41. In the **Inbound rules** section, choose **Add rule**, and then configure the following settings:

- For **Type**, choose **HTTP**.

From the **Source type** dropdown list, choose **Anywhere IPv4**.

For Description, enter
 ```
Allow web access.
```

Choose **Create security group**.

 

# Task 8: Explore the configuration settings for launching an EC2 instance into your custom VPC

In this task, you explore the Launch an instance page, and enter the settings required to launch a new EC2 instance into your custom VPC. However, you will not complete the process and launch a new EC2 instance.

Note: In this lab, you do not have permission to create a new EC2 instance.

 

42. On the **Services**  menu, choose **EC2**.

43. In the **Launch instance** section, choose the **Launch instance** button. Configure the following options:

- In the **Name and tags pane**, in the **Name** text box, enter 

```
Web-Server2
```

- Choose an Amazon Machine Image (AMI).

a. In the **Application and OS Images (Amazon Machine Image)** section, choose **Amazon Linux**.

From the list of Amazon Machine Images, select **Amazon Linux 2 AMI**.

**Note:** Do not choose **Amazon Linux 2023 AMI**. 

- Choose an Instance Type:

- Select **t2.micro**.

- In the **Key pair (login)** section, from the **Key pair name - required** dropdown list, choose **Proceed without a key pair (not recommended)**.

- In the **Network settings** section, choose **Edit**.

- For **VPC - required**, choose **Lab-vpc**.

- For **Subnet**, choose the subnet with **public1** in the name.

- For **Auto-assign public IP**, choose **Enable**.

- For **Firewall (security groups)**, choose **Select an existing security group**.

- From the **Common security groups** dropdown list, choose the **Web-Server2-SG** security group.

- In the  **Advanced Details** section, for **IAM instance profile**, choose **Work-Role**.

- In the **Advanced Details** section, copy the following commands, and paste them into the User data text box:

```
#!/bin/bash
# Install Apache Web Server and PHP
yum install -y httpd mysql
amazon-linux-extras install -y php7.2
# Download Lab files
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-EDNETW-1-60961/1-lab-getting-started-vpc/s3/inventory-app.zip
unzip inventory-app.zip -d /var/www/html/

# Download and install the AWS SDK for PHP
wget https://github.com/aws/aws-sdk-php/releases/download/3.62.3/aws.zip
unzip aws -d /var/www/html
# Turn on web server
chkconfig httpd on
service httpd start

```
- Take a moment to review the settings you entered.

- In the Summary section, choose Cancel.

- I successfuly created a custom vpc following these steps


# Closing the Lab

Choose **End Lab** at the top of this page, and then choose **Yes** to confirm that you want to end the lab.

A panel indicates that **DELETE has been initiated... You may close this message box now. Lab resources are terminating**.

Select the **X** in the upper-right corner to close the panel.