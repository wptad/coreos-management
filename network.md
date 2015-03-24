# network


## Bond example

```
coreos:
  etcd:
    discovery: <%= discoveryURL %>
    addr: <%= requestIP %>:4001
    peer-addr: <%= requestIP %>:7001
  fleet:
    metadata: "role=services,cabinet=one"
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start
    - name: reset-interfaces.service
      command: start
      content: |
        [Unit]
        Description=Setting interfaces to down and restarting networking post boot.
        After=network-online.target

        [Service]
        Type=oneshot
        ExecStart=/tmp/reset-interfaces

write_files:
  - path: /etc/ssh/sshd_config
    permissions: 0600
    owner: root:root
    content: |
      # Use most defaults for sshd configuration.
      UsePrivilegeSeparation sandbox
      Subsystem sftp internal-sftp
      ClientAliveInterval 180
      UseDNS no
      PermitRootLogin no
  - path: /tmp/reset-interfaces
    permissions: 0700
    owner: root
    content: |
      #!/bin/bash
      logger "Resetting network interfaces for bonding."
      ip link set enp1s0f0 down
      ip link set enp1s0f1 down
      systemctl restart systemd-networkd
      logger "Network interfaces have been reset"
      rm /tmp/reset-interfaces
  - path: /etc/systemd/network/10-enp.network
    permissions: 0644
    owner: root
    content: |
      [Match]
      Name=enp*

      [Network]
      Bond=bond0
  - path: /etc/systemd/network/20-bond.netdev
    permissions: 0644
    owner: root
    content: |
      [NetDev]
      Name=bond0
      Kind=bond

      [Bond]
      Mode=1
  - path: /etc/systemd/network/30-setup-bond-ipv4-public.network
    permissions: 0644
    owner: root
    content: |
      [Match]
      Name=bond0

      [Network]
      Address=<%= requestIP %>/24
      Gateway=<%= productionEtcdGateway %>
      DNS=114.114.114.114
```

 * bonding model <http://blog.sina.com.cn/s/blog_89a8a72d01018kqf.html>
 * <https://github.com/coreos/bugs/issues/36#issuecomment-79328829>
 * bond <http://www.reversengineered.com/2014/08/21/setting-up-bonding-in-systemd/>
 