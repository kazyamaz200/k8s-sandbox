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
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns1 '{"host":"NODE_IP01"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns2 '{"host":"NODE_IP02"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns3 '{"host":"NODE_IP03"}'
```

5. modify domain settings

nameservers
```
ns1.ns.dns.kubernetes.cf
ns2.ns.dns.kubernetes.cf
ns3.ns.dns.kubernetes.cf
```

gluerecords
```
ns1.ns.dns.kubernetes.cf. IN A NODE_IP01
ns2.ns.dns.kubernetes.cf. IN A NODE_IP02
ns3.ns.dns.kubernetes.cf. IN A NODE_IP03
```

6. deploy external-dns
```
kubectl apply -f external-dns.yaml
```

7. deploy cert-manager
```
kubectl apply -f cert-manager.yaml
```

8. get certificate
```
kubectl apply -f cert-manager-acme.yaml
```

9. deploay nginx
```
kubectl apply -f example-nginx.yaml
```
