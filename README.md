
# Task Description

This task involves deploying a multi-component application in a Kubernetes cluster using Minikube. The primary objectives are:

1. **Setup Minikube with Multiple Nodes**: Start a Minikube instance configured with 2 nodes to simulate a multi-node environment.

2. **Create Namespaces**: Establish three namespaces within the cluster:
   - `front-end`: For the frontend application.
   - `mongo-db`: For the MongoDB database deployment.
   - `mongo-express`: For the Mongo Express application.

3. **Deployments and Services**:
   - **Frontend Application**: Deploy a simple web frontend application within the `FE` namespace. The application will consist of 2 replicas using an `emptyDir` volume to store web content, which will be mounted to `/usr/share/nginx/html` in the pod. A NodePort service named `frontend-service` will be created to expose the Nginx application externally on port 80.
   
   - **MongoDB Deployment**: Deploy a MongoDB instance in the `mongo-db` namespace. This will include a single replica using the `mongo:latest` image. A Kubernetes secret named `mongodb-secret` will be created to securely store the MongoDB root username (`MONGO_INITDB_ROOT_USERNAME`) and password (`MONGO_INITDB_ROOT_PASSWORD`). A persistent volume and persistent volume claim (PVC) named `mongodb-pvc` will be utilized to store MongoDB data at `/data/db`. A ClusterIP service named `mongodb-service` will expose the database internally on port 27017.

   - **Mongo Express Deployment**: Deploy Mongo Express in the `mongo-express` namespace using the `mongo-express:latest` image. A config map named `mongo-express-config` will be created to store environment variables, allowing the application to access the MongoDB instance. A NodePort service named `mongo-express-service` will be established to expose the Mongo Express interface externally on port 8081.

4. **Taints and Tolerations**:
   - Apply a taint to one of the Minikube nodes with the key `db:NoSchedule` to control pod scheduling.
   - A toleration will be applied to the MongoDB deployment, allowing it to be scheduled on the tainted node.
   - Ensure that the MongoDB pod is scheduled on the tainted node using node affinity rules.


