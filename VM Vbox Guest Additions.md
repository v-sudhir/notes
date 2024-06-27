# Installing VirtualBox Guest Additions
```bash
yum install gcc kernel-devel kernel-headers dkms make bzip2 perl vim wget telnet net-tools nmap-ncat.x86_64 binutils gcc make patch libgomp glibc-headers glibc-devel elfutils-libelf-devel
sh ./VBoxLinuxAdditions.run --nox11
# The --nox11 option tells the installer not to spawn an xterm window.
```

# Install on Oracle Linux
```bash
# Oracle Linux 9
dnf install epel-release -y
dnf install dkms kernel-uek-devel gcc make bzip2 perl elfutils-libelf-devel
sudo dnf update kernel-uek-* kernel-uek
sh ./VBoxLinuxAdditions.run
```
