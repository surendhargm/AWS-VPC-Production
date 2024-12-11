# VPC with servers in private subnets and NAT
## OVERVIEW:
In this project,entailed the design, implementation, and configuration of a highly secure and scalable Virtual Private Cloud (VPC) on Amazon Web Services (AWS), tailored to support the deployment of web applications and services. The VPC architecture features a sophisticated network topology, comprising public and private subnets, each configured with customized routing tables and access controls. This design enables seamless communication between internal components, while providing tightly controlled internet access through carefully configured network address translation (NAT) gateways and security groups, thereby ensuring the confidentiality, integrity, and availability of sensitive data and applications.

![alter text](images/vpc.png)

## STEP 1:  Log in to AWS Management Console
a.Navigate to the AWS Management Console and ensure you are in the region where you want to create the VPC.
## STEP 2: Create a New VPC
### 1.Go to VPC Dashboard:
a.In the AWS Console, search for VPC in the search bar and click on it.

### 2.Create the New VPC:
a.Click Create VPC.<br>
b.Choose "Create VPC and more".<br>
c.Name your VPC, define an IPv4 CIDR block (network range), and select a default tenancy.<br>
![alter text](images/01.png)

### 3.Configure Subnets:
a.For high availability, pick at least 2 Availability Zones.<br>
b.Create public and private subnets for resource management (e.g., 1public, 2private).<br>
c.Set up a NAT gateway choose 1 per AZ.<br>
d.Leave VPC endpoints as "None" unless required.<br>

### 4. Create VPC:
e.Click "Create VPC" to complete the setup.<br>
![alter text](images/02.png)

## STEP 3:Create an Auto Scaling Group
### 1.Navigate to the EC2 Console.
a. Navigate to Services > EC2 under the Compute section.<br>
b.Select "Auto Scaling groups" from the menu . <br>
c.Click Create Auto Scaling group.<br>
![alter text](images/03.png)

### 2.Create a Launch Template:
a.Open the AWS Management Console and go to the EC2 dashboard after click on Launch Templates option in EC2 dashbord.<br>
b.Click the "Create launch template" button.<br>
![alter text](images/04.png)
c.Provide a Name and Description for your launch template. <br>
![alter text](images/05.png)
d.Select a Amazon Machine Image AMI (Ubuntu server).<br>
e.Select a free tier eligible instance type(eg.t2.micro).<br>
f.Create the key pair (use same key pair).<br>
![alter text](images/06.png)

### 3.Create a Security Group:
a.Click the "Create Security Group" button.<br>
b.Provide a Name and Description for the security group.<br>
![alter text](images/07.png)

### 4.Configure Security Group Rules:
#### I.Inbound Rules:
Type: SSH, Protocol: TCP, Port Range: 22, Source: Anywhere IPv4<br>
Type : All Traffic , Protocol: All, Port Range: All, Source: Anywhere IPv4<br>
Type: All TCP, Protocol: TCP, Port Range: All, Source: Anywhere IPv4<br>
![alt text](images/08.png)

#### II.Outbound Rules:
Type: All Traffic, Protocol: All, Port Range: All, Destination: Anywhere IPv4<br>
Click "Create Security Group" to finalize.<br>
### 5.Save the Launch Template:
a.Set any additional configurations as needed.<br>
b.Click "Create launch template" to save your configuration.<br>


### 6.Configure Auto Scaling Group Settings:
a.Enter a name for your Auto Scaling group.<br>
b.Choose a pre-created Launch Template defining your instance configuration.<br>
c.Select the VPC where your instances will be launched.<br>
d.Choose private subnets with in the selected VPC.<br>
![alt text](images/09.png)
![alt text](images/10.png)

### 7.Scaling Settings:
a.Minimum Capacity: Set the minimum number of instances (select2).<br>
b.Maximum Capacity: Set the maximum number of instances (select4).<br>
c.Desired Capacity: Set the initial number of instances (select 2).<br>
![alt text](images/11.png)

### 8.Finalize the Auto Scaling Group:
a.Configure any additional settings as needed.<br>
b.click Create Auto Scaling group.<br> 
![alt text](images/12.png)

## STEP 4:Create an instance
1.Navigate to Services > EC2 from the top menu.<br>
2.Click on Instances from the left-hand menu, then click on the Launch Instances button to start creating a new instance.<br>
3.Choose an Amazon Machine Image (AMI).<br>
4.Select an AMI based on your requirements. For example:<br>
a.Use Ubuntu AMI for general-purpose workloads.<br>
b.Pick a pre-configured AMI if your application requires specific software.<br>
![alt text](images/13.png)

5.Select an Instance Type:<br>
6.Choose an instance type that matches your performance and cost requirements. For example:<br>
a. t2.micro is suitable for lightweight workloads and is free-tier eligible.<br>
b. For larger workloads, select an instance type with more CPU or memory.<br>
![alt text](images/14.png)

7.Configure the Network Settings:<br>
8.Under Network settings, choose the VPC you want the instance to be part of.<br>
9.Select a public subnet within your VPC.<br>
10.Enable Auto-assign Public IP to ensure your instance can be accessed from the internet.<br>
![alt text](images/15.png)

#### 11.Set Up a Security Group: 
#### 12.Choose a Security Group: 
a.Select an existing group or create a new one as per your requirements.  
#### 13.Configure Security Rules:
a.Ensure the following inbound rules are added:  
#### a.Inbound Rules:  
        i. SSH Access: Protocol: TCP, Port: 22, Source: Anywhere or your specific IP address. 
        ii. HTTP Access: Protocol: TCP, Port: 80, Source: Anywhere (if hosting a website).  
#### 14.Review and Launch Your Instance:  
#### 15.Verify Configurations: 
a.Double-check all settings, such as AMI, instance type, storage, and networking configurations. 
#### 16.Launch the Instance:
a. Click the launch button and select a Key Pair for SSH access. If a key pair does not exist, create one and download it securely.  
#### 17.Validate the Instance Setup:  
#### 18.Navigate to Instances Section:
a. In the EC2 dashboard, confirm the instance is listed.  
#### 19.Verify Instance State:
a. Ensure the instance status is “Running” and note the Public IP Address.  
#### 20.Test Connectivity: 
a.Use the public IP to connect via SSH or verify web accessibility if applicable.  
![alt text](images/16.png)

