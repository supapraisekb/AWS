# Task 1: Launching an EC2 instance

In this task, an EC2 instance is launched with termination protection

## Steps

1. Search for EC2 in the AWS Services management console and click on EC2

2. Choose EC2 dashboard from the left navigation pane to be sure that you are on the dashboard page

3. choose launch instance from the launch instance section

## Name Your EC2 Instance
Tags help us to categorize our instances in a variety of ways. It helps to us to easily filter and  identify a resource based on the tags assigned to them.

Name of an instance comprises of a key-value pair. 

## Steps

4. Enter ``` Web-Server ``` as the Instance name in the **Name** Text box under the  **Name and Tags** pane

5. Choose **Add Additional Tags**
6. From the **Resource Types dropdown list, choose **Instances and Volumes**.

![Instances and Volumes](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/06-instances-and-volumes.JPG)


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

![Search for Windows Server 2019 base](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/08a-windows-server-search.JPG)

9. Choose **Select**

![Choose Select](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/09-choose-select.JPG)

10. Choose **Confirm Changes**


## Choose an Instance Type

Different Amazon EC2 Instance types supprt different use-cases.

An **instance type** comprises of the various combinations of CPU, memory and storage. The Instance type chosen here will be t2.micro and the specifications for this instance are:
- virtual CPU: 1
- 1 GiB of RAM

## Steps  

11. In the instance type Section, choose the default instance type of T2.micro.

![Instance type t2.micro0-](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/11-instance-type-t2.JPG)
## Carry out your key pair configuration

Amazon EC2 makes use of Public Key Cryptography to encrypt and decrypt login information.  

A key pair is mandatory when you want to connect to your instance using ssh or rdp. 

For this lab, we continue without a key pair

## Steps:

12.  In the **Key pair (login)** Section, From the **Key pair name - required** dropdown, select  **Proceed without a key pair (not recommended)**

![Proceed without a key paid](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/12-proceed-without-key.JPG)


## Configuring the Network Settings

Network configuration is about choosing  a VPC which you want to launch the EC2 instance into. A single EC2 instance can be launched into several VPCs at once such as Development, Testing, and Production

## Steps

13. Under **Network Settings** section, Select **Edit**

![Select Edit button](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/13-select-edit.JPG)

14. From the **VPC - required** dropdown list, choose **Lab VPC**. 

![Network and security group settings](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/14-16-network-and-sg-settings.JPG )

Lab VPC is a VPC created for the lab and has two public subnets in two different availability zones

15. For **Security group name  - required**, select **Select existing security group**.

16. From **Common Security groups**, select **Web Server security group**

A security group acts as a virtual firewall and controls the traffic for one or more instances.

## Add a Storage

Amazon EC2 stores data on an Elastic Block Storage which is a network-attached virtual disk called the Elastic Block Storage (Amazon EBS).

The EC2 instance has a root or boot volume of 30 GiB

## Steps:

17. In the **Configure storage** section, keep the defaulty storage configuration.

![Configure Storage](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/17-configure%20-storage.JPG)

## Setup  Advanced Details

One of the major configurations in this section is the Termination protection. Instances terminated cannot be restarted and all the data will be lost. It is best practice to configure terminatin protection under the advanced details.

18. Expand the **Advanced details**

19. For the **IAM Instance profile**, choose the role LabStack

![IAM instance profile](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/19-iam-instance-profile.JPG)


20. From **Termination protection** dropdown, choose **Enable**.

![Enable Termination Protection](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/20-termination-protection.JPG)

Another important configuration in the Amazon EC2 Advanced details is the configuration for user data. setting up this can help you perform common automation configuration tasks and even run scripts after the instance has started.

21. Copy the following commands, and paste them into the **User data** text box

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

![Launch Instance](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/22-launch-instance.JPG)

23. Choose **View Instance**

![Instance showing running state](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/23-instance-running-state.JPG)

There are two states 

- **Pending State:** 

This indicate that the EC2 instace is in the state of being launched

- **Running State:** 
This indicates that the Instance is now booting but wait a bit before you can access the instance 

24. Next to the Web-server Instance, select the  - [ ] check box. Click actions and select **View Details** tab which gives detailed information about the instance

![View Instance Details](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/24--instance-details.JPG)

You can drag the windows divider upwards to see more infomation in the **details** tab.

25. Your instance is ready when it displays the following:

- Instance State: Running
- Status Checks: 2/2 checks passed

![Instance Ready](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/25-instance-ready.JPG)
# Task 2: Monitoring the Instance

To maintain the reliability, availability and performance of your EC2 instance, it is imparative to monitor you Instances. This section deals with monitoring your instances. 

## Steps:
26. Choose the **Status checks** tab

![Status Checks tab](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/26-status-reachability.JPG)

Status monitoring gives a quick view of any problems that have been detected and that may prevent the instances from running application. 

Confirm that the **System reachability** and **Instance reachability** checks have passed.

27. Select the **Monitoring** tab

Normally, this tabs displays the **CloudWatch metrics** for the running instances. Notice that there are not many metrics to display because the instance was recently launched. Click on the graph to get an expanded view.

By default, **Basic Monitoring** (5 Minutes) is the default setting but you can choose the **Detailed Monitoring** (1 Minute) which attracts a cost per metric sent to the CloudWatch 

28. At the top of the page, choose the **Actions** dropdown menu. Select **Monitor and troubleshoot** then **Get system log**.

![Get System Log](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/28-get-system-log.JPG)

System log is a valuable tool to diagnose anomalies in the instance. It is particularly useful for troubleshooting service configuration issues especially when an iinstance terminates or becomes unreachable.
Sytem logs may be initially unavailble but will typically appear after a few minutes.

29. Scroll through the log and checkout the messages in the output.

30. Choose **Cancel** to revert to the EC2 dashboard

31. to get the instance screenshot, select the **Web-server** instance, chooe the **Actions** dropdown, click **Monitor and troubleshoot** the select **Get instance Screenshot**

![Get Instance Screenshot](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/31-get-instance-screenshot.JPG)

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

![Web Server not accessible](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/35-web-server-not-accessible.JPG)

To solve this issue, you now update the security  group to permit web traffic on port 80.

36. Return to the EC2 Management Console tab.

37. In the left navigation pane, choose **Security Groups**

![Choose Security groups](/AWS/aws-educate-labs//assets/screenshots/003-amzon_compute_lab/37-choose-security-groups.JPG)

38. Next to **Web Server security group**, select the check box

39. Choose the **Inbound rules tab**

NOtice that the security group currently has no rules.

40. Select **Edit Inbound rules**, Choose **Add rule** and then configure the following options:

- Under **Type**: choose **HTTP**
- Under Source: Choose **Anywhere-IPV4

![Edit Inbound Rules](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/40-edit-inbound-rules.JPG)

**Note:** Notice the “Rules with source of 0.0.0.0/0 allow all IP addresses to access your instance. We recommend setting security group rules to allow access from known IP addresses only.” While this is true and common best practice, this lab allows access from any IP address (Anywhere) to simplify both the security group configuration and testing of the website running on your EC2 instance.

you can only add a new ingress rule but cannnot chge a rule once you click **Save rules** in this lab.

41. Chhoose **Save Rules**

42. Refresh the web page that was opened earlier and **Welcome Students!** should appear 
 ![](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/42-welcome-page.JPG)

 BE sure that the URL address bar begins with ``http://`` and not ``https://``


# Task 4: Connecting to your Amazon EC2 instance using AWS systems Manager Fleet Manager

One convenient feature of Fleet Manager is the ability to connect to your EC2 instance using a browser. In this task, you connect to your Windows desktop using Fleet Manager.

## Steps:
43. in the AWS Management Console on the **Services** menu, search for and select **Systems Manager**

44. In the left pane, select **Fleet Manager**

![Select Fleet Manager](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/44-select-fleet-manager.JPG)

45.  Under **Managed Nodes**, tick -[x] your **Web-Server** EC2 instance.
46. from the **Node actions** dropdown list, choose **Connect with Remote Desktop**.

47. On the new Tab, enter the following credentials:

- **Username**: ```Administrator```
- **Password**: ```P@ssWOrD!```

48. Choose **Connect**

The pane displays the Windows desktop which you then navigate as you would on a local PC.

49.  To disconnect from the **Web-Server** instance, Choose **Action** and then choose **End session**

50. a window will pop up, Choose **End Session** one more time.

# Task 5: Resizing the instance

Scaling an instance can involve increasing or reducing the size of an instance type to appropriately suit the purpose and use of the. 
For example you can inscrease the instance from t2.micro to m5.medium

## Steps.

## Stop the instance

The instance must be stopped before you resize you instance.

There  is no charged when an instance is stopped. However, the chrge for the attached EBS volume remains.

51. From the AWS Manangement console, Search and select **EC2**

52. On the **EC2  Management Console** left navigation pane, select **Instances**

53. Selecct the checkbox next to your **Web-Server** instance. At the top of the page, choose the **Instance State** drop down menu and then choose **Stop Instance**. 

![Stop Instance](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/53-stop-instance.JPG)

54. A pop up window for confirmation appears, Choose **Stop** 

![Pop up window](/aws/aws-educate-labs//assets//screenshots/003-amzon_compute_lab/54-pop-up-window-stop-instance.JPG)

The instance shorts down as it would in a  normal Server.

55. Confirm that the **Instance state is changed to **Stopped**

![Confirm Instance state Stopped](/aws/aws-educate-labs//assets/screenshots//003-amzon_compute_lab/55-confirm-instance-state-stopped.JPG)

## Changing the Instance Type

56. Select the checkbox next to the **Web-Server** instance. From the **Actions** dropdown menu, sselect **Instance Setings**, then  **Change instance type**. Make the following changes:

- **Instance type**: Select **t2.nano

![Chnage instance type](/aws/aws-educate-labs//assets//screenshots/003-amzon_compute_lab/56a-change-instance-type.JPG)


![Choose Instance type](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/56b-choose-instance-type.JPG)



57.  Choose **Apply**

## Restart the Resized Instance  
58. In the left navigation pane, choose **Instances**. Next to the **Web-Server**, select the checkbox

59. From the **Instance state** dropdown menu, choose **Start Instance**

![Start the instance](/AWS//aws-educate-labs//assets/screenshots/003-amzon_compute_lab/59-start-instance.JPG)

Confirm that the **Instance state** displays **Running**

# Task 6: Testing the Termination protection Feature:

Terminating an instance means to delete an instance when it is no longer needed. 

60. Select the check box next to your **Web-Server** instance. From the **Instance state**  dropdown menu, choose **Terminate instance**.

61. Observe the message whwich says *Termination protection is enabled for one or more of the selected instances* just next to the **Terminate instance** option.
![Terminate instance protection Enbled](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/61-termination-protection-enabled.JPG)
It is a safe guard to to prevent the accidental termination of an instance.  

Use the **Actions** dropdown menu to enable and disable the termination protection option.

62. From the **Actions** dropdown menu, choose **Instance settings**, and then choose **Change termination protection**

![Temination Protection disables](/AWS/aws-educate-labs/assets/screenshots/003-amzon_compute_lab/62-disbled-termination-protection.JPG)

63. Clear the check box for  **Enable.**

64. Choose **Save**

65. When you to terminate the instance again, the instance state will successfully be terminated.

# Task 7: Exploring EC2 Limits

For every region, there are default limits on the resuorces you can use. These resources include instances, snapshots, volumes and so on.
 
 ## Steps
66. in the left Navigation pane, choose **Limits**

**NOte:** There is a limit on the number of instances that you can launch in this Region. When launching an instance, the request must not cause your usage to exceed the current instance limit in that Region.

You can request an increase for many of these limits.

# Summary

The creation of an EC2 instance was achieved. knowlede via Practice on mnaging the instance type was gained and applied. Secutiry groups setting were modified to permit HTTP traffic to reach the website from outside. Also, termination protection was setup to prevent the accidental deletion of an Instance. The need to change an instance may arise hence practice on starting, stopping and terminating an instace was achieved. Finally, checking the limits to the AWS instance was done.

# End the Lab

## Steps

67. Return to the **AWS Management Console**. 

68. At the upper-right corner of the page, choose **AWSLabsUser**, and then choose **Sign out**

71. Choose **End Lab**





