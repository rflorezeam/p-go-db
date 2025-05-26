# Servicio de Base de Datos MongoDB para Microservicios de Libros

## Desarrollador
Ricardo Florez

## Descripción
Este servicio proporciona la capa de persistencia de datos para todos los microservicios del sistema de gestión de libros. Utiliza MongoDB como base de datos y está configurado con almacenamiento persistente mediante Kubernetes PersistentVolume.

## Características
- MongoDB versión latest
- Almacenamiento persistente mediante PV y PVC
- Credenciales configurables mediante variables de entorno
- Expuesto internamente en el puerto 27017

## Configuración Kubernetes
El servicio incluye:
- PersistentVolume (1Gi de almacenamiento)
- PersistentVolumeClaim
- Deployment (1 réplica)
- Service (ClusterIP)

## Variables de Entorno
- MONGO_INITDB_ROOT_USERNAME: root
- MONGO_INITDB_ROOT_PASSWORD: example

## Estructura de Datos
Colección: `libros`
```json
{
    "_id": "ObjectId",
    "titulo": "String",
    "autor": "String"
}
```

## Despliegue
```bash
kubectl apply -f k8s/persistent-volume.yaml
kubectl apply -f k8s/persistent-volume-claim.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

## Mantenimiento
Para respaldar la base de datos:
```bash
kubectl exec -it [pod-name] -- mongodump --uri="mongodb://root:example@localhost:27017"
``` 