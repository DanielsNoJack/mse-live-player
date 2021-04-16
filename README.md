# mse-live-player

Fork version from original kevinGodell

1. Removed the need to recode video to mjpeg, because of too much CPU used on small pltaform such as Odroid or Raspberry

If you don't define pipe:4 for mjpeg transcode CPU load will decline rapidly from 14 to 0.5
Only feature you lost is posibbility of making snapshots

2. Added posibility to set different ws url

If you want to integrate player into website on differen url
Especially for vpn access.

For example:

```
# Main web server:

server {
   listen 443;
   server_name www.adamassistant.com;
   ...
}
# One of VPN proxy server with mse-live-player server part on port 8080:

server {
   listen 443;
   server_name 7f54b664522d.adamassistant.com;

   location /socket.io {
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $host;
      proxy_pass http://10.8.1.71:8080/socket.io;
      proxy_bind 10.8.0.1;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
   }

   location / {
        proxy_buffers 16 4k;
        proxy_buffer_size 2k;
        proxy_bind 10.8.0.1;
        proxy_pass http://10.8.1.71:8080;
    }
}

```

Then I use this video element on web page:

```
<video autoplay="" muted="" data-namespace="cam1" data-socket="wss://7f54b664522d.adamassistant.com" data-controls="startstop|fullscreen|cycle" class="mse-video"></video>

```

=========== INSTALL ================


install files with git

```
git clone https://github.com/kevinGodell/mse-live-player.git
```

move into directory

```
cd mse-live-player
```

install node module dependencies

```
npm install
```

start the example server

```
npm start
```

open compatible browser to localhost:8080



