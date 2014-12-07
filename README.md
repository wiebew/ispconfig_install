ispconfig_install
=================

Installation of ubuntu platform, dovecot, squirrelmail, nginx for ispconfig


Basically this script works on a cleanly installed  ssl enabled ubuntu 14.04 host that allows internet access to mail, ssh, http, https, 8080 and 8081 ports. An ansible script for preparing a server on Hetzner (my provider) can be found here: https://github.com/wiebew/hetzner-scripts 

__IMPORTANT__ It assumes you are using a __startssl__ provided free ssl key. It will pull root certificates from startssl.com to create a keyfile that nginx can use. See https://www.startssl.com/?app=42. 

In the folder roles/ispconfig/files you need to add
* `site.crt.startssl`, the public startssl key
* `site.key.crypted`, password protected private keyfile from startssl. The ansible script will prompt for a password

You need to copy the `hosts.example` to a `hosts` file and change the content to your needs
* `yourserverhere` the FQDN of your server e.g. `example.server.com`
* `ansible_ssh_user` the username for ssh, e.g. username `ubuntu` if you are using amazon.
* `mysql_root_password` the root password of the sqlserver that you want set
* `php_time_zone`, the timezone used by php, see http://php.net/manual/en/timezones.php

Install with:

`ansible-playbook -i hosts playbook.yml`
