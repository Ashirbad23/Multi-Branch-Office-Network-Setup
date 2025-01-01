# Multi-Branch Office Network Setup

## Objective
Design and configure a network for a company with three branches in different cities, connected via WAN links. The configuration includes subnetting, routing, and Port Address Translation (PAT) to ensure efficient communication between branches and secure access to the internet.

---

## Network Requirements

### General Requirements
1. Subnetting must be used to allocate IP addresses efficiently for departments within each branch.
2. Routing must be configured to enable communication between the three branches over the WAN links.
3. Port Address Translation (PAT) must be implemented to provide internet access to all devices using a single public IP.
4. The design must ensure scalability for future department additions.

### Offices and Departments
- **Bangalore Office**: HR and IT
- **Cuttack Office**: HR and IT
- **Bhubaneswar Office**: HR and IT
- **Two WAN Links**: WAN 1 and WAN 2

---

## Subnetting Details

The network `198.168.1.0/24` is divided using a mix of fixed-length and variable-length subnet masks (VLSM) to efficiently allocate IP addresses. Below are the details:

### VLSM Subnet Allocation for WAN Links
To allocate only two usable IPs per WAN link, the `198.168.1.224/27` subnet was further divided into smaller subnets using a `/30` mask:

| Subnet | Range                  | Usable IPs        | Purpose  |
|--------|------------------------|-------------------|----------|
| 1      | 198.168.1.224/30      | 198.168.1.225-226 | WAN 1    |
| 2      | 198.168.1.228/30      | 198.168.1.229-230 | WAN 2    |
| 3      | 198.168.1.232/30      | 198.168.1.233-234 | Reserved |
| 4      | 198.168.1.236/30      | 198.168.1.237-238 | Reserved |
| 5      | 198.168.1.240/30      | 198.168.1.241-242 | Reserved |
| 6      | 198.168.1.244/30      | 198.168.1.245-246 | Reserved |
| 7      | 198.168.1.248/30      | 198.168.1.249-250 | Reserved |
| 8      | 198.168.1.252/30      | 198.168.1.253-254 | Reserved |

### Subnet Allocation for Branches
The remaining subnets were divided using a `/27` mask:

| Subnet | Range                 | Usable IPs                | Location              |
|--------|-----------------------|---------------------------|-----------------------|
| 1      | 198.168.1.0/27       | 198.168.1.1 - 198.168.1.30 | Bangalore HR         |
| 2      | 198.168.1.32/27      | 198.168.1.33 - 198.168.1.62 | Bangalore IT         |
| 3      | 198.168.1.64/27      | 198.168.1.65 - 198.168.1.94 | Cuttack HR           |
| 4      | 198.168.1.96/27      | 198.168.1.97 - 198.168.1.126 | Cuttack IT           |
| 5      | 198.168.1.128/27     | 198.168.1.129 - 198.168.1.158 | Bhubaneswar HR       |
| 6      | 198.168.1.160/27     | 198.168.1.161 - 198.168.1.190 | Bhubaneswar IT       |
| 7      | 198.168.1.192/27     | 198.168.1.193 - 198.168.1.222 | Reserved for Future Branch |
| 8      | 198.168.1.224/27     | 198.168.1.225 - 198.168.1.254 | Reserved for WAN Links |

---

## Subnetting Calculation Details

### Formula
- **Subnet Mask for `/30`**:
  - Block size: `2^(32 - subnet bits) = 2^(32 - 30) = 4`
  - Usable IPs: Block size - 2 (network and broadcast addresses)
  - Usable IPs per subnet: 2
- **Subnet Mask for `/27`**:
  - Block size: `2^(32 - 27) = 32`
  - Usable IPs: Block size - 2
  - Usable IPs per subnet: 30

### Steps for WAN Link Subnetting
1. Start with `198.168.1.224/27`.
2. Subdivide into `/30` subnets:
   - Subnet 1: `198.168.1.224/30` (Usable: `198.168.1.225-226`)
   - Subnet 2: `198.168.1.228/30` (Usable: `198.168.1.229-230`)
   - Subnet 3: `198.168.1.232/30` (Usable: `198.168.1.233-234`)
   - Subnet 4: `198.168.1.236/30` (Usable: `198.168.1.237-238`)
   - Subnet 5: `198.168.1.240/30` (Usable: `198.168.1.241-242`)
   - Subnet 6: `198.168.1.244/30` (Usable: `198.168.1.245-246`)
   - Subnet 7: `198.168.1.248/30` (Usable: `198.168.1.249-250`)
   - Subnet 8: `198.168.1.252/30` (Usable: `198.168.1.253-254`)

### Steps for Department Subnetting
1. Allocate `/27` subnets for each department.
2. Assign the subnets in sequence:
   - Bangalore HR: `198.168.1.0/27`
   - Bangalore IT: `198.168.1.32/27`
   - Cuttack HR: `198.168.1.64/27`
   - Cuttack IT: `198.168.1.96/27`
   - Bhubaneswar HR: `198.168.1.128/27`
   - Bhubaneswar IT: `198.168.1.160/27`
   - Reserved for Future Branch: `198.168.1.192/27`

---

## Router Configuration

### PAT Setup Commands
Below are the PAT configuration commands for setting up NAT on the routers:

```shell
Router> enable
Router# configure terminal
Router(config)# interface gig0/0/0
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface gig0/0/1
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface se0/2/0
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface se0/2/1
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface se0/1/0
Router(config-if)# ip nat outside
Router(config-if)# exit

Router(config)# access-list 10 permit 198.168.1.0 0.0.0.255
Router(config)# ip nat inside source list 10 interface se0/1/0 overload
Router(config)# exit
```

### Static Routing Example
Static routes must be configured to enable communication between the branches via the WAN links. Example:

```shell
Router(config)# ip route 198.168.1.64 255.255.255.224 <WAN_next_hop_IP>
Router(config)# ip route 198.168.1.128 255.255.255.224 <WAN_next_hop_IP>
```

---

## Verification Steps

### Testing Branch Communication
1. **Ping Between Devices**:
   - From a device in Bangalore HR (Subnet 1), ping a device in Cuttack IT (Subnet 4).
   - Example command:
     ```shell
     ping 198.168.1.100
     ```
2. Ensure devices in all subnets can communicate across the WAN links.

### Testing Internet Access
1. On any PC in the network, configure the default gateway and DNS.
2. Test internet access by pinging a public IP (e.g., `8.8.8.8`).
3. Open a browser and access a website to confirm connectivity.

---

## Deliverables

1. **Network Topology**:
   - Fully functional in Cisco Packet Tracer.
2. **Configuration Files**:
   - Subnetting details for each department.
   - Static routing setup.
   - PAT configuration for internet access.
3. **Testing Verification**:
   - Documentation of successful pings between branches.
   - Proof of internet access from any PC.

---

## Scalability Considerations
To ensure scalability:
- Reserve unused subnets for future department expansions.
- Consider implementing VLANs if more departments are added to the same branch.
- Upgrade WAN bandwidth as the number of devices increases.

---

**End of Document**
