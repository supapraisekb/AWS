# Task 1: Launching an EC2 instance

In this task, an EC2 instance is launched with termination protection

## Steps

1. Search for EC2 in the AWS Services management console and click on EC2

2. Choose EC2 dashboard from the left navigation pane to be sure that you are on the dashboard page

3. choose launch instance from the launch instance section

## Name Your EC2 Instance
Tas help us to categorize our instances in a variety of ways. It helps to us to easily filter and  identify a resource based on the tags assigned to them.

Name of an instance comprises of a key-value pair. 

## Steps

4. Enter ``` Web-Server ``` as the Instance name in the **Name** Text box under the  **Name and Tags** pane

5. Choose **Add Additional Tags**
6. From the **Resource Types dropdown list, choose **Instances and Volumes**.


## Choose an Amazon Machine Image (AMI)

An **Instance** is a virtual Server in the cloud. An AMI holds the information that is required to launch an instance.

An AMI includes 

- A template representing the OS or server with applications
- Launch permissions that determine which AWS accounts can use the AMI to launch instances
- A block device mapping telling us which volumes to attach to the instance when launched

There are some veryy commonly used AMIs which are listed in the **Quick Start**

## Steps

7. Scroll to ** Application and OS Images (Amazon MAchine Image) section
8. Enter ```Windows Server 2019 Base``` in the search box and enter
9. Choose **Select**
10. Choose **Confirm Changes**

## Choose an Instance Type

Different Amazon EC2 Instance types supprt different use-cases.

An **instance type** comprises of the various combinations of CPU, memory and storage. The Instance type chosen here will be t2.micro and the specifications for this instance are:
- virtual CPU: 1
- 1 GiB of RAM

## Steps  

11. In the instance type Section, choose the default instance type of T2. micro.

## Carry out your key pair configuration

Amazon EC2 makes use of Public Key Cryptography to encrypt and decrypt login information.  

A key pair is mandatory when you want to connect to your instance using ssh or rdp. 

For this lab, we continue without a key pair

## Steps:

12.  In the **Keyp pair (login)** Section, From the **Key pair name - required** dropdown, select  **Proceed without a key pair (not recommended)**

## Configuring the Network Settings

Network configuration is about choosing  a VPC which you want to launch the EC2 instance into. A single EC2 instance can be launched into several VPCs at once such as Development, Testing, and Production

## Steps

13. Under **Network Settings** section, Select **Edit**

14. From the **VPC - required** dropdown list, choose **Lab VPC**. 

Lab VPC is a VPC created for the lab and has two public subnets in two different availability zones

15. For **Security group name  - required**, select **Select existing security group**.

16. From **Common Security groups**, select **Web Server security group**

A security group acts as a virtual firewall and controls the traffic for one or more instances.

## Add a Storage

Amazon EC2 stores data on an Elastic Block Storage which is a network-attached virtual disk called the Elastic Block Storage (Amazon EBS).

The EC2 instance has a root or boot volume of 30 GiB

## Steps:

17. In the **Configure storage section, keep the defaulty storage configuration.

## Setup  Advanced Details

One of the major configurations in this section is the Termination protection. Instances terminated cannot be restarted and all the data will be lost. It is best practice to configure terminatin protection under the advanced details.

18. Expand the **Advanced details**
19. For the **Instance profile**, choose the role LabInstanceProfile

20. From **Termination protection** dropdown, choose **Enable**.

Another important configuration in the Amazon EC2 Advanced details is the configuration for user data. setting up this can help you perform common automation configuration tasks and even run scripts after the instance has started.

21. Copy th following commands, and paste them into the **User data** text box

```
<powershell>
# Installing web server
Install-WindowsFeature -name Web-Server -IncludeManagementTools
# Getting website code
wget https://us-east-1-tcprod.s3.amazonaws.com/courses/CUR-TF-100-EDCOMP/v1.0.4.prod-ef70397c/01-lab-ec2/scripts/code.zip -outfile "C:\Users\Administrator\Downloads\code.zip"
# Unzipping website code
Add-Type -AssemblyName System.IO.Compression.FileSystem
function Unzip
{
    param([string]$zipfile, [string]$outpath)
    [System.IO.Compression.ZipFile]::ExtractToDirectory($zipfile, $outpath)
}
Unzip "C:\Users\Administrator\Downloads\code.zip" "C:\inetpub\"
# Setting Administrator password
$Secure_String_Pwd = ConvertTo-SecureString "P@ssW0rD!" -AsPlainText -Force
$UserAccount = Get-LocalUser -Name "Administrator"
$UserAccount | Set-LocalUser -Password $Secure_String_Pwd
</powershell>

 ```

The above code is a script that does the following:

- installs a Microsoft Internet Information Service (IIS) web server

- creates a simple we site 
- Sets the password for the Admin User

## Launch the EC2 Instance

You launch the configured instance for use

22. In the **Summary** section, choose **Launch Instance** 

23. Choose **View Instance**

There are two states 

- **Pending State:** 

This indicate that the EC2 instace is in the state of being launched

- **Running State:** 
This indicates that the Instance is now booting but wait a bit before you can access the instance 

24. Next to the Web-server Instance, select the  - [ ] check box. This displays the **Details** tab which gives detailed information about the instance

You can drag the windows divider upwards to see more infomation in the **details** tab.

25. Your instance is ready when it displays the following:

- Instance State: Running
- Status Checks: 2/2 checks passed

# Task 2: Monitoring the Instance

To maintain the reliability, availability and performance of your EC2 instance, it is imparative to monitor you Instances. This section deals with monitoring your instances. 

## Steps:
26. Choose the **Status checks** tab

Status monitoring gives a quick view of any problems that have been detected and that may prevent the instances from running application. 

Confirm that the **System reachability** and **Instance reachability** checks have passed.

27. Select the **Monitoring** tab

Normally, this tabs displays the **CloudWatch metrics** for the running instances. Notice that there are not many metrics to display because the instance was recently launched. Click on the graph to get an expanded view.

By default, **Basic Monitoring** (5 Minutes) is the default setting but you can choose the **Detailed Monitoring** (1 Minute) which attracts a cost per metric sent to the CloudWatch 

28. At the top of the page, choose the **Actions** dropdown menu. Select **Monitor and troubleshoot** then **Get system log**.

System log is a valuable tool to diagnose anomalies in the instance. It is particularly useful for troubleshooting service configuration issues especially when an iinstance terminates or becomes unreachable.
Sytem logs may be initially unavailble but will typically appear after a few minutes.

29. Scroll through the log and checkout the messages in the output.

30. Choose **Cancel** to revert to the EC2 dashboard

31. to get the instance screenshot, select the **Web-server** instance, chooe the **Actions** dropdown, click **Monitor and troubleshoot** the select **Get instance Screenshot**

Usually, the option shows what the EC2 instance looks like with a screen. It is helpful when you cannot connect t the instance via SSH or RDP. you can use this option to visualize you page fo quicker troubleshooting.

32. Choose **Cancel** at the bottom of the page

# Task 3: Updating the security group and accessing the web server installed
 
Recall that in **step 21**, we launched the EC2 instance with a script we provided to install the web server in order to create a simple web page. 
The goal of this task os to access the content from the webserver.

## Steps:

33. Select the **check box** next to the EC2 **Web-Server** instance created and choose the **Details Tab**

34. Copy the **public IPV4 address** of the instance

35. In your web browser, open a new tab, and paste the IP address you copied and then press Enter

**Notice** that the web server is not accessible because the security group has not been set to permit inbound traffic on port 80 (port 80 is used for HTTP web requests)

To solve this issue, you now update the security  group to permit web traffic on port 80.

36. Return to the EC2 Mabagement Console tab.

37. In the left navigation pane, choose **Security Groups**

38. Next to **Web Server security group**, select the check box
39. Choose the **Inbound rules tab**

NOtice that the security group currently has no rules.

40. Select **Edit Inbound rules**, Choose **ADD Rule**







