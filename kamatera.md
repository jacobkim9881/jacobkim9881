## How to make a node js server at kamatera
After signing in Kamatera service, create node.js service at kamatera console. And after clicking my new cloud server on kamatera console, open remote console at connect tab. On remote console, id is `root` and password is the one you have written when creating the service. You can access remote control on your local terminal by typing, 
``` 
ssh root@your.ip.address.of.service
```

### Configuring domain
There is already sample node.js server. You can run the server or can edit for your domain. First, set your service ip address on your domain. Set DNS setting on your domain provider site like below:

Type: A record, host: @, Value: your.service.ip.address, TTL: Automatic

Also you can add setting for www like below:

Type: A record, host: www, Value: your.service.ip.address, TTL: Automatic

On node.js server, you should set host and port for yoru domain. Host is your domain name and port is `80` for http and `443` for https.
```
let host = `your.domain.com`
, httpPort = `80`
, httpsPort = `443`;
```

But you won't access your domain on web, maybe because of firewall on your remote server.

### Unblock firewall for http, https
Open the firewall for accessing your domain.
```
firewall-cmd --add-service http --permanent
firewall-cmd --add-service https --permanent
```

[Reference is here](https://www.redhat.com/sysadmin/secure-linux-network-firewall-cmd)
