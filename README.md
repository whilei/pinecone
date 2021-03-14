### Defaults

`user=kde password=123456`
`user=root password=123456`

### Steps

- Log in to the phone
- Connect to wifi

On laptop.
Figure out what the Pinecone's local IP address is.
```
ip route | grep default
arp-scan --interface=wlp0s20f3 --localnet
```

SSH to Pinecone.
```
ssh kde@192.168.86.60 # pass=123456
> mkdir .ssh
> passwd # Change password maybe.
```

Set up SSH keys.
```
scp /home/ia/.ssh/id_rsa.pub kde@192.168.86.60:~/.ssh/authorized_keys

tail /home/ia/.ssh
Host pinecone
  Hostname 192.168.86.60
  User kde
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes
```

Take stock.
```
[kde@plasma-mobile ~]$ uname -a
Linux plasma-mobile 5.9.12-1-MANJARO-ARM #1 SMP Wed Dec 2 11:41:52 CET 2020 aarch64 GNU/Linux
# After pacman upgrade (below), new kernel.
[kde@plasma-mobile ~]$ uname -a
Linux plasma-mobile 5.11.3-1-MANJARO-ARM #1 SMP Thu Mar 4 17:54:13 UTC 2021 aarch64 GNU/Linux
```

Update things on the Pinecone.
```
sudo pacman -Syu elinks
```

Install stuff.
```
pacman -S gpsd
pacman -S rsync
pacman -S geoclue
```

```
[kde@plasma-mobile ~]$ /usr/lib/geoclue-2.0/demos/where-am-i
```
