# RetailBank_ElasticBeanStalk_Deployment

**Deploying an application with AWS**

**The purpose of this project is to deploy a Retail Bank application that is fully managed by AWS.** 

[**Retail Bank Application**](http://retailbank3-env.eba-5jaad6mx.us-east-1.elasticbeanstalk.com/)

**Steps Taken:**

**Step 1: Clone Repository to Github**

Cloning a repo into you own Github repository allows for a dev to make changes locally and doesn’t interfere with the main branch. It also helps with tracking changes and version control.

**Step 2: Create an EC2 Instance** 
Creating a virtual server allows a developer to configure and customize for specific requirements and it also allows for scalability and flexibility for resources being used.

	**Step 2.1: Update and Upgrade Server**   
	  
	Run \`sudo apt update’ and \`sudo apt upgrade\` to make sure your server is updated and upgraded. This is to prevent any issues that may cause configuration drift between the server and any dependencies that may be added to the server.

         **Step 2.2: Create security Group for EC2 Instance**  
	  
         Creating a security group controls traffic and ensures only authorized access is permitted to your site and server.  
        
           
 **Step 3: Install Jenkins**  
Jenkins helps streamline the process of building, testing, and deploying code. It makes it easier to detect bugs and run test.   
To successfully install Jenkins, root user permissions are needed. Use the command `sudo su`. This allows for a regular user ([ubuntu@ip.address](mailto:ubuntu@ip.address)) to gain privileges and access to all commands and files without needing the root user password. 

Once Jenkins has been added to your server, run `sudo systemctl start jenkins`. To make sure Jenkins is running, run the command `sudo systemctl status jenkins`.


 **Step 4: Log into Jenkins**
Once Jenkins is up and running on your EC2, open your browser to [https://localhost:8080](https://localhost:8080) (Jenkins default port is 8080). The following screen should appear. 
<img width="731" alt="Screenshot 2024-08-01 at 9 34 54 PM" src="https://github.com/user-attachments/assets/b8323d3a-a2bf-4880-96c4-b6b841066803">


Follow the path /var/jenkins_home/secrets/initalAdminPassword  

Copy and paste the password, follow the steps to create your 1st admin user.

 **Step 5: Create a Multibranch Pipeline**

After creating the 1st admin user, It’s time to create a multibranch pipeline. This step allows for different branches to be built and tested without compromising the main branch and causing potential issues. 


 
 **Step 6: Connect Github Repo to Jenkins**

Once you have successfully created the multibranch pipeline, Look for Branch Sources, click “Add source” and select “GitHub. Click “+ Add” and select “Jenkins”. Make sure “Kind” reads “Username and password”. Enter your Github username under Username and enter your Github Personal Access Token under Password.   
This step is important because any code pushed to the repo will automatically trigger builds and test, which makes it easier to detect any issues without affecting the main branch. Once build has successfully been created, You should see the following screen: 


<img width="1142" alt="JenkinsSuccess" src="https://github.com/user-attachments/assets/bcfa652d-87d2-47ce-a6cc-f6dd18fc12d0">



 **Step 7: Create an AWS IAM role for Amazon Elastic Beanstalk and EC2.** 

Navigate to the AWS Management console and search for IAM to create IAM roles for Elastic Beanstalk environment and EC2 Instance. It is important to create the IAM roles to secure your instances and makes it easier for permissions to be granted to your instances and to use different resources they may need.


 **Step 8: Create an Elastic Beanstalk Environment**  
After creating your IAM roles, add Elastic Beanstalk to your AWS Management console.  Click services, search for Elastic Beanstalk. Click the star next to Elastic Beanstalk. It will be added to your dashboard in the AWS Management console. This makes it easier to access Elastic Beanstalk. 


<img width="621" alt="Screenshot 2024-08-02 at 11 09 41 AM" src="https://github.com/user-attachments/assets/6d4f4cd5-fdf1-4424-b1bb-ff9b5386855e">

  
Now navigate to Elastic Beanstalk. Once there click, Create Environment. 


<img width="621" alt="Screenshot 2024-08-02 at 11 10 17 AM" src="https://github.com/user-attachments/assets/6e80579f-52bb-4574-b7d2-293d7d15583a">


Once you have clicked create your environment, The following page will display. Follow each step to configure the environment. 


<img width="626" alt="Screenshot 2024-08-02 at 11 11 30 AM" src="https://github.com/user-attachments/assets/4c6ee05f-0522-43fa-848a-0ac204f295fe">


**Step 8.1: Upload your source code** 

**This step is very important! While configuring your environment, you will see the following section. 


<img width="634" alt="Screenshot 2024-08-02 at 11 12 45 AM" src="https://github.com/user-attachments/assets/f9ac560c-c5e0-4e91-95f9-bc051518d2e8">


Upload your source code as a **.zip file. DO NOT PUT THE FILES IN A PARENT DIRECTORY. SUB DIRECTORIES ARE FINE\!** Be sure that all of your files can be seen by Elastic Beanstalk. **When files are in a parent directory, it prevents Elastic Beanstalk from properly deploying your application.** All files should be accessible within your source bundle. 

  
**Step 9: Launch Your Application**

**After your environment has been successfully launched. You should see the following screen:** 


<img width="1434" alt="Screenshot 2024-08-05 at 9 01 59 AM" src="https://github.com/user-attachments/assets/7ce1dc98-b479-4cc4-8eb6-61f943fa7fa3">


  
**Step 9.1: Click the Domain Name generated by Elastic BeanStalk** 

<img width="1434" alt="Screenshot 2024-08-05 at 8 40 44 AM" src="https://github.com/user-attachments/assets/f09acb7f-3149-4339-8690-89558e12c4d4">



**Issues/Troubleshooting**

1. **502 Bad Gateway Nginx Error**
   <img width="1172" alt="Screenshot 2024-08-05 at 9 09 05 AM" src="https://github.com/user-attachments/assets/1541947f-3b29-4898-b3cb-21f15ac66883">

   I received this error the first time I tried to launch the application. I recreated the environment and received the same error.  Before checking anything in Elastic Beanstalk, I inspected the webpage and checked the console for additional information. It confirmed that it was a server error.
   
<img width="1172" alt="Screenshot 2024-08-05 at 9 42 27 AM" src="https://github.com/user-attachments/assets/ec3dbbe3-fbda-4ab8-bad2-9565ad4c8917">


After seeing that my error was being thrown due to the server, I went back to Elastic Beanstalk to check for additional error messages. 

I checked the Event log and Health status but I continued to see that there were no issues in the environment. I rechecked my configurations but was still receiving the same error. After research, I was guided to check the logs in the Elastic Beanstalk environment. 

2. **Failure to Retrieve Logs**

   <img width="1172" alt="Screenshot 2024-08-05 at 9 43 42 AM" src="https://github.com/user-attachments/assets/3389439f-fd36-4646-aa60-5b757828c816">

When requesting the logs, I continued to get “Failed to Retrieve requested logs”. This issue was resolved by changing my EC2 Instance profile permissions. My EC2 Instance didn’t have the proper IAM role assigned to the EC2 instance profile. Once that was resolved, I finally saw the logs. 


3. **Refusing to connect to Upstream**
<img width="618" alt="Screenshot 2024-08-05 at 9 46 20 AM" src="https://github.com/user-attachments/assets/a2ff8a48-2ef9-4ef4-8dc9-d0db1410e580">


  
I first checked the Nginx error logs and received the following error:   
2024/07/31 07:08:50 \[error\] 2713\#2713: **\*1 connect() failed (111: Connection refused) while connecting to upstream,** client: 185.254.196.173, server: , request: "GET /.env HTTP/1.1", upstream: "http://127.0.0.1:8000/.env", host: "52.3.93.84".  

I wasn’t familiar with upstream, so I researched the internet to find any help in relation to the error. I learned in relation to Nginx that the upstream server was the application server. The backend server and application server were not talking to each other. 



<img width="629" alt="Screenshot 2024-08-05 at 9 46 44 AM" src="https://github.com/user-attachments/assets/0b99abe5-47e9-4dc0-b15f-2a7fad7f71b6">


I solved my error by taking my application.py file, all other files, and subdirectories out of the parent directory. Zipped the files and uploaded them as the source code. That resolved the 502 Bad gateway Nginx error.
