# AB Comercial Full Stack Docker

Repositorio opcional para levantar el frontend y backend juntos usando Docker Compose.

La entrega principal de la prueba vive en dos repositorios separados:

- Backend: configura aqui el link publico del repositorio backend.
- Frontend: configura aqui el link publico del repositorio frontend.

## Estructura Esperada

Clona los tres repositorios dentro de una misma carpeta:

```text
workspace/
  ab-comercial-backend/
  ab-comercial-frontend/
  ab-comercial-fullstack-docker/
```

El `docker-compose.yml` usa rutas relativas para construir las imagenes desde los repos de backend y frontend.

## Variables

Copia el archivo de ejemplo:

```bash
cp .env.example .env
```

Valores principales:

```env
BACKEND_CONTEXT=../ab-comercial-backend
FRONTEND_CONTEXT=../ab-comercial-frontend
BACKEND_ENV_FILE=../ab-comercial-backend/.env
NEXT_PUBLIC_API_URL=http://localhost:8000/api/v1
```

El backend debe tener su propio `.env` configurado. Si el backend corre dentro de Docker y la base de datos esta en tu maquina, usa `host.docker.internal` en `DATABASE_URL`.

Los logs del backend salen por consola y se pueden consultar con:

```bash
docker compose logs -f backend
```

## Uso

Levantar backend y frontend:

```bash
docker compose up --build
```

El servicio `migrate` ejecuta las migraciones antes de iniciar la API. El backend conserva el `CMD` definido en su `Dockerfile`.

Frontend:

```text
http://localhost:3000
```

Backend:

```text
http://localhost:8000/docs
```

Cargar datos demo:

```bash
docker compose --profile tools run --rm seed
```

## Nota

Este repositorio es un plus de desarrollo local. La prueba sigue organizada en frontend y backend separados para mantener despliegues y responsabilidades claras.
