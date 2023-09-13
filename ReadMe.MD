# !!! WIP


### Why do we need a K8S Operator?

- Kubernetes' operator pattern concept lets you extend the cluster's behaviour without modifying the code of Kubernetes itself by linking controllers to one or more custom resources.(1*)

### Precondition
- Install Kubebuilder (2*)
- Kubernetes Cluster

### Creating Operator

1. Create an empty directory, i.e 'operator'

- ```mkdir operator```

2. Initialize a new project
- ```cd operator```
- ```kubebuilder init --domain dev.mehmetgrsl --repo=github.com/mehmetmgrsl/k8s-operator-work/operator```

3. Create an API
- ```kubebuilder create api --group core --version v1 --kind Pod```
  - Create Resource: y
  - Create Controller: y

4. Add the following code into "Reconcile" method of "pod_controller.go" file
```
	l := log.FromContext(ctx)

	pod := &corev1.Pod{}
	if err := r.Get(ctx, req.NamespacedName, pod); err != nil {
		return ctrl.Result{}, client.IgnoreNotFound(err)
	}

	l.Info("Pod", "Name", pod.Name, "Namespace", pod.Namespace)

	if pod.Namespace == "dev" {
		pod.Annotations = map[string]string{
			"dev-team/ingress": "true",
		}
	}

	if err := r.Update(ctx, pod); err != nil {
		return ctrl.Result{}, err
	}
```

### Test

1. Create a "dev" namespace

```kubectl create ns dev```

2. Create a pod in "dev" namespace

```kubectl run nginx --image=nginx ns dev```

3. Describe the pod and see the annotation that is added by custom controller:

```kubectl describe pod nginx ns dev``` :

Annotations:  dev-team/ingress: true


### Resources
1. https://kubernetes.io/docs/concepts/extend-kubernetes/operator/
2. https://book.kubebuilder.io/quick-start.html#installation
3. [Everything you need to know about Kubebuilder: Write operators like a pro - Cloud Native Skunkworks](https://www.youtube.com/watch?v=_XUJ1HoinWA&t=13s)
4. [Get on board with Kubernetes Operators - The Null Channel](https://www.youtube.com/watch?v=JNDjE9-2Bg4)