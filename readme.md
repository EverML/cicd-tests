# Anotaciones Tutorial Kubernetes


Probando con:
 * Minikube 1.5.1
 * Kubernetes v1.16.2 
 * Docker 18.09.9


# Setear version  de kubernetes
minikube start --memory 4000 --cpus 2 --kubernetes-version v1.11.10 



# Habilitar el addon del dashboard (deshabilitado por defecto)
minikube addons enable dashboard



# Hello World con Minikube from scratch


# Crear 3 archivos.
1. server.js
2. dockerfile.
3. ingress.yaml



# server.js

    var http = require('http');
    
    var handleRequest = function(request, response) {
      console.log('Received request for URL: ' + request.url);
      response.writeHead(200);
      response.end('Hello Ever');
    };
    var www = http.createServer(handleRequest);
    www.listen(8081);
    

# dockerfile
    FROM node:6.14.2
    EXPOSE 8081
    COPY server.js .
    CMD node server.js

# ingress.yaml

    apiVersion: networking.k8s.io/v1beta1
    kind: Ingress
    metadata:
      name: ingress-prueba-ever
    spec:
      backend:
        serviceName: hello-ever
        servicePort: 8081



Despues de realizar las alteraciones al archivo server.js


# Para generar la imagen de docker.

```bash
docker build -t cicdtest .

docker tag cicdtest:latest <username>/cicdtest:latest

docker push <username>/cicdtest:latest

```




# Para montar dentro de un pod en kubernetes (Ejemplo minikube)
    minikube start
    
    
    kubectl create deployment nombreCualquiera --image=<username>/cicdtest:latest
    
    
    kubectl expose deployment nombreCualquiera --type=LoadBalancer --port=8081
    
    
    
    minikube service nombreCualquiera
    


# Para eliminar el servicio

    kubectl delete service nombreCualquiera
    
    kubectl delete deployment nombreCualquiera
    
    minikube stop


//Opcional
`minikube delete`






# Para hacer el reverse proxy
```bash

kubectl apply -f ingress.yaml
```



























