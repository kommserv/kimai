# Kimai

This Ansible role has been tested to install
[Kimai](https://www.kimai.org/) on an LXC container behind
an Apache reverse proxy.

This role was adapted from [Webarchitects Co-operative's Ansible role](https://git.coop/webarch/kimai/)
of the same name. 


## Apache vhost on the reverse proxy

```
<VirtualHost *:80>
   ServerAdmin {{ vhost_email }}
   ServerName {{ vhost_domain }}

   Redirect permanent / https://{{ vhost_domain }}/

   ErrorLog ${APACHE_LOG_DIR}/{{ vhost_domain }}_error.log
   CustomLog ${APACHE_LOG_DIR}/{{ vhost_domain }}_access.log combined
</VirtualHost>

<VirtualHost *:443>
   ServerAdmin {{ vhost_email }}
   ServerName {{ vhost_domain }}

   ProxyPreserveHost On
   RequestHeader add X-Forwarded-Proto https
   ProxyPass / http://{{ vhost_ip }}:80/
   ProxyPassReverse / http://{{ vhost_ip }}:80/

   SSLEngine on
   SSLCertificateKeyFile   /etc/letsencrypt/live/{{ vhost_domain }}/privkey.pem
   SSLCertificateFile      /etc/letsencrypt/live/{{ vhost_domain }}/cert.pem
   SSLCertificateChainFile /etc/letsencrypt/live/{{ vhost_domain }}/chain.pem
	
   ErrorLog ${APACHE_LOG_DIR}/{{ vhost_domain }}_error.log
   CustomLog ${APACHE_LOG_DIR}/{{ vhost_domain }}_access.log combined
</VirtualHost>
```
