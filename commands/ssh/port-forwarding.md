# SSH: Port Forwarding

After establishing the port forwarding, the local connection will be forwarded
over the secure channel to the target host.

```sh
ssh <HOST> -N -L <LOCAL_PORT:TARGET_HOST:TARGET_PORT>

# [EXAMPLE]
# ssh bastion.simcept.com -N -L 5432:psql.simcept.com:5432
```

> `-N`: Do not execute a remote command. This is useful for port forwarding.
