![s3](https://github.com/user-attachments/assets/22a20a70-90bf-444c-a4f6-030f924d341a)



# Three-Tier-Applications-Practice

🚀 I completed Project of AWS Cloud on, A Building a Scalable Three-Tier Application on AWS ☁
project where I designed and deployed a robust three-tier application using Amazon Web Services
(AWS)

👨💻In the Project we basically hosted Three-Tier Applications, in software development, it’s very
common to see applications built with a specific architectural paradigm in mind. One of the most
prevalent patterns seen in modern software architecture is the 3-tier (or three-tier) architecture. This
model structures an application into three distinct tiers: presentation (user interface), logic (business
logic), and data (data storage).each tier serves a specific purpose and can be scaled, managed, deployed
independently

✨Get ready to enhance your AWS skills and boost your confidence in cloud technology

Prerequisites -
Before we start, make sure you have:-
An AWS account [Free Tier]
Basic understanding of AWS EC2 / Data based (Aurora MySQL) / VPN / IAM / LB / S3
Basic Knowledge of High Availability & Scalability

STEP 1: Networking and Security
Create a VPC (Virtual Private Cloud): This creates a logically isolated network for your resources.
Create Subnets: Create 6 subnets across 2 Availability Zones (AZs).Each AZ will have 3 subnets: Public,
Private-App, and Private-DB. Choose a CIDR range that allows for at least 6 subnets.
Create an Internet Gateway: This provides internet access for your public subnets.
Create a NAT Gateway (in each public subnet): This allows your private instances to access the internet.
Create Route Tables: Configure routes for each subnet
Public subnets: route traffic to the internet gateway.
Private app subnets: route traffic to the NAT gateway in the same AZ.
Create Security Group: security rules for each layer (web, app, and database) to control inbound traffic.

Step 2: Database Deployment
Create a Subnet Group: Group specifies which subnets your database can reside in (one for each AZ).
Create a Multi-AZ Database (Aurora MySQL): This provides a highly available database across multiple
AZs.
Configure Database Settings: Choose a username, password, and security group for database access.

Step 3: App Tier Instance Deployment
Launch an EC2 Instance (in a private subnet): his instance will run your application code.
Connect to the Instance: Session Manager to connect securely without needing an SSH key.
Before, you need to create IAM Role for accessing the following AWS managed policies. You can search
for them and select them. These policies will allow our instances to download our code from S3 & use
Systems Manager Session Manager to securely connect to our instances without SSH keys through the
AWS console. [AmazonSSMManagedInstanceCore / AmazonS3ReadOnlyAccess]
Configure Software Stack: Install Node.js and PM2 (process manager) on the instance.
Configure Database Connection: Update your application code with the database credentials.
Upload Code and Start Application: Upload your application code to the instance and start it using PM2.

Step 4: Internal Load Balancing and Auto Scaling
Create an AMI (Amazon Machine Image) of the App Tier Instance: This creates a template for your app
tier instances. Create a Launch Template This defines the configuration for launching new app tier
instances. Configure this automatically scales your app tier instances based on load. Set a desired,
minimum, and maximum capacity for instances.
Create an Internal Load Balancer: This distributes traffic across your app tier instances. Configure it to
listen on port 80 and forward traffic to your app tier.

Step 5: Web Tier Instance Deployment
Update NGINX Configuration File: Update the configuration to point to your internal load balancer's
DNS.
Launch an EC2 Instance (in a public subnet): This instance will run your NGINX web server and React.js
application. Connect to the Instance Use Session Manager to connect to the instance.
Configure Software Stack: Install Node.js and NVM on the instance.
Configure Web Instance: Download your web tier code from S3.
Build and deploy your React application using npm commands.
Notes: This is a general overview, and specific configurations may vary depending on your application.
Remember to replace placeholders like BUCKET_NAME with your actual values.
Additional Note: Consider using AWS documentation for in detailed instructions.
I hope this breakdown helps! Feel free to ask if you have any further questions about specific steps &
Don’t forgot to prevent unnecessary Big Costs must delete the resources you created on any Cloud
Practices

Step 6: Clean up -
To prevent unnecessary Costs, Delete the resources that you created as part of this tutorial.
