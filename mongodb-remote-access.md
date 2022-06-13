## Configuring a Pulic bindIP

MongoDB by default bound to 127.0.0.1, the local loopback network interface. This mean MongoDB is only able to accept connections that originate on the server where it's installed.

To allow remote connections, you must edit the MongoDB configuration file `/etc/mongod.conf`


### Warning
This is by no mean a good approach, you gonna expose your instance to the world to try to messing with it. For staging and dev it ok.
But to be used in production is not a very good idea, I use this on a private network so this is somewhat acceptable. 


Open the MongoDB configuration file in your preferred text editor. The following example uses `vim`:

`sudo vim /etc/mongod.conf`

Find the `network interfaces` section, then bindIp value:

```
. . .
# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1,10.0.10.143

. . .
```
Then, restart MongoDB to put this change into effect:

`sudo systemctl restart mongod.service`
