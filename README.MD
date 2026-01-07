# Repositorio de Orquestación de Contenedores con Docker-Compose

## Iniciar el sistema completo
Construye las imágenes locales y levanta los contenedores en segundo plano:
```
docker-compose up -d --build
```

## Detener el sistema
Detiene los contenedores pero mantiene la infraestructura creada:
```
docker-compose stop
```
## Limpiar el entorno
Detiene y elimina los contenedores, redes y configuraciones efímeras:
```
docker-compose down
```

## Resetear datos (Borrado físico)
Si necesitas eliminar los volúmenes de las bases de datos para limpiar los datos persistentes:
```
docker-compose down -v
```

## Ver estado actual
Mirar si el contenedor está corriendo o si se está reiniciando:
```
docker ps
```

## Ver los logs
Para ver exactamente qué error está lanzando Java (el StackTrace):
```
docker logs -f order-service-dev
```

# Solución Flyway
## 1. Baja el contenedor de órdenes y borra su volumen de datos específico
```
docker-compose down
```
## 2. Borra el volumen de la base de datos de órdenes (esto limpia las tablas)
Si no sabes el nombre exacto del volumen, bórralos todos con:
```
docker volume rm $(docker volume ls -q | grep order) 
```

## 3. Vuelve a levantar todo
```
docker-compose up -d --build
```