# Basic Hierarchy - 10 June, 2022 - Day8
1. IETF
    1. Internet Engineering Task Force
    2. A standards organisation for the Internet and is responsible for the technical standards that comprise the Internet protocol suite. It has no formal membership roster or requirements and all its participants are volunteersvoluntary Internet Standards
2. IANA
    1. Internet Assigned Numbers Authority
    2. Oversees global IP address allocation, autonomous system number allocation, root zone management in the Domain Name System, media types, and other Internet Protocol-related symbols and Internet numbers.
3. RIRs
    1. Regional Internet Registries
    2. An organisation that manages the allocation and registration of Internet number resources (IP, ASN) within a region of the world.
    3. Five RIRs → **APNIC, ARIN, RIPE NCC, LACNIC, and AFRINIC**
4. ISPs
    1. Internet Service Providers
    2. An organisation that provides services for accessing, using, or participating in the Internet.
5. User

# Types Of IP Addresses
1. IPv4 - 32bits
    
    IP Addressing with default class subnet mask is called **Classfull Addressing**.
    
    IP Addressing with non default subnet masks to reduce IP Address depletion is called **Classless Addressing**.
    
    1. Class A 
        1. N.H.H.H
        2. Subnet Mask: 255.0.0.0
        3. 0 - 127
    2. Class B
        1. N.N.H.H
        2. Subnet Mask: 255.255.0.0
        3. 128 - 191
    3. Class C
        1. N.N.N.H
        2. Subnet Mask: 255.255.255.0
        3. 192 - 223
    4. Class D - **Multicasting**
        1. Used by routers for routing purposes
        2. 224 - 239
    5. Class E - **Future Use**
        1. 240 - 255
2. IPv6 - 128 bits

# Subnet Masks
![subnet-masks](https://www.tutorialspoint.com/ipv4/images/class_a_subnets.jpg)

# ---------------------NO DATE TRACK--------------------------

OSI Model
![image](https://user-images.githubusercontent.com/66965591/174161349-bbdcf1cb-7e44-4245-887c-628b80b050bd.png)

#Adv Topic
ISPs can create the vpm or network for u via many ways → l3vpn, l2vpn, mpls etc

Router At Home is actually Router + Modem (many timez)

→ ADSL or DSL Device (Asymmetric Digital Subscriber Line)

Modem 

- Modulation - Analog to Digital
- DeModulation - Digital to Analog

In Corporate World U may see the firbre cable directly to Some Routers (They are High End Routers / Servers)

→ They have a small chip called SFP (SMALL FORM PLUGGABLE) ADAPTER

→ Converts Optical to Electrical Signals

Else Normally U get 

- PSTN (PUBLIC SWITCH TELEPHONE NETWORK) cable
    - We use ADSL
- Fibre Cable
    - We use Fibre Modems

## IP Addrs
1. IETF
    1. Internet Engineering Task Force
    2. A standards organisation for the Internet and is responsible for the technical standards that comprise the Internet protocol suite. It has no formal membership roster or requirements and all its participants are volunteersvoluntary Internet Standards
2. IANA
    1. Internet Assigned Numbers Authority
    2. Oversees global IP address allocation, autonomous system number allocation, root zone management in the Domain Name System, media types, and other Internet Protocol-related symbols and Internet numbers.
3. RIRs
    1. Regional Internet Registries
    2. An organisation that manages the allocation and registration of Internet number resources (IP, ASN) within a region of the world.
    3. Five RIRs → **APNIC, ARIN, RIPE NCC, LACNIC, and AFRINIC**
4. ISPs
    1. Internet Service Providers
    2. An organisation that provides services for accessing, using, or participating in the Internet.
5. User

1. IPv4 - 32bits
    IP Addressing with default class subnets is called Classfull Addressing.
    IP Addressing with non default subnet masks to reduce IP Address depletion is called Classless Addressing.
    1. Class A 
        1. NHHH
        2. 0 - 127
    2. Class B
        1. NNHH
        2. 128 - 191
    3. Class C
        1. NNNH
        2. 192 - 223
    4. Class D - Multicasting 
        1. Used by routers for routing purposes
    5. Class E - Future Use
2. IPv6 -128 bits


## Did You Know?
1. It’s not ur PCs that have MAC Addresses but the NICs that they have.
    1. i.e. No. of MAC Addrs = No. of NICs (Wireless, Wired, Bluetooth, etc)
2. Naming Conventions
    1. Ethernet → 10mbps
    2. Fast Ethernet → 100mbps
    3. GigaEthernet → 1gbps
3. Loopback Server
    1. Ur laptop itself has a server for ur machine
    2. All the images, icons n ol of the files
4. ncpa.cpl : Control Panel → Network Connections 
5. Ping (echo request):  **Packet Internet or Inter-Network Groper**
    1. How does the pc understand that it’s a echo req → Type Code = 8
    2. And Echo Reply Type Code = 0
    3. So, if we’re getting a msg (00001000) we need to reply (00000000)
6. To check MAC ADDr in Windows
    1. getmac -v
    2. ipconfig/all
7. 
![image](https://user-images.githubusercontent.com/66965591/174160955-c08a1d95-542a-41e7-8bd8-c158700a0f9d.png)
8. IANA - Internet Assigned Numbered Authority
    1. Can’t directly go to IANA for IPs
    2. For that it has formed 
    3. RIRs → Regional Internet Registries
9. Routers (Cisco) (Large) (Used by service providers)
    1. Branch (4000 Series)
    2. ASR (**Aggregation Services Router**)
    3. ISR (Integrated Series Router)
    4. CSR (Carrier Sensitive Router)
10. IP Protocols → TCP (protocol no → 6) & UDP (protocol no → 17)
![image](https://user-images.githubusercontent.com/66965591/174161122-264ffee3-65c7-4c11-873c-80075837029a.png)

### Basics Of Subnetting
![image](https://user-images.githubusercontent.com/66965591/174161173-b3255cd8-89b6-4c42-8135-273f83251b47.png)
- First IP -> Network ID
- Last IP -> Broadcast ID
![image](https://user-images.githubusercontent.com/66965591/174161307-2b674cd2-7ac5-4fdd-87bb-f52d1a7be26c.png)


![image](https://user-images.githubusercontent.com/66965591/174161498-0c94b827-3e8c-46cb-a0a8-09d2918a26de.png)


# ----------------------------X--------------------------------

# ARP | Career Path - 16 June, 2022 - Day12

ARP (Address Resolution Protocol)
- arp -a → shows ARP Table
- arp -d → clears ARP Table
- arp -s <ip-addr> <mac-addr> → adds an entry in the ARP Table

Pvt IPs

![image](https://user-images.githubusercontent.com/66965591/174162384-f997a3bb-4391-4a92-aefb-129c7f7da63d.png)



