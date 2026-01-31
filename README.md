# Build a Custom VPC with Public and Private Subnets  
**Designing a Secure and Isolated AWS Network Architecture**
## Architecture Screenshots

### VPC and Subnet Configuration
![VPC Setup](./Image/Screenshot%202026-01-27%20114913.png)

### Route Table and Internet Gateway
![Route Table Setup](./Image/Screenshot%202026-01-27%20120144.png)

---

## STEP 1 / Overview

### Lab Overview
**DISCLAIMER:**  
This document is created for learning and academic demonstration only. For real-world or production use, always refer to the official AWS documentation.  
The steps are aligned with the AWS Console experience for **2024–2025**.

### Problem Statement (Real-World Use Case)
You are designing the network layer for an application where:
- The **frontend** must be accessible from the internet.
- The **backend/database** must remain isolated and secure with no direct internet exposure.

### What You Will Build
A custom **Virtual Private Cloud (VPC)** with clearly separated **public and private subnets**, using routing rules to control traffic flow.

---

## STEP 2 / Curriculum

### Learning Objectives
- Understand CIDR block planning.
- Create and configure a custom VPC.
- Design public and private subnets.
- Configure Internet Gateway and route tables.
- Validate network-level isolation.

---

## STEP 3 / AWS Services Used

| Service | Purpose |
|-------|--------|
| Amazon VPC | Provides logical isolation for cloud resources |
| Subnets | Divide the VPC IP range into smaller networks |
| Route Tables | Control how traffic is directed |
| Internet Gateway | Enables internet access for public resources |

---

## STEP 4 / Architecture

### Network Design Overview

- **VPC CIDR:** `10.0.0.0/16`
- **Public Subnet:** `10.0.1.0/24`  
  - Internet accessible
- **Private Subnet:** `10.0.2.0/24`  
  - No direct internet access

### Architecture Logic
- Public subnet routes traffic to the Internet Gateway.
- Private subnet relies only on internal routing (no IGW attached).

---

## STEP 5 / Prerequisites

Before starting this lab, ensure:
- You have an active AWS account.
- You understand basic networking concepts such as IP address ranges and CIDR notation.
- You have permissions to create VPC-related resources.

---

## STEP 6 / Execution

### Task 1: Create the VPC

1. Open **VPC Dashboard**.
2. Select **Create VPC**.
3. Choose **VPC Only**.
4. Set IPv4 CIDR block to: `10.0.0.0/16`.
5. Provide a name tag (example: `Custom-VPC`).
6. Create the VPC.

---

### Task 2: Create Subnets

1. Navigate to **Subnets** → **Create Subnet**.
2. Select your newly created VPC.

#### Subnet 1: Public Subnet
- Name: `Public-Subnet`
- Availability Zone: Any
- IPv4 CIDR: `10.0.1.0/24`

#### Subnet 2: Private Subnet
- Name: `Private-Subnet`
- Availability Zone: Any
- IPv4 CIDR: `10.0.2.0/24`

Create both subnets.

---

### Task 3: Configure Internet Gateway

1. Go to **Internet Gateways**.
2. Click **Create Internet Gateway**.
3. Name it (example: `Custom-IGW`).
4. Attach the IGW to your VPC.

---

### Task 4: Configure Route Tables

#### Public Route Table
1. Go to **Route Tables** → **Create Route Table**.
2. Name: `Public-RT`
3. Select your VPC.

#### Add Route
- Destination: `0.0.0.0/0`
- Target: Internet Gateway

#### Subnet Association
- Associate `Public-Subnet` with `Public-RT`.

---

#### Private Subnet Routing
- Leave the **Main Route Table** unchanged.
- Do NOT add any internet route to it.
- This ensures the private subnet remains isolated.

---

## STEP 7 / Verification

### Validation Checklist

1. Public Route Table contains:
   - `0.0.0.0/0 → Internet Gateway`
2. Private subnet is NOT associated with the public route table.
3. Main route table does NOT have an internet route.

### Success Criteria
- Public subnet has internet access.
- Private subnet remains fully internal.
- Tier-based isolation is achieved.

---

## STEP 8 / Troubleshooting

### Common Issues and Fixes

- **Overlapping CIDR Blocks**  
  Ensure all subnet CIDRs are unique and within the VPC range.

- **No Internet Access in Public Subnet**  
  Check whether the Internet Gateway is attached to the VPC.

- **Private Subnet Exposed**  
  Verify that it is not associated with the public route table.

---

## STEP 9 / Cleanup

To avoid unwanted charges:
1. Delete the VPC.
2. This action will automatically remove:
   - Subnets
   - Route tables
   - Internet Gateway associations

---

## STEP 10 / Advanced Enhancements (Optional)

- Add a **NAT Gateway** to allow private subnet outbound internet access.
- Implement **Network ACLs** for subnet-level security.
- Configure **VPC Peering** for cross-VPC communication.

---

## STEP 11 / Notes

- This setup reflects a basic production-ready network foundation.
- Always apply security groups and least-privilege rules when launching resources.
- Extend this architecture for multi-tier or high-availability designs.

---

**End of Document**
