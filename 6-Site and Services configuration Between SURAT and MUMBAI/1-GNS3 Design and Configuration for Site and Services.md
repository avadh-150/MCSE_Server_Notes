---
# GNS3 Design and Configuration for Site and Services

![image](https://github.com/avadh-150/MCSE_Server_Notes/blob/main/MCSE%20Class%20Notes/img/SIte%20to%20services/1-GNS3%20IMAGE.png?raw=true)
---

## 🔹 R1 – **MUMBAI Edge Router (NAT + LAN + OSPF)** 🌆🌐

```plaintext
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
hostname R1

no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
ip cef
no ip domain lookup

interface FastEthernet0/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto

interface FastEthernet0/1
 no ip address
 shutdown

interface FastEthernet1/0
 ip address 192.168.20.1 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto

interface FastEthernet2/0
 ip address 10.0.13.1 255.255.255.252
 duplex auto
 speed auto

router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes
 network 192.168.20.0 0.0.0.255 area 0
 network 10.0.13.0 0.0.0.3 area 0
 default-information originate

ip nat inside source list 1 interface FastEthernet0/0 overload
access-list 1 permit any

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
```

👉 **Role:**

- Mumbai LAN gateway
    
- Internet NAT
    
- OSPF default route source
    
- DC network exit point
    

---

## 🔹 R2 – **WAN Transit Router (No LAN, Pure Routing)** 🔁

```plaintext
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
hostname R2

no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
ip cef
no ip domain lookup

interface FastEthernet0/0
 ip address 10.0.23.2 255.255.255.252
 duplex auto
 speed auto

interface FastEthernet0/1
 ip address 10.0.13.2 255.255.255.252
 duplex auto
 speed auto

interface FastEthernet1/0
 no ip address
 shutdown

interface FastEthernet2/0
 no ip address
 shutdown

router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes
 network 10.0.13.0 0.0.0.3 area 0
 network 10.0.23.0 0.0.0.3 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
```

👉 **Role:**

- Pure WAN router
    
- No NAT
    
- No LAN
    
- Keeps OSPF adjacency alive
    

If this router goes down → **sites are isolated** ❌

---

## 🔹 R3 – **SURAT Edge Router (LAN Gateway + OSPF)** 🏢

```plaintext
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
hostname R3

no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
ip cef
no ip domain lookup

interface FastEthernet0/0
 ip address 10.0.23.1 255.255.255.252
 duplex auto
 speed auto

interface FastEthernet0/1
 no ip address
 shutdown

interface FastEthernet1/0
 ip address 172.16.1.1 255.255.255.0
 duplex auto
 speed auto

interface FastEthernet2/0
 no ip address
 shutdown

router ospf 1
 router-id 2.2.2.2
 log-adjacency-changes
 network 10.0.23.0 0.0.0.3 area 0
 network 172.16.1.0 0.0.0.255 area 0

line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous

line vty 0 4
 login
```

👉 **Role:**

- Surat LAN gateway
    
- ADC network access
    
- OSPF site advertisement
    

---
