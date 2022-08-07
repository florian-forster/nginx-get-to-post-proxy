# nginx-get-to-post-proxy
NGINX proxy that sends get requests as posts to the upstream

Environment parameters:
 * `TARGET_SERVER`: The target server url to which the proxy sends the requests to to, e.g., `https://somehostname.com` or `http://<IP ADDRESS>`
 * HOST_SERVER: The host name that the proxy should send to the target server, so the correct virtual server is chosen, e.g., `somehostname.com`

Note: Proxy supports proxying to a `https` server, but can only accept `http` connections.

You can run several proxy server containers on the same host. Just make sure use different ports in the `-p` parameter.

Examples:

```
docker run --rm -d \
  -p 9080:80 \
  -e TARGET_SERVER=https://myhost.com \
  -e HOST_SERVER=myhost.com \
  nginx-get-to-post-proxy-image
```

=> `curl http://localhost:9080` proxies to `http://13.135.194.234`, setting the host name to `myhost`

```
docker run --rm -d \
  -p 9081:80 \
  -e TARGET_SERVER=http://13.135.194.234 \
  -e HOST_SERVER=myhost \
  nginx-get-to-post-proxy-image
```
