https://psnmc.atlassian.net/wiki/spaces/PSNMC/pages/1318355470/Telephony+Provision+Operate+Troubleshoot

Phones 
- [[TCCCP]]
- [[TIPT]] 
- [[Alcatel]]

Printers

--------------------------------------------------------------------------

MAB
4043449
exodus$435

--------------------------------------------------------------------------

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
view /etc/dhcp/c-fabric-classes
```
Edit
```
sudo vi /etc/dhcp/c-fabric-classes
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
