# Simple HTTP servers for file transfers

- Examples of how to set up simple HTTP servers with different languages / libaries
- Main use case is for 
   - HTML pages
   - file transfers
- Access via a browser with a format like `http://your.ip.address.or.hostname.here:8080` (e.g. `http://127.0.0.1:8080` / `http://localhost:8080` / `http://192.168.0.1:8080`)
   - Local access IP: `127.0.0.1` / `localhost`
   - Remote access IP:
      - Some servers will show the IP address in the output
      - If not shown use OS specific commands/features to find appropriate IPs (`ifconfig` / `ipconfig`)
      - For remote access, the server must be started on an accessible address (i.e. not `127.0.0.1` / `localhost`)
- Some may allow local development of the language but check for docs if it is possiible

## Python

- https://docs.python.org/3/library/http.server.html

### How to use
```
python3 -m http.server [--bind ADDRESS] [--directory DIRECTORY] [port]
python3 -m http.server --help
```

### Example Usage
```
python3 -m http.server
python3 -m http.server --directory /var/www 8080
```

### Example Output
- Serves on all IP addresses
```
Serving HTTP on :: port 8000 (http://[::]:8000/) ...
```


## Node
- https://github.com/http-party/http-server

### Installation
Installation optional when using `npx` (see exampel below)
```
npm install --global http-server
```

## How to use
```
npx http-server [path] [options] # No install method

http-server [path] [options]
http-server --help
```

### Example Usage
```
http-server
http-server /var/www -p 8080 -d true
```

### Example output
```
Starting up http-server, serving ./

http-server version: 14.0.0

http-server settings: 
CORS: disabled
Cache: 3600 seconds
Connection Timeout: 120 seconds
Directory Listings: visible
AutoIndex: visible
Serve GZIP Files: false
Serve Brotli Files: false
Default File Extension: none

Available on:
  http://127.0.0.1:8080
  http://192.168.1.1:8080
  http://10.1.2.3:8080
Hit CTRL-C to stop the server
```

## PHP
- https://www.php.net/manual/en/features.commandline.webserver.php
- Allows local PHP development

## How to use
```
php [options] -S <addr>:<port> [-t docroot] [router]
php -S
```

### Example Usage
```
php -S 0.0.0.0:8080    # this serves on all IP addresses
php -S localhost:8080  # only serve on localhost 
php -S localhost:8080 -t /var/www
php -S localhost:8080 -t /var/www router.php
```

### Example Output
```
[Sun Dec 12 08:54:23 2021] PHP 8.0.12 Development Server (http://localhost:8080) started
```