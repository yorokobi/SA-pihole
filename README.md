# PiHole/dnsmasq Statistics Search Add-On for Splunk

This is adapted from the TA-pihole add-on on splunkbase.splunk.com

This add-on uses data received by a Splunk Connect for Syslog (SC4S) container.

## Configure dnsmasq

Create `/etc/dnsmasq.d/99-pihole.conf` with the following entries:

```
log-facility=DAEMON
log-queries=extra
```

## Ensure your syslog configuration is set up to forward to your syslog receiver.

I have PiHole running on a Raspberry Pi with rsyslog. In my `/etc/rsyslog.conf` file, I added the following entry at the top of the `RULES` block.

```
*.*                 @192.168.0.19:514
```

Change `192.168.0.19` is the IP or hostname of your syslog (SC4S) receiver.
