# PiHole/dnsmasq Statistics Search Add-On for Splunk

This is adapted from the TA-pihole add-on on splunkbase.splunk.com

This add-on uses data received by a Splunk Connect for Syslog (SC4S) container.

## Configure rsyslog

Create `/etc/rsyslog.d/pihole.conf` with the following contents:

```text
input(type="imfile"
      File="/var/log/pihole/pihole.log"
      Tag="pihole")
```

Create `/etc/rsyslog.d/pihole-ftl.conf` with the following contents:

```text
input(type="imfile"
      File="/var/log/pihole/FTL.log"
      Tag="pihole-ftl")
```

## Configure dnsmasq

Create `/etc/dnsmasq.d/99-pihole.conf` with the following entries:

```text
log-facility=DAEMON
log-queries=extra
```

## Ensure your syslog configuration is set up to forward to your syslog receiver.

I have PiHole running on a Raspberry Pi with rsyslog.
In my `/etc/rsyslog.conf` file, I added the following entry at the top of the `RULES` block.

```text
module(load="imfile" PollingInterval="10") # provide support for files
*.*                 @192.168.0.19:514
```

Where `192.168.0.19` is the IP of the SC4S host.
