# Docker Dev Workflow – NestJS + GraphQL

Este proyecto demuestra cómo utilizar **Docker como entorno de desarrollo**, ejecutando una aplicación NestJS dentro de un contenedor usando **bind mounts** para permitir live reload.

⚠️ No se utilizan Dockerfile ni Docker Compose.
El objetivo es aprender el flujo de desarrollo directamente con `docker run`.

---

## 🎯 Objetivo del laboratorio

Practicar:

* Ejecutar aplicaciones Node dentro de contenedores
* Bind mounts (host ↔ contenedor)
* Live reload
* Terminal interactiva
* Inspección del file system del contenedor
* Desarrollo sin instalar Node localmente

Simula un entorno real donde Docker actúa como entorno aislado de desarrollo.

---

## 🧰 Stack

* Node 16 (node:16-alpine)
* NestJS
* GraphQL
* Docker CLI

---

## 🚀 Ejecutar la aplicación

Desde la raíz del proyecto:

docker container run 
--name nest-app 
-w /app 
-p 80:3000 
-v "$(pwd)":/app 
node:16-alpine3.16 
sh -c "yarn install && yarn start:dev"

Abrir en el navegador:

[http://localhost/graphql](http://localhost/graphql)

---

## 📦 ¿Qué hace cada parámetro?

* `-v "$(pwd)":/app` → bind mount del código local
* `-w /app` → directorio de trabajo
* `-p 80:3000` → publicar puerto
* `yarn install` → instalar dependencias dentro del contenedor
* `yarn start:dev` → modo watch / hot reload

---

## 🔄 Live reload

Cualquier cambio en:

src/

se refleja automáticamente en el navegador gracias al bind mount.

---

## 🖥️ Acceder al contenedor

docker exec -it nest-app /bin/sh

Explorar filesystem:

cd /app
ls
cat src/hello-world/hello-world.resolver.ts

Modificar archivos desde el contenedor también afecta el host.

---

## 🧠 Conceptos aprendidos

✅ desarrollo sin instalar Node local

✅ aislamiento del entorno

✅ bind mounts

✅ live reload

✅ debugging dentro del contenedor

✅ exploración del filesystem

Este patrón es común en equipos que usan Docker como entorno estándar de desarrollo.

---

## 📌 Nota

Este repositorio forma parte de mi portafolio DevOps.

Otros repos relacionados:

* docker-cli-fundamentals → comandos básicos, redes, volúmenes
* próximos: Dockerfile, Docker Compose y orquestación
