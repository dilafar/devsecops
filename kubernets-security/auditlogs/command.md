### doc
    https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/
### in kube-adm kluster create a folder in /etc/kubernets
    mkdir audit

### edit kube-api-server config in /etc/kubernets/manifests/kube-apiserver.yml
## create hostpath volume
    volumes:
        - hostPath:
            path: /etc/kubernetes/audit
            type: DirectoryOrCreate
          name: auditing
    volumeMounts:
        - mountPaths: /etc/kubernetes/audit
          name: auditing

### create audit policy in audit folder , audit-policy.yaml

### configure audit policy in /etc/kubernets/manifests/kube-apiserver.yaml
      - --audit-policy-file=/etc/kubernetes/audit/audit-policy.yaml
      - --audit-log-path=/etc/kubernetes/audit/audit.log

### view audit logs with jq
    cat /etc/kubernetes/audit/audit.log | jq

### create new audit log
    kubectl create ns prod
    echo > audit.log
### restart kube-apiserver


