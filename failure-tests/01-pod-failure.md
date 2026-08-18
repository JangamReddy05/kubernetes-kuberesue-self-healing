# Pod Failure Test

## Objective

Verify that Kubernetes automatically detects a failed pod and creates a replacement pod when the workload is managed by a Deployment.

## Failure Introduced

A running application pod was manually deleted to simulate an unexpected pod failure.

## Command Used

powershell commands
kubectl get pods -n kuberesue
kubectl delete pod <pod-name> -n kuberesue
kubectl get pods -n kuberesue -w

## Expected Behavior

The deleted pod should terminate and Kubernetes should create a replacement pod automatically.

The Deployment should continue maintaining the desired replica count.

## Actual Result

The pod was successfully deleted.

Kubernetes automatically created a replacement pod and the application returned to the desired state.

Record the actual pod names and status observed during the test.

Example:
kuberesue-app-xxxxx   Running
kuberesue-app-yyyyy   Running

## Kubernetes Recovery Mechanism

The Kubernetes Deployment controller continuously compares the desired state with the current state.

When the pod was deleted, the Deployment controller detected that the desired replica count was no longer satisfied and created a replacement pod.

## Evidence

Capture screenshots of:

1. Pods before deletion.
2. `kubectl delete pod` command.
3. New pod being created.
4. Final `kubectl get pods` showing the replacement pod in `Running` state.

## Conclusion

The Kubernetes Deployment successfully recovered from the simulated pod failure without manually recreating the workload.
