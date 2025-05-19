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

### Configuración con Nginx

Para una configuración de producción óptima, se recomienda utilizar Nginx como proxy inverso:

```nginx
server {
    listen 80;
    server_name tudominio.com;

    location /static/ {
        alias /ruta/a/CineCloud-backend/static/;
    }

    location /media/ {
        alias /ruta/a/CineCloud-backend/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
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

| Variable | Descripción | Valor por defecto |
|----------|-------------|-------------------|
| `DJANGO_SECRET_KEY` | Clave secreta para la aplicación | `''` (generada automáticamente) |
| `DEBUG` | Modo de depuración | `False` |
| `DATABASE_URL` | URL de conexión a la base de datos | `postgresql://postgres:postgres@db:5432/cinecloud` |
| `ALLOWED_HOSTS` | Hosts permitidos | `localhost,127.0.0.1` |
| `CORS_ALLOWED_ORIGINS` | Orígenes permitidos para CORS | `http://localhost:4200` |

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
