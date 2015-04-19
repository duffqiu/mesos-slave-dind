# mesos-slave-dind
the docker file for mesos slave based on centos7 which will use its own docker in container

### start a slave in coreos's docker

- docker command
```
docker run -d --name=mesos-slave  --privileged -p 5051:5051 duffqiu/mesos-slave-dind --route=<your os host route addr> --containerizers=docker --work_dir=/var/lib/mesos/slave --master=zk://<zk ip>:<zk port>/mesos --hostname=<slave's name>
```
- note: you must need to set the static route addr at the first parameter, otherwise you can't connect to the zookeeper which also in the same docker
- note: other parameters are the mesos slave's parameters. you can specify more parameters
- note: must use --privileged to run the container
- note: if run mutiple slave in the same docker, need to change the port's mapping
- note: don't use the `--ip` parameter because it is set by the script auto

### example:

```
docker run -d --name=mesos-slave  --privileged -p 5051:5051 duffqiu/mesos-slave-dind --route=10.0.2.0/24 --containerizers=docker --work_dir=/var/lib/mesos/slave --master=zk://10.0.2.15:2181/mesos --hostname=10.0.2.15
```

### docker in docker challenge
- need to do the network design.
