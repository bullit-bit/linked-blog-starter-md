
1. Confirm switch doesn't already have VLAN
```
show vlans | match 
show interfaces irb
```

2. Check Switch Core 

```
show interfaces irb.
```

3. Check Router 

```

```

4. Schedule Change 

5. Add VLAN and commit
```
set vlans VLAN_NAME description VLAN_NAME_ID
set vlans VLAN_NAME vlan-id ID

commit check
commit comment "OPS-MYCHANGENO"
```


![[Pasted image 20250205183834.png]]