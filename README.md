# Pi-hole-rules-for-FR---US
### Custom Adblock rules for Pi-hole / AdGuard DNS filter including mobile (iOS &amp; Android). Useful for to block tracking ads &amp; telemetry on every devices including IoT.


# The goal is to allow Pi-hole to talk to dnscrypt-proxy which in turn would talk to NextDNS (DNS over TLS)
## Set up dnscrypt-proxy with Pi-hole
### dnscrypt-proxy
1. Let's go the the opt directory : `cd /opt/ `
2. Download le latest version of dnscrypt-proxy (arm 64 or 32 bit) via : https://github.com/jedisct1/dnscrypt-proxy/releases/latest
` $@raspberrypi:/opt# wget https://github.com/DNSCrypt/dnscrypt-proxy/releases/download/2.0.44/dnscrypt-proxy-linux_arm-2.0.44.tar.gz `
3. Untar the archive :
 sudo tar -xvzf ./dnscrypt-proxy-linux_arm-2.0.44.tar.gz 
 4. Remove the tar :
 sudo rm dns...
 5. Go the dns dir : cd linux-arm
 6. Create the configuration file like following the example found in the directory :
 sudo cp ./example-dnscrypt-proxy.toml ./dnscrypt-proxy.toml
 7. Edit the conf file with nano: 
 server_names = ['cloudflare']
 listen_addresses = ['127.0.0.1:54']
 You can find all DNS providers from the link : https://dnscrypt.info/public-servers
 8. Install the dnscrypt-proxy : sudo ./dnscrypt-proxy -service install
 9. Start the service : sudo ./dnscrypt-proxy -service start

## Set up dnscrypt-proxy -> DNS over TLS via NextDNS
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


# PiHole blocklist:

[i] Neutrino emissions detected...
  [✓] Pulling blocklist source list into range

  [✓] Preparing new gravity database
  [i] Target: https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
  [✓] Status: Retrieval successful
  [i] Received 56596 domains

  [i] Target: https://mirror1.malwaredomains.com/files/justdomains
  [✓] Status: No changes detected
  [i] Received 26854 domains

  [i] Target: http://sysctl.org/cameleon/hosts
  [✓] Status: No changes detected
  [i] Received 20567 domains

  [i] Target: https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt
  [✓] Status: No changes detected
  [i] Received 34 domains

  [i] Target: https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt
  [✓] Status: No changes detected
  [i] Received 2701 domains

  [i] Target: https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/ParsedBlacklists/EasyList.txt
  [✓] Status: Retrieval successful
  [i] Received 1069 domains

  [i] Target: https://raw.githubusercontent.com/0Zinc/easylists-for-pihole/master/easylist.txt
  [✓] Status: Retrieval successful
  [i] Received 30965 domains

  [i] Target: https://raw.githubusercontent.com/0Zinc/easylists-for-pihole/master/easyprivacy.txt
  [✓] Status: Retrieval successful
  [i] Received 29697 domains

  [i] Target: https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/ParsedBlacklists/EasyList-Liste-FR.txt
  [✓] Status: Retrieval successful
  [i] Received 3251 domains

  [i] Target: https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/CountryCodesLists/France.txt
  [✓] Status: Retrieval successful
  [i] Received 5126 domains

  [i] Target: https://github.com/r4vi/block-the-eu-cookie-shit-list/blob/master/filterlist.txt
  [✓] Status: Retrieval successful
  [i] Received 485 domains, 485 domains invalid!
      Sample of invalid domains:
      - content="github.com">
      - content="github.com">
      - js-file-line">1and1.es,1and1.pl,1and1.co.uk,1and1.com
      - js-file-line">20minutes.fr
      - js-file-line">3.dk

  [i] Target: https://raw.githubusercontent.com/r-a-y/mobile-hosts/master/AdguardMobileAds.txt
  [✓] Status: Retrieval successful
  [i] Received 1019 domains

  [i] Target: https://raw.githubusercontent.com/r-a-y/mobile-hosts/master/AdguardMobileSpyware.txt
  [✓] Status: Retrieval successful
  [i] Received 347 domains

  [i] Target: https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/android-tracking.txt
  [✓] Status: Retrieval successful
  [i] Received 80 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/adaway.org/list.txt
  [✓] Status: Retrieval successful
  [i] Received 7950 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/adblock-nocoin-list/list.txt
  [✓] Status: Retrieval successful
  [i] Received 688 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/adguard-simplified/list.txt
  [✓] Status: Retrieval successful
  [i] Received 36335 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/anudeepnd-adservers/list.txt
  [✓] Status: Retrieval successful
  [i] Received 40867 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-ad/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2701 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-malvertising/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2735 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-malware/list.txt
  [✓] Status: Retrieval successful
  [i] Received 1 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/disconnect.me-tracking/list.txt
  [✓] Status: Retrieval successful
  [i] Received 34 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/easylist/list.txt
  [✓] Status: Retrieval successful
  [i] Received 10155 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/easyprivacy/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2793 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/eth-phishing-detect/list.txt
  [✓] Status: Retrieval successful
  [i] Received 1059 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.2o7net/list.txt
  [✓] Status: Retrieval successful
  [i] Received 1286 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.dead/list.txt
  [✓] Status: Retrieval successful
  [i] Received 20 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.risk/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2567 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/fademind-add.spam/list.txt
  [✓] Status: Retrieval successful
  [i] Received 73 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/kadhosts/list.txt
  [✓] Status: Retrieval successful
  [i] Received 13082 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomainlist.com/list.txt
  [✓] Status: Retrieval successful
  [i] Received 1104 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomains.com-immortaldomains/list.txt
  [✓] Status: Retrieval successful
  [i] Received 3203 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/malwaredomains.com-justdomains/list.txt
  [✓] Status: Retrieval successful
  [i] Received 26858 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/matomo.org-spammers/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2033 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/mitchellkrogza-badd-boyz-hosts/list.txt
  [✓] Status: Retrieval successful
  [i] Received 842 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/pgl.yoyo.org/list.txt
  [✓] Status: Retrieval successful
  [i] Received 3546 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/ransomwaretracker.abuse.ch/list.txt
  [✓] Status: Retrieval successful
  [i] Received empty file: using previously cached list

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/someonewhocares.org/list.txt
  [✓] Status: Retrieval successful
  [i] Received 14507 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/spam404.com/list.txt
  [✓] Status: Retrieval successful
  [i] Received 8189 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/stevenblack/list.txt
  [✓] Status: Retrieval successful
  [i] Received 2924 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/winhelp2002.mvps.org/list.txt
  [✓] Status: Retrieval successful
  [i] Received 9513 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/zerodot1-coinblockerlists-browser/list.txt
  [✓] Status: Retrieval successful
  [i] Received 3595 domains

  [i] Target: https://raw.githubusercontent.com/hectorm/hmirror/master/data/zeustracker.abuse.ch/list.txt
  [✓] Status: Retrieval successful
  [i] Received empty file: using previously cached list

  [i] Target: https://raw.githubusercontent.com/CHEF-KOCH/Audio-fingerprint-pages/master/AudioFp.txt
  [✗] Status: Not found
  [✗] List download failed: using previously cached list
  [i] Received 371 domains

  [i] Target: https://raw.githubusercontent.com/CHEF-KOCH/Canvas-fingerprinting-pages/master/Canvas.txt
  [✗] Status: Not found
  [✗] List download failed: using previously cached list
  [i] Received 14333 domains

  [i] Target: https://raw.githubusercontent.com/CHEF-KOCH/WebRTC-tracking/master/WebRTC.txt
  [✗] Status: Not found
  [✗] List download failed: using previously cached list
  [i] Received 807 domains

  [i] Target: https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt
  [✓] Status: Retrieval successful
  [i] Received 13427 domains

  [i] Target: https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt
  [✓] Status: Retrieval successful
  [i] Received 370 domains

  [i] Target: https://www.stopforumspam.com/downloads/toxic_domains_whole.txt
  [✓] Status: Retrieval successful
  [i] Received 14393 domains

  [i] Target: https://raw.githubusercontent.com/Akamaru/Pi-Hole-Lists/master/other.txt
  [✓] Status: Retrieval successful
  [i] Received 659 domains

  [i] Target: https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt
  [✓] Status: Retrieval successful
  [i] Received 367 domains

  [i] Target: https://raw.githubusercontent.com/Cauchon/NSABlocklist-pi-hole-edition/master/HOSTS%20(including%20excessive%20GOV%20URLs)
  [✓] Status: Retrieval successful
  [i] Received 8178 domains

  [i] Target: https://blocklist.site/app/dl/ransomware
  [✓] Status: Retrieval successful
  [i] Received 1903 domains

  [i] Target: https://blocklist.site/app/dl/tracking
  [✓] Status: Retrieval successful
  [i] Received 15057 domains

  [i] Target: https://blocklist.site/app/dl/spam
  [✗] Status: Not found
  [✗] List download failed: using previously cached list
  [i] Received 0 domains

  [i] Target: https://raw.githubusercontent.com/Firestorrrm/Minimal-Hosts-Blocker/master/iosadlist.txt
  [✓] Status: Retrieval successful
  [i] Received 30648 domains

  [i] Target: https://thepenguin.eu/download/tp-adblock.txt
  [✓] Status: Retrieval successful
  [i] Received 142 domains

  [i] Target: https://raw.githubusercontent.com/deathbybandaid/piholeparser/master/Subscribable-Lists/ParsedBlacklists/AdAway-Default-Blocklist.txt
  [✓] Status: Retrieval successful
  [i] Received 12566 domains

  [i] Target: https://adaway.org/hosts.txt
  [✓] Status: No changes detected
  [i] Received 7950 domains

  [i] Target: https://someonewhocares.org/hosts/hosts
  [✓] Status: Retrieval successful
  [i] Received 14525 domains

  [i] Target: https://mirror.cedia.org.ec/malwaredomains/justdomains
  [✓] Status: No changes detected
  [i] Received 26854 domains

  [i] Target: https://mirror.cedia.org.ec/malwaredomains/immortal_domains.txt
  [✓] Status: No changes detected
  [i] Received 3196 domains

  [i] Target: https://www.malwaredomainlist.com/hostslist/hosts.txt
  [✓] Status: No changes detected
  [i] Received 1104 domains

  [i] Target: http://winhelp2002.mvps.org/hosts.txt
  [✓] Status: No changes detected
  [i] Received 9513 domains

  [i] Target: https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=1&mimetype=plaintext
  [✓] Status: Retrieval successful
  [i] Received 3546 domains

  [i] Target: https://hostfiles.frogeye.fr/firstparty-only-trackers-hosts.txt
  [✓] Status: Retrieval successful
  [i] Received 13965 domains

  [i] Target: https://github.com/koff75/Pi-hole-rules-for-FR---US/blob/master/resultat_nextDNS.txt
  [✓] Status: Retrieval successful
  [i] Received 2 domains, 2 domains invalid!
      Sample of invalid domains:
      - content="github.com">
      - content="github.com">

  [i] Target: https://gitlab.com/ookangzheng/dbl-oisd-nl/raw/master/dbl.txt
  [✗] Status: https://gitlab.com/ookangzheng/dbl-oisd-nl/raw/master/dbl.txt (429)
  [✗] List download failed: using previously cached list
  [i] Received 1102680 domains

  [i] Target: https://raw.githubusercontent.com/koff75/Pi-hole-rules-for-FR---US/master/simple_tracking2.txt
  [✓] Status: Retrieval successful
  [i] Received 1239 domains

  [i] Target: https://raw.githubusercontent.com/Akamaru/Pi-Hole-Lists/master/mobile.txt
  [✓] Status: Retrieval successful
  [i] Received 734 domains

  [✓] Storing downloaded domains in new gravity database
  [✓] Building tree
  [✓] Swapping databases
  [i] Number of gravity domains: 1675493 (1222458 unique domains)
