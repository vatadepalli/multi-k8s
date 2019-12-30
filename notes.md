# execute

    minikube start
    minikube status
    kubectl cluster-info


    kubectl apply -f client-pod.yaml
    kubectl apply -f client-node-port.yaml
    kubectl get pods
    kubectl get services

    minikube ip
    kubectl cluster-info

# access

    http://192.168.64.3:31515/

# change declaration

    <!-- update yaml file -->

# get pod/service information

    kubectl describe <object_type> <object_name>
    kubectl describe pod client-pod

# get rid of pod

    kubectl delete -f <config_file>
    kubectl get pods

# deployment

    kubectl apply -f client-deployment.yaml
    kubectl get pods
    kubectl get deployments
    minikube ip
    kubectl get pods -o wide
    kubectl describe pods

# refresh image

    kubectl set image <object_type>/<object_name> <container_name> = <new_image>

    kubectl set image deployment/client-deployment client=stephengrider/multi-client:v5

# reconfigure docker-cli

    <!-- Temporary Connection Only-->
    eval $(minikube docker-env)
    docker ps
    docker kill b8f5e140570a
    docker get pods

### stuff to with docker-cli reconfigured

    docker exec -it b8f5e140570a sh
        <!-- kubectl exec -it client-deployment-545b694544-qc5l5 sh -->

    docker logs b8f5e140570a
        <!-- kubectl get pods
        kubectl logs client-deployment-545b694544-qc5l5 -->

    docker system prune -a

# delete deployments

    kubectl get deployments
    kubectl delete deployment client-deployment

    kubectl get services
    kubectl delete service client-node-port

# ---------------------------------------------------------

# Group deployments

    kubectl apply -f k8s
    kubectl get pods
    kubectl get services

# Volumes

- Volumes are particular to a pod and can persist across pod restarts.
- But is lost when the pod is destroyed.

# Persistent Volume

- Outside a pod.
- Persists across pod destruction.

# Persistent Volume Claim

- Statically provisoned persistent volume
- Dynamically provisoned peristent volume

        kubectl get storageclass
        kubectl describe storageclass


        kubectl get pv
        kubectl get pvc

# Secret

    kubectl create secret generic <secret_name> --from-literal key=value
    kubectl create secret generic pgpassword --from-literal PGPASSWORD=12345asdf
    kubectl get secrets

# Load Balancer vs. Ingress

- Load balancer can only connect to one pod.
- Load balancer An old way of doing stuff.
- Load balancer creates cloud specific load balancer service.

## Ingress

- Nginx Ingress

        kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml

        minikube addons enable ingress

## Minikube Dashboard

    minikube dashboard
