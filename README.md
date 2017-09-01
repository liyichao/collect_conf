# Introduction

collector_conf Manages the configuration for metric collectors like collectd, telegraf, etc.

Metric collectors are good, but we have to configure which target to collect metric from, Let's
see an example.

We have many MySQL instances, say we use
[collectd's MySQL plugin](https://collectd.org/wiki/index.php/Plugin:MySQL) to collect their metrics, to
do that we have to configure MySQL instances' addresses. how to do that?

* you can deploy collectd on every MySQL host, and write your own plugin that discovers their addresses
locally by, maybe `ls /etc/mysql_conf_dir/`, and collect the metric yourself.  It is bad for these reasons:
  * You have to write a new MySQL plugin with the discovery feature, and for every collectd plugin, like redis, etc, you have to do the
same thing.
  * It is not very efficient. Every collect period, you have to discover MySQL instances, even if the MySQL instances list rarely
changes.
  * It is hard to be integrated with existing MySQL management system. For example, a PaaS may provide API to create/read/update/delete MySQL instances. The PaaS knows how many MySQL instances are there and which hosts are they in, then how does collector system use pass's information? By query PaaS for MySQL instances' addresses every time a collect period starts?

* Or, we can do it another way, offer a central configuration center, and generates collector (for example collectd) configuration from the central center, then notify collector to reload. To discover instances, first we provide an API for configuration center, and write discovery plugins to call the API to keep configuration center in sync with outside world.
