
https://psnmc.atlassian.net/wiki/spaces/PSNMC/pages/1565982725/Unable+to+commit+due+to+storage+is+full+Old+package+exist
```
request system storage cleanup
```
```
start shell user root
```
```
find / -size +100000
```
```
file delete <file name>
```

- Try to only remove .arg files

---

https://psnmc.atlassian.net/wiki/spaces/PSNMC/pages/1648852993/Unable+to+commit+due+to+storage+is+full+Large+.arg+file

```
start shell user **root**
```
```
request session member 0
```
```
du -xhs /packages/db
```
```
pkg setop rm previous
pkg delete old
```
```
show system storage
```
