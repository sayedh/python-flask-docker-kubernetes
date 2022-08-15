# Deploying a Flask app with Docker into Kubernetes Pods with Load Balancing
In this project I used a simple Flask app that lists the instance ID, dockerized it, and put it into pods that are load balanced. So when the Flask app is refreshed you can see that it is a new instance ID meaning that it changed pods. 
![Pods](https://user-images.githubusercontent.com/30685241/184702096-d04faf9a-bebb-4ce6-8a44-7725742d0265.jpg)


## Technologies Used
* Flask
* Docker
* Kubernetes

## Dependencies
* Install Flask - https://pypi.org/project/Flask/
* Install Docker - https://docs.docker.com/get-docker/
* Install Kubernetes (minikube) - https://kubernetes.io/docs/tasks/tools/

## Executing program
* Download the repository to your computer go to project file
```
git clone https://github.com/sayedh/python-flask-docker-kubernetes
cd python-flask-docker-kubernetes
```
* Run the Flask app
```
flask run
```

* Build the Docker image and run it
```
docker build -t flask-app-testing .
docker run --name test-flask -p 5000:5000 flask-app-testing
```

* Now start Kubernetes and load the docker image
```
minikube start
minikube image load flask-app-testing
```

* Apply the YAML files and run the app
```
kubectl apply -f kubernetes/flask_deployment.yaml
kubectl apply -f kubernetes/flask_service.yaml
minikube service flask-app-service –url
```

* Now if your refresh the page, you will see that the instance ID changes meaning the pods change. 
![InstanceChange](https://user-images.githubusercontent.com/30685241/184712443-5ea99544-53fc-4997-bc51-7095eba7e271.png)


* Use this command to change the number of pods. You go up or down in the number of pods. 
```
kubectl scale deployment flask-app --replicas=10
```

* You can also view the Kubernetes dashboard with this command 
```
minikube dashboard
```
![Dashboard](https://user-images.githubusercontent.com/30685241/184712942-476ba95c-acd2-4a93-8e86-bbfbe79609b3.jpg)
