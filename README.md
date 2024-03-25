# EC2-Webserver
EC2 Web Server Management and Scaling Project

## **OBJECTIVES**
 1. Launch a web server with termination protection enabled
 ​
 2. Monitor Your EC2 instance
 
 3. Modify the security group that your web server is using to allow HTTP access​
 
 4. Resize your Amazon EC2 instance to scale​
 
 5. Test termination protection
 ​
 6. Terminate your EC2 instance​

## Task 1: Launch Your Amazon EC2 Instance​

In this task, you will launch an Amazon EC2 instance with termination protection. Termination protection prevents you from accidentally terminating an EC2 instance. Your instance will include a User Data script that will install a simple web server.​

1. From the AWS Management Console, use the AWS search bar to search for EC2  and then choose the service from the list of results.​
   
<img width="948" alt="Screenshot 2024-03-21 145551" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/17434179-f964-449b-a77f-9e2c691ffd8e">
 

2. Choose the Launch instance  drop down menu and choose Launch instance.​
    

<img width="960" alt="Screenshot 2024-03-21 145910" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/c36981cd-62c5-485a-9161-86a54877f3fa">

3. In the Name and tags section, enter  Web Server  in the Name box.​
    
<img width="960" alt="Screenshot 2024-03-21 150402" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/720c6175-ef43-4c4f-bcee-778c0acf814c">

4. For Amazon Machine Image (AMI), select Amazon Linux 2 AMI.​
An Amazon Machine Image (AMI) provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes:​

a. A template for the root volume for the instance (for example, an operating system or an application server with applications)​.

b. Launch permissions that control which AWS accounts can use the AMI to launch instances​.

c. A block device mapping that specifies the volumes to attach to the instance when it is launched​.

​
The Quick Start list contains the most commonly-used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.​

​

<img width="960" alt="Screenshot 2024-03-21 151031" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/c92fdc2d-e2a0-4e0f-bada-d268bd2ab09a">


<img width="960" alt="Screenshot 2024-03-21 151031" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/e14aa374-32dc-46ac-91d4-12e98a59b069">

5. In the Instance Type section, choose the Instance type drop down menu and choose  t3.micro​

     Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes, allowing you to scale your resources to the requirements of your target workload.​

A t3.micro instance type has 2 virtual CPUs and 1 GiB of memory.​

<img width="960" alt="Screenshot 2024-03-21 153948" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/fae42aa9-c1ae-49a2-8894-345b7fa55f86">

6. In the Key pair (login) section, locate the Key pair name drop down menu and choose Proceed without a key pair (Not recommended).​

Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance.​

In this lab you will not log into your instance, so you do not require a key pair.​

​<img width="545" alt="Screenshot 2024-03-21 154641" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/839acb81-01e1-4117-b0b4-f69f11299982">

7. In the Network settings section, choose the Edit button. Make the following selections:​
VPC: Choose the VPC with the name that contains Lab VPC​.


<img width="546" alt="Screenshot 2024-03-21 155210" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/df157f2b-49e5-42f7-aaee-a7e963538eb4">

8. Subnet: Choose the Subnet with the name that contains  Public Subnet 1​
The Network indicates which Virtual Private Cloud (VPC) you wish to launch the instance into. You can have multiple networks, such as different ones for development, testing and production.​

The Lab VPC was created using a CloudFormation template during the setup process of your lab. This VPC includes two public subnets in two different Availability Zones.​

<img width="960" alt="Screenshot 2024-03-21 155501" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/b73d23d9-cca0-4024-8b7e-92e6af6b3bc4">

9. In the Firewall (security groups) section, choose  Create security group
     ​
Security group name =  **Web Server security group​**

Description =  **Security group for my web server​**

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.​

In this lab, you will not log into your instance using SSH. Removing SSH access will improve the security of the instance.​

<img width="960" alt="Screenshot 2024-03-22 094042" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/dfbac318-0471-4964-bd58-048844b453d1">

10. Choose the Remove button to remove the existing SSH rule. We should have no security group rules.​

<img width="960" alt="Screenshot 2024-03-22 094312" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/8d324d5d-a1fe-4775-9751-c0a85206351c">

11. The Configure storage section default choices can be left alone.​

 Amazon EC2 stores data on a network-attached virtual disk called Elastic Block Store.​

We will launch the Amazon EC2 instance using a default 8 GiB disk volume. This will be your root volume (also known as a ‘boot’ volume).​

<img width="960" alt="Screenshot 2024-03-22 094812" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/ee63f9af-9fa9-4ad3-9239-6a7b3b04ee8f">


12. Expand the Advanced details section. Scroll down to the Termination protection drop down menu and set to Enable.​

 When an Amazon EC2 instance is no longer required, it can be terminated, which means that the instance is stopped and its resources are released. A terminated instance cannot be started again. If we want to prevent the instance from being accidentally terminated, we can enable termination protection for the instance, which prevents it from being terminated.​

<img width="960" alt="Screenshot 2024-03-22 100029" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/ea6e845b-f66d-46b9-9304-6b508967ae0b">

13. Scroll all the way to the bottom until you see a field for User data.​

 When you launch an instance, you can pass user data to the instance that can be used to perform common automated configuration tasks and even run scripts after the instance starts.​

Your instance is running Amazon Linux, so you will provide a shell script that will run when the instance starts.​
Copy the following text and paste it into the User data field:​
**#!/bin/bash​**

**yum -y install httpd**​

**systemctl enable httpd**​

**systemctl start httpd​**

"**echo <html><h1>Hello Vishwanath ! From Your Web Server!</h1></html> > /var/www/html/index.html**"​

<img width="960" alt="Screenshot 2024-03-22 100514" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/9e3a6bda-aaef-4eca-baf1-4f4d48c03fa3">

15. The script will:​

Install an Apache web server (httpd)​

Configure the web server to automatically start on boot​

Activate the Web server​

Create a simple web page​

Choose Launch instance ​
​
Choose Instances from the collapsible menu on the left pane. You may need to expand the menu to see this option.​

The instance might appear in a pending state, which means it is being launched. It will then change to running, which indicates that the instance has started booting. When creating a new instance, there will usually be a short time before you can access the instance.​

Wait for your instance to display the following:​

**Instance state:  Running** .​

**Status check:  2/2 checks passed** .​

<img width="769" alt="Screenshot 2024-03-22 102003" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/768e8765-69ef-44f4-a15d-288d3cf5453c">

Periodically refresh the page if you don’t see a change in the Instance state or Status check values.​

16. Select the  for your newly-created Web Server and the Details tab displays detailed information about your instance.​

 To view more information in the Details tab, drag the window divider upwards.​

Review the information displayed in the Details tab. It includes information about the instance type, security settings, network settings, and more. The instance receives a Public IPv4 DNS name that you can use to communicate with the instance from the Internet.​

Now we have successfully launched your first Amazon EC2 instance.​

<img width="960" alt="Screenshot 2024-03-22 102333" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/12718b32-e932-47a8-bc9c-5a3b6a8a152a">


18. Monitor the Instance​

Monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon Elastic Compute Cloud (Amazon EC2) instances and your AWS solutions.​

Select the Status checks tab.​

With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues.​

Notice that both the System reachability and Instance reachability checks have passed.​

<img width="960" alt="Screenshot 2024-03-22 103147" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/a4a817c4-396a-4c93-8db1-6f1c44fe82f0">

19. Select the Monitoring tab.​

This tab displays CloudWatch metrics for your instance. Currently, there are not many metrics to display because the instance was recently launched.​

You can choose a graph to see an expanded view.​

 Amazon EC2 sends metrics to Amazon CloudWatch for your EC2 instances. Basic (five-minute) monitoring is enabled by default. You can enable detailed (one-minute) monitoring.​

Select the Actions  menu (in the upper right of the console), choose Monitor and troubleshoot  and select Get system log.​

 Expected output:​
 Note: If you do not see a system log, wait a couple of minutes and refresh the log screen until it appears.​

The System Log displays the console output of the instance, which is a valuable tool for problem diagnosis. It is especially useful for troubleshooting kernel problems and service configuration issues that could cause an instance to terminate or become unreachable before its SSH daemon can be started.​

​
<img width="960" alt="Screenshot 2024-03-22 103543" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/fa5508ed-2085-46e1-ab34-3818c1455775">

20. Select the  for Web Server, then select the Actions  menu, choose Monitor and troubleshoot  and select Get instance screenshot.​

 Expected output:​

​<img width="960" alt="Screenshot 2024-03-22 104727" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/982bc08f-682e-476a-8521-0d2e3b6bbd14">

This shows you what your Amazon EC2 instance console would look like if a screen were attached to it.​

 If you are unable to reach your instance via SSH or RDP, you can capture a screenshot of your instance and view it as an image. This provides visibility as to the status of the instance, and allows for quicker troubleshooting.​

Scroll down to the bottom of the browser window and select Cancel.​

Now we have explored several ways to monitor your instance.​

21. Update Your Security Group and Access the Web Server​

When we launched the EC2 instance, we provided a script that installed a web server and created a simple web page. In this task, we will access content from the web server.​
Select the  for Web Server, then choose the Details tab.​
Copy the Public IPv4 address of your instance to your clipboard​
Open a new tab in your web browser, type ​

http://  in the browser and paste the IP address we just copied, then press Enter.​

<img width="960" alt="Screenshot 2024-03-22 113908" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/14160ed7-3f7f-4324-b9de-068503fe16ae">

22. Consider:​
Are we able to access your web server? Why not?​

we are not currently able to access web server because the security group is not permitting inbound traffic on port 80, which is used for HTTP web requests. This is a demonstration of using a security group as a firewall to restrict the network traffic that is allowed in and out of an instance.​

To correct this, you will now update the security group to permit web traffic on port 80.​

Keep the browser tab open, but return to the EC2 Management Console tab.​

<img width="960" alt="Screenshot 2024-03-22 114135" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/7d185cd3-2f7d-4ee8-995d-0b457f7631c7">

23. In the left navigation pane, select Security Groups.​

Select the  for the Security group ID with the Security group name Web Server security group.​

The security group currently has no rules.​

​<img width="960" alt="Screenshot 2024-03-22 114617" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/02e46aae-019e-41ab-bf8e-8cc9316dd1e4">

24. Choose the Inbound rules tab.​

Choose Edit inbound rules.​

Choose Add rule then configure:​

​ <img width="960" alt="Screenshot 2024-03-22 115242" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/f632ef7c-8600-4f86-a6b8-52cf76f28891">

25. Type: HTTP​

Source: Anywhere-IPv4​

Choose Save rules .​

​<img width="960" alt="Screenshot 2024-03-22 115456" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/0d145f10-08c0-4806-89b9-b0516e0cc818">

The new Inbound HTTP rule will create an entry for both IPV4 IP address (0.0.0.0/0) as well as IPV6 IP address (::/0).​

 Note: using “Anywhere”, or more specifically, using 0.0.0.0/0 or ::/0 is not a recommended best practice for production workloads.​

 <img width="960" alt="Screenshot 2024-03-22 115634" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/ccb76a11-ecf6-4fa1-9019-02ffdce837a2">

 26. Return to the web server tab that we previously opened and refresh  the page.​
     We should see the message Hello From Your Web Server!​

<img width="960" alt="Screenshot 2024-03-22 115840" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/45fd2d39-0f7d-45c6-88ca-1dd5791340d2">


## Task2:Resize Your Instance: Instance Type and EBS Volume​

1. As your needs change, you might find that your instance is over-utilized (too small) or under-utilized (too large). If so, you can change the instance type. For example, if a t3.micro instance is too small for its workload, you can change it to an t3.small instance. Similarly, you can change the size of a disk.​
STOP YOUR INSTANCE​

Before you can resize an instance, you must stop it.​

When you stop an instance, it is shut down. There is no charge for a stopped EC2 instance, but the storage charge for attached Amazon EBS volumes remains.​
On the EC2 Management Console, in the left navigation pane, choose Instances.​

If it is not already selected, select the  for Web Server .​

Select Instance state , then Stop instance.​

Choose Stop .​

<img width="960" alt="Screenshot 2024-03-22 121452" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/a424eb1e-ee1e-491f-ae53-455061993a94">

2. Your instance will perform a normal shutdown and then will stop running. This may take a couple minutes.​

Wait for the Instance State to display: Stopped .​

​<img width="960" alt="Screenshot 2024-03-22 122236" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/0b63dd8b-8ec0-4b3d-a587-8bd4d01f2495">

3. CHANGE THE INSTANCE TYPE​

If it is not already selected, select the  for Web Server .​

Select the Actions  menu, select Instance settings  and Change instance type, then configure:​

<img width="960" alt="Screenshot 2024-03-22 122627" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/c15bf5af-b6d3-46d4-9562-9d56c9abfb2c">

4. Instance type: t3.small​

Choose Apply .​

When the instance is started again it will be a t3.small, which has twice as much memory as a t3.micro instance.​

​<img width="346" alt="Screenshot 2024-03-22 123205" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/40f23ab9-5601-47b4-a538-fbab08274bd9">

5. Instance type: t3.small​

Choose Apply .​

When the instance is started again it will be a t3.small, which has twice as much memory as a t3.micro instance.​

​<img width="960" alt="Screenshot 2024-03-22 123736" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/351c7491-cbb3-4a33-b238-f021eb969532">

6. RESIZE THE EBS VOLUME​

In the left navigation pane, select Volumes from the  Elastic Block Store section.​

Select  the volume there.​

In the Actions  menu, select Modify volume.​

​<img width="960" alt="Screenshot 2024-03-22 124717" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/304c6aa4-db4b-4d02-9a3d-68a213caeb29">

7. The disk volume currently has a size of 8 GiB. You will now increase the size of this disk.​

Change the size (GiB) to: 10​

Choose Modify .​

Choose Modify to confirm and increase the size of the volume.​

​<img width="960" alt="Screenshot 2024-03-22 124913" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/1fb92a9e-d330-4a5f-a307-393fd05331dd">

 <img width="739" alt="Screenshot 2024-03-22 125029" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/11975324-74fe-4594-b792-c7b4ee18847e">

8. START THE RESIZED INSTANCE​

You will now start the instance again, which will now have more memory and more disk space.​

In left navigation pane, select Instances.​

Select  the Web Server.​

Select Instance state  and then Start instance.​

Note: An EBS volume being modified goes through a sequence of states: Modifying, Optimizing, and finally Complete.​

 Now we have successfully resized your Amazon EC2 Instance. In this task you changed your instance type from t3.micro to a t3.small. You also modified your root disk volume from 8 GiB to 10 GiB.​

 <img width="960" alt="Screenshot 2024-03-22 125900" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/8089efea-293e-42d8-920b-d211ed730443">

 <img width="741" alt="Screenshot 2024-03-22 130229" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/a4a6d333-42b0-4390-8278-ccf4fd9ad8eb">

9. Test Termination Protection​

You can delete your instance when you no longer need it. This is referred to as terminating your instance. You cannot connect to or restart an instance after it has been terminated.​

In this task, you will learn how to use termination protection.​

In left navigation pane, select Instances.​

Select  the Web Server.​

Select Instance state  and then Terminate instance.​

Choose Terminate .​

​<img width="960" alt="Screenshot 2024-03-22 130824" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/6e95ada9-42e5-44a8-820b-5fef3dd077f2">

At this point you see the following error message on top of the page:​

Failed to terminate an instance: The instance ‘i-xxxxxxxx’ may not be terminated. Modify its ‘disableApiTermination’ instance attribute and try again.​

The above error is expected, and this is a safeguard to prevent the accidental termination of an instance. If you really want to terminate the instance, you will need to disable the termination protection.​

​<img width="740" alt="Screenshot 2024-03-22 130932" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/4e03a279-0077-4eb1-bdae-025bde460d49">

10. Select Actions , choose Instance settings , and Change termination protection.​

Unselect  Enable.​

Choose Save .​

You can now terminate the instance.​

<img width="960" alt="Screenshot 2024-03-22 131227" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/a3ca2da2-69d8-4919-b146-a532a99fa6dd">

11. We can now terminate the instance.​

Refresh  the instance console screen.​

Select  the Web Server​

Choose Instance state  , and Terminate instance .​

Choose Terminate .​

 Expected output:​

The Instance state of the Web Server instance should change to Terminated after about 30 seconds. You may have to refresh the page a few times​

<img width="960" alt="Screenshot 2024-03-22 131433" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/43e05407-f742-422a-bc36-e6eaba675cb3">


12. The Instance state of the Web Server instance should change to Terminated after about 30 seconds. You may have to refresh the page a few times​.

    <img width="736" alt="Screenshot 2024-03-22 131725" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/77b8d193-42d9-4638-9468-47fcb9a41b9d">


# **Conclusion​**

We have successfully done the following:​

Launched a web server with termination protection enabled.​

Monitored Your EC2 instance.​

Modified the security group that our web server is using to allow HTTP access.​

Resized your Amazon EC2 instance to scale.​

Tested termination protection.​

Terminated our EC2 instance.​



​


​

 



​
​
​

​
 







​




​

​

​


​


​




​


​



​

​

​

​




​


​




.​

​


​

​

​



​

​


​


​

​

​

​

​

​

​







   

​


​

​


​


​

​
​

​
