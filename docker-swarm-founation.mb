# Docker swarm foundation

## Docker swarm init and join
```
docker swarm init --advertise-addr ens224

#To add a worker to this swarm, run the following command:
docker swarm join --token SWMTKN-1-653dgd6sthm0yflf40erzcdl9c60thw0zw3jrx47h1vabura6s-0se8k7n6pr64fn7elae3u13bl 10.0.0.102:2377

 ```

## Docker swarm - deploy service
```
docker service create --detach=true --name nginx1 --publish 8080:80 --mount source=/etc/hostname,target=/usr/share/nginx/html/index.html,type=bind,ro nginx:1.12 #failed - unknwon flag: --detach
docker service create --name nginx1 --publish 8080:80 --mount source=/etc/hostname,target=/usr/share/nginx/html/index.html,type=bind,ro nginx:1.12 #succedd
docker service ls
docker service ps nginx1curl 
curl localhost:80

```

## Scale your service
```
docker service update --replicas=5 nginx1
```

## Apply rolling update
```
docker service update --image nginx:1.13 nginx1
```

## Reconcile problems with containers
```
docker service create --name nginx2 --replicas=5 --publish 81:80 --mount source=/etc/hostname,target=/usr/share/html/index.html,type=bind,ro nginx:1.12

# On node1, use the `watch` utility to watch the update frrom the output of the `docker service ps` command. Tip: `watch`is a Linux utility and might not be available on other operating systems.

watch -n 1 docker service ps nginx2

# Click node3 and enter the command to leave the swarm cluster:
docker swarm leave

tip: This is the typical way to leave the wararm, but you can also kill the node and the behavior will be the same.

# check service
docker service ps nginx2

```

