Juniper
```
set interfaces ge-0/0/0 disable
set poe interface ge-0/0/0 disable
```
```
delete interfaces ge-0/0/0 disable
delete poe interface ge-0/0/0 disable
```

Checks
```
show poe interface | match ge-0/0/0
show interfaces terse | match ge-0/0/0

request diagnostics tdr start interface ge-0/0/0
show diagnostics tdr interface ge-0/0/0
```

---

Cisco
```
shut
power inline never
```
```
no shut
power inline auto
```

Checks
```
show power inline
show interface status  

test cable-diagnostics tdr interface Gi1/0/1
show cable-diagnostics tdr int Gi1/0/1
```


---
Cable test meanings

|                      |                                                                                                                                                            |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Result               | Explaination                                                                                                                                               |
| Normal               | Ideal result you want.<br><br>- If testing **FastEthernet**, you want Pair A and B as “Normal”.<br>- If testing GigabitEthernet, you want ALL as “Normal”. |
| Open                 | Open circuit. This means that one (or more) pair has “no pin contact”.                                                                                     |
| Short                | Short circuit.                                                                                                                                             |
| Impedance Mismatched | Bad cable. For more explanation, go [here](http://www.epanorama.net/circuits/tdr.html).                                                                    |
