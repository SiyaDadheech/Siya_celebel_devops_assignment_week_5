#Expose NodePort Service  
A NodePort allows you to access a service from outside the Kubernetes cluster by exposing it on a static port on each node's IP address.  
> vim node-port.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80       # Service port (internal)
      targetPort: 8080  # Pod port
      nodePort: 30036   # External port on node
> access it: http://<node-port-ip>:30036

# Expose ClusterIP Service
A ClusterIP is the default service type in Kubernetes and is used to expose services internally within the cluster only. It allows pods within the cluster to communicate with each other via a stable, internal IP address.  
> vim cluster-ip.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-clusterip-service
spec:
  type: ClusterIP
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
> access it: http://<ip>:8080

# Expose Load Balancer Service
A LoadBalancer service in Kubernetes exposes your application to the internet by provisioning an external IP address using a cloud provider’s load balancer (like AWS ELB, Azure Load Balancer, GCP, etc.).  
> vim lb-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
> access it: http://<ip>:8080
