# Storage Recovery Test

## Objective

Verify that application data stored on a PersistentVolume remains available after the application pod is deleted and recreated.

## Failure Introduced

The application pod using persistent storage was deleted.

## Command Used

Check the storage resources:
powershell
kubectl get pv
kubectl get pvc -n kuberesue
Verify the application pod:
kubectl get pods -n kuberesue
Write test data into the mounted volume:
kubectl exec -it <pod-name> -n kuberesue -- sh
Inside the container:
echo "Kubernetes storage recovery test" > /data/recovery-test.txt
cat /data/recovery-test.txt
Delete the pod:
kubectl delete pod <pod-name> -n kuberesue
Wait for the replacement:
kubectl get pods -n kuberesue -w
Verify the data:
kubectl exec -it <new-pod-name> -n kuberesue -- sh
cat /data/recovery-test.txt

## Expected Behavior

The pod should be recreated automatically.

The PersistentVolumeClaim should remain bound.

The data stored on the persistent volume should remain available after pod recreation.

## Actual Result

The original pod was deleted and Kubernetes created a replacement pod.

The PersistentVolumeClaim remained bound and the test data was available from the replacement pod.

Record the actual result observed during the test.

## Kubernetes Recovery Mechanism

The Deployment recreates the failed pod.

The PersistentVolumeClaim provides persistent storage independently of the pod lifecycle.

Because the data resides on persistent storage rather than the container filesystem, pod recreation does not remove the stored data.

## Conclusion

The storage recovery test demonstrated that application data persisted across pod recreation when using persistent storage correctly.
