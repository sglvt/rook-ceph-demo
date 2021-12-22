# Add Helm repo and save values file 

```
helm repo add rook-release https://charts.rook.io/release
helm search repo rook-ceph
export ROOK_CHART_VERSION='v1.8.1'
helm show values rook-release/rook-ceph --version ${ROOK_CHART_VERSION} > values.yaml.orig
cp values.yaml.orig values.yaml
```

# Install chart using default values
Installing the chart
```
helm install \
  --create-namespace -n rook-ceph \
  rook-ceph \
  rook-release/rook-ceph \
  --version ${ROOK_CHART_VERSION} \
  -f values.yaml
```

will result in the following output
```
The Rook Operator has been installed. Check its status by running:
  kubectl --namespace rook-ceph get pods -l "app=rook-ceph-operator"

Visit https://rook.io/docs/rook/latest for instructions on how to create and configure Rook clusters

Important Notes:
- You must customize the 'CephCluster' resource in the sample manifests for your cluster.
- Each CephCluster must be deployed to its own namespace, the samples use `rook-ceph` for the namespace.
- The sample manifests assume you also installed the rook-ceph operator in the `rook-ceph` namespace.
- The helm chart includes all the RBAC required to create a CephCluster CRD in the same namespace.
- Any disk devices you add to the cluster in the 'CephCluster' must be empty (no filesystem and no partitions).
```



# Reference
https://rook.io/docs/rook/v1.8/helm-operator.html
