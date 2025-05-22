# 📦 Guía Rápida de Instalación – Backend Cinecloud

Esta guía te ayudará a instalar el backend de **Cinecloud** fácilmente, ya sea en **Linux** o **Windows**, para desarrollo o producción.

---

## ⚙️ Variables de Entorno

Configura las siguientes variables de entorno en los archivos correspondientes (`.env.local` o `.env.docker`), según si decides usar Docker o no:

| Variable                      | Descripción                        | Valor por defecto              |
|------------------------------|------------------------------------|-------------------------------|
| `DJANGO_SECRET_KEY`          | Clave secreta de Django            | `clave-supersecreta-X`  |
| `DJANGO_DEBUG`               | Modo de depuración (`True/False`)  | `False`                       |
| `DJANGO_ALLOWED_HOSTS`       | Hosts permitidos                   | `web,localhost,127.0.0.1`     |
| `CORS_ALLOW_ALL_ORIGINS`     | Permitir todos los orígenes CORS   | `True`                        |
| `CORS_ALLOWED_ORIGINS`       | Orígenes permitidos CORS           | `http://localhost:4200`       |
| `CSRF_TRUSTED_ORIGINS`       | Orígenes confiables para CSRF      | `http://localhost:4200`       |
| `POSTGRES_DB`                | Nombre de la BD                    | `bd`                          |
| `POSTGRES_USER`              | Usuario de BD                      | `admin`                       |
| `POSTGRES_PASSWORD`          | Contraseña de BD                   | `secret_password`             |
| `POSTGRES_HOST`              | Host de la BD                      | `db`                          |
| `POSTGRES_PORT`              | Puerto de la BD                    | `5432`                        |
| `REDIS_HOST`                 | Host Redis                         | `redis`                       |
| `REDIS_PORT`                 | Puerto Redis                       | `6379`                        |
| `CELERY_BROKER_URL`          | URL de Celery                      | `redis://redis:6379/0`        |
| `CELERY_RESULT_BACKEND`      | Backend de resultados de Celery    | `redis://redis:6379/0`        |
| `DJANGO_SUPERUSER_USERNAME`  | Nombre del superusuario            | `admin`                       |
| `DJANGO_SUPERUSER_PASSWORD`  | Contraseña del superusuario        | `admin`                       |

---
## 🚀 Opción 1: Instalación con Docker (Recomendada)

### ✅ Requisitos

- Tener **Docker** y **Docker Compose** instalados.  
- [Instalar Docker en Linux](https://docs.docker.com/engine/install/)
- [Instalar Docker Desktop en Windows](https://docs.docker.com/desktop/install/windows-install/)


### 🔧 Pasos

1. Clona el repositorio:
   ```bash
   git clone https://github.com/NaviStarp/CineCloud-backend.git
   cd CineCloud-backend
   ```

2. Configura las variables de entorno en los archivos `.env` y `.env.docker`.
```bash
USE_DOCKER=yes
```
> **Nota:** Asegúrate de que la variable `USE_DOCKER` en el archivo `.env` esté configurada en `yes` para que se utilicen correctamente las variables definidas en `.env.docker`.

3. Inicia los servicios con Docker:
   ```bash
   docker-compose up
   ```
   O en segundo plano:
   ```bash
   docker-compose up -d
   ```

4. Verifica que todo esté corriendo:
   ```bash
   docker ps
   ```

5. En caso de que el usuario administrador no exista, puedes crearlo:
   ```bash
   docker compose exec app python manage.py createsuperuser
   ```

📍 Accede a la app en tu navegador:  
👉 `http://localhost:8000/`

---

## ⚙️ Opción 2: Instalación Manual (sin Docker)

### ✅ Requisitos

- Tener Python 3.10+ instalado
- Tener PostgreSQL (si no usas Docker para la base de datos)
- Redis (opcional para tareas con Celery)

### 🔧 Pasos en Linux o WSL (Windows)

1. Clona el repositorio:
   ```bash
   git clone https://github.com/NaviStarp/CineCloud-backend.git
   cd CineCloud-backend
   ```

2. Crea y activa un entorno virtual:
   ```bash
   python -m venv .venv
   source .venv/bin/activate      # Linux o WSL
   .venv\Scripts\activate         # Windows CMD/PowerShell
   ```

3. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```
3. Cambia la variable `USE_DOCKER` en el archivo `.env`
   ```bash
   USE_DOCKER=no
   ```

4. Configura tu base de datos PostgreSQL editando el archivo `.env.local` según tus necesidades.  
   > **Nota:** Aunque no es obligatorio para el despliegue, se recomienda encarecidamente cambiar las contraseñas predeterminadas por razones de seguridad.

5. Inicia la base de datos:
   ```bash
   cd database
   docker-compose up -d # Puede que necesites usar sudo en Linux
   cd ..
   ```

6. Aplica las migraciones:
   ```bash
   python manage.py migrate
   ```
7. Crea el usuario administrador:
   ```bash
   python manage.py create_admin
   ```

8. Inicia el servidor:

   > Para desarrollo:
     ```bash
     python manage.py runserver
     ```

   > Para producción (Recomendado):
     ```bash
     uvicorn --host 0.0.0.0 --port 8000 cinecloud.asgi:application
     ```


## 🤖 Inicio Automático (Linux)

Si usas Linux, puedes arrancar todo automáticamente con:

```bash
chmod +x start.sh
./start.sh
```

Este script:
- Activa el entorno virtual
- Inicia Docker (base de datos)
- Aplica migraciones
- Lanza Uvicorn
> Nota: Este código requiere que el entorno virtual esté creado y que las dependencias necesarias estén instaladas.
Asegúrate de haber configurado el entorno virtual utilizando herramientas como `venv` o `virtualenv` y de haber
instalado las dependencias especificadas en el archivo `requirements.txt` antes de ejecutar el código.
---

## 📘 Más Información

- [📐 Arquitectura del Proyecto](arquitectura.md)
