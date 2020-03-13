# mod_pascal

Apache 2.4 module implementation which execute Pascal program.

## Requirement

- [Free Pascal compiler](https://www.freepascal.org)
- [Apache 2.4](https://httpd.apache.org/docs/2.4/)

## Setup

- Clone this repository

```
$ git clone https://github.com/zamronypj/mod_pascal.git
```

- Compile mod_pascal

```
$ fpc mod_pascal
```

- Add Apache configuration to load module

For example in Debian,

Create `pascal.conf` file in `/etc/apache2/mods-available` directory with content as follows,

```
<IfModule pascal_module>
    # handle all files having .pas extension
    SetHandler pascal_module .pas
</IfModule>
```

Create `pascal.load` file in `/etc/apache2/mods-available` directory with content as follows,

```
LoadModule pascal_module /path/to/libmod_pascal.so
```

Create symlink to `pascal.conf` and `pascal.load` in `/etc/apache2/mods-enabled` directory

```
$ cd /etc/apache2/mods-enabled
$ sudo ln -s /etc/apache2/mods-available/pascal.conf
$ sudo ln -s /etc/apache2/mods-available/pascal.load
```

- Reload Apache

```
$ sudo systemctl reload apache2
```

## Execute Pascal program

Create Pascal program, for example  `/var/www/test.pas` as follows,

```
begin
    writeln('Hello from Pascal');
end.
```

Open URL http://localhost/test.pas from Internet browser.