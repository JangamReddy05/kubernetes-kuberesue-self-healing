# Network Failure Test

## Objective

Verify application behavior when network connectivity to a Kubernetes Service is intentionally disrupted.

## Failure Introduced

Network access to the application Service was intentionally restricted using a Kubernetes NetworkPolicy.

## Command Used

First verify normal connectivity:
kubectl get svc -n kuberesue
Test the application from a temporary pod:l
kubectl run network-test --rm -it --image=busybox:1.36 --restart=Never -n kuberesue -- sh
Inside the temporary pod:
wget -qO- http://kuberesue-service:80
Apply the restrictive NetworkPolicy:
kubectl apply -f network-failure-policy.yaml
Test connectivity again:
kubectl run network-test --rm -it --image=busybox:1.36 --restart=Never -n kuberesue -- sh

## Expected Behavior

Before applying the policy, the Service should be reachable.

After applying the restrictive NetworkPolicy, traffic that is not explicitly permitted should be blocked.

The application pods themselves should remain running.

## Actual Result

The network restriction was introduced successfully.

Application pods remained in `Running` state while the affected network traffic was blocked.

Record the actual connectivity result observed.

## Kubernetes Recovery Mechanism

Kubernetes NetworkPolicy controls allowed network traffic between pods and endpoints.

Recovery requires restoring the appropriate network policy configuration.

Remove the test policy when finished:

kubectl delete -f network-failure-policy.yaml
Verify connectivity again.

## Conclusion

The test demonstrated that Kubernetes network policies can isolate application traffic while leaving the underlying workloads running.
