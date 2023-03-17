## 1.k8s有几个组件?

k8s 宏观结构可分为两部分，控制面（master 节点）和工作节点（node）。其中关键组件如下：

控制面内的组件
- kube-api-server: 资源对象的唯一操作接口。其他组件都是通过它提供的 API 来操作数据源。它也是唯一一个与 etcd 通信的组件。
- kube-controller-manager: 负责执行各种控制器，通过控制器进行 control loop。
- kube-scheduler: 负责将 pod 调度到符合条件的 node 上。
- etcd: 分布式存储组件，用来存储整个集群包括 API 对象的状态。

工作节点内的组件
- kubelet: 控制容器，同步 pod 状态给 kube-api-server。
- kube-proxy: 为 service 创建 proxy 进程并监听相应的服务端口。根据 load banlancer 将外部请求分发到后端正确的容器上。

## 2.写下创建pod的yaml

一个容器模版为 nginx 的 pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

## 3.说下select有什么作用

select 会让当前 goroutine 阻塞，直到 case 列表中任一 case 可执行。它会执行这个 case。如果多个 case 都可以执行，它会随机选一个执行。
