# How to Setup Prometheus in Minikube Kubernetes Environment?

# Welcome to Prometheus Setup!

Hi! This is a basic setup of the following using **Kubernetes YAML** files:
1. Prometheus.
2. Prometheus Alert Manager.
3. Nginx-Prometheus-Exporter

## Installation Instructions

1. Clone this repository.
2. Change directory (cd 'repo-dir' ) to the repository directory.
3. Create a namespace called 'prometheus' (or your choice)
4. Kubectl apply all the files in the directory.
5. Set the Minikube IP in the hosts file entry for the required DNS mappings.

## Installation Commands

    cd prometheus-repo
    minikube kubectl -- delete namespace prometheus  # if exists already.
    minikube kubectl -- create namespace prometheus 
    minikube kubectl -- apply -f . -n prometheus 
    minikube kubectl -- get all,cm,service,serviceaccount,ingress -n prometheus 

In the **C:\Windows\System32\drivers\etc\hosts** file, add the minikube ip address entry against the local DNS used in the YAML files.
    
    minikube ip

example:

    1.2.3.4	  prometheus.local  prometheus-alert.local  nginx.local

Then try the following URLs in the browser.
In Browser: http://prometheus.local  
In Browser: http://prometheus-alert.local   
curl http://prometheus-alert.local/api/v2/alerts  
In Browser: http://nginx.local/nginx_status  
In Browser: http://nginx.local:30113/metrics

---

### Troubleshooting in Powershell
to know the pod name of prometheus (in case of 1 replica count)

    set PRO_POD_NAME $(minikube kubectl -- get pods --namespace prometheus -l "app=prometheus" -o jsonpath="{.items[0].metadata.name}")  
    echo $PRO_POD_NAME  

***Describe:***

    minikube kubectl -- describe pod/$PRO_POD_NAME -n prometheus  
    example: minikube kubectl -- describe pod/prometheus-dbf56485c-j9bhp -n prometheus

Same way, for alert manager and nginx-prometheus-exporters.

    minikube kubectl --  describe pod/alertmanager-6f776b4474-fxcmw -n prometheus  
    minikube kubectl --  describe pod/nginx-prometheus-exporter-5876dd5844-mcv77 -n prometheus  


***Logs:***

    minikube kubectl -- logs prometheus-dbf56485c-ngrk5 -c prometheus -n prometheus  
    minikube kubectl -- logs alertmanager-579b4d67-5kbzv  -c alertmanager -n prometheus  
    minikube kubectl -- logs nginx-prometheus-exporter-5876dd5844-mcv77 -n prometheus  

***Scaling:***

    minikube kubectl -- scale deployment.apps/alertmanager --replicas=1 -n prometheus 


***Deleting:***

    minikube kubectl -- delete pod/nginx-prometheus-exporter-5876dd5844-mcv77 -n prometheus
