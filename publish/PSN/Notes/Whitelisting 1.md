
Working on DHCP servers cit-dhcp-01 and pol-dhcp-01. Please don't make any changes on these servers at this time.


View without affecting sheet
```
view /etc/dhcp/c-fabric-classes 
```

Edit Sheet
```
sudo vi /etc/dhcp/c-fabric-classes
```

/MACADDRESS

dd - delete line
i - insert
esc - finish editing

:q! - don't save changes
:wq! - save changes


Check for errors
```
sudo dhcpd -t
```

Check status
```
sudo systemctl status dhcpd
```

Restart server, don't at same time
```
sudo systemctl restart dhcpd 
```