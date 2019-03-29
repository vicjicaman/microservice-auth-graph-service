# microservice-auth-graph-service
Service configuration for kubernetes


Mount modules to minikube
minikube mount /host-mount-path:/vm-mount-path


minikube mount /home/victor/nodeflow/workspace/workspaces/microservices/instances/auth-init/modules:/workspace/instances/auth-init/modules



apiVersion: apps/v1
kind: Deployment
metadata:
  name: auth-graph-deployment
  namespace: microservices
  labels:
    app: auth-graph-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: auth-graph-deployment
  template:
    metadata:
      labels:
        app: auth-graph-deployment
    spec:
      containers:
      - name: auth-graph-container
        image: 919446158824.dkr.ecr.us-east-1.amazonaws.com/microservice-auth-graph-container:1.0.0-master
        env:
        - name: SERVICE_PORT
          value: ${SERVICE_PORT}
        ports:
        - containerPort: ${SERVICE_PORT}
        volumeMounts:
          - mountPath: "/app/node_modules/@nebulario/microservice-auth-graph"
            name: auth-graph-mount
      volumes:
        - name: auth-graph-mount
          hostPath:
            path: "/workspace/instances/auth-init/modules/microservice-auth-graph"
