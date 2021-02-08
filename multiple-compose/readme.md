# Introduction

This sample starts traefik in front,

and 2 sample nginx websites as backend in a different docker-compose file.

From src: [hollo.me](https://hollo.me/devops/routing-to-multiple-docker-compose-development-setups-with-traefik.html)
, [traefik/stripprefix](https://doc.traefik.io/traefik/middlewares/stripprefix/)

# start

````
docker network create gateway
docker-compose -f gateway.docker-compose.yml up -d
docker-compose -f sites.docker-compose.yml up -d
````

Notice: don't start both in the same command line as traefik must be started first

# show me

- http://127.0.0.1:8001/dashboard - **traefik dashboard** with a
  stripprefix [middleware](http://127.0.0.1:8001/dashboard/#/http/middlewares) for site1

- http://localhost:8080/site1 - using `stripprefix` will show `wwwsite1/index.html` resource.
- http://localhost:8080/site2 - will show `wwwsite2/site2/index.html` resource.

# stop

````
docker-compose -f gateway.docker-compose.yml -f sites.docker-compose.yml down
````
