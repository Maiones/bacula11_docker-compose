Bacula 11 server + postgres:11.13-stretch + baculum11 and bacula client in docker FROM alt:p10.
Server and bd released in docker-compose v.3
The server use:

network:
server	192.162.42.3/29
db	192.162.42.2/29

ports: 	9101 9102 9095 9096 5432

db mount in local directory /home/user/docker/data:/var/lib/postgresql/data

