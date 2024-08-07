# Proyecto Kubernetes con Minikube y kubectl

## Requisitos previos

### Instalación de Minikube
1. Visita la página de [instalación de Minikube](https://minikube.sigs.k8s.io/docs/start/).
2. Sigue las instrucciones para tu sistema operativo (Linux, macOS, Windows).

### Instalación de kubectl
1. Visita la página de [instalación de kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
2. Sigue las instrucciones para tu sistema operativo (Linux, macOS, Windows).

## Paso a paso

### 1. Iniciar Minikube

```sh
minikube start
```

### 2. Crear un Namespace

```sh
kubectl create namespace mi-proyecto
```

### 3. Aplicar los Archivos de Configuración

1. **Crear la Base de Datos MySQL y el Deployment**

   Ejecuta el siguiente comando para crear un pod con MySQL usando una imagen de Docker Hub y configurar la base de datos:

   ```sh
   kubectl apply -f bd-dp.yaml --namespace=mi-proyecto
   ```

   Este comando descarga una imagen de MySQL y crea una base de datos en el pod según lo definido en `bd-dp.yaml`.

2. **Exponer el Servicio de la Base de Datos**

   Aplica la configuración del servicio para exponer el pod de la base de datos y permitir el acceso:

   ```sh
   kubectl apply -f service-db.yaml --namespace=mi-proyecto
   ```

   Esto crea un servicio que expone el pod de MySQL, permitiendo que otros pods se conecten a él usando el nombre del servicio.

3. **Crear el Pod de la API**

   Aplica la configuración del deployment para crear un pod que descarga una imagen desde tu Docker Hub:

   ```sh
   kubectl apply -f dp-api-ait-be.yaml --namespace=mi-proyecto
   ```

   Este comando crea un pod que usa una imagen de Docker Hub y pasa las conexiones a la base de datos a través de las variables de entorno. En este caso, el host de la base de datos será el nombre del servicio definido en `service-db.yaml`.


### 4. Exponer el Servicio
Para poder testear y probar la api

```sh
minikube service myservice --namespace=mi-proyecto
```

