## 1. Introducing pods
* A pod is a co-located group of containers and represents the basic building block in Kubernetes.
* Instead of deploying containers individually, you always deploy and operate on a pod of containers.
* We’re not implying that a pod always includes more than one container—it’s common for pods to contain only a single container.
* The key thing about pods is that when a pod does contain multiple containers, all of them are always run on a single worker node—it never spans multiple worker nodes
* All containers of a pod run on the same node. A pod never spans two nodes.


## Creating pods from YAML or JSON descriptors
* Pods and other Kubernetes resources are usually created by posting a JSON or YAML manifest to the Kubernetes REST API endpoint.


## Organizing pods with labels
## Listing subsets of pods through label selectors
## Using labels and selectors to constrain pod scheduling
## Annotating pods
* In addition to labels, pods and other objects can also contain annotations.
* Annotations are also key-value pairs, so in essence, they’re similar to labels, but they aren’t meant to hold identifying information.
* They can’t be used to group objects the way labels can.
* While objects can be selected through label selectors, there’s no such thing as an annotation selector.
* On the other hand, annotations can hold much larger pieces of information and are primarily meant to be used by tools.
* Certain annotations are automatically added to objects by Kubernetes, but others are added by users manually.
* Annotations are also commonly used when introducing new features to Kubernetes.
* Usually, alpha and beta versions of new features don’t introduce any new fields to API objects.
* Annotations are used instead of fields, and then once the required API changes have become clear and been agreed upon by the Kubernetes developers, new fields are introduced and the related annotations deprecated.
* A great use of annotations is adding descriptions for each pod or other API object, so that everyone using the cluster can quickly look up information about each individual object.
* For example, an annotation used to specify the name of the person who created the object can make collaboration between everyone working on the cluster
much easier.


## Using namespaces to group resources
## Stopping and removing pods
* You’ve created a number of pods, which should all still be running.
* You have four pods running in the default namespace and one pod in custom-namespace.
* You’re going to stop all of them now, because you don’t need them anymore.




## Summary
* How to decide whether certain containers should be grouped together in a pod or not.
* Pods can run multiple processes and are similar to physical hosts in the noncontainer world.
* YAML or JSON descriptors can be written and used to create pods and then examined to see the specification of a pod and its current state.
* Labels and label selectors should be used to organize pods and easily perform operations on multiple pods at once.
* You can use node labels and selectors to schedule pods only to nodes that have certain features.
* Annotations allow attaching larger blobs of data to pods either by people or tools and libraries.
* Namespaces can be used to allow different teams to use the same cluster as
though they were using separate Kubernetes clusters.
* How to use the kubectl explain command to quickly look up the information on any Kubernetes resource.
