# !!! WIP


### Why do we need a K8S Operator?

- Kubernetes' operator pattern concept lets you extend the cluster's behaviour without modifying the code of Kubernetes itself by linking controllers to one or more custom resources.(1*)

### Precondition
- Install Kubebuilder (2*)

### Installation

1. Create an empty directory, i.e 'operator'

- ```mkdir operator```

2. Initialize a new project
- ```cd operator```
- ```kubebuilder init --domain dev.mehmetgrsl --repo=github.com/mehmetmgrsl/k8s-operator-work/operator```

3. Create an API
- ```kubebuilder create api --group injector --version v1 --kind Injector```



### Precondition




### Resources
1. https://kubernetes.io/docs/concepts/extend-kubernetes/operator/
2. https://book.kubebuilder.io/quick-start.html#installation
3. [Get on board with Kubernetes Operators - The Null Channel](https://www.youtube.com/watch?v=JNDjE9-2Bg4)