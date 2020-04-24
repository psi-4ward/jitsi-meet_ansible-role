# Jitsi-Meet Ansible Role !WIP!

**For scaled setups: 1x jitsi-meet + n Videobridges**

Variables to be defined:
  * `jitsi_meet_domain`
  * `jitsi_jicofo_secret`
  * `jitsi_focus_secret`
  * `jitsi_jvb_secret`

Optional variables:
  * `jitsi_meet_domain_aliases`: Array of alternative server names
  * `jitsi_meet_turnservers`: Array of turnservers (coturn)
  * `coturn_secret`: For turnserver use

Depends on `jitsi` and `jvb` host-groups. See [task-includes](./tasks/main.yml#L68)

Konventions:
  * `jvb-1`.`meet.example.com`: Videobridge-Domains must be Subdomain of `jitsi_meet_domain` and match `jvb-[0-9]+`

Restarting jitsi: See [jitsi-restart.sh](./templates/utils/jitsi-restart.sh.j2).
Seems that order and timeouts are mandatory. 

## ACME.sh (optional, manual task)

```bash
acme.sh --issue -w /usr/share/jitsi-meet -d meet.example.conf

acme.sh \
  --install-cert -d meet.example.conf \
  --key-file /etc/jitsi/meet/meet.example.conf.key \
  --fullchain-file /etc/jitsi/meet/meet.example.conf.crt \
  --reloadcmd 'systemctl reload nginx'
```
