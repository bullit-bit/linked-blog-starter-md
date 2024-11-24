1. RoIP virtual circuit - both sides
```
sh voice port summary
```
```
sh voice call summary
```

2. LMR session - both sides

```
sh voice lmr 0/1/0
```

3. Config - both sides
```
sh running-config | sec dial-peer
```

-------

Bouncing ports
```
voice-port 0/0/0
```
```
shut
```
```
no shut
```


Example when trying to ping between VG's:
```
dial-peer voice 100 voip
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 destination-pattern 481001103
 session target ipv4:10.185.32.9   <------------    Ping this on the other VG side
 incoming called-number .
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
```


E-lead = Receive 
M-lead = Transmit 
