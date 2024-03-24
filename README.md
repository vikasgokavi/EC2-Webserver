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

5. For Amazon Machine Image (AMI), select Amazon Linux 2 AMI.​
An Amazon Machine Image (AMI) provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes:​

a. A template for the root volume for the instance (for example, an operating system or an application server with applications)​.

b. Launch permissions that control which AWS accounts can use the AMI to launch instances​.

c. A block device mapping that specifies the volumes to attach to the instance when it is launched​.

​
The Quick Start list contains the most commonly-used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.​

​

<img width="960" alt="Screenshot 2024-03-21 151031" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/c92fdc2d-e2a0-4e0f-bada-d268bd2ab09a">


<img width="960" alt="Screenshot 2024-03-21 151031" src="https://github.com/vikasgokavi/EC2-Webserver/assets/105034318/e14aa374-32dc-46ac-91d4-12e98a59b069">

6. In the Instance Type section, choose the Instance type drop down menu and choose  t3.micro​

Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes, allowing you to scale your resources to the requirements of your target workload.​

- A t3.micro instance type has 2 virtual CPUs and 1 GiB of memory.​





   

​


​

​


​


​

​
​

​
