# Network
Network+ Lab: 3 Debian VMs in a virtual LAN with static IPs, ping tests, and Apache web services.

# Network+ Virtual Lab Project

This project demonstrates a small virtual network lab using 3 Debian VMs.  
The goal is to create a network where VMs can **ping each other** and provide basic **network services**.

---

## VM Setup and IP Configuration

| VM   | IP Address      | Subnet Mask     | Gateway       | Services             | Ports  |
|------|----------------|----------------|---------------|--------------------|--------|
| VM1  | 192.168.10.11  | 255.255.255.0  | 192.168.10.1  | Ping               | -      |
| VM2  | 192.168.10.12  | 255.255.255.0  | 192.168.10.1  | Apache Web Server  | 80     |
| VM3  | 192.168.10.13  | 255.255.255.0  | 192.168.10.1  | Apache Web Server  | 80     |

---

## Configuration Steps

### 1. Checking Current IPs
- Initially, some VMs had multiple IPs on the network interface:
```bash
ip a

Observed primary and secondary IPs


2. Removing Unnecessary Secondary IPs

To simplify the network, extra IPs were removed:


sudo ip addr del 192.168.10.20/24 dev ens33  # remove secondary IP
sudo ip addr del 169.254.100.10/24 dev ens33  # remove auto-generated IP

Verified only primary IP remained:


ip a

3. Setting Static IPs

Each VM was assigned a static IP in the subnet 192.168.10.0/24


sudo ip addr add 192.168.10.11/24 dev ens33  # VM1
sudo ip addr add 192.168.10.12/24 dev ens33  # VM2
sudo ip addr add 192.168.10.13/24 dev ens33  # VM3

sudo ip route add default via 192.168.10.1


---

4. Installing Apache Web Server

On VM2 and VM3 to provide HTTP service:


sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2


---

5. Testing Network and Services

Ping Test

ping 192.168.10.12  # VM1 to VM2
ping 192.168.10.13  # VM1 to VM3

All VMs responded successfully


Web Service Test

Access from any VM in the LAN:


http://192.168.10.12
http://192.168.10.13

Apache default page loaded successfully



---

Lessons Learned (Network+ Concepts)

Ping: Verifies connectivity between VMs

Static IPs: Ensures predictable addressing

Subnetting: VMs within same subnet can communicate directly

Services & Ports: Each VM can run network services (HTTP/SSH) and respond on its ports

VLAN concept: All VMs currently in same LAN; VLAN can be added for logical separation



---

Optional Next Steps

Add VLANs and test trunk vs access ports

Install additional services like SSH or FTP

Configure routing between subnets

Document network diagrams



---

Summary

All 3 VMs are configured with static IPs in the same subnet

Network connectivity confirmed via Ping

Apache service installed and successfully tested

Demonstrates key Network+ objectives: IP configuration, subnetting, services, and basic LAN connectivity


---


