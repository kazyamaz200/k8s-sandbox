## Example02

public-dns & letsencrypt

### steps

1. deploy etcd-operator
```
kubectl apply -f etcd-operator.yaml
```

2. deploy etcd-cluster
```
kubectl apply -f etcd-cluster.yaml
```

3. deploy coredns
```
kubectl apply -f coredns.yaml
```

4. config nameservers
```
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns1 '{"host":"35.194.97.231"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns2 '{"host":"35.190.227.3"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns3 '{"host":"35.190.232.96"}'
```

5. deploy external-dns
```
kubectl apply -f external-dns.yaml
```

6. deploy cert-manager
```
kubectl apply -f cert-manager.yaml
```

7. get certificate
```
kubectl apply -f cert-manager-acme.yaml
```

8. deploay nginx
```
kubectl apply -f example-nginx.yaml
```
