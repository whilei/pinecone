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

Update things on the Pinecone.
```
sudo pacman -Syu elinks
```



