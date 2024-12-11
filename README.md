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
c.Name your VPC, define an IPv4 CIDR block (network range), andselect adefault tenancy.<br>
![alter text](images/01.png)

### 3.Configure Subnets:
a.For high availability, pick at least 2 Availability Zones.<br>
b.Create public and private subnets for resource management (e.g., 1public, 2private).<br>
c.Set up a NAT gateway choose 1 per AZ.<br>
d.Leave VPC endpoints as "None" unless required.<br>

### 4. Create VPC:
e.Click "Create VPC" to complete the setup.<br>
![alter text](images/02.png)
