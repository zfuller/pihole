# Pihole Rasberry Pi Role

Role installs and configures Pihole https://pi-hole.net/

Documents relating to pi-hole are at https://docs.pi-hole.net/

## Requirements
Raspberry Pi with Raspbian

## Role Variables
```yaml
pihole_repo: https://github.com/pi-hole/pi-hole.git
pihole_directory:

pihole_setupvars_PIHOLE_INTERFACE:
pihole_setupvars_IPV4_ADDRESS:
pihole_setupvars_IPV6_ADDRESS:
pihole_setupvars_QUERY_LOGGING:
pihole_setupvars_INSTALL_WEB_SERVER:
pihole_setupvars_INSTALL_WEB_INTERFACE:
pihole_setupvars_LIGHTTPD_ENABLED:
pihole_setupvars_WEBPASSWORD:
pihole_setupvars_BLOCKING_ENABLED:
pihole_setupvars_PIHOLE_DNS_1:
pihole_setupvars_PIHOLE_DNS_2:
pihole_setupvars_DNS_FQDN_REQUIRED:
pihole_setupvars_DNS_BOGUS_PRIV:
pihole_setupvars_DNSSEC:
pihole_setupvars_CONDITIONAL_FORWARDING:
pihole_setupvars_CONDITIONAL_FORWARDING_IP:
pihole_setupvars_CONDITIONAL_FORWARDING_DOMAIN:
pihole_setupvars_CONDITIONAL_FORWARDING_REVERSE:
pihole_setupvars_DNSMASQ_LISTENING:
```

### DNS
Alternative DNS Providers
```yaml
Google:
  - 8.8.8.8
  - 8.8.4.4
OpenDNS:
  - 208.67.222.222
  - 208.67.220.220
Level3:
  - 4.2.2.1
  - 4.2.2.2
Comodo:
  - 8.26.56.26
  - 8.20.247.20
Cloudflare:
  - 1.1.1.1
  - 1.0.0.1
```

### Required Variables
#### pihole_setupvars_WEBPASSWORD
You will need to generate a admin password for the `pihole_setupvars_WEBPASSWORD` variable, password is hashed with sha256 twice. You can genearte a password with the following shell command.

With the password in a file (reccomended).
```shell
echo -n $(cat ~/piholepass.word) | sha256sum | awk '{printf "%s", $1}' | sha256sum
```

With the password in shell command (not reccomended)
```shell
echo -n notsosecretpassword | sha256sum | awk '{printf "%s", $1}' | sha256sum
```

Reccomended to store this variable in ansible vault.

#### pihole_setupvars_IPV4_ADDRESS
IPv4 adress of the pihole

#### pihole_setupvars_PIHOLE_DNS_1/2
DNS servers you want the pihole to use
