##openvpn-install
OpenVPN [road warrior](http://en.wikipedia.org/wiki/Road_warrior_%28computing%29) installer for Debian, Ubuntu and CentOS.

This script will let you setup your own VPN server in no more than a minute, even if you haven't used OpenVPN before. It isn't bulletproof but has been designed to be as unobtrusive and universal as possible.

This version differs from Angristan's version in that it DOES write logs (for debugging and verifying), and is intended for personal use, only allowing up to 3 simultaneous clients. It also allows a weaker TLS cipher to support older iOS and android clients, although any client that supports it will prefer a better one with GCM.

##Fork
This fork includes :
- No comp-lzo [compression is a vector for oracle attacks, e.g. CRIME or BREACH](https://github.com/BetterCrypto/Applied-Crypto-Hardening/pull/91#issuecomment-75388575)
- Better encryption (see below)
- Avoid DNS leak
- UFW support
- TLS 1.2 only
- Strong ciphers, DH keys and certificates. (see variants)
- AES-256-CBC and SHA-512 for HMAC (instead of BF-128-CBC and SHA1)
- Run server in unprivileged mode, reducing risks to the system
- TLS-auth to help [thwart DoS attacks](https://openvpn.net/index.php/open-source/documentation/howto.html#security) and provide a 2nd line of defense to the TLS channel.
- [FDN's DNS Servers](http://www.fdn.fr/actions/dns/)
- Nearest [OpenNIC DNS Servers](https://www.opennicproject.org/)
- Up-to-date OpenVPN (2.3.11) thanks to [EPEL](http://fedoraproject.org/wiki/EPEL) and [swupdate.openvpn.net](https://community.openvpn.net/openvpn/wiki/OpenvpnSoftwareRepos)
- Support for either SNAT or MASQUERADE for forwarding
- Every feature of the [original script](https://github.com/Nyr/openvpn-install) (I check periodically to sync the latest commits from source)

## Variants

When you lauch the script you will be asked to choose a mode. Both will work the same way, but *slow* has higher encryption settings, so it may slow down your connection and take more time to install.

If you're just using your VPN at home, you may choose "fast". But if you're often using public Wi-Fi or traveling a lot, you choose use *slow*.

FYI, "fast" is still more secured than default OpenVPN settings.

### Slow (high encryption)
Features :
- 4096 bits RSA private key
- 4096 bits Diffie-Hellman key
- 256 bits AES-GCM
- SHA-384 RSA certificate

### Fast (lower encryption)
Features :
- 2048 bits RSA private key
- 2048 bits Diffie-Hellman key
- 128 bits AES-GCM
- SHA-256 RSA certificate

## Compatibility

The script is made to work on these OS :
- Debian 7
- Debian 8
- Ubuntu 12.04 LTS
- Ubuntu 14.04 LTS
- Ubuntu 15.10
- Ubuntu 16.04 LTS
- CentOS 6
- CentOS 7

Each one has been test by myself.

##Installation

Run the script and follow the assistant:

```
wget --no-check-certificate https://bit.ly/ovpn-install -O openvpn-install.sh
chmod +x openvpn-install.sh
./openvpn-install.sh
```

Once it ends, you can run it again to add more users, remove some of them or even completely uninstall OpenVPN.


You can get a cheap VPS for 2€/month at [PulseHeberg](https://bit.ly/pulse-vpn).

## Licence

Based on the work of [Nyr](https://github.com/Nyr/openvpn-install)

[MIT Licence](https://raw.githubusercontent.com/Angristan/openvpn-install-nyr/master/LICENSE)
