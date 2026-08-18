# Deployment Rollback Test

## Objective

Verify that Kubernetes Deployment revision history can be used to recover from a faulty application release.

## Failure Introduced

A new Deployment revision was introduced with an intentionally incorrect configuration.

For example:
yaml
image: nginx:invalid-version

## Command Used
Deploy the initial healthy version:
powershell
kubectl apply -f deployment-v1.yaml
kubectl rollout status deployment/kuberesue-app -n kuberesue
Deploy the faulty version:
kubectl apply -f deployment-v2-bad.yaml
Check rollout status:
kubectl rollout status deployment/kuberesue-app -n kuberesue
View rollout history:
kubectl rollout history deployment/kuberesue-app -n kuberesue
Rollback:
kubectl rollout undo deployment/kuberesue-app -n kuberesue
Verify:
kubectl rollout status deployment/kuberesue-app -n kuberesue

## Expected Behavior

The faulty release should fail to become healthy.

The previous known-good Deployment revision should remain available in the Deployment history.

After `rollout undo`, Kubernetes should restore the previous revision.

## Actual Result

The faulty revision was detected.

The Deployment was rolled back to the previous healthy revision.

Record the final status:
<actual-rollout-status>

## Kubernetes Recovery Mechanism

Kubernetes Deployments maintain revision history.

The `kubectl rollout undo` command changes the Deployment back to a previous revision.

## Conclusion

The Deployment rollback mechanism successfully restored the application to a known-good revision after a faulty release.
