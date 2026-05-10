# AWS Project 1: VPC, Public Subnet, and EC2 Web Server

## Objective

Build a basic AWS network from scratch and deploy a web server accessible from the internet.

## Services Used

- VPC
- Subnet
- Internet Gateway
- Route Table
- Security Group
- EC2

## Architecture

The project uses a custom VPC with a public subnet. An Internet Gateway and route table allow internet access to an EC2 web server.

## Build Steps

1. Created custom VPC
2. Created public subnet
3. Attached Internet Gateway
4. Configured route table
5. Created security group
6. Launched EC2 instance
7. Installed Apache web server

## Screenshots

### VPC
![VPC](screenshots/vpc.png)

### EC2
![EC2](screenshots/ec2.png)

## Lessons Learned

- How VPC networking works
- How route tables control traffic
- How security groups protect resources

  ## Cleanup

Resources were terminated after testing to avoid unnecessary charges.
