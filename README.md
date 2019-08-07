# Kubernates Playground

## Kubernates Installation

### CentOS 7
https://www.linuxtechi.com/install-kubernetes-1-7-centos7-rhel7/
```bash
yum install kubeadm docker -y
systemctl restart docker && systemctl enable docker
systemctl  restart kubelet && systemctl enable kubelet
kubeadm init --ignore-preflight-errors Swap
kubectl get nodes
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
export kubever=$(kubectl version | base64 | tr -d '\n')
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
```

## Kubernates Examples

### Kubernates Cassandra
https://kubernetes.io/docs/tutorials/stateful-application/cassandra/

```bash
# Create service to track all cassandra stateful nodes
kubectl apply -f ./cassandra/cassandra-service.yaml

# Validate
kubectl get svc cassandra

# Create stateful set
kubectl apply -f ./cassandra/cassandra-statefulset.yaml

# Validate
kubectl get statefulset cassandra
kubectl get pods -l="app=cassandra"

# Authenticate Cassandra cluster
kubectl exec -ti cassandra-0 -- nodetool status

```
