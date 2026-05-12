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

## Screenshots

### VPC
VPC created
<img width="1898" height="740" alt="VPC Overview" src="https://github.com/user-attachments/assets/6a936f43-2128-4d1e-95b1-f6af8aeb041c" />

Subnet created
<img width="1898" height="750" alt="Subnet Overview" src="https://github.com/user-attachments/assets/29f53da1-3ba2-4a84-a627-029b5a146b5c" />

Internet Gateway attached
<img width="1904" height="745" alt="Internet Gateway attached Overview" src="https://github.com/user-attachments/assets/fa6f5d0f-34bb-4ad2-960a-130f608b77c5" />

Route table configured
<img width="1908" height="739" alt="Route table Overview" src="https://github.com/user-attachments/assets/6c85a5f2-cf47-4c67-95e1-0d93b929c499" />

Securit Group Created
<img width="1903" height="747" alt="Security Group Overview" src="https://github.com/user-attachments/assets/0898de3c-2d92-44fc-97f7-aeb54d90b07f" />
Inbound Rules
<img width="1869" height="746" alt="Inbound Rules" src="https://github.com/user-attachments/assets/fbb5e6e9-8c9c-4983-8dfb-eba2f904ab6f" />
Outbound Rules
<img width="1849" height="352" alt="Outbound Rules" src="https://github.com/user-attachments/assets/30ab1b61-2a72-4f9a-9271-b30999146874" />

EC2 Dashboard
<img width="1908" height="442" alt="EC2-Dashboard" src="https://github.com/user-attachments/assets/810bd8d6-da0b-42a6-b3ea-6d07b38db099" />
EC2 Instance Details
<img width="1902" height="747" alt="EC2 Instance-Details" src="https://github.com/user-attachments/assets/2f1e760c-1a3d-47cc-a444-064299dcc3b2" />
EC2 Networking
<img width="1891" height="744" alt="EC2-Networking" src="https://github.com/user-attachments/assets/b686da6f-edc0-4d92-81df-f76472e6cc41" />
EC2 Instance Connect Terminal
<img width="1916" height="619" alt="Appache install terminal" src="https://github.com/user-attachments/assets/4ec85e81-2ca5-4f19-993e-f5c23073a4f1" />
Apache Status Running
<img width="1914" height="610" alt="Apache status running" src="https://github.com/user-attachments/assets/e6b03940-6f91-4fff-a0ae-83e11fefc274" />
Website in Browser
<img width="1473" height="423" alt="website-working" src="https://github.com/user-attachments/assets/c34df3b9-cc48-4cce-ae18-4a6ecfcb4d45" />








