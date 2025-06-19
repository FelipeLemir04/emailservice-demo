# README - Despliegue CI/CD para microservicio emailservice

Este README documenta el proceso para clonar, versionar, dockerizar y configurar un pipeline de integración continua (CI) para el microservicio `emailservice` del proyecto [microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo).

---

1. Selección del microservicio

Se seleccionó el microservicio `emailservice` desarrollado en Python, ubicado en:

2. Clonar y subir a repositorio propio

a) Clonar el microservicio


git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo/src/emailservice

b) Crear repositorio público en GitHub
Crear un repositorio público llamado, por ejemplo:
emailservice-demo

c) Subir el código al nuevo repositorio
bash
Copiar
Editar
git init
git remote add origin https://github.com/tu-usuario/emailservice-demo.git
git add .
git commit -m "Microservicio emailservice de microservices-demo"
git push -u origin main

3. Crear Dockerfile

Crear el archivo .github/workflows/docker-build-publish.yml con el siguiente contenido:

    name: Build and Push Docker image

      on:
        push:
          branches:
            - main

      jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout repo
        uses: actions/checkout@v3



     - name: Log in to DockerHub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_PASSWORD }}



    - name: Build and push Docker image
      uses: docker/build-push-action@v5
      with:
        context: .
        push: true
        tags: tu-usuario/emailservice-demo:latest

5. Configuración de secretos en GitHub
Ir a:
Settings > Secrets and variables > Actions

Agregar los secretos:

DOCKERHUB_USERNAME → usuario de Docker Hub

DOCKERHUB_PASSWORD→ contraseña de Docker Hub

6. Verificar publicación en Docker Hub
La imagen Docker se debe publicar automáticamente en:
https://hub.docker.com/repository/docker/tu-usuario/emailservice-demo

