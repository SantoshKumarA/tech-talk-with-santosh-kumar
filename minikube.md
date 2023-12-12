# To enable dashboard:

1. First enable required addons.
<code>minikube addons list</code>
<code>minikube addons enable dashboard</code>
<code>minikube addons enable metrics-server</code>

To disable,
<code>minikube addons disable dashboard</code>
<code>minikube addons disable metrics-server</code>

minikube dashboard --url

More details at https://kubernetes.io/docs/tutorials/hello-minikube/

