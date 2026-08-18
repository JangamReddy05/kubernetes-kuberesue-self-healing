# Resource Stress Test

## Objective

Verify Kubernetes behavior when a workload consumes excessive CPU resources and determine whether resource limits and monitoring mechanisms respond as expected.

## Failure Introduced

CPU-intensive workload behavior was intentionally generated inside the application container.

## Command Used

Check current resources:
kubectl top pods -n kuberesue
Start CPU stress:
kubectl exec -it <pod-name> -n kuberesue -- sh


Example:
while true; do :; done
monitor the workload:
kubectl top pods -n kuberesue
Check the pod:
kubectl get pod <pod-name> -n kuberesue

## Expected Behavior

CPU consumption should increase during the stress test.

If CPU limits are configured, the container should be constrained by the configured resource limit.

Monitoring tools should show the increased CPU utilization.

## Actual Result

CPU utilization increased during the test.

Record the observed CPU usage:
<actual CPU usage>
Record whether the configured CPU limit was reached:
<actual observation>

## Kubernetes Recovery Mechanism

Kubernetes uses resource requests and limits to control workload resource allocation.

The kubelet and container runtime enforce configured container limits.

Monitoring systems such as Metrics Server, Prometheus, and Grafana can expose resource utilization and help identify resource pressure.

## Conclusion

The resource stress test demonstrated how Kubernetes resource controls and monitoring can be used to observe and manage excessive workload consumption.
