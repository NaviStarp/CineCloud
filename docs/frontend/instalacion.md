# Instalación

## Requisitos previos

Asegúrate de tener instalado lo siguiente:

- Node.js (v14.x o superior)
- npm (incluido con Node.js)
- Angular CLI
- Backend de Cinecloud (necesario para la funcionalidad completa)

## Clonar el repositorio

```bash
git clone https://github.com/NaviStarp/CineCloud-frontend.git
cd CineCloud-frontend
```
## Instalar dependencias
```bash
npm install
```
## Iniciar servidor de desarollo 
```bash
ng serve
```
La aplicación estará disponible en http://localhost:4200.

Para usar otro puerto:
```bash
ng serve --port 4201
```
## Configuración del entorno

En el archivo de configuración de entorno de Angular (`src/environments/environment.ts`), puedes especificar la IP y el puerto del backend:

```typescript
export const environment = {
    url: 'http://<IP_DEL_BACKEND>',
    port: '<PUERTO_DEL_BACKEND>',
};
```

# Construcción para producción
```bash
ng build --configuration production
```
Los archivos se generan en el directorio dist/.
```markdown
# Estructura del proyecto
├── src/
│ ├── app/
│ │ ├── app.component.*
│ │ ├── general/
│ │ ├── login/
│ │ ├── login-signup/
│ │ ├── media-list/
│ │ ├── not-found/
│ │ ├── pages/
│ │ ├── services/
│ │ ├── signup/
│ │ └── video-card/
│ ├── environments/
│ ├── index.html
│ ├── main.*
│ └── styles.css
├── public/
├── angular.json
├── package.json
├── tailwind.config.js
├── tsconfig.*
├── LICENSE
└── README.md


### Principales directorios

- `app/general/`: Componentes reutilizables
- `app/pages/`: Páginas principales como `admin`, `media-gallery`, `movie-detail`, etc.
- `app/services/`: Servicios e interceptores
- `app/login-signup/`: Componentes y formularios de autenticación
- `media-gallery/`: Vista y carrusel de películas y series
- `serie-detail/`: Gestión de temporadas y episodios
```
