**1*. RoIP checks - both sides
```
sh voice port summary
```
```
sh voice call summary
```
```
sh running-config | sec dial-peer
```
```
sh running-config | sec voice-port
```
```
sh voice lmr 0/0/0
```



---
Bouncing ports
```
voice-port 0/0/0
```
```
shut
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
2. Get Config for both sides

belghpst-vg2

```
voice-port 0/1/3
 operation 4-wire
 type 5
 signal lmr
 bootup e-lead off
 lmr m-lead audio-gate-in
 lmr led-on
 timeouts call-disconnect 3
 connection trunk 422102010 answer-mode
 description RoIP Circuit PAMBHPST-BELGHPST-1

dial-peer voice 103 voip
 description RoIP Circuit BELGHPST-PAMBHPST-1
 destination-pattern 422102010
 session protocol sipv2
 session target ipv4:10.145.1.96
 incoming called-number .
 voice-class sip bind control source-interface Loopback1411
 voice-class sip bind media source-interface Loopback1411
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 203 pots
 description RoIP Circuit BELGHPST-PAMBHPST-1
 destination-pattern 420702013
 port 0/1/3
```


pambhpst-vg2

```
voice-port 0/1/0
 operation 4-wire
 type 5
 signal lmr
 bootup e-lead off
 lmr m-lead audio-gate-in
 lmr led-on
 timeouts call-disconnect 3
 connection trunk 420702013
 description RoIP Circuit PAMBHPST-BELGHPST-1

dial-peer voice 100 voip
 description RoIP Circuit PAMBHPST-BELGHPST-1
 destination-pattern 420702013
 session protocol sipv2
 session target ipv4:10.145.1.97
 incoming called-number .
 voice-class sip bind control source-interface Loopback1411
 voice-class sip bind media source-interface Loopback1411
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 200 pots
 description RoIP Circuit PAMBHPST-BELGHPST-1
 destination-pattern 422102010
 port 0/1/0
```


3. Example changing pambhpst-vg2 voice-port 0/1/0 to 0/1/1

Removing old voice-port 0/1/0 settings
```
voice-port 0/1/0
 shut
 no connection trunk 420702012 <------------ Remove
 description RoIP Circuit SPARE

dial-peer voice 100 voip
 description RoIP Circuit SPARE <------------ SPARE
 no destination-pattern 420702013 <------------ Remove
 session protocol sipv2
 no session target ipv4:10.145.1.97 <------------ Remove
 incoming called-number .
 voice-class sip bind control source-interface Loopback1411 
 voice-class sip bind media source-interface Loopback1411
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 200 pots
 description RoIP Circuit SPARE <------------ SPARE
 destination-pattern 422102010
 port 0/1/0

```

Adding new voice-port 0/1/1 settings
```
voice-port 0/1/1
 operation 4-wire
 type 5
 signal lmr
 bootup e-lead off
 lmr m-lead audio-gate-in
 lmr led-on
 timeouts call-disconnect 3
 connection trunk 420702013 <--------------------- Add
 description RoIP Circuit PAMBHPST-BELGHPST-1 <--------------------- Add

dial-peer voice 101 voip
 description RoIP Circuit PAMBHPST-BELGHPST-1 <--------------------- Add
 destination-pattern 420702013 <--------------------- Add
 session protocol sipv2
 session target ipv4:10.145.1.97 <--------------------- Add
 incoming called-number .
 voice-class sip bind control source-interface Loopback1411
 voice-class sip bind media source-interface Loopback1411
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 201 pots
 description RoIP Circuit PAMBHPST-BELGHPST-1 <--------------------- Add
 destination-pattern 422102011 <--------------------- Add
 port 0/1/1
```

belghpst-vg2 - Need to point to the new voice-port 0/1/1 
```
dial-peer voice 103 voip
 description RoIP Circuit BELGHPST-PAMBHPST-1
 destination-pattern 422102011 <--------------------- Add
 session protocol sipv2
 session target ipv4:10.145.1.96 <--------------------- Add/Check
 incoming called-number .
 voice-class sip bind control source-interface Loopback1411
 voice-class sip bind media source-interface Loopback1411
 ip qos dscp 45 media
 ip qos dscp 45 media rsvp-fail
 ip qos dscp 45 media rsvp-pass
 ip qos dscp cs3 signaling
 no vad
dial-peer voice 203 pots
 description RoIP Circuit BELGHPST-PAMBHPST-1
 destination-pattern 420702013
 port 0/1/3
```

5. Bounce ports 

---

#### Change voice-port speed - ROIP is working but slow. etc

Changing the port speed

1. locate what switch it's connected too
```
sh lldp neighbors
```

2. go to the port 
```
show interfaces descriptions | match vg
```
3. set the port to auto-negotiation, this is done by default from removing no-auto-negotiation
```
delete interfaces ge-0/0/19 speed 100m  
delete interfaces ge-0/0/19 link-mode full-duplex  
delete interfaces ge-0/0/19 ether-options no-auto-negotiation
```
4. Bounce the voice-ports