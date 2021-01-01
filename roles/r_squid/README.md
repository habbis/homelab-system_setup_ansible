# squid

Base configuration for a squid server.

Parameters that may be set:

- r_squid_disksize: the size, in megabytes, to allocate to a spool
  file systems for a permanent cache.  Defaults to 1024.

- r_squid_vg: the volume group for the above.  Defaults to 'vg0'.

- r_squid_http_port: the port to listen at.  Defaults to 8888.

The role creates a directory /etc/squid/conf.d, where customer
specific additional configuration should be placed.  Anything ending
in ".conf" will be included after the base config file has been read.
