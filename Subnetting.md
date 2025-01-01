# Subnetting Documentation for Multi-Branch Office Network

## Problem Statement
The goal is to design and configure a network for a company with two branches in different cities, connected via WAN links. The network must use efficient subnetting, enable routing between branches, and implement Port Address Translation (PAT) for internet access.

## Requirements
1. Subnetting to allocate IP addresses efficiently for each department.
2. Routing to enable communication between branches over the WAN links.
3. PAT configuration to provide internet access using a single public IP.
4. Scalability for future departmental additions.

## IP Address Details
We are given the network `198.168.1.0/24` to subnet into 8 subnets, including WAN links with minimal IP requirements.

---

## Step-by-Step Subnetting

### Step 1: Determine the Number of Subnets Required
- **Departments:** Each branch has two departments (HR and IT), requiring separate subnets.
- **WAN Links:** Two WAN links connecting the branches require subnets.
- **Total Subnets Needed:** 6 for departments + 2 for WAN links = 8 subnets.

### Step 2: Subnetting for Departments
Using the formula for subnetting:
- **Formula:** `2^n ≥ Required Subnets` (where `n` is the number of bits borrowed).
- For 8 subnets: `2^3 = 8` (3 bits borrowed).

**New Subnet Mask:**
- Default mask for `/24` is `255.255.255.0`.
- Borrowing 3 bits gives `/27` with a subnet mask of `255.255.255.224`.
- Each subnet has `2^(32-27) = 32` total IPs (30 usable).

**Subnet Ranges for Departments:**
1. **Subnet 1 (198.168.1.0/27):**
   - Network: `198.168.1.0`
   - Broadcast: `198.168.1.31`
   - Usable: `198.168.1.1 - 198.168.1.30` (Assigned to Bangalore HR)
2. **Subnet 2 (198.168.1.32/27):**
   - Network: `198.168.1.32`
   - Broadcast: `198.168.1.63`
   - Usable: `198.168.1.33 - 198.168.1.62` (Assigned to Bangalore IT)
3. **Subnet 3 (198.168.1.64/27):**
   - Network: `198.168.1.64`
   - Broadcast: `198.168.1.95`
   - Usable: `198.168.1.65 - 198.168.1.94` (Assigned to Cuttack HR)
4. **Subnet 4 (198.168.1.96/27):**
   - Network: `198.168.1.96`
   - Broadcast: `198.168.1.127`
   - Usable: `198.168.1.97 - 198.168.1.126` (Assigned to Cuttack IT)
5. **Subnet 5 (198.168.1.128/27):**
   - Network: `198.168.1.128`
   - Broadcast: `198.168.1.159`
   - Usable: `198.168.1.129 - 198.168.1.158` (Assigned to Bhubaneswar HR)
6. **Subnet 6 (198.168.1.160/27):**
   - Network: `198.168.1.160`
   - Broadcast: `198.168.1.191`
   - Usable: `198.168.1.161 - 198.168.1.190` (Assigned to Bhubaneswar IT)

### Step 3: VLSM for WAN Links
WAN links require only 2 usable IPs per link. To allocate IPs efficiently, we subnet the last available `/27` subnet (`198.168.1.224/27`) further into `/30` subnets.

**Subnetting Formula for WAN Links:**
- **Formula:** `2^(32-new_mask) ≥ Required Hosts`
- For 2 usable IPs: `2^(32-30) = 4` total IPs (2 usable).
- **New Subnet Mask:** `/30` with `255.255.255.252`.

**Subnet Ranges for WAN Links:**
1. **Subnet 1 for WAN 1 (198.168.1.224/30):**
   - Network: `198.168.1.224`
   - Broadcast: `198.168.1.227`
   - Usable: `198.168.1.225 - 198.168.1.226`
   - Assigned to WAN Link 1
2. **Subnet 2 for WAN 2 (198.168.1.228/30):**
   - Network: `198.168.1.228`
   - Broadcast: `198.168.1.231`
   - Usable: `198.168.1.229 - 198.168.1.230`
   - Assigned to WAN Link 2

---

## Summary of Subnets

| Subnet No. | CIDR          | Network Address | Usable IP Range       | Broadcast Address | Purpose           |
|------------|---------------|-----------------|-----------------------|-------------------|-------------------|
| 1          | 198.168.1.0/27  | 198.168.1.0     | 198.168.1.1 - 198.168.1.30 | 198.168.1.31     | Bangalore HR      |
| 2          | 198.168.1.32/27 | 198.168.1.32    | 198.168.1.33 - 198.168.1.62 | 198.168.1.63     | Bangalore IT      |
| 3          | 198.168.1.64/27 | 198.168.1.64    | 198.168.1.65 - 198.168.1.94 | 198.168.1.95     | Cuttack HR        |
| 4          | 198.168.1.96/27 | 198.168.1.96    | 198.168.1.97 - 198.168.1.126| 198.168.1.127    | Cuttack IT        |
| 5          | 198.168.1.128/27| 198.168.1.128   | 198.168.1.129 - 198.168.1.158| 198.168.1.159   | Bhubaneswar HR    |
| 6          | 198.168.1.160/27| 198.168.1.160   | 198.168.1.161 - 198.168.1.190| 198.168.1.191   | Bhubaneswar IT    |
| 7          | 198.168.1.224/30| 198.168.1.224   | 198.168.1.225 - 198.168.1.226| 198.168.1.227   | WAN Link 1        |
| 8          | 198.168.1.228/30| 198.168.1.228   | 198.168.1.229 - 198.168.1.230| 198.168.1.231   | WAN Link 2        |

---


