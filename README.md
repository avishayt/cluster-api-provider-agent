# cluster-api-provider-agent
Kubernetes-native declarative infrastructure for agent based installation

cluster-api-provider-agent serves as infrastructure provider for [Kubernetes cluster-api](https://github.com/kubernetes-sigs/cluster-api)

## Deploying the cluster-api-provider-agent provider
In order for your clusterctl to be aware of this provider, you need to update the clusterctl config located at "$HOME/.cluster-api/clusterctl.yaml" with the following field:\
providers:\
  &nbsp; \- name: "agent" \
    &nbsp;&nbsp;&nbsp;&nbsp;url: "https://github.com/eranco74/cluster-api-provider-agent/releases/latest/infrastructure-components.yaml" \
    &nbsp;&nbsp;&nbsp;&nbsp;type: "InfrastructureProvider"\
After adding that field to the config, you should run "clusterctl init --infrastructure agent" to set up the provider.

## How to install cluster-api-provider-agent

cluster-api-provider-agent is deployed into an existing OpenShift / Kubernetes cluster.

**Prerequisites:**
* Admin access to the OpenShift / Kubernetes cluster specified by the KUBECONFIG environment variable

Build the cluster-api-provider-agent image and push it to a container image repository:
```shell
make docker-build docker-push IMG=<your docker repository>:`git log -1 --short`
```

Deploy cluster-api-provider-agent to your cluster:
```shell
make deploy IMG=<your docker repository>:`git log -1 --short`
```
