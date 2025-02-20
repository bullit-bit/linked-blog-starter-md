```
Cisco Vendor config
==============================================
hostname hostname-r1


interface GigabitEthernet0/0/0
description NBN AVC
bandwidth 100000
no ip address
no ip redirects
no ip proxy-arp
media-type rj45
negotiation auto
no cdp enable
no lldp transmit
no shut
!
interface GigabitEthernet0/0/0.700
description <carriage>
encapsulation dot1Q 700
ip address 172.31.64.129 255.255.255.248
no negotiation auto
duplex full
speed 100
no shut
!
username root secret cisco123
enable secret cisco123
!
no aaa new-model
!
line vty 0 15
history size 50
no access-class in
no access-class 23 in
session-timeout 15
exec-timeout 15 0
!
transport input telnet ssh
transport output telnet
login local
exit

!
line con 0
session-timeout 15
exec-timeout 15 0
transport output telnet ssh
!
router bgp 64739
neighbor 172.31.64.133 remote-as 24479
neighbor 172.31.64.133 description eBGP Peer to Nexium PE
!
address-family ipv4
   neighbor 172.31.64.133 activate
  no auto-summary
  no synchronization
exit-address-family

! ####---- End Configuration
```