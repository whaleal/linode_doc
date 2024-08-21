### Q：LKE 如何进入到每个Worker Node中

A：借助node-shell，安装步骤如下：

```bash
 curl -LO https://github.com/kvaps/kubectl-node-shell/raw/master/kubectl-node_shell
   chmod +x ./kubectl-node_shell
   sudo mv ./kubectl-node_shell /usr/local/bin/kubectl-node_shell
kubectl get nodes 

kubectl node-shell <node-name>
```



### Q：如何修改kubelet的配置，以支持配置 --allowed-unsafe-sysctls

A：暂时没有较好的方案，只能一个node一个node的进去修改kubelet配置

```bash
vim /var/lib/kubelet/config.yaml 

#在末尾追加
allowedUnsafeSysctls:
  - net.core.somaxconn
  - net.ipv4.tcp_max_syn_backlog

#然后重启kubelet服务即可， 这里即使重启服务导致断开与node的连接也没关系，也会重启成功
systemctl restart kubelet
```



### Q：LKE如何给一个节点池，打标签或污点

A：需要借助LKE的API去更新

```bash
curl -H "Content-Type: application/json" \
   -H "Authorization: Bearer ${api_token}" \
   -X PUT -d '{
       "taints": [
           {
               "key": "node",
               "value": "hpc",
               "effect": "NoSchedule"
           },
           {
               "key": "group",
               "value": "at5-adx",
               "effect": "NoSchedule"
           }
       ],
       "labels": {
           "node": "hpc",
           "group": "at5-adx"
       }
   }' https://api.linode.com/v4/lke/clusters/${clusterId}/pools/${poolId}
```

更新后，节点池中原有节点会都加上这些标签/污点，新加入的节点也会默认应用这些配置



### Q：LKE如何把节点与firewalls 关联起来

A：有以下两种方式：

方式一：手动关联，

方式二：借助lke-operator，这种方式可以监控到新加入的node，并且自动进行关联，具体实现步骤如下：

1. 创建命名空间

```bash
 kubectl create ns lke-firewalls
```

2. 创建对应operator

```bash
curl -s https://raw.githubusercontent.com/gangyi89/deploy-linode-operator/main/deploy-linode-fw-operator.sh | bash -s -- lke-firewalls
```

3. 根据防火墙id与api token创建配置文件(vim cluster-firewall.yaml)，firewallId 是防火墙ID，api-key是账号下的api-token

   要用自己的替换下面的这两个参数

```bash
apiVersion: firewall.operator.linode.io/v1alpha1
kind: ClusterFirewall
metadata:
  labels:
    app.kubernetes.io/name: linodeoperator
  name: clusterfirewall
spec:
  firewallId: 796279
  apiKeySecret:
    name: linode-api-key
    key: api-key
---
apiVersion: v1
kind: Secret
metadata:
  name: linode-api-key
type: Opaque
stringData:
  api-key: "bf29612a7407bf235b11eba3e11213cb4eaf380d3f9d096070ebfdbf37851dde"
```

4. 应用

```bash 
kubectl apply -f cluster-firewall.yaml -n lke-firewalls
```

5. 验证

```bash
kubectl describe clusterfirewall -n lke-firewalls
```



### Q： 集群是没法自行配置 pod 网段, 节点网段吗

A：暂时不支持

