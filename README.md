# Self-hosted media server with torrent

- qBittorrent with VPN kill switch
- Jackett - API Support for torrent trackers
- FlareSolverr - Proxy server to bypass Cloudflare protection
- Radarr - movie collection manager
- Sonarr - TV shows collection manager
- Bazarr - companion application to Sonarr and Radarr that manages and downloads subtitles

## Run:

- set env variables as described in `.env.example`

```
$ docker-compose up -d
```

## Issues:

### Cannot open TUN/TAP dev /dev/net/tun: No such file or directory

Check if you have the `tun` module installed:

```
$ lsmod | grep tun
```

If the result comes out empty, try installing it:

```
$ modprobe tun
```

If it exit with a failure error code, locate the module and use insmod with the returned path:

```
$ find /lib/modules/ -iname 'tun.ko.*'
/lib/modules/6.1.21-v8+/kernel/drivers/net/tun.ko.xz
$ insmod /lib/modules/6.1.21-v8+/kernel/drivers/net/tun.ko.xz
```

#### Test if the tun.ko module works

```
$ cat /dev/net/tun
```

If the result of the `cat` command was `File descriptor in bad state`, it means the module has been correctly installed.
