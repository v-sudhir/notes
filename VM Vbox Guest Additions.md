# Installing VirtualBox Guest Additions
```bash
yum install gcc kernel-devel kernel-headers dkms make bzip2 perl vim wget telnet net-tools nmap-ncat.x86_64 binutils gcc make patch libgomp glibc-headers glibc-devel elfutils-libelf-devel
sh ./VBoxLinuxAdditions.run --nox11
# The --nox11 option tells the installer not to spawn an xterm window.
```

# Install on OL7
```bash
[ol7_developer]
name=Oracle Linux $releasever Development Packages ($basearch)
baseurl=http://yum.oracle.com/repo/OracleLinux/OL7/developer/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=1

yum install kmod-vboxguest-uek4.x86_64 vboxguest-tools.x86_64
```
