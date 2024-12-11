
```
set interfaces ge-0/0/0 unit 0 description "###### BWC ######"
set switch-options interface ge-0/0/0.0 interface-mac-limit 10
set switch-options interface ge-0/0/0.0 interface-mac-limit packet-action drop-and-log
```

```
set interfaces ge-0/0/0 disable 
set poe interface ge-0/0/0 disable  
```

```
delete interfaces ge-0/0/0 disable 
delete poe interface ge-0/0/0 disable 
```

**