# Nifi chart

A helm chart for Nifi.
Includes zookeeper subchart.
Ready to roll.

_If my zookeeper chart is accepted into `helm/charts` I will apply to have this chart added also and remove the vendor folder._


## Installation

```bash
helm install . --namespace=nifi
```

Be prepared to wait a while - the election process in Nifi takes around 5 minutes.
You'll want to see:
```
nifi-1 nifi 2019-09-03 08:16:51,422 INFO [main] o.a.n.c.c.node.NodeClusterCoordinator This node is now connected to the cluster. Will no longer require election of DataFlow.
```

With logs afterwards containing:
```
nifi-1 nifi 2019-09-03 08:17:09,879 INFO [Process Cluster Protocol Request-4] o.a.n.c.p.impl.SocketProtocolListener Finished processing request 538bf832-9a5d-4f53-93c6-1f35047ca1f8 (type=HEARTBEAT, length=3566 bytes) from nifi-2:8080 in 4 millis
nifi-1 nifi 2019-09-03 08:17:11,734 INFO [Process Cluster Protocol Request-5] o.a.n.c.p.impl.SocketProtocolListener Finished processing request 6d12fcd6-99e1-4b30-a78b-a70e18e9183c (type=HEARTBEAT, length=3566 bytes) from nifi-1:8080 in 3 millis
nifi-1 nifi 2019-09-03 08:17:11,735 INFO [Clustering Tasks Thread-1] o.a.n.c.c.ClusterProtocolHeartbeater Heartbeat created at 2019-09-03 08:17:11,727 and sent to nifi-1:2882 at 2019-09-03 08:17:11,735; send took 8 millis
```

## Configuration

Set a custom zookeeper subchart connection string

```yaml
zookeeper:
  nodeList: zk-0.zk-hs,zk-1.zk-hs,zk-2.zk-hs
  nodePort: 2888
```

### Specifying Values

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm upgrade --install --wait my-release \
    --set zookeeper.heapSize=512 \
    .
```
_For more information around subchart values look within vendor/zookeeper_
