
```
set interfaces ge-0/0/0 unit 0 description "###### BWC ######"
set switch-options interface ge-0/0/0.0 interface-mac-limit 10
set switch-options interface ge-0/0/0.0 interface-mac-limit packet-action drop-and-log
```


