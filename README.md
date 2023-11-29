# Deploy Application Using AWS
Deploying a web application on Amazon Web Services (AWS). The application consists of a frontend built using HTML, CSS, and JavaScript and a backend built with Node.js. 
By using Amazon EC2, Amazon S3, Amazon RDS, Amazon VPC, and AWS Identity and Access Management (IAM) in your plan. 

## Step 1: AWS Account Setup
Create an AWS Account:

-If you don't have an AWS account, create one at AWS Management Console.

## Step 2:Create IAM User
In the IAM dashboard, click on "Users" in the left navigation pane.

-Click on "Add user" and provide a username.

-Choose "Programmatic access" for API access and click "Next."

-Set Permissions:

  -Choose "Attach existing policies directly" to assign policies.
  
  -For a frontend developer, you might use the "AmazonS3FullAccess" policy.
  
  -For a backend developer, consider creating a custom policy allowing EC2 access and attaching it.
  
  -Review and Create:Review your choices and click "Create user."
  
  -Make note of the Access Key ID and Secret Access Key for each user.

## Step 3: Frontend Deployment with Amazon S3
##### Create an S3 Bucket:

-Go to the S3 section in the AWS Console.

-Click "Create bucket" and give it a unique name and choose a region.

-Keep other settings default and click "Create."

##### Configure S3 for Static Website Hosting:

-In the bucket properties, go to the "Static website hosting" section.

-Select "Use this bucket to host a website" and configure index and error documents.

#### Enable Versioning:

-In the bucket properties, go to the "Management" tab.

-Enable versioning to keep track of changes to your files.

#### Configure S3 Bucket Policy:

-In the bucket permissions, go to the "Bucket Policy" tab.

-Add a policy that allows public read access. Modify the following policy:
          
          json
          
          Copy code
          
          {
          
             "Version":"2012-10-17",
             
             "Statement":[
             
                {
                
                   "Effect":"Allow",
                   
                   "Principal":"*",
                   
                   "Action":[
                   
                      "s3:GetObject"
                  ],
                  
                  
                   "Resource":[
                   
                      "arn:aws:s3:::app1/*"
                   ]
                   
                
                }
             
             
            ]
          
          }
#### Replace "your-bucket-name" with the actual name of your S3 bucket

## Step 3: Backend Deployment with Amazon EC2
#### Launch an EC2 Instance:

-In the EC2 dashboard, click "Launch Instance."

-Choose an Amazon Machine Image (AMI) suitable for Node.js (e.g., Amazon Linux).

-Configure the instance details, add storage, and configure security groups.

##### Configure Security Groups:
-In the security groups section, allow inbound traffic on the required ports (e.g., 80 for HTTP, 443 for HTTPS).

-Create a security group rule allowing inbound traffic on port 22 (SSH) for your IP address.

-Connect to Your EC2 Instance:

-Use SSH to connect to your EC2 instance using the key pair associated with the instance.

#### Install and Configure Node.js:
-Update the package list: sudo yum update -y (for Amazon Linux).

-Install Node.js and npm: sudo yum install nodejs npm -y.




Open a web browser and enter the S3 website endpoint provided in the "Static website hosting" tab. It should be something like http://your-bucket-name.s3-website-your-region.amazonaws.com

-Copy your Node.js backend code to the EC2 instance, either manually or using tools like scp or version control systems like Git.

-Start your Node.js application: node app.js (replace "app.js" with your main application file).


