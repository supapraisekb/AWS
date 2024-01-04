# Task 1: Task 1: Launching an EC2 instance

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