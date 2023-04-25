# Virtual Private Cloud (VPC)

</br>

## Table of Contents

- [5.0 - VPC General](#5.0)
- [5.1 - VPC Sizing and Structure - PART1](#5.1)
- [5.2 - VPC Sizing and Structure - PART2](#5.2)
- [5.3 - Custom VPCs - PART1](#5.3)
- [5.4 - Custom VPCs - PART2](#5.4)
- [5.5 - VPC Subnets](#5.5)
- [5.6 - Implement multi-tier VPC subnets](#5.6)
- [5.7 - VPC Routing, Internet Gateway & Bastion Hosts](#5.7)
- [5.8 - Configuring A4l public subnets and Jumpbox - PART1](#5.8)
- [5.9 - Configuring A4l public subnets and Jumpbox - PART2](#5.9)

</br>

<h2>5.0 - VPC General</h2><a name="5.1"></a>

- VPCs work within **one account** and **one region with multiple availability zones** 
- VPCs are **private and isolated by default**
- VPCs type may be **Default** (only one per region and comes pre-configured by AWS) or **Custom** (can have multiple per region, but needs to be configured end-to-end)
- **Default VPC** always has the 172.31.0.0/16 range 

</br>

<h2>5.1 - VPC Sizing and Structure - PART1</h2><a name="5.1"></a>

**Design Plan:**

- **What is the VPC IP range?** The **VPC CIDR** should be carefully planned due to it being hard to change later on
- **What size should a VPC be?** How many services fit inside the VPC
- **What are the network limitations?** Overlapping and duplicate ranges may create communication problems
- **What could happen in the future?** The VPC needs to conform not only with the present
- **What is the structure of the VPC?** The IP range should be divided into availability zones which in turn are divided into tiers (web, app, db, etc)

</br>

<h2>5.2 - VPC Sizing and Structure - PART2</h2><a name="5.2"></a>

- No notes in this lesson

</br>

<h2>5.3 - Custom VPCs - PART1</h2><a name="5.3"></a>

- Custom VPCs support **hybrid networks** to connect to other cloud platforms or on-premises networks
- **Default Tenancy** resources may go on shared hardware or dedicated hardware
- **Dedicated Tenancy** locks the VPC so that all resources created inside the VPC **has to go on dedicated hardware**
- VPCs have **one primary private IPv4 CIDR block**, which has to be **between /28 (16 IPs) and /16 (65536 IPs)**

</br>

<h2>5.4 - Custom VPCs - PART2</h2><a name="5.4"></a>

- No notes in this lesson

</br>

<h2>5.5 - VPC Subnets</h2><a name="5.5"></a>

- Subnets are created entirely **private** and in a **single availability zone**
- A subnet by default use **IPv4** and its CIDR is a **subset of the VPC CIDR** 
- The subnet CIDR **can't overlap with other subnets' CIDR**
- Subnets by default **can communicate with other subnets within the VPC**
- Each subnet has **five reserved IPs**. Example with 10.16.16.0/20 
  1. **Network Address** (10.16.0.0): represents the network itself
  2. **Network+1** / **VPC Router** (10.16.0.1): moves data **between subnets** plus **in or out of the VPC**, if configured so
  3. **Network+2** / **DNS Reserved** (10.16.0.2): reserved by AWS for DNS usage
  4. **Network+3** / **Future Reserve** (10.16.0.3): reserved by AWS for future requirements
  5. **Network Broadcast Address** (10.16.0.255): last IP of the subnet, although broadcasting is not supported in VPC

</br>

<h2>5.6 - Implement multi-tier VPC subnets</h2><a name="5.6"></a>

- Subnet calculator for IPv4: https://www.site24x7.com/tools/ipv4-subnetcalculator.html

</br>

<h2>5.7 - VPC Routing, Internet Gateway & Bastion Hosts</h2><a name="5.7"></a>

- The **Internet Gateway** allows communication between the VPC and the public internet