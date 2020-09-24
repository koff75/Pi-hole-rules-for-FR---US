# Pi-hole-rules-for-FR---US
### Custom Adblock rules for Pi-hole / AdGuard DNS filter including mobile (iOS &amp; Android). Useful for to block tracking ads &amp; telemetry on every devices including IoT.


# The goal is to allow Pi-hole to talk to dnscrypt-proxy which in turn would talk to NextDNS (DNS over TLS)

1. Install stubby via apt : `sudo apt-get install stubby`
2. Edit the config file : `sudo nano /etc/stubby/stubby.ytml`
3. Under the listen_adresses add te following :
```
listen_addresses:
  - address_data: 127.0.0.1
    port: 5353
  - address_data: 0::1
    port: 5353
 ```
9. Change `round_robin_upstreams: *1*` to become `round_robin_upstreams: *0*`
10. Change the `/upstream_recursive_servers/` section with the code found on the setup section in your NextDNS dashboard (https://my.nextdns.io/ -> section Linux -> Stubby)
11. Restart stubby: sudo systemctl restart stubby
12. In your Pi-hole instance, change your upstream DNS become `127.0.0.1#5353/`
13. Test you configuration: `dig @<pi-hole_ip> www.google.fr`
