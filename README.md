Pound
=====

This Ansible role enables users to install and configure the pound reverse proxy, load balancer and HTTPS front-end for Web server(s)

Updated to include the build from source tasks

Changelog:

 - build from source
 - get from apsis.ch or if that fails get from https://github.com/goochjj/pound/tree/upstream/branch/v2.7
 - create DH Params (although) not used as compiled with --with-dh=2048 in any case

 ToDo:
  - consider if we need to set --with-maxbuf=8192 (default = 4096)


Apsis - pgp = iEYEABECAAYFAlTGb7kACgkQq3LGKoaR3QJUxwCdFVEZszYnet9a2BWcwkFMzcbP
frsAn0x07+n1godgsT3UCLBx2Wlu09Eq
=nTJD

Requirements
------------

This role requires Ansible 1.4 or higher, and platform requirements are listed
in the metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows. See the Pound configuration documentation for details:


	pound_svc_name: pound

	# What level to log at
	pound_log_level: 1

	# What ip address should pound listen on?
	pound_listen_http_address: 127.0.0.1

	# What port should pound listen on?
	pound_listen_http_port: 80

	# What ip will pound be proxying traffic to?
	# - add more by adding additional items in the form ['ip', 'port']
	pound_backend_servers:
	  - [ '127.0.0.1', '8080' ]
	  - [ '192.168.100.100', '8080']

Pound and rewriting:
    rewriteloc: 0 - this is critical is you want host based rewrites in Apache to work!!!

Examples
--------

1) Install pound and set the default settings.

	- hosts: all
	  roles:
	    - role: pound

Notes:
#  Ciphers "-ALL:!SSLv1:!SSLv2:!CAMELLIA:!kEDH:TLSv1+HIGH:SSLv3+HIGH:!aNULL"
#  Ciphers "AES256+EECDH:AES256+EDH:!SSLv1:!SSLv2:!SSLv3"
#  Ciphers "ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA"

#  Ciphers "!EXPORT:TLSv1.1:TLSv1.2:TLSv1:!SSLv2:!MD5:!aNULL:!NULL:!RC4:RSA:ALL:!LOW"
#  Ciphers "ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5"


Dependencies
------------

To install Pound in RedHat derivatives you will need the EPEL repository.

License
-------

BSD

Author Information
------------------

curtis@serverascode.com

Thanks
------

This was based on the [NTP module](https://github.com/bennojoy/ntp).
ref:
Pound logging - https://blog.bandinelli.net/index.php?post/2013/10/16/Enregistrer-les-logs-de-Pound-avec-rsyslog-et-logrorate
