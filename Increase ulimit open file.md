$ vi /etc/sysctl.conf
```bash
# Disable IP forwarding
net.ipv4.ip_forward = 0

# Disable source routing
net.ipv4.conf.default.accept_source_route = 0

# Disable the Magic System Request key
kernel.sysrq = 0

# Enable TCP SYN cookie protection
net.ipv4.tcp_syncookies = 1

# Enable SYN flood protection
net.ipv4.tcp_synack_retries = 5

# Don’t accept source-routed packets
net.ipv4.conf.all.accept_source_route = 0

# Don’t accept ICMP redirects
net.ipv4.conf.all.accept_redirects = 0

# Log packets with suspicious addresses
net.ipv4.conf.all.log_martians = 1

# Ignore broadcast requests
net.ipv4.icmp_echo_ignore_broadcasts = 1

# Ignore bad ICMP errors
net.ipv4.icmp_ignore_bogus_error_responses = 1

fs.file-max = 65536
```
$ vi /etc/security/limits.conf
```bash
* soft     nproc          65535
* hard     nproc          65535
* soft     nofile         65535
* hard     nofile         65535

ulimit -a```

# set ulimit at runtime
ulimit -n 65536
