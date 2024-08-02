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

