# nginx-proxy-docker
A simple docker-compose file that wraps jwilder/nginx-proxy for easy use.

## Installation & getting started

- Clone this project: `git clone git@github.com:mace015/nginx-proxy-docker.git`.
- Start the proxy: `docker-compose up`.
- If the applications you want to proxy run on their own docker network, make sure to add those networks to the `nginx-proxy` container: `docker network connect [network name here] nginx-proxy`.
- Now start any container you wish to be proxied with the `VIRTUAL_HOST` env var, for more information please refer to [this documentation](https://github.com/jwilder/nginx-proxy).

## Usage

#### Start the proxy:

`docker-compose up`

#### Start the proxy in daemon mode:

`docker-compose up -d`

#### Stop the proxy:

`docker-compose stop`

## FAQ

##### I get a 503 error.
Make sure your nginx-proxy container is connected to the same network as the container you try to proxy to, see the installation instructions for more information.

## Todo

- Add automatic Let's Encrypt certificate generation for production environments.
