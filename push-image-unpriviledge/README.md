```
jumphost:~$ podman image ls
docker.io/user-09/training-ngninx  v1          52f656661975  50 minutes ago  191 MB
```

but you cannot push it as you are not using your repo - for example "cral"
then you have to tag the image:

```podman image tag 52 docker.io/cral/training-ngninx:v1```

```jumphost:~$ podman image ls
REPOSITORY                         TAG         IMAGE ID      CREATED         SIZE
docker.io/user-09/training-ngninx  v1          52f656661975  50 minutes ago  191 MB
docker.io/cral/training-ngninx     v1          52f656661975  50 minutes ago  191 MB
```


Writing the Manifests
You will need at least the following manifests:

Deployment
named nginx-custom
runs 1 replica of a pod using the docker.io/<user>/training-nginx:v1 image (where <user> is your Docker ID!)
uses a selector of app: nginx-custom (and, of course, uses the same as a label for the pods in the template)
Service:
named nginx-custom
type: ClusterIP
uses the pods in the nginx-custom deployment as backends
Ingress:
named nginx-custom
uses ingressClassName openshift-default
uses host webserver-09.apps.cluster1.openshift.vms.sass.ro


```agsl
oc apply -f .
oc get pod

POD_NAME=$(oc get pod -l app=nginx-custom -o jsonpath={.items[0].metadata.name})
oc describe pod $POD_NAME

POD_NAME=$(oc get pod -l app=nginx-custom -o jsonpath={.items[0].metadata.name})
oc logs $POD_NAME
```