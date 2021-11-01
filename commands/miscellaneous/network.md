# Network


### netstat

#### Linux

```sh
$ netstat -anp
```

> `-a`: Show both listening and non-listening (for TCP this means established connections) sockets.  
> `-n`: Show numerical addresses instead of trying to determine symbolic host, port or user names.  
> `-p`: Show the PID and name of the program to which each socket belongs.

#### Mac

```sh
$ lsof -n -i
```

> `-i`: displays all open network connections and the name of the process that is using the connection. Adding a 4, as in `-i4`, will display only IPv4 connections. Adding a 6 instead (`-i6`) will display only IPv6 connections.  
> The `-i` flag can also be expanded to specify further details. `-iTCP` or `-iUDP` will only return TCP and UDP connections. `-iTCP:25` will only return TCP connections on port 25. A range of ports can be specified with a dash, as it `-iTCP:25-50`.  
> Using `-i@1.2.3.4` will return only connections to the IPv4 address 1.2.3.4. IPv6 addresses can be specified in the same fashion. The @ precursor can also be used to specify hostnames in the same way, but both remote IP addresses and hostnames cannot be used simultaneously.  
> 
> `-P`: disables the conversion of port numbers to port names, speeding up output.  
>
> `-n`: disables the conversion of network numbers to host names. When used with -P above, it can significantly speed up lsof's output.  
> 
> `-u`: user only returns commands owned by the named user.  
> 
> _Source: [How to Use the Netstat Command on Mac](https://www.lifewire.com/using-netstat-command-on-mac-4176069)_

