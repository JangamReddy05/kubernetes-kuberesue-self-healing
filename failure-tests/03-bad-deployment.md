# Bad Deployment Test

## Objective

Verify how Kubernetes handles an invalid Deployment configuration and demonstrate the difference between a failed rollout and a healthy application state.

## Failure Introduced

A deliberately incorrect Deployment configuration was applied.

The failure can be introduced using an invalid container image:

yaml
image: nginx:this-image-does-not-exist

## Command Used

powershell
kubectl apply -f bad-deployment.yaml
kubectl get pods -n kuberesue
kubectl describe pod <pod-name> -n kuberesue
kubectl get events -n kuberesue --sort-by=.lastTimestamp

## Expected Behavior

Kubernetes should create the pod, but the container should fail to start because the specified image does not exist.

The pod may enter a state such as:

ErrImagePull
or:
ImagePullBackOff

## Actual Result

The intentionally invalid image caused the workload to fail during image retrieval.

Record the exact status observed:
<actual-status>

## Kubernetes Recovery Mechanism

Kubernetes continuously retries the failed image pull using backoff behavior.

However, Kubernetes cannot successfully recover from an invalid image reference because the requested image itself does not exist.

The configuration must be corrected.

## Conclusion

This test demonstrates an important distinction in Kubernetes self-healing: Kubernetes can automatically restart failed workloads, but it cannot correct an invalid application configuration automatically.

Correct configuration is required for successful recovery.
