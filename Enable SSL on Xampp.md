
# How to Enable SSL on Xampp with Vhosts

If you need to enable SSL on Xampp whilst stilling using vhosts, follow the next few steps. It assumes that you already have vhosts enabled.

Open xampp/apache/conf/extra/httpd-vhosts.conf Around line 19 you should see
```
NameVirtualHost *:80
```
below this line add
```
NameVirtualHost *:443
```
Then add a new vhost site just like a normal one but with 443 instead on 80 and the following lines:
```
SSLEngine on
SSLCertificateFile conf/ssl.crt/server.crt
SSLCertificateKeyFile conf/ssl.key/server.key
```
An example of this is:
```
<VirtualHost *:443>
    DocumentRoot "C:/xampp/htdocs/myproject/public"
    ServerName mysite.local
    ServerAlias mysite.local
	SSLEngine on
	SSLCertificateFile conf/ssl.crt/server.crt
	SSLCertificateKeyFile conf/ssl.key/server.key 
</VirtualHost>
```
Restart Xampp apache and everything should work fine.
