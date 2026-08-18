# Scheduling Failure Test

## Objective

Verify how Kubernetes handles a pod that cannot initially be scheduled because the available nodes do not satisfy the pod's scheduling requirements.

## Failure Introduced

A deliberately unsatisfiable scheduling constraint was introduced.

For example, a pod was configured with a node selector for a label that does not exist:

yaml
nodeSelector:
  kuberesue-test-node: "true"


## Command Used

Apply the test workload:
kubectl apply -f scheduling-failure.yaml
Check the pod:
kubectl get pods -n kuberesue
Check scheduling events:
kubectl describe pod <pod-name> -n kuberesue
Check cluster nodes:
kubectl get nodes --show-labels
Correct the scheduling requirement or add the required node label.
Example:
kubectl label node <node-name> kuberesue-test-node=true
Then monitor:
kubectl get pods -n kuberesue -w

## Expected Behavior

The pod should initially remain in:

Pending

The scheduler should report that no suitable node satisfies the scheduling requirement.

After correcting the scheduling condition, the scheduler should place the pod on an eligible node.

## Actual Result

The pod initially remained unscheduled.

The pod events showed the scheduling reason.

After correcting the scheduling requirement, the pod was successfully scheduled and transitioned to `Running`.

Record the actual scheduling event observed.

## Kubernetes Recovery Mechanism

The Kubernetes scheduler continuously evaluates pending pods and available nodes.

When the scheduling requirements become satisfiable, the scheduler can assign the pod to an eligible node.

## Conclusion

The scheduling failure test demonstrated how Kubernetes identifies unschedulable workloads and successfully schedules them once their placement requirements are satisfied.
