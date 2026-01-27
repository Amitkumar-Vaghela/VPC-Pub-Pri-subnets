# VPC-Pub-Pri-subnets
Build a Custom VPC with Public and Private Subnets
# Secure AWS VPC Architecture for E-Commerce Application

## Real-World Scenario

You are building a secure network for an e-commerce application:

- The frontend (web application) must be publicly accessible.  
- The backend, such as the database, must be completely isolated from the internet.  

This requires a custom AWS VPC with public and private subnets, proper routing, and controlled internet access.

---

## What You Are Building

A tiered VPC architecture:

- A public subnet for internet-facing resources.  
- A private subnet for sensitive backend resources.  
- Controlled routing using route tables.  
- Internet access only where required.

---

## Learning Objectives

After completing this project, you will learn:

- How to design CIDR blocks.  
- How to create public and private subnets.  
- How Internet Gateways (IGW) work.  
- How route tables control network traffic.  
- How AWS enforces network isolation.

---

## AWS Services Used

| Service | Purpose |
|--------|---------|
| Amazon VPC | Creates an isolated virtual network. |
| Subnets | Divide the VPC into public and private zones. |
| Route Tables | Control where network traffic flows. |
| Internet Gateway (IGW) | Allows internet access for public resources. |

---

## Architecture Overview

Network topology:

