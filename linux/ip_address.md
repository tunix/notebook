# Getting IP address of specific NIC on Linux

`ip` command shows possible output options. One of them is `-j` which outputs in JSON format.

Getting IP address of a specific NIC:

```
ip -j -f inet addr show dev ens160 \
    | jq -r '.[].addr_info[].local'
```

`-f inet` option is to limit output with IPv4 interfaces so that the JQ input is simpler.

The command can be made even shorter by using short versions of each parameter (ex: using "a" instead of "addr") but
that would make the command less readable.
