# Subnetting for Multi-Branch Office Network Setup

## Objective
To efficiently allocate IP addresses for multiple offices and WAN links, ensuring scalability and future expandability using Variable Length Subnet Masking (VLSM).

---

## Network Address
- **Base Network**: 198.168.1.0/24
- **Total Hosts**: 256 (including network and broadcast addresses)

---

## Requirements
1. Subnets for three branches:
   - Bangalore Office: HR and IT departments
   - Cuttack Office: HR and IT departments
   - Bhubaneswar Office: HR and IT departments
2. Two WAN links connecting the branches.
3. Reserved subnets for:
   - **Six future WAN connections**.
   - **One future branch**.

---

## Step-by-Step Subnetting Process

### Step 1: Calculate Subnet Mask
We need subnets for departments, WAN links, and future requirements. Use VLSM to optimize IP usage.

### Step 2: Allocate Subnets for Current and Future Needs

#### Subnet 1: Bangalore Office
- **Departments**: HR and IT
- **Hosts Required**: ~30 hosts per department
- **Subnet Mask**: /27 (32 IPs per subnet, 30 usable IPs)
- **Allocation**:
  - HR: 198.168.1.0/27 (Usable: 198.168.1.1 - 198.168.1.30)
  - IT: 198.168.1.32/27 (Usable: 198.168.1.33 - 198.168.1.62)

#### Subnet 2: Cuttack Office
- **Departments**: HR and IT
- **Hosts Required**: ~30 hosts per department
- **Subnet Mask**: /27 (32 IPs per subnet, 30 usable IPs)
- **Allocation**:
  - HR: 198.168.1.64/27 (Usable: 198.168.1.65 - 198.168.1.94)
  - IT: 198.168.1.96/27 (Usable: 198.168.1.97 - 198.168.1.126)

#### Subnet 3: Bhubaneswar Office
- **Departments**: HR and IT
- **Hosts Required**: ~30 hosts per department
- **Subnet Mask**: /27 (32 IPs per subnet, 30 usable IPs)
- **Allocation**:
  - HR: 198.168.1.128/27 (Usable: 198.168.1.129 - 198.168.1.158)
  - IT: 198.168.1.160/27 (Usable: 198.168.1.161 - 198.168.1.190)

#### Subnet 4: WAN Links
- **Hosts Required**: 2 hosts per WAN link
- **Subnet Mask**: /30 (4 IPs per subnet, 2 usable IPs)
- **Allocation**:
  - WAN 1: 198.168.1.224/30 (Usable: 198.168.1.225 - 198.168.1.226)
  - WAN 2: 198.168.1.228/30 (Usable: 198.168.1.229 - 198.168.1.230)

#### Reserved Subnets for Future Needs
- **Future WAN Links**:
  - 198.168.1.232/30 (Usable: 198.168.1.233 - 198.168.1.234)
  - 198.168.1.236/30 (Usable: 198.168.1.237 - 198.168.1.238)
  - 198.168.1.240/30 (Usable: 198.168.1.241 - 198.168.1.242)
  - 198.168.1.244/30 (Usable: 198.168.1.245 - 198.168.1.246)
  - 198.168.1.248/30 (Usable: 198.168.1.249 - 198.168.1.250)
  - 198.168.1.252/30 (Usable: 198.168.1.253 - 198.168.1.254)

- **Future Branch**:
  - 198.168.1.192/27 (Usable: 198.168.1.193 - 198.168.1.222)

---

## Final Subnet Allocation Table

| Subnet         | CIDR           | Range                  | Usable IPs              | Purpose                     |
|----------------|----------------|------------------------|-------------------------|-----------------------------|
| Subnet 1       | 198.168.1.0/27 | 198.168.1.0 - 198.168.1.31   | 198.168.1.1 - 198.168.1.30   | Bangalore HR               |
| Subnet 2       | 198.168.1.32/27| 198.168.1.32 - 198.168.1.63  | 198.168.1.33 - 198.168.1.62  | Bangalore IT               |
| Subnet 3       | 198.168.1.64/27| 198.168.1.64 - 198.168.1.95  | 198.168.1.65 - 198.168.1.94  | Cuttack HR                 |
| Subnet 4       | 198.168.1.96/27| 198.168.1.96 - 198.168.1.127 | 198.168.1.97 - 198.168.1.126 | Cuttack IT                 |
| Subnet 5       | 198.168.1.128/27| 198.168.1.128 - 198.168.1.159| 198.168.1.129 - 198.168.1.158| Bhubaneswar HR             |
| Subnet 6       | 198.168.1.160/27| 198.168.1.160 - 198.168.1.191| 198.168.1.161 - 198.168.1.190| Bhubaneswar IT             |
| Subnet 7       | 198.168.1.224/30| 198.168.1.224 - 198.168.1.227| 198.168.1.225 - 198.168.1.226| WAN 1                      |
| Subnet 8       | 198.168.1.228/30| 198.168.1.228 - 198.168.1.231| 198.168.1.229 - 198.168.1.230| WAN 2                      |
| Reserved WAN 1 | 198.168.1.232/30| 198.168.1.232 - 198.168.1.235| 198.168.1.233 - 198.168.1.234| Reserved for future WAN    |
| Reserved WAN 2 | 198.168.1.236/30| 198.168.1.236 - 198.168.1.239| 198.168.1.237 - 198.168.1.238| Reserved for future WAN    |
| Reserved WAN 3 | 198.168.1.240/30| 198.168.1.240 - 198.168.1.243| 198.168.1.241 - 198.168.1.242| Reserved for future WAN    |
| Reserved WAN 4 | 198.168.1.244/30| 198.168.1.244 - 198.168.1.247| 198.168.1.245 - 198.168.1.246| Reserved for future WAN    |
| Reserved WAN 5 | 198.168.1.248/30| 198.168.1.248 - 198.168.1.251| 198.168.1.249 - 198.168.1.250| Reserved for future WAN    |
| Reserved WAN 6 | 198.168.1.252/30| 198.168.1.252 - 198.168.1.255| 198.168.1.253 - 198.168.1.254| Reserved for future WAN    |
| Future Branch  | 198.168.1.192/27| 198.168.1.192 - 198.168.1.223| 198.168.1.193 - 198.168.1.222| Reserved for future branch |

---

This configuration ensures efficient IP address allocation while keeping scalability for future needs.

