---
layout: default
title:  "a simple web server"
date:   2018-02-02 20:37:38 -0700
categories: www
---

It is as easy as saying,
computer,
start an web server
with CGI

```
python -m http.server 9999 -b 127.0.0.1 --cgi
```

PS
Tested on 3.5
for 2.7
```
#!/usr/bin/python
# start a web server and show current location
#


import os, sys;
from BaseHTTPServer import HTTPServer;
from CGIHTTPServer import CGIHTTPRequestHandler;

server_address =  ("", 9999);
server = HTTPServer(server_address,  CGIHTTPRequestHandler);
server.serve_forever()
```
