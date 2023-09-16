### Useful commands 

(config)# ip domain-lookup

(config)# ip name-server <domain IP>   

show arp

ping <domain name>

###

![image](https://github.com/M4gOo/Python/assets/57456345/1fd9df3e-c675-4cd0-85df-e3865ec21902)

>>>>>  The routers cannot be DNS servers in Packet Tracer (doesn't support the ip dns server), in this case I will use DNS-Server  


10.10.10.10 - DNS Server


### 1) Configure R1, R2 and R3 to use 10.10.10.10 as their DNS server.

--- R1

R1>en 

R1#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

R1(config)#ip domain-lookup

R1(config)#ip name-server 10.10.10.10   

--- R2

R2>en

R2#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

R2(config)#ip domain-lookup

R2(config)#ip name-server 10.10.10.10

--- R3

R3>en

R3#conf t

Enter configuration commands, one per line.  End with CNTL/Z.

R3(config)#ip domain-lookup

R3(config)#ip name-server 10.10.10.10


###  2) Verify you can ping R2 and R3 from R1 using their hostnames

R1(config)#exit

R1#

%SYS-5-CONFIG_I: Configured from console by console

R1#ping R2

Translating "R2"...domain server (10.10.10.10)

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 10.10.10.2, timeout is 2 seconds:

!!!!!

Success rate is 100 percent (5/5), round-trip min/avg/max = 0/0/2 ms


### 3) Check ARP cache

R1#show arp

Protocol  Address          Age (min)  Hardware Addr   Type   Interface

Internet  10.10.10.1              -   0090.0CD7.0D01  ARPA   FastEthernet0/0

Internet  10.10.10.2              9   0004.9A96.A9A5  ARPA   FastEthernet0/0

Internet  10.10.10.10             9   0090.21C6.D284  ARPA   FastEthernet0/0

R2#show arp

Protocol  Address          Age (min)  Hardware Addr   Type   Interface

Internet  10.10.10.1              9   0090.0CD7.0D01  ARPA   FastEthernet0/0

Internet  10.10.10.2              -   0004.9A96.A9A5  ARPA   FastEthernet0/0

Internet  10.10.10.10             5   0090.21C6.D284  ARPA   FastEthernet0/0

Internet  10.10.20.1              8   0030.F2BA.30E7  ARPA   FastEthernet1/0

Internet  10.10.20.2              -   0060.2FCA.ACA0  ARPA   FastEthernet1/0

R3#show arp

Protocol  Address          Age (min)  Hardware Addr   Type   Interface

Internet  10.10.20.1              -   0030.F2BA.30E7  ARPA   FastEthernet0/0

Internet  10.10.20.2              5   0060.2FCA.ACA0  ARPA   FastEthernet0/0


>>>>>>>>>>>>   IMPORTANT!!!!

R1 can reach R3 via R2 (this IP is included in the ARP cache). The DNS server is also in the same IP subnet as R1 so will appear in the ARP cache

R2 is directly connected to both networks as shown on arp cache

R3 is directly connect to R2 only, so it doesn't have any entries for the 10.10.10.0/24 network



Packet Tracer CLI view for all command done before

![image](https://github.com/M4gOo/Python/assets/57456345/58b6f368-7659-46ce-9acf-fa3aa8fdc7b2)

