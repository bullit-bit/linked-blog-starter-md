Teams

```
Working on DHCP servers cit-dhcp-01 and pol-dhcp-01. Please don't make any changes on these servers at this time.
```

```
Completed
```

--------------------------------------------------------------------------

View
```
view /etc/dhcp/c-fabric-subnets.full
```

Edit
```
sudo vi /etc/dhcp/c-fabric-subnets.full
```

dd - Delete line from file
i - Edit  text file
ESC - exit out of editing
:q! - don't save and exit
:wq! - save and exit

Check for Errors in Syntax
```
sudo dhcpd -t
```
Check status of DHCP server
```
sudo systemctl status dhcpd
```
Restart DHCP Server (one at a time)
```
sudo systemctl restart dhcpd
```


---

Example - Getting IPR100 up
```
subnet 10.240.142.0 netmask 255.255.255.240 {
        option routers 10.240.142.1;
        pool {
                failover peer "cit-01-her-01";
                deny dynamic bootp clients;
                range 10.240.142.4 10.240.142.14;
                allow members of "vc";
                allow members of "PSN_CUCM";		
        }
        host IPR100 {
        hardware ethernet 00:50:C2:52:A0:A3;
        fixed-address 10.240.142.5;
  }

}

sh ip arp vrf cP-0001 | i 10.240.142.5

```
