# pihole raspberry pi ansible role

Role installs and configures Pihole https://pi-hole.net/

Documents relating to pi-hole are at https://docs.pi-hole.net/

## Requirements
Raspberry Pi with Raspbian

## Role Variables
[defaults/main.yml](defaults/main.yml) for default values
```yaml
pihole_repo: https://github.com/pi-hole/pi-hole.git
pihole_directory:
pihole_branch:

pihole_setupvars_pihole_interface:
pihole_setupvars_ipv4_address:
pihole_setupvars_ipv6_address:
pihole_setupvars_query_logging:
pihole_setupvars_install_web_server:
pihole_setupvars_install_web_interface:
pihole_setupvars_lighttpd_enabled:
pihole_setupvars_webpassword:
pihole_setupvars_blocking_enabled:
pihole_setupvars_pihole_dns_1:
pihole_setupvars_pihole_dns_2:
pihole_setupvars_dns_fqdn_required:
pihole_setupvars_dns_bogus_priv:
pihole_setupvars_dnssec:
pihole_setupvars_conditional_forwarding:
pihole_setupvars_conditional_forwarding_ip:
pihole_setupvars_conditional_forwarding_domain:
pihole_setupvars_conditional_forwarding_reverse:
pihole_setupvars_dnsmasq_listening:
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
#### pihole_setupvars_webpassword
You will need to generate a admin password for the `pihole_setupvars_webpassword` variable, password is hashed with sha256 twice. You can genearte a password with the following shell command.

With the password in a file (reccomended).
```shell
echo -n $(cat ~/piholepass.word) | sha256sum | awk '{printf "%s", $1}' | sha256sum
```

With the password in shell command (not reccomended)
```shell
echo -n notsosecretpassword | sha256sum | awk '{printf "%s", $1}' | sha256sum
```

Reccomended to store this variable in ansible vault.

#### pihole_setupvars_ipv4_address
IPv4 adress of the pihole

#### pihole_setupvars_pihole_dns_1/2
DNS servers you want the pihole to use
