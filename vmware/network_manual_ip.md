# Manual IP Configuration in VMWare vCD Environment

With the help of vmtools, VMWare is able to configure the VM. However, this can only be done during first boot or when
customization is triggered.

If (for some reason) the VM cannot get an IP, it may stuck indefinitely during boot. This behaviour can be prevented
by disabling network configuration inside cloud-init. To disable network configuration of cloud-init, create
`/etc/cloud/cloud.cfg.d/99-disable-network-config.cfg` with the following content:

```
network: { config: disabled }
```

For DNS search, create `/etc/netplan/00-dns-search.yaml` with the following content:

```
network:
    version: 2
    ethernets:
        ens160:
            nameservers:
                search:
                    - dr.local
```

netplan reads YAML files in lexical order. Lexicographically later files (regardless of in which directory they are)
amend (new mapping keys) or override (same mapping keys) previous ones. See
[documentation](https://netplan.io/reference/) for more information.

In our case, VMWare creates a backup of above configuration, creates a separate configuration file called
`99-netcfg-vmware.yaml` with all necessary network configuration. In this case, above configuration file adds DNS
search configuration to VMWare's configuration.
