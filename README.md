# PiVPN WireGuard GUI 
###### A simple (unofficial) GUI for PiVPN.  
![Image of WireGuard VPN Home](https://user-images.githubusercontent.com/17494632/100802791-f0982500-3421-11eb-9060-682388e63c3c.png)
Add, revoke and download WireGuard vpn profiles with QR Code support.
## Setup
 1. `composer install`
 2. `cp .env.example .env`
 3. Set `APP_KEY` to a random string.
 4. `cp ./storage/app/users/users.json.example ./storage/app/users/users.json`
 5. Setup a user with a username and password **I strongly recommend the use of a UUID as a password**
 6. Serve `./public`
 
 ## Extend
 New drivers can be added by implementing the `VPNDriver.php` interface. 


## Serve with lighttpd

To reuse the lighttpd installed by pihole, you need:
- add this to allow vhosts easily:

```bash
root@raspberrypi:/etc/lighttpd# grep vhosts lighttpd.conf
# para incluir vhosts
include_shell "cat /etc/lighttpd/vhosts.d/*.conf"
```

- create vhost config to serve `public`:

```bash
root@raspberrypi:/etc/lighttpd/vhosts.d# cat pivpn-wireguard-gui.conf
$HTTP["host"] == "pivpn-wireguard-gui.lan" {

        server.document-root = "/home/pi/pivpn-wireguard-gui/public"
        server.errorlog = "/var/log/lighttpd/pivpn-wireguard-gui.error.log"
        accesslog.filename = "/var/log/lighttpd/pivpn-wireguard-gui.access.log"
}
```
