**1*. RoIP virtual circuit - both sides
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

---

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

But only if you send the command at the same time they are transmitting.   So if on Radio, they do a quick press on the " press to talk" on handset, you may miss it.   If they hold for longer you have more chance of seeing anything RES have squark box's that can send continuous signal down line.  So easy to see if being received. If they attach one at PCC end you will need e-lead command and at far end you will need m-lead command


---

#### Swapping ports

1. Shut ports
2. Config

```
#Port 0/1/0 - shutdowm
dial-peer voice 100 voip
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 incoming called-number .
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 200 pots
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 destination-pattern 448200010
 port 0/1/0
 
#Port 0/1/1 - online
dial-peer voice 101 voip
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 destination-pattern 481001103
 session target ipv4:10.185.32.9
 incoming called-number .
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 201 pots
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 destination-pattern 448200011
 port 0/1/1
```

```
#Port 0/1/0 - shutdowm
voice-port 0/1/0
 operation 4-wire
 type 5
 signal lmr
 bootup e-lead off
 lmr m-lead audio-gate-in
 lmr led-on
 timeouts call-disconnect 3
 shutdown
 description RoIP Circuit BIVLLPST-townsvllpcm-1
 
 #Port 0/1/1 - online
voice-port 0/1/1
 operation 4-wire
 type 5
 signal lmr
 bootup e-lead off
 lmr m-lead audio-gate-in
 lmr led-on
 timeouts call-disconnect 3
 connection trunk 481001103
 description RoIP Circuit BIVLLPST-townsvllpcm-1
```

3. Bounce ports
