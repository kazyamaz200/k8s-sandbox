## Example02

public-dns & letsencrypt

### preps
- NODE01 => controlplane, etcd
- NODE02 => worker
- NODE03 => worker
- TCP => 53,80,443,2379,2380,4001,6443,10250,10254,10255,30000-32767
- UDP => 53

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
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns1 '{"host":"NODE01_IP"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns2 '{"host":"NODE02_IP"}'
$ etcdctl set /skydns/cf/kubernetes/dns/ns/ns3 '{"host":"NODE03_IP"}'
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
ns1.ns.dns.kubernetes.cf. IN A NODE01_IP
ns2.ns.dns.kubernetes.cf. IN A NODE02_IP
ns3.ns.dns.kubernetes.cf. IN A NODE03_IP
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
