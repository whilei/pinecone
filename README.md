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

```
[kde@plasma-mobile ~]$ cat /proc/cpuinfo
processor       : 0
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 1
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 2
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4

processor       : 3
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x0
CPU part        : 0xd03
CPU revision    : 4
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

```
pacman -Syu git
pacman -S make gcc
```

```
cd /tmp
wget 'https://golang.org/dl/go1.16.2.linux-arm64.tar.gz'
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.16.2.linux-arm64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' | sudo tee -a /etc/profile
```
