# Kubernetes

## Basic Concepts

### Cluster

A collection of nodes + a master to manage them.

### Node

A virtual machine to run out containers.

### Pod

It is basically a node but it can run multiple containers.

### Development

Monitors a set of pods, it makes sure they stay running. (Kubernetes object intended to manage a set of pods)

### Service

easy-to-remember URL to access a running container. (does all the networking things).

### Config Files

Used to tell Kubernetes what pods, deployments and services we want to create. They are created as objects in YAML syntax.

### Networking

Any type of communication in any shape or form

## Basic Commands

| Syntax                                         | Description                                                                                                 |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Kubectl apply -f config_file                   | Runs a config file                                                                                          |
| Kubectl get pods                               | Gets all pods created                                                                                       |
| Kubectl exec -it pod_name cmd                  | Executes a command in a container in a running pod, like opening a shell in posts kubectl exec -it posts sh |
| Kubectl pod                                    |                                                                                                             |
| Kubectl describe pod                           |                                                                                                             |
| Kubectl get deployments                        |                                                                                                             |
| Run kubectl apply -f depl file_name            | Apply a development file                                                                                    |
| Kubectl rollout restart deployment [depl_name] | Update an image used in development                                                                         |

## Development in Kubernetes

### How to update an image used in development

There are 2 methods for this.

### 1rst Method

1. Make changes in your project code.
2. Rebuild the image with new image version
3. Update version of image in deploy config file
4. Run kubectl apply -f depl file_name

### Second Method

1. Use ‘latest’ tag in the pod spec section
2. Update your code
3. Build the image
4. Push the image to docker hub (docker push tag_name/file)
5. Run kubectl rollout restart deployment [depl_name]

## SERVICES

There are 4 different types. (3 watched in the course).

1. Cluster IP
2. Node Port
3. Load Balancer

### Node Port Service

Makes a pod accessible from outside the cluster (used for dev purposes) more for testing and stuff.

There are actually 3 ports:

| Node Port                                           | Port                                       | Target Port                                          |
| --------------------------------------------------- | ------------------------------------------ | ---------------------------------------------------- |
| Which goes to the node that is running the service. | Which goes to the service inside the node. | Which goes to the container running the image (pod). |

### Cluster IP Service

Communication between different pods inside of our cluster, only exposes words to other pods inside the cluster.

(At this point of the course, in our example app) our posts service makes a request to the event bus every time a post is created, that event bus takes that event and sends it back to posts and to every other service as well.
But they cannot reach out directly, each image (post or event bus) makes a request to the cluster IP service of each pod, which is the one that takes over all the networking.

> So, reminder, in this case the posts pod is going to make communication requests to the event bus through the cluster IP service,
> So, the posts pod needs to know the URL to that IP service (event-bus)

    Ex: http://exact_name_we_want_to_reach_out_to:corresponding_port

**LAST STEP**: Make a load balancer service to connect the app to all the cluster IP´s

### Load Balancer:

Same as NODE PORT but this is the right way to expose a pod to the outside world. It gets traffic into a single pod. Tells Kubernetes to reach out to its provider and provision a load balancer.

#### Ingress or Ingress Controllers

Pod with a set of routing rules to distribute traffic to other services

#### Use case of load balancer

> Your cluster is in the cloud (Azure, AWS, GC, whatever), so, to get traffic from the outside world to some pod in your cluster u need a config file for a Load Balancer Service, which is going to ask the cloud provider (Azure, AWS, GC, whatever) for a Load Balancer, which is going to handle that traffic from the outside world to an ingress controller to whatever pod u need, I mean, to whatever cluster IP u need.

### Important Notes

The biggest challenge in microservices is to handle data.
This data can be shared between different services in different ways.

The course is focused on Async communication specifically.
This type of communication uses an event bus, which takes every service's request as an event and returns some kind of response.
One big advantage of this type of communication is self-sufficiency. Iit makes sure that all services keep running as normally as they would even if one of them crashes.

**What Docker does in these situations is that it makes it easier to package up these services.
And Kubernetes, as painful as it is to set up, makes it really easy to deploy and scale these services.**
