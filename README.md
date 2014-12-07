ispconfig_install
=================

Installation of ubuntu platform, dovecot, squirrelmail, nginx for ispconfig.

The content of this script is based on the excellent tutorial from Falko Timme on howtoforge: http://www.howtoforge.com/the-perfect-server-ubuntu-14.04-nginx-bind-mysql-php-postfix-dovecot-and-ispconfig3

I am using ispconfig for a number of years now, but I find I make too many errors with the manual entries needed to implement the howto. So I have automated the howto.

Basically this script works on a cleanly installed  SSH enabled ubuntu 14.04 host that allows internet access to mail, ssh, http, https, 8080 and 8081 ports. An ansible script for preparing a server on Hetzner (my provider) can be found here: https://github.com/wiebew/hetzner-scripts 

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

After the install the server will reboot. Once running again the 8080 and /webmail access should work.

Should phpmyadmin not work ssh to host and run `sudo dpkg-reconfigure phpmyadmin` and choose reinstall phpmyadmin database.