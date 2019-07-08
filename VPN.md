## PiVPN & pi-hole

- http://www.pivpn.io/
- https://pi-hole.net/

### Ad Blocking When Using VPN

- https://github.com/pivpn/pivpn/issues/66
- https://github.com/pivpn/pivpn/wiki/FAQ#installing-with-pi-hole

Edit `/etc/dnsmasq.conf`:

`listen-address=127.0.0.1, 192.168.1.88, 10.8.0.1`

### Adding Routes

Default install has IP range of `10.8.0.0`, but our internal network might be a diffrent range. Edit `/etc/openvpn/server.conf`:

`push "route 192.168.1.0 255.255.255.0"`

## Notes

- OpenVPN on Raspberry Pi -- [piVPN](http://www.pivpn.io/)

### Troubleshooting

#### No Internet Connectivity

- Usually an issue with routing
- Needs the correct `route` to be pushed in config file

##### Non-working client

Output from `ip route`:

```
0.0.0.0/1 via 10.8.0.1 dev tun0 
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100 
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100 
10.0.2.0/23 via 10.8.0.1 dev tun0 
10.1.10.0/23 via 10.8.0.1 dev tun0 
10.8.0.0/24 dev tun0 proto kernel scope link src 10.8.0.2 
128.0.0.0/1 via 10.8.0.1 dev tun0 
167.179.168.199 via 10.0.2.2 dev enp0s3 
169.254.0.0/16 dev enp0s3 scope link metric 1000 
192.168.1.0/24 via 10.8.0.1 dev tun0 
```

##### Non-working server

OpenVPN config file:

```
server 10.8.0.0 255.255.255.0

push "route 192.168.1.0 255.255.255.0"

push "route 10.1.10.0 255.255.254.0"
push "route 10.0.2.0 255.255.254.0"

#push "route 10.8.0.0 255.255.254.0"
#push "route 10.0.2.0 255.255.255.0"
```

## piVPN

### Renew Certificate

To check the expiration date:

```
cd /etc/openvpn
sudo openssl crl -in crl.pem -text
```

To renew it:

```
cd /etc/openvpn/easy-rsa
sudo ./easyrsa gen-crl
sudo cp pki/crl.pem /etc/openvpn/crl.pem
sudo systemctl restart openvpn
```
