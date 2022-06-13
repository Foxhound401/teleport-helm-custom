### Configurint postgresql.conf

In order to allow remote access to postgres we need to find `postgresql.conf`. In different systems it is located at different place. I usually search for it.

`find / -name "postgresql.conf`


Open `postgresql.conf` file and replace line

```
listen_addresses = 'localhost'
```
with
```
listen_addresses = '*'
```
