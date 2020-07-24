## Keeping pods healthy
* One of the main benefits of using Kubernetes is the ability to give it a list of containers and let it keep those containers running somewhere in the cluster.
* You do this by creating a Pod resource and letting Kubernetes pick a worker node for it and run the pod’s containers on that node.
* But what if one of those containers dies? What if all containers of a pod die?
* As soon as a pod is scheduled to a node, the Kubelet on that node will run its containers and, from then on, keep them running as long as the pod exists.
* If the container’s main process crashes, the Kubelet will restart the container.
* If your application has a bug that causes it to crash every once in a while, Kubernetes will restart it automatically, so even without doing anything special in the app itself, running the app in Kubernetes automatically gives it the ability to heal itself.
* But sometimes apps stop working without their process crashing.
* For example, a Java app with a memory leak will start throwing OutOfMemoryErrors, but the JVM process will keep running.
* It would be great to have a way for an app to signal to Kubernetes that it’s no longer functioning properly and have Kubernetes restart it.
* We’ve said that a container that crashes is restarted automatically, so maybe you’re thinking you could catch these types of errors in the app and exit the process when they occur.
* You can certainly do that, but it still doesn’t solve all your problems.
* For example, what about those situations when your app stops responding because it falls into an infinite loop or a deadlock?
* To make sure applications are restarted in such cases, you must check an application’s health from the outside and not depend on the app doing it internally.


## Introducing ReplicationControllers
* A ReplicationController is a Kubernetes resource that ensures its pods are always kept running.
* If the pod disappears for any reason, such as in the event of a node disappearing from the cluster or because the pod was evicted from the node, the ReplicationController notices the missing pod and creates a replacement pod.
* Pod A was created directly and is therefore an unmanaged pod, while pod B is managed by a ReplicationController.
* After the node fails, the ReplicationController creates a new pod (pod B2) to replace the missing pod B, whereas pod A is lost completely nothing will ever recreate it.
* The ReplicationController in the figure manages only a single pod, but Replication Controllers, in general, are meant to create and manage multiple copies (replicas) of a pod.


## Using ReplicaSets instead of ReplicationControllers
* Initially, ReplicationControllers were the only Kubernetes component for replicating pods and rescheduling them when nodes failed.
* Later, a similar resource called a ReplicaSet was introduced.
* It’s a new generation of ReplicationController and replaces it completely (ReplicationControllers will eventually be deprecated).



## Running exactly one pod on each node with DaemonSets
* Both ReplicationControllers and ReplicaSets are used for running a specific number of pods deployed anywhere in the Kubernetes cluster.
* But certain cases exist when you want a pod to run on each and every node in the cluster.
* Those cases include infrastructure-related pods that perform system-level operations.
* For example, you’ll want to run a log collector and a resource monitor on every node.
* Another good example is Kubernetes’ own kube-proxy process, which needs to run on all nodes to make services work.
* DaemonSets run only a single pod replica on each node, whereas ReplicaSets scatter them around the whole cluster randomly.
* Outside of Kubernetes, such processes would usually be started through system init scripts or the systemd daemon during node boot up.
* On Kubernetes nodes, you can still use systemd to run your system processes, but then you can’t take advantage of all the features Kubernetes provides.


## Running pods that perform a single completable task
* Up to now, we’ve only talked about pods than need to run continuously.
* You’ll have cases where you only want to run a task that terminates after completing its work.
* ReplicationControllers, ReplicaSets, and DaemonSets run continuous tasks that are never considered completed.
* Processes in such pods are restarted when they exit.
* But in a completable task, after its process terminates, it should not be restarted again.


## Scheduling Jobs to run periodically or once in the future
* Job resources run their pods immediately when you create the Job resource.
* But many batch jobs need to be run at a specific time in the future or repeatedly in the specified interval.
* In Linux- and UNIX-like operating systems, these jobs are better known as cron jobs.
* Kubernetes supports them, too.
* A cron job in Kubernetes is configured by creating a CronJob resource.
* The schedule for running the job is specified in the well-known cron format, so if you’re familiar with regular cron jobs, you’ll understand Kubernetes’ CronJobs in a matter of seconds.
* At the configured time, Kubernetes will create a Job resource according to the Job template configured in the CronJob object.
* When the Job resource is created, one or more pod replicas will be created and started according to the Job’s pod template.


## Summary
**You’ve now learned how to keep pods running and have them rescheduled in the event of node failures. You should now know that**
* You can specify a liveness probe to have Kubernetes restart your container as soon as it’s no longer healthy (where the app defines what’s considered healthy).
* Pods shouldn’t be created directly, because they will not be re-created if they’re deleted by mistake, if the node they’re running on fails, or if they’re evicted
from the node.
* ReplicationControllers always keep the desired number of pod replicas running.
* Scaling pods horizontally is as easy as changing the desired replica count on a Replication Controller.
* Pods aren’t owned by the Replication Controllers and can be moved between them if necessary.
* A Replication Controller creates new pods from a pod template. Changing the template has no effect on existing pods.
* Replication Controllers should be replaced with ReplicaSets and Deployments, which provide the same functionality, but with additional powerful features.
* Replication Controllers and ReplicaSets schedule pods to random cluster nodes, whereas DaemonSets make sure every node runs a single instance of a pod defined in the DaemonSet.
* Pods that perform a batch task should be created through a Kubernetes Job resource, not directly or through a ReplicationController or similar object.
* Jobs that need to run sometime in the future can be created through CronJob resources.
