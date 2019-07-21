# Docker Orchestration
>Docker swarm is a very powerful configuration management tool which ensure that the the container is always up and running using master and slave node.

- Use the below script to create a master node:
swarm init --advertise-addr <192.168.0.38>
- This will generate a slave link which on running on the slave node(independent container) will join the master cluster.
- We can have any number of slave nodes and master nodes.
- The instruction will always go through the master node and the master node assign the task to the slave nodes.
- The master node takes care of load balancing, replicaiton, monitoring, etc.
- The docker compose is use to configure the load balancing of the container replication via master slave technique.
- create a docker compose file(we can configire multiple services and can scale up/down via services using compose script) which can be either written in .yml or .json. Here we are using json based file.
- Script to create a compose file(compose-file.json) to run jenkins:

{
	"version": "3",
	"services": {
		"jenkins": {
			"image": "jenkins/jenkins",
			"deploy": {
				"replicas": 10
			},
			"ports": [
				"8080:8080",
				"50000:50000"
			]
		}
	}
}

- use the below script to run the compose script:
-- docker stack deploy -c docker-compose.json jenkins(any stake name)

- Use the below script to check the container and the stack status:
-- docker service ls
-- docker stack ls

> Note: Even  though we forcefully remove any container from master/slave node, the master node will immediately bring up the new container to meet the replication factor.

# Documentiotion:
 - [Docker](https://docs.docker.com/)
 - [Docker Swarm](https://docs.docker.com/engine/swarm/)
 - [Jenkins](https://jenkins.io/doc/tutorials/)
 
 Note: Please go through the Documentation for practical usage.




