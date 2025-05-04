# Multi-Tier-Load-Balancing
Multi-Tier Load Balancing with Public-Private Subnets, AWS Infrastructure
# AWS Architecture with Reverse Proxy, Internal Load Balancer, Auto Scaling, and Patch Management

## Overview

This project sets up a scalable web architecture in AWS using EC2 instances as reverse proxies, an internal load balancer, and private EC2 instances running Apache. The infrastructure is automatically scaled using Auto Scaling Groups (ASG), and patch management is handled via AWS Systems Manager.

## Architecture Diagram

![Architecture Diagram](path/to/your/diagram.png)

### Components:
1. **Public EC2 Instances (Reverse Proxies)**:
   - Apache or Nginx is configured to act as a reverse proxy.
   - These instances receive traffic and forward it to the internal load balancer.

2. **Internal Load Balancer (ELB)**:
   - Distributes incoming traffic to private EC2 instances.
   - Only accessible within the VPC.

3. **Private EC2 Instances (Apache)**:
   - Run Apache to handle the incoming requests from the internal load balancer.

4. **Auto Scaling**:
   - Auto Scaling Groups (ASG) ensure that the number of EC2 instances in the private subnet adjusts based on demand (CPU utilization, etc.).

5. **AWS Systems Manager (Patch Management)**:
   - Patches are managed and applied automatically to EC2 instances using Systems Manager.

## Step-by-Step Setup

### 1. Set Up Public EC2 Instances (Reverse Proxies)
- Launch two EC2 instances in the public subnet.
- Install and configure Apache or Nginx as reverse proxies.
- Configure the proxy to forward traffic to the internal load balancer.

### 2. Set Up Internal Load Balancer (ELB)
- Create an internal ELB in your VPC.
- Register private EC2 instances with the load balancer.

### 3. Set Up Private EC2 Instances (Apache)
- Launch two EC2 instances in the private subnet.
- Install Apache on these instances to handle incoming requests from the internal load balancer.

### 4. Set Up Auto Scaling Group
- Create an Auto Scaling Group for the private EC2 instances.
- Define scaling policies based on CPU utilization.

### 5. Set Up Patch Management with AWS Systems Manager
- Install Systems Manager agent on EC2 instances.
- Create a patching baseline and apply patches using `AWS-RunPatchBaseline`.

## Auto Scaling and Scaling Policy

- **Scale Out Policy**: If CPU usage > 70% for 5 minutes, launch new instances.
- **Scale In Policy**: If CPU usage < 30% for 5 minutes, terminate instances.

## Patching with AWS Systems Manager

- Patches are applied using `AWS-RunPatchBaseline` to ensure all EC2 instances are up-to-date.

## Conclusion

This setup ensures that your architecture is both scalable and easy to maintain. The reverse proxy setup with an internal load balancer ensures secure traffic routing, and the Auto Scaling Group ensures that your application can handle varying loads. Systems Manager automates the patching process, keeping your infrastructure secure and up-to-date.

