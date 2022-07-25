# Helm Task

## 1. Create a helm chart for the python app
docker image for python app:

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled.png) 

to push the image to docker hub:

```bash
# make a new tag to the image
docker tag python-app mnaggar3396/python-app
# push it 
docker push mnaggar3396/python-app
```

---

create a new helm chart:

```bash
helm create python-app
```

to create a new release:

```bash
heml install python-app-release python-app/
```


check deployments, services and helm releases:

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%201.png)


to get python-app service ip:

```bash
minikube service python-app-svc --url
```


![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%202.png)


---

## 2- Deploy Jenkins Chart on the cluster and login to jenkins

```bash
helm search repo jenkins

# install jenkins
helm install jenkins-release jenkins/jenkins
```

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%203.png)

check releases:

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%204.png)

login to jenkins:

```bash
# git admin password
kubectl exec --namespace default -it svc/jenkins-release -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo

# to open jenkins
kubectl --namespace default port-forward svc/jenkins-release 8085:8080
```

login with username: admin and password

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%205.png)

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%206.png)

---

## 3- Bonus: package, sign, and push your chart to artifact hub

```bash
# package python-app chart
helm package python-app

# create index.yaml
helm repo index python-app
```

![Untitled](Helm%20Task%20155db36e2fd04790adf64770eb74ad17/Untitled%207.png)