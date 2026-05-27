# n8n Local (Nginx + PostgreSQL + pgAdmin)

Este repositorio contiene una infraestructura local completa y modular utilizando **Docker Compose**. El entorno despliega **n8n** como plataforma de automatización de flujos de trabajo, utilizando **PostgreSQL** como base de datos para la persistencia de datos y **Nginx** como un proxy inverso centralizado para gestionar el tráfico web de forma limpia a través del puerto estándar HTTP (80).

Adicionalmente, se incluye **pgAdmin 4** mapeado bajo una subruta proxy para administrar la base de datos de manera cómoda y centralizada.

---

## 🏗️ Entorno Local

El entorno está basado en servicios independientes que se comunican a través de la red interna de Docker:

- **Nginx (`nginx_proxy`)**: El único punto de acceso expuesto al exterior. Recibe las peticiones en el puerto 80 y las redirige internamente según la ruta.
- **n8n (`n8n_service`)**: Motor de automatización conectado a la base de datos relacional. Soporta WebSockets nativos para la actualización en tiempo real de la interfaz.
- **PostgreSQL (`postgres_service`)**: Base de datos principal optimizada con scripts de _Healthcheck_ para garantizar que los servicios dependientes arranquen solo cuando la DB esté lista.
- **pgAdmin 4 (`pgadmin4_service`)**: Interfaz web de administración de Postgres, servida de forma segura a través de la subruta proxy `/pgadmin/`.

---

## 🛠️ Tecnologías Utilizadas

- [Docker & Docker Compose](https://www.docker.com/)
- [n8n](https://n8n.io/)
- [Nginx](https://www.nginx.com/)
- [PostgreSQL 16](https://www.postgresql.org/)
- [pgAdmin 4](https://www.pgadmin.org/)

---

## 🚀 Requisitos Previos

1.  Tener instalado **Docker** y **Docker Desktop** (en Windows/Mac) o el motor de Docker (en Linux).
2.  Tener instalado **Git**.

---

## 💻 Instalación y Despliegue

### 1. Clonar el repositorio

```bash
git clone [https://github.com/Juanvivas043/n8n-nginx-proxy.git](https://github.com/Juanvivas043/n8n-nginx-proxy.git)
cd n8n-nginx-proxy
```

### 2. Configurar las Variables de Entorno (`.env`)

El proyecto evita exponer credenciales reales en el repositorio. Para ello, se incluye un archivo de plantilla llamado `.env.example`.

Debes duplicar este archivo en la raíz del proyecto y renombrarlo a `.env`:

```bash
cp .env.example .env
```

### 3. Inicializar la Infraestructura (`docker compose up`)

Ya con las variables abre tu terminal dentro de la carpeta raíz del proyecto, crea los volumenes para la persistencia de datos y ejecuta el siguiente comando para levantar los servicios:

```bash
docker volume create volumenesArchivoCompose

docker compose up
```
