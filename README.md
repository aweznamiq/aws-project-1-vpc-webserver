# AWS Project 1: VPC, Public Subnet, and EC2 Web Server

## Objective

Build a basic AWS network from scratch and launch a web server that can be reached from the internet.

## Services Used

- VPC
- Subnet
- Internet Gateway
- Route Table
- Security Group
- EC2 Instance

## Architecture

Internet Gateway connects the VPC to the internet.
Route table sends internet traffic to the Internet Gateway.
Public subnet hosts the EC2 instance.
Security group controls access to the server

##Diagram
                    Internet
                        │
                        ▼
              Internet Gateway
                  (dev-igw)
                        │
                        ▼
                 Route Table
                  (public-rt)
          Route: 0.0.0.0/0 → IGW
                        │
                        ▼
                Public Subnet
                  10.0.1.0/24
                        │
                        ▼
                 EC2 Web Server
                    Apache
                 Public IP

                 
## Build Steps

Step 1: Create the VPC

Open the VPC console.
Create a new VPC named dev-vpc.
Use CIDR block 10.0.0.0/16.
Save the VPC.
Step 2: Create the public subnet

Go to Subnets.
Create a subnet named public-subnet-1.
Place it in dev-vpc.
Use CIDR block 10.0.1.0/24.
Select one Availability Zone.
Enable auto-assign public IPv4 if available.

Step 3: Create and attach the Internet Gateway
Open Internet Gateways.
Create one named dev-igw.
Attach it to dev-vpc.

Step 4: Create the route table
Open Route Tables.
Create a route table named public-rt.
Select dev-vpc.
Add a route:
Destination: 0.0.0.0/0
Target: dev-igw
Save the route.

Step 5: Associate the route table with the subnet
Open Subnet associations.
Edit subnet associations.
Select public-subnet-1.
Save the association.

## Step 6: Create Security Group

Created a security group named `web-sg` inside the `dev-vpc` VPC.

Configured inbound rules:
- SSH (Port 22) allowed only from my IP address
- HTTP (Port 80) allowed from anywhere (`0.0.0.0/0`)

Configured outbound rules:
- Allowed all outbound traffic (default configuration)

Purpose:
The security group acts as a virtual firewall for the EC2 web server and controls inbound and outbound traffic.

Security Best Practices:
- Restricted SSH access to my IP only
- Allowed HTTP publicly so the website can be accessed from the internet

## Step 7: Launch EC2 Instance

Launched an EC2 instance named `web-server` using Amazon Linux.

Configuration:
- Instance Type: t3.micro
- VPC: dev-vpc
- Subnet: public-subnet-1
- Security Group: web-sg
- Public IP: Enabled

Created a new key pair named `web-server-key` for secure access.

The EC2 instance will host the web server for the project.

## Step 8: Install Apache Web Server

Connected to the EC2 instance using EC2 Instance Connect.

Installed Apache web server:

sudo yum install httpd -y

Started and enabled Apache service:

sudo systemctl start httpd
sudo systemctl enable httpd

Created a simple HTML page inside:

/var/www/html/index.html

Verified website accessibility using the EC2 public IP address.








