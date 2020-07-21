# Kafka-Connect-UI Helm Chart
This helm chart creates a [Kafka-Connect-UI server](https://github.com/lensesio/kafka-connect-ui).

This is a web tool for Kafka Connect for setting up and managing connectors for multiple connect clusters.

## Prerequisites
* Kubernetes 1.8
* A running Kafka Installation
* A running Zookeeper Installation
* A running Kafka-Connect installation

## Chart Components
This chart will do the following:

* Create a Kafka-Connect-UI deployment
* Create a Service configured to connect to the available Kafka-Connect-UI pods on the configured
  client port.

## Installing the Chart
You can install the chart with the release name `kcui` as below.


```
$ kubectl get all -l app=kafka-connect-ui
NAME                          DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deploy/kcui-kafka-connect-ui   1         1         1            1           23m

NAME                                DESIRED   CURRENT   READY     AGE
rs/kcui-kafka-connect-ui-bcb4c994c   1         1         1         23m

NAME                                      READY     STATUS    RESTARTS   AGE
po/kcui-kafka-connect-ui-bcb4c994c-qjqbj   1/1       Running   1          23m
```

1. `deploy/kcui-kafka-connect-ui` is the Deployment created by this chart.
1. `rs/kcui-kafka-connect-ui-bcb4c994c` is the ReplicaSet created by this Chart's Deployment.
1. `po/kcui-kafka-connect-ui-bcb4c994c-qjqbj` is the Pod created by the ReplicaSet under this Chart's Deployment.

## Configuration
You can specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml kafka-connect-ui
```

> **Tip**: You can use the default [values.yaml](values.yaml)

### Parameters
The following table lists the configurable parameters of the KafkaConnectUI chart and their default values.

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `replicaCount` | The number of `KafkaConnectUI` Pods in the Deployment | `1` |
| `image.repository` | The `KafkaConnectUI` image repository | `landoop/kafka-connect-ui` |
| `image.tag` | The `KafkaConnectUI` image tag | `0.9.5` |
| `image.imagePullPolicy` | Image Pull Policy | `IfNotPresent` |
| `kafkaConnect.url` | URL to the kafka connect endpoint | `http://localhost` |
| `kafkaConnect.port` | Port for the kafka connect | `8083` |
| `kafkaConnect.proxy` | Whether to proxy Kafka Connect endpoint via the internal webserver | `false` |
| `kafkaConnect.allowGlobal` | Support for global compatibility level configuration support —i.e change the default compatibility level of your kafka connect | `false` |
| `kafkaConnect.allowTransitive` | Support for transitive compatibility levels (Kafka Connect version 3.1.1 or better) | `false` |
| `kafkaConnect.allowDeletion` | Support for Connector deletion (Kafka Connect version 3.3.0 or better) | `false` |
| `kafkaConnect.readOnlyMode` | Support for readonly mode (overwrites settings for global compatibility configuration and Connector deletion) | `false` |
| `service.type` | Type of the service | `LoadBalancer` |
| `service.port` | Port to use | `80` |
| `service.annotations` | Kubernetes service annotations | `{}` |
| `service.loadBalancerSourceRanges` | Limit load balancer source IPs to list of CIDRs (where available)) | None |
| `ingress.enabled` | Ingress rules. Disabled by default | `false` |
| `ingress.annotations` | Ingress annotations | `{}` |
| `ingress.path` | Ingress path | `/` |
| `ingress.hosts` | Ingress accepted hostnames | `[kafka-connect-ui.local]` |
| `ingress.tls` | Ingress TLS configuration | `/` |
| `nodeSelector` | Node labels for pod assignment | `{}` |
| `tolerations` | List of node taints to tolerate | `[]` |
| `affinity` | Node/pod affinities | `{}` |
| `resources` | CPU/Memory resource requests/limits | `{}` |
