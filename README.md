Synopsis
========

Just an small example related with JWT implementation to secure an API made with Symfony4 using [lexik/LexikJWTAuthenticationBundle](https://github.com/lexik/LexikJWTAuthenticationBundle)

Requirements
============

- Apache >= 2.4
- PHP >= 7.1.13
- Composer (latest)
- Git (latest)

Instalation
===========

- Clone this repository
- From the command-line:

```
:~$ cd jwt-xample
:~$ composer install
:~$ bin/console doctrine:database:create
:~$ bin/console doctrine:schema:update --force
:~$ bin/console fos:user:create admin admin@example.com admin --super-admin
```

How to run it?
==============

You got two options:

1. [Configure an apache site for the project](docs/configure_jwtxample_site_in_apache.md)
2. From the command-line:

```
:~$ bin/console server:run
```

Troubleshooting
===============

## The directory "/jwt-xample/var/cache/dev/easy_admin" is not writable.

The `var` directory must be writable both by the web server and the command line user. In order to fix:

```
:~$ HTTPDUSER=$(ps axo user,comm | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1)
:~$ sudo setfacl -dR -m u:"$HTTPDUSER":rwX -m u:$(whoami):rwX var
:~$ sudo setfacl -R -m u:"$HTTPDUSER":rwX -m u:$(whoami):rwX var
```

Contributors
============

- Richard Melo [Twitter](https://twitter.com/allucardster), [Linkedin](https://www.linkedin.com/in/richardmelo)