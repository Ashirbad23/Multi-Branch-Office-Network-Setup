- Bangalore Office (HR and IT)
- Cuttack Office (HR and IT)
- Bhubaneswar Office (HR and IT)
- Two WAN links (WAN 1 and WAN 2).

---

### 1. **Subnet Mask Calculation**
   - **Requirement:** 8 subnets
   - Formula: \( 2^n \geq \text{Number of subnets} \)
     - \( n = 3 \) because \( 2^3 = 8 \).
   - Subnet mask: 
     - Original mask: `/24` (255.255.255.0)
     - Add 3 bits for subnetting: `/27` (255.255.255.224)

---

### 2. **Subnet Ranges**
   Each subnet will have:
   - \( 2^5 = 32 \) addresses (since \( 32 - 27 = 5 \)).
   - Usable IPs per subnet: \( 32 - 2 = 30 \) (excluding network and broadcast addresses).

   Subnet ranges for `198.168.1.0/27`:
   - Subnet 1: `198.168.1.0 - 198.168.1.31` (Usable: `198.168.1.1 - 198.168.1.30`)
   - Subnet 2: `198.168.1.32 - 198.168.1.63` (Usable: `198.168.1.33 - 198.168.1.62`)
   - Subnet 3: `198.168.1.64 - 198.168.1.95` (Usable: `198.168.1.65 - 198.168.1.94`)
   - Subnet 4: `198.168.1.96 - 198.168.1.127` (Usable: `198.168.1.97 - 198.168.1.126`)
   - Subnet 5: `198.168.1.128 - 198.168.1.159` (Usable: `198.168.1.129 - 198.168.1.158`)
   - Subnet 6: `198.168.1.160 - 198.168.1.191` (Usable: `198.168.1.161 - 198.168.1.190`)
   - Subnet 7: `198.168.1.192 - 198.168.1.223` (Usable: `198.168.1.193 - 198.168.1.222`)
   - Subnet 8: `198.168.1.224 - 198.168.1.255` (Usable: `198.168.1.225 - 198.168.1.254`)

---

### 3. **Subnet Allocation**
   Based on your requirements:
   - **Bangalore Office**
     - HR: Subnet 1 (198.168.1.0/27)
     - IT: Subnet 2 (198.168.1.32/27)
   - **Cuttack Office**
     - HR: Subnet 3 (198.168.1.64/27)
     - IT: Subnet 4 (198.168.1.96/27)
   - **Bhubaneswar Office**
     - HR: Subnet 5 (198.168.1.128/27)
     - IT: Subnet 6 (198.168.1.160/27)
   - **WAN Links**
     - WAN 1: Subnet 7 (198.168.1.192/27)
     - WAN 2: Subnet 8 (198.168.1.224/27)

---

### 4. **Validation**
   - **Number of usable IPs:** Each office department (HR and IT) gets 30 IPs, which should be sufficient.
   - **WAN links:** Even though they only need 2 IPs, each WAN is allocated a full subnet for simplicity.

---
