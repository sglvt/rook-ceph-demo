# Add Helm repo 

```
helm repo add rook-release https://charts.rook.io/release
helm search repo rook-ceph
export ROOK_CHART_VERSION='v1.8.1'
```

# ceph-operator
Save value file
```
pushd rook-ceph-operator
helm show values rook-release/rook-ceph --version ${ROOK_CHART_VERSION} > values.yaml.orig
cp values.yaml.orig values.yaml
popd
```

Installing the chart
```
helm install \
  --create-namespace -n rook-ceph \
  rook-ceph \
  rook-release/rook-ceph \
  --version ${ROOK_CHART_VERSION} \
  -f rook-ceph-operator/values.yaml
```

Important note: Any disk devices you add to the cluster in the 'CephCluster' must be empty (no filesystem and no partitions)

# ceph-cluster
```
pushd rook-ceph-cluster
helm show values rook-release/rook-ceph-cluster --version ${ROOK_CHART_VERSION} > values.yaml.orig
cp values.yaml.orig values.yaml
popd
```

Installing the chart
```
helm install \
  -n rook-ceph \
  rook-ceph-cluster \
  rook-release/rook-ceph-cluster \
  --version ${ROOK_CHART_VERSION} \
  -f rook-ceph-cluster/values.yaml
```


# Reference
https://rook.io/docs/rook/v1.8/helm-operator.html
https://rook.io/docs/rook/v1.8/helm-ceph-cluster.html