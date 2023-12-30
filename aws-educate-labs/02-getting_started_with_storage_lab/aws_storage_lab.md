# PREREQUIITES FOR THE LAB

PREREQUISITES
This lab requires the following:

- A notebook computer running Microsoft Windows, macOS, or Linux (Ubuntu, SUSE, or Red Hat)
- An internet connection
- For Microsoft Windows users, administrator access to the computer




# Instrcutions to complete the Lab:

1. **Navigate to the lab page in the course. Choose Start Lab to begin.**

2. A pop-up window will open with the AWS Customer Agreement and AWS Learner Terms and Conditions. You can review the agreement documents by choosing the links. Choose the **check box** to accept the terms. Then choose **Start Lab.**

![Click Start Lab](/AWS/aws-educate-labs/assets/screenshots/002-amazon_storage_lab/start_lab.JPG)

3. The lab will begin provisioning. This may take several minutes. Once the lab has completed provisioning you may begin the lab.

4. Choose **Open Console**

    ![click open console](/AWS/aws-educate-labs/assets/screenshots/002-amazon_storage_lab/open_console.JPG). 

    This will open a new tab and take you to the console home

5. Carefully follow the lab instructions through the tasks. A best practice is to use a split screen or work on two monitors to be able to have the AWS Management console open on one side and the lab instructions on the other. 6.When you have successfully completed the tasks choose End Lab. 

6. When you have successfully completed the tasks choose End Lab.

7. 7.A pop-up will ask you to confirm that you want to end the lab. 


# Task 1: Creating a bucket in Amazon S3

This task involves the creation of an S3 bucket and to configure it for static web hosting

## Steps:

1. In the AWS Management Console, on the Services menu, choose S3

2. Choose **Create bucket** 


![choose Create Bucket](/AWS/aws-educate-labs/assets/screenshots/002-amazon_storage_lab/choose_create_bucket.JPG)

An S3 bucket name is globally unique, and all AWS accounts share the namespace. After you create a bucket, no other AWS accounts in any AWS Regions can use the name of that bucket unless you delete the bucket.

For this lab,  use a bucket name that includes a random number, such as **website-123**.

3. For Bucket name, enter 

```
website-<random number>
```
 and replace <123> with actual digits.

**Public access** to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access.

4. For Object Ownership, choose **ACLs enabled.**

5. Choose **Bucket owner preferred.**

6. For **Block Public Access settings for this bucket**, clear the check box for Block all public access, and then select the box that states **I acknowledge that the current settings might result in this bucket and the objects within becoming public**.

7. For **Bucket Versioning**, choose **Enable**.

**Note:** Once you turn on (enable) bucket versioning, you can’t turn it off.

8. For Tags, choose Add tag, and enter the following:

**Key:** ``Department``

**Value:** ``Marketing``
 
 You can add additional information to a bucket, using tags such as a project code, cost center, or owner.
Choose **Create bucket**

9. In the **Buckets** section, choose the name of your new bucket.

10. Choose the **Properties** tab.

# Task 2: Configuring a static website on Amazon S3

Here we configure the bucket for static website hosting.

## Steps:

11. Scroll to the **Static website hosting** panel.

12. Choose **Edit**

13. Configure the following settings:

- Static web hosting: Choose Enable.
- Hosting type: Choose Host a static website.
- Index document: Enter ``index.html``
- Error document: Enter ``error.html``
 
 14. Choose **Save changes**

In the **Static website hosting** panel under Bucket website endpoint, click the link.

You will get a 403 Forbidden message 


![403 Forbidden message](/AWS/aws-educate-labs/assets/screenshots/002-amazon_storage_lab/403_forbidden.JPG)

because you have not yet configured the bucket permissions. Keep this browser tab open in your web browser so that you can return to it later.

### Summary 

  You have configured your bucket to host a static website.

# Task 3: Uploading content to your bucket

In this task, the static web files are uploaded to the bucket.

## Steps:

In this task, you upload the static files to your bucket.

15. Choose (right-click) each of the following links (links provided by the aws educate labs environment), and download the files to your computer. IF you already have your html, javascript and css files on your pc jump to 
 Ensure that each file keeps the same file name, including the extension.

index.html
script.js
style.css

16. Return to the Amazon S3 console, and choose the **Objects** tab.

17. Choose **Upload**

18. Choose **Add files**

19. Choose the three files that you downloaded or you have on your pc

20. Choose **Upload**

Your files are uploaded to the bucket.

21. Choose **Close**

# Task 4: Turning on public access to the objects

Objects that are stored in Amazon S3 are private by default. This setting helps keep your organization’s data secure.

In this task, you make the uploaded objects publicly accessible so users can view your website.

## Steps

22. Return to the browser tab that showed the 403 Forbidden message.

23. Refresh the webpage.

 If you accidentally closed this tab, go to the Properties tab, and in the Static website hosting panel, choose the **Bucket website endpoint** link again.

You should still see a 403 Forbidden message. This response is expected! This message indicates that your static website is being hosted by Amazon S3 but that the content is private.

You can make Amazon S3 objects public through two different ways:

- To make either a whole bucket public or a specific directory in a bucket public, use a bucket policy.

- To make individual objects in a bucket public, use an access control list (ACL). It is normally safer to make individual objects public because doing so avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.

You now configure the individual objects to be publicly accessible.

24. Keep the website tab open, and return to the web browser tab with the Amazon S3 console.

25. Choose  all three objects.

In the Actions menu, choose Make public using ACL.

A list of the three objects is displayed.

26. Choose **Make public**
Your static website is now publicly accessible.

27. Choose **Close**

28. Return to the web browser tab that has the 403 Forbidden message.

29. Refresh  the webpage.

The static website that is being hosted by Amazon S3 should be up and running.

# Task 5: Securely sharing an object using a presigned URL


When you need to temporarily and securely share an object with a person or group of people, you can create a presigned URL. When you create the URL, you must configure how long the URL will be valid. Then, you can share this URL with the users who should have access to the object.

 As long as the presigned URL is valid, anyone who has it can get to the object. Avoid keeping the URL active longer than necessary, and only share the URL with people you trust.


## Steps:

30. Choose (right-click) the link (provided in the lab environment), and download the file to your computer:  Ensure that the file keeps the same file name, including the extension.
``new-report.png``

31. Return to the Amazon S3 console, and 

32. choose the **Objects** tab.

33. Choose **Upload**

34. Choose **Add files**

35. Choose the file that you downloaded.

36. Choose Upload

37. You have uploaded your file to the bucket.

Choose **Close**

Like when you first uploaded the website files, the ***new-report.png*** file is private by default. This time, instead of making the object public, you create a presigned URL to access the file.

38. In the Objects tab, choose  **new-report.png.**

39. From the Actions menu, select **Share with a presigned URL**

40. In the pop-up window, configure the **Time interval** until the presigned URL expires:

41. Choose **Minutes**
42. Choose **Create presigned URL**

43. From the banner at the top of the page, choose **Copy presigned URL.**

44. Open a new browser tab, and paste the URL you copied into the address bar.

A report is displayed in the web browser.

If you wait beyond the time you chose and use the link again, you will find that the URL has expired and no longer works.


# Task 6: Using a bucket policy to secure your bucket

Here, we seek to protect your website files and make sure that no one can delete them. To do this, you apply a bucket policy that denies delete privileges on your website files.


## Steps

45. Return to the Amazon S3 console, and choose the **Permissions** tab.

46. Under **Bucket policy**, choose **Edit**
Copy the following policy text. In the Policy text editor:

```
{
	"Version": "2012-10-17",
	"Id": "MyBucketPolicy",
	"Statement": [
		{
			"Sid": "BucketPutDelete",
			"Effect": "Deny",
			"Principal": "*",
			"Action": "s3:DeleteObject",
			"Resource": [
				"arn:aws:s3:::<bucket-name>/index.html",
				"arn:aws:s3:::<bucket-name>/script.js",
				"arn:aws:s3:::<bucket-name>/style.css"
        ]
		}
	]
}

```

This policy prevents everyone from deleting the three files that make your website work.

47. Next, you update the text in the policy editor. In the following lines of code in the policy editor, replace the <bucket-name> placeholders with the name of your bucket.

```
"arn:aws:s3:::<bucket-name>/index.html",
"arn:aws:s3:::<bucket-name>/script.js",
"arn:aws:s3:::<bucket-name>/style.css"

```
Your updated code should look similar to the following:

```
"arn:aws:s3:::website-1234/index.html",
"arn:aws:s3:::website-1234/script.js",
"arn:aws:s3:::website-1234/style.css"

```
Note: Your bucket name will be different. Be sure to use the name of the bucket that you created.

48. Choose **Save changes**

49. eturn to the the **Object tab**

50. Select  **index.html**

51. Choose **Delete**.

52. In the **Delete objects** panel, enter 

``delete``
 
 to confirm that you want to remove this file.

53. Choose **Delete objects**

Notice that the index.html file is listed in the Failed to delete pane.

This confirms that your policy is working and preventing the website’s files from being deleted.

Choose Close to return to the Objects tab.

# Task 7: Updating the website

Although you have configured a policy to prevent deletion of website files, you can still update the website by editing the HTML file and uploading it to the S3 bucket again.

Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object; instead, you must replace the whole object.


# Steps

54. On your computer, load the ``index.html`` file into a text editor (for example, Notepad or TextEdit).

55. Find the text **Served from Amazon S3**, and replace it with 

Created by <YOUR-NAME>
and substitute your name for *<YOUR-NAME>* (for example, **Created by Joe**).

56. Save the file.

57. Return to the Amazon S3 console, and upload the ``index.html`` file that you just edited.

58. Choose  ``index.html``, and in the Actions menu, choose the **Make public using ACL** option again.

59. Choose **Make public**.

60. Return to the web browser tab with the static website, and refresh  the page.

Your name should now be on the page.


# Task 8: Exploring file versions

Bucket versioning is turned off by default. When versioning is turned off, changes to objects can’t be undone. For example, if you upload a new version of a file, the old file is replaced with the new one. The original file is lost. If you delete a file, it is permanently deleted, and you can’t get it back.

It is important to remember that once you turn on version, you cannot turn it off. However, you can suspend versioning

Recall that when you created your bucket, you turned on versioning. In this task, you view the object versions available in your bucket.

## Steps: 

61. Return to the Amazon S3 console, and choose the **Objects** tab.

62. Choose  **Show versions** to turn on bucket versioning.

63. Review the list of objects in the bucket.

S3 console, objects list with Show versions enabled

- Notice that each file has a Version ID. These IDs are automatically generated by Amazon S3 when versioning is turned on.

- You should also find two versions of the index.html file because you uploaded a new version of the file. The current version is the file that you uploaded when you updated your website.

# Summary

In this lab, you created a personalized, publicly accessible static website. You learned how to use a presigned URL to temporarily share objects in your bucket. You also protected your work with a bucket policy that prevents file deletion and turned on bucket versioning in case you need to recover previous versions of files. Excellent work!


