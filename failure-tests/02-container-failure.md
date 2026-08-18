# Container Failure Test

## Objective

Verify that Kubernetes detects a failed container and restarts it according to the pod's restart policy.

## Failure Introduced

A container failure was simulated by terminating the application process inside the container.

## Command Used

powershell commands
kubectl get pods -n kuberesue
kubectl get pod <pod-name> -n kuberesue
kubectl describe pod <pod-name> -n kuberesue
kubectl exec -it <pod-name> -n kuberesue -- sh

Inside the container:

kill 1

Then monitor the pod:

kubectl get pods -n kuberesue -w

Check restart information:

## Expected Behavior

The container should terminate.

Kubernetes should restart the container because the pod is managed with an appropriate restart policy.

The pod should eventually return to `Running`.

## Actual Result

The application container was terminated intentionally.

Kubernetes detected the container failure and restarted the container.

Record the observed restart count:

RESTARTS: <actual-value>

## Kubernetes Recovery Mechanism

The kubelet running on the Kubernetes node monitors containers.

When the application container terminates unexpectedly, the kubelet restarts the container according to the pod's restart policy.

## Conclusion

The Kubernetes kubelet successfully detected the container failure and restarted the failed container automatically.
