# Multi-Cluster Kustomize Example

This example will deploy a GO-application using kustomize. 
The app will be deployed into the `go-app` namespace.

The application will be customized as follows per environment:

* hp-server cluster: Using the AMD64 architecture image.
* raspberry-pi cluster: Using the ARM64 architecture image.

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: go-app-multi-cluster
  namespace: fleet-default
spec:
  branch: main
  repo: https://git.fullstaq.com/nico-public/rancher/fleet/multi-cluster.git
  paths:
  - multi-cluster
  
  targets:
  - name: hp-server
    clusterSelector:
      matchLabels:
        name: hp-server
        
  - name: raspberry-pi
    clusterName: raspberry-pi
```