# ensemble
Run books designed for Ops to follow in the event we see issues with our application stack.


1. Check Pod Logs:

    Use kubectl logs <pod-name> to view the logs of the crashing pod. 

Look for error messages, stack traces, or any other clues that might indicate the root cause of the crash. 
If the pod is in a CrashLoopBackOff state, the logs might contain information about why the container is failing to start or run. 

2. Analyze Pod Events:

    Use kubectl describe pod <pod-name> to inspect events and error messages related to the pod.
    Events can provide valuable insights into why the pod is crashing or failing to start. 

3. Check Resource Requirements:

    Ensure the pod has sufficient CPU and memory resources (requests and limits) to run correctly. 

If the pod is crashing due to resource exhaustion, increase the resource limits or requests. 
Use kubectl describe pod <pod-name> to view the resource requests and limits of the pod. 

4. Verify Liveness and Readiness Probes:

    Ensure liveness and readiness probes are correctly configured to avoid premature restarts.
    Incorrectly configured probes can cause the pod to restart unnecessarily.
    Review the probe configuration in the pod's YAML file. 

5. Check Init Containers:

    Ensure init containers complete successfully, as their failure can cause the main container to crash.
    Review the logs of init containers to identify any issues. 

6. Inspect Node Resource Utilization:

    If pods are crashing on a specific node, check the node's resource utilization (CPU, memory, disk).
    Overloaded nodes can cause pods to crash due to resource contention.
    Consider adding more nodes to the cluster or rescheduling pods to different nodes. 

7. Restart Pods:

    Sometimes, simply restarting the pod can resolve temporary issues.
    Use kubectl delete pod <pod-name> and then wait for Kubernetes to recreate the pod.
    If the issue persists after restarting, it indicates a deeper problem that needs to be addressed. 

8. Check for Network Issues:

    Ensure the pod can access the necessary services and resources.
    Check DNS resolution and network connectivity.
    Verify that the pod's network policies are not blocking traffic. 

9. Review Configuration:

    Double-check all references to resources (files, databases, external services) in the pod configuration.
    Ensure that the paths and endpoints are correct.
    Verify that the command-line arguments and environment variables are correctly set. 

10. Check for Kubelet Malfunction:

    If the kubelet on a node crashes, it can prevent pods from starting or running correctly.
    Monitor the kubelet logs for any errors or issues. 
