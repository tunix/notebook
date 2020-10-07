# VMWare Guest Info

VMWare allows the VM to fetch some configuration settings about itself with the following command:

```
vmtoolsd --cmd "info-get guestinfo.ovfenv"
```

It prints some important details about the guest OS in XML format. Some important ones are:

* MAC Address
* Gateway IP (`vCloud_gateway_0`)
* IP address of the VM (`vCloud_ip_0`)

In order to parse this information, a package called `xmlstarlet` can be installed.

```
apt install xmlstarlet
```

Then we can use the following command to fetch the IP address of the VM:

```
vmtoolsd --cmd "info-get guestinfo.ovfenv" \
    | xmlstarlet sel -N oe="http://schemas.dmtf.org/ovf/environment/1" \
        -N ve="http://www.vmware.com/schema/ovfenv" \
        --net -t -v '//oe:Property[@oe:key="vCloud_ip_0"]/@oe:value'
```
