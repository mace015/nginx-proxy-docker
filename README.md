# nginx-proxy-docker
A simple docker-compose file that wraps jwilder/nginx-proxy for easy use.

## Installation & getting started

- Clone this project: `git clone git@github.com:mace015/nginx-proxy-docker.git`.
- If the applications you want to proxy runs on their own docker network, make sure to add those networks to the `nginx-proxy` container (`docker network connect [network name here] nginx-proxy`) and add those networks to the docker-compose file you're using so the `nginx-proxy` container automatically connects to those networks the next time it starts, if not: remove the `example-network` references from the `docker-compose*.yml` file you're using (plain, letsencrypt or ssl).
- Start the proxy: `docker-compose up`.
- Now start any container you wish to be proxied with the `VIRTUAL_HOST` env var, for more information please refer to [this documentation](https://github.com/jwilder/nginx-proxy).

## Usage

#### Start the proxy:

`docker-compose up`

#### Start the proxy in daemon mode:

`docker-compose up -d`

#### Stop the proxy:

`docker-compose stop`

## SSL Support
To use SSL, place both the `.crt` and `.key` file for all domains you want to host in the `/certs` folder.
The files names must be the complete virtual host + `.crt` or `.key`, for example: for example.com we need `/certs/example.com.crt` and `/certs/example.com.key`.
Then start the nginx proxy with the following command: `docker-compose -f docker-compose-ssl.yml up -d`.

## Letsencrypt support (automated SSL)
To use Letsencrypt for automated SSL, all proxied containers must have these 3 variables set: `VIRTUAL_HOST, LETSENCRYPT_HOST and LETSENCRYPT_EMAIL`.
Both the virtual host and the letsencrypt host must match and must be publicly reachable.
Then start the nginx proxy with the following command: `docker-compose -f docker-compose-letsencrypt.yml up -d`.

## Custom configuration
To set any custom nginx configuration, add your custom configuration to `custom_nginx_config.conf` and restart the container.

## FAQ

##### I get a 503 error.
Make sure your nginx-proxy container is connected to the same network as the container you try to proxy to, see the installation instructions for more information.

##### When using SSL or Letsencrypt the proxy refuses connections on port 443/HTTPS.
This is due to [this issue](https://github.com/jwilder/nginx-proxy/issues/317), to remedy this, remove the nginx-proxy container (`docker rm nginx-proxy`) and restart the proxy.
