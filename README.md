# Solution

The application is a web app with the three tier architecture

  1. client (react)
  2. server (spring boot)
  3. database (mysql)

## Task A

1. Two dockerfiles created for client (client/Dockerfile) and server (server/Dockerfile).
2. Build backend jar using maven.

    Prerequisite: maven and java installed in local`

    ```bash
    $ mvn clean install -DskipTests
    ```
3. Build and push docker images for backend and frontend into dockerhub

    ```bash
    $ docker login -u <dockerhub_username> -p <dockerhub_password>
    $ cd client
    $ docker build -t <dockerhub_username>/client:latest .
    $ docker push <dockerhub_username>/client:latest
    $ cd ../server
    $ docker build -t <dockerhub_username>/server:latest .
    $ docker push <dockerhub_username>/server:latest
    ```

## Task B

1. Have used minikube for running kubernetes in local.
2. Have deployed 3 kubernetes manifests to deploy database (database.yaml), server (server.yaml) and client (client.yaml) into minikube.
3. database.yaml used mysql:5.7 public image to run the database.
4. server.yaml and client.yaml uses server and client images build and pushed to docker hub in Task A.
5. Start minikube
    Prerequisite: minikube and kubectl installed in local

    ```bash
    $ minikube start
    ```

6. Deploying kubernetes manifests

    ```bash
    $ kubectl apply -f database.yaml
    $ cd server
    $ kubectl apply -f server.yaml
    $ cd ../client
    $ kubectl apply -f client.yaml
    ```
7. Test

    ```bash
    $ minikube tunnel
    ```

    Get the loadbalancer IP of the frontend service by running

    ```bash
    $ kubectl get svc -n app
    ```

    And then access the URL in the browser.
