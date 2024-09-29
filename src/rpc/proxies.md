# HTTP Proxies

HTTP proxies can be used to route traffic to the Kaspa p2p nodes. This is useful when you want to expose the p2p node to the public internet, but you don't want to expose the node directly. This can be done by using an HTTP proxy like NGINX or HAProxy.

Proxies also allow you to map multiple nodes to different subdomains or paths. This can be useful when you have multiple networks running on the same machine.

## NGINX

Here is an example of an NGINX configuration that routes traffic to different Kaspa p2p nodes based on the path:

```nginx

server {
        listen 80;
        listen [::]:80;
        
        # Replace example.com with your domain
        server_name *.example.com;

        client_max_body_size 1m;

        # Kaspa p2p node (kaspa-mainnet)
        location /kaspa/mainnet/wrpc/borsh {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:17110/;
        }

        # Kaspa p2p node (kaspa-mainnet)
        location /kaspa/mainnet/wrpc/json {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:18110/;
        }

        # Kaspa p2p node (kaspa-testnet-10)
        location /kaspa/testnet-10/wrpc/borsh {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:17210/;
        }

        # Kaspa p2p node (kaspa-testnet-10)
        location /kaspa/testnet-10/wrpc/json {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:18210/;
        }

        # Kaspa p2p node (kaspa-testnet-11)
        location /kaspa/testnet-11/wrpc/borsh {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:17310/;
        }

        # Kaspa p2p node (kaspa-testnet-11)
        location /kaspa/testnet-11/wrpc/json {
                proxy_http_version 1.1;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "Upgrade";
                proxy_pass http://127.0.0.1:18310/;
        }
}

```

#### Note on use of NGINX

The default NGINX configuration allows for 768 simultaneous connections per CPU core. If you need to increase this limit, you can do so by modifying the `worker_connections` directive in the `nginx.conf` file.

