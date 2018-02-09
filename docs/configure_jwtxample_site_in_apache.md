Configure "jwt-xample" site in Apache
====================================

- Add `jwtxample.loc` to /etc/hosts:

```
# /etc/hosts
0.0.0.0         jwtxample.loc
```

- Add a new site in apache and configure as following:

```
# /etc/apache2/sites-enabled/jwt-xample.conf
<VirtualHost *:80>
    <IfModule mod_rewrite.c>
        # Added this for Authorization for JWT
        RewriteEngine On
        RewriteCond %{HTTP:Authorization} ^(.*)
        RewriteRule .* - [e=HTTP_AUTHORIZATION:%1]
    </IfModule>

    ServerAdmin admin@example.com

    ServerName jwtxample.loc

    ServerAlias www.jwtxample.loc

    DocumentRoot /your/project/location/jwt-xample/public

    <Directory /your/project/location/jwt-xample/public>
        Options +FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
        <Limit GET POST PUT DELETE OPTIONS>
            Require all granted
        </Limit>
        <LimitExcept GET POST PUT DELETE OPTIONS>
            Require all denied
        </LimitExcept>
        <IfModule mod_rewrite.c>
            RewriteEngine On
            RewriteRule ^index.php - [L]
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteRule ^(.*)$ index.php [QSA,L]
        </IfModule>
    </Directory>
</VirtualHost>
```

- Restart apache server and in a browser open the following url:
```
http://jwtxample.loc
```
