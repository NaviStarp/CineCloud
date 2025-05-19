# Instalación del Backend

Esta guía detalla los diferentes métodos para instalar el backend de Cinecloud en entornos de desarrollo y producción.

## Instalación con Docker (Recomendado)

Docker permite una configuración rápida y consistente del entorno de Cinecloud.

### Requisitos previos

- Docker y Docker Compose instalados
- Clonar el repositorio: `git clone https://github.com/NaviStarp/CineCloud-backend.git`

### Pasos para la instalación

1. Navega al directorio del proyecto:
   ```bash
   cd CineCloud-backend
   ```

2. Ejecuta Docker Compose:
   ```bash
   docker-compose up
   ```

   Para ejecutar en segundo plano:
   ```bash
   docker-compose up -d
   ```

3. Verifica que los contenedores estén funcionando:
   ```bash
   docker ps
   ```

La aplicación estará disponible en `http://localhost:8000/`.

### Configuración de Docker

El archivo `docker-compose.yml` incluye:

- Servicio de base de datos PostgreSQL
- Servicio web para la aplicación Django
- Configuración de variables de entorno
- Mapeo de puertos y volúmenes

Para personalizar la configuración, edita los archivos `Dockerfile` y `docker-compose.yml`.

## Servidor de Desarrollo

Para entornos de desarrollo o pruebas rápidas:

```bash
# Activar entorno virtual
source .venv/bin/activate

# Iniciar servidor de desarrollo
python manage.py runserver
```

Para especificar un puerto diferente:

```bash
python manage.py runserver 8001
```

## Servidor de Producción

Para entornos de producción se recomienda utilizar Uvicorn como servidor ASGI:

```bash
# Activar entorno virtual
source .venv/bin/activate

# Iniciar servidor de producción
uvicorn --host 0.0.0.0 --port 8000 cinecloud.asgi:application
```

## Inicio Automático (Linux)

El proyecto incluye un script para iniciar automáticamente la aplicación en sistemas Linux:

```bash
chmod +x start.sh
./start.sh
```

Este script:
1. Activa el entorno virtual
2. Verifica que la base de datos esté en funcionamiento
3. Aplica migraciones pendientes
4. Inicia el servidor con Uvicorn

## Variables de Entorno
Las siguientes variables de entorno pueden ser configuradas para personalizar la instalación:

| Variable               | Descripción                                      | Valor por defecto                          |
|------------------------|--------------------------------------------------|--------------------------------------------|
| `DJANGO_SECRET_KEY`    | Clave secreta para la aplicación                 | `clave-supersecreta-docker`                |
| `DEBUG`                | Modo de depuración                               | `False`                                    |
| `ALLOWED_HOSTS`        | Hosts permitidos                                 | `web,localhost,127.0.0.1`                  |
| `CORS_ALLOW_ALL_ORIGINS` | Permitir todos los orígenes para CORS          | `True`                                     |
| `CORS_ALLOWED_ORIGINS` | Orígenes permitidos para CORS                    | `http://localhost:4200`                    |
| `CSRF_TRUSTED_ORIGINS` | Orígenes confiables para CSRF                    | `http://localhost:4200`                    |
| `DATABASE_URL`         | URL de conexión a la base de datos              | `postgresql://admin:secret_password@db:5432/bd` |
| `POSTGRES_DB`          | Nombre de la base de datos                      | `bd`                                       |
| `POSTGRES_USER`        | Usuario de la base de datos                     | `admin`                                    |
| `POSTGRES_PASSWORD`    | Contraseña de la base de datos                  | `secret_password`                          |
| `POSTGRES_HOST`        | Host de la base de datos                        | `db`                                       |
| `POSTGRES_PORT`        | Puerto de la base de datos                      | `5432`                                     |
| `REDIS_HOST`           | Host del servidor Redis                         | `redis`                                    |
| `REDIS_PORT`           | Puerto del servidor Redis                       | `6379`                                     |
| `CELERY_BROKER_URL`    | URL del broker para Celery                      | `redis://redis:6379/0`                     |
| `CELERY_RESULT_BACKEND`| Backend de resultados para Celery               | `redis://redis:6379/0`                     |

## Recomendaciones para producción

1. **Asegura los secretos**: No almacenes claves secretas en el repositorio
2. **Configura HTTPS**: Utiliza certificados SSL para conexiones seguras
3. **Monitoreo**: Implementa herramientas como Prometheus o Grafana
4. **Copias de seguridad**: Configura respaldos automáticos de la base de datos
5. **Logs**: Centraliza y monitorea los registros de la aplicación

## Escalabilidad

Para escalar horizontalmente:

1. Utiliza un balanceador de carga (como HAProxy o Nginx)
2. Configura múltiples instancias del servidor
3. Utiliza una base de datos compartida o replicada
4. Considera servicios de almacenamiento compartido para archivos multimedia

## Siguientes pasos

- [Arquitectura](architecture.md): Comprende la estructura del proyecto
