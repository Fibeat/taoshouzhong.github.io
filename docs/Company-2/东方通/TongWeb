# Welcome to MkDocs

1.tongweb的httpserver的文件与nginx有一些区别
跟apache很像
在/software/TongWeb/tonghttpserver/THS/bin/https.conf文件
#HTTPS port:
Listen 8099

<VirtualHost *:8099>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "/software/TongWeb/tonghttpserver/THS/htdocs/workflow-front"
    ServerName localhost:8099
    <Directory "/software/TongWeb/tonghttpserver/THS/htdocs/workflow-front">
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    ProxyPass /api http://192.168.147.129:10800
    ProxyPassReverse /api http://192.168.147.129:10800
    ProxyPass  /deploy_api http://192.168.147.129:10801
    ProxyPassReverse /deploy_api http://192.168.147.129:10801
    ProxyPass /socket.io/pty/ http://192.168.147.129:10800/socket.io/pty
    ProxyPassReverse /socket.io/pty/ http://192.168.147.129:10800/socket.io/pty
    ProxyPass /socket.io/api/ http://192.168.147.129:10800/socket.io/api
    ProxyPassReverse /socket.io/api/ http://192.168.147.129:10800/socket.io/api
    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule ^/?(.*) "ws://192.168.147.129:10800/$1" [P,L]
    ProxyTimeout  50m
    ProxyPass /  !

</VirtualHost>


LogLevel warn

<IfModule log_config_module>
    LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%h %l %u %t \"%r\" %>s %b" common

    <IfModule logio_module>
        LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" %I %O" combinedio
    </IfModule>

    CustomLog "| /software/TongWeb/tonghttpserver/THS/bin/rotatelogs /software/TongWeb/tonghttpserver/THS/logs/access_log_%Y%m%d 86400 480" combined
</IfModule>






2.查看httpserver.conf
前期简单修改ServerRoot

#Running directory
#ServerRoot "/usr/local/tonghttpserver/THS"
ServerRoot "/software/TongWeb/tonghttpserver/THS"

#Execution user
<IfModule unixd_module>
User daemon
Group daemon
#KeepAlive on
#KeepAliveTimeout 1200
#MaxKeepAliveRequests 100
#ProxyTimeout 1200
#Timeout 1200
</IfModule>


#Server administrator
ServerAdmin you@example.com

#Server
ServerName 127.0.0.1:8084
#ServerName 127.0.0.1:9084

ServerName 127.0.0.1:15004
ServerName 127.0.0.1:15000

#Specify default page if access is a directory
<IfModule dir_module>
    DirectoryIndex index.html index.php
</IfModule>

#Prevent .htaccess and .htpasswd files from being accessed by clients
<Files ".ht*">
    Require all denied
</Files>

#header Set
<IfModule headers_module>
    RequestHeader unset Proxy early
</IfModule>

#json API
<Location /balancer/set>
SetHandler worker_set
Order Deny,Allow
#Deny from all
Allow from localhost
Allow From 192.168.1.0/24
</Location>
<Location /balancer/common>
SetHandler balancer_common
Order Deny,Allow
#Deny from all
Allow from localhost
Allow From 192.168.1.0/24
</Location>
 Security Settings
ServerSignature Off
ServerTokens Prod
Header always set X-Frame-Options sameorigin
Header always set X-XSS-Protection "1, mode=block"
Header always set Strict-Transport-Security "max-age=30, includeSubDomains"
Header always set Expect-CT "enforce, max-age=86400"
Header always set X-Content-Type-Options nosniff
TraceEnable off

#mime module
<IfModule mime_module>
    TypesConfig conf/mime.types
    AddType application/x-compress .Z
    AddType application/x-gzip .gz .tgz
        AddType application/x-httpd-php-source .phps
    AddType application/x-httpd-php .php
</IfModule>

#SSL module Support
Include bin/https.conf
<IfModule ssl_module>
SSLRandomSeed startup builtin
SSLRandomSeed connect builtin
</IfModule>

#Load php module
#<IfModule prefork.c>
#  LoadModule php7_module hmod/libphp7.so
#</IfModule>

<FilesMatch \.php$>
         SetHandler "proxy:fcgi://127.0.0.1:9000"
</FilesMatch>

# iphash
LoadModule lbmethod_iphash_module hmod/mod_lbmethod_iphash.so
LoadModule lbmethod_bydelay_module hmod/mod_lbmethod_bydelay.so
LoadModule lbmethod_byhost_module hmod/mod_lbmethod_byhost.so
LoadModule lbmethod_byminconn_module hmod/mod_lbmethod_byminconn.so
LoadModule lbmethod_byqueue_module hmod/mod_lbmethod_byqueue.so
LoadModule lbmethod_byuri_module hmod/mod_lbmethod_byuri.so
LoadModule lbmethod_byurl_module hmod/mod_lbmethod_byurl.so

# mod_bw
LoadModule bw_module hmod/mod_bw.so





