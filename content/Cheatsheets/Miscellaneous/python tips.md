### Run a upload server for exfiltration

> PIP : https://pypi.org/project/uploadserver/

You can access the upload form to : `http://<attacker ip>:<port>/upload`

```bash
root@ip-10-10-48-198:~/Desktop# python3 -m venv venv
root@ip-10-10-48-198:~/Desktop# source venv/bin/activate
(venv) root@ip-10-10-48-198:~/Desktop# pip install uploadserver
Collecting uploadserver
  Downloading https://files.pythonhosted.org/packages/67/29/6ca1699c4eefe7a2839cb3d99385fa7a0e7ef1628ecaa4839bdff58348bd/uploadserver-4.2.0-py3-none-any.whl
Installing collected packages: uploadserver
Successfully installed uploadserver-4.2.0
(venv) root@ip-10-10-48-198:~/Desktop# python -m uploadserver 8000
File upload available at /upload
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.248.242 - - [17/Mar/2023 21:17:21] "GET /upload HTTP/1.1" 200 -
10.10.248.242 - - [17/Mar/2023 21:17:41] "POST /upload/validateToken HTTP/1.1" 204 -
10.10.248.242 - - [17/Mar/2023 21:17:41] [Uploaded] "EncStageless.exe" --> /root/Desktop/EncStageless.exe
10.10.248.242 - - [17/Mar/2023 21:17:41] "POST /upload HTTP/1.1" 204 -
```

### Run a https server

let's set up a simple HTTPS server. First, we will need to create a self-signed certificate with the following command:
```shell-session
user@AttackBox$ openssl req -new -x509 -keyout localhost.pem -out localhost.pem -days 365 -nodes
```
You will be asked for some information, but feel free to press enter for any requested information, as we don't need the SSL certificate to be valid. Once we have an SSL certificate, we can spawn a simple HTTPS server using python3 with the following command:
```shell-session
user@AttackBox$ python3 -c "import http.server, ssl;server_address=('0.0.0.0',443);httpd=http.server.HTTPServer(server_address,http.server.SimpleHTTPRequestHandler);httpd.socket=ssl.wrap_socket(httpd.socket,server_side=True,certfile='localhost.pem',ssl_version=ssl.PROTOCOL_TLSv1_2);httpd.serve_forever()"
```