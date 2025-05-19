# Backend de Cinecloud

## Visión general

Cinecloud Backend es una aplicación desarrollada en Django que proporciona funcionalidades avanzadas para la autenticación de usuarios, renderización de contenido multimedia y transmisión en streaming de videos clasificados como películas y series.

Este sistema está diseñado para ofrecer una experiencia fluida y segura, permitiendo a los usuarios acceder a contenido de alta calidad de manera eficiente. Además, su arquitectura modular facilita la escalabilidad y el mantenimiento del proyecto, adaptándose a las necesidades de crecimiento y evolución de la plataforma.

## Tecnologías principales

- **Django**: Framework web Python de alto nivel
- **Django REST Framework**: Para la creación de APIs RESTful
- **Django Channels**: Para funcionalidades WebSocket y ASGI
- **FFmpeg**: Procesamiento de archivos multimedia para streaming HLS
- **Docker**: Contenedores para facilitar el despliegue
- **PostgreSQL**: Base de datos relacional

## Características clave

- **Autenticación robusta**: Sistema completo de registro, inicio de sesión y gestión de perfiles
- **Streaming HLS**: Transmisión adaptativa de contenido multimedia
- **API RESTful**: Endpoints bien documentados para integraciones fáciles
- **WebSockets**: Comunicación en tiempo real para funcionalidades interactivas
- **Procesamiento multimedia**: Conversión y optimización de archivos de video
- **Arquitectura modular**: Aplicaciones Django independientes para una mejor organización

## Requisitos previos

Antes de comenzar con la instalación, asegúrate de tener instalado:

- Python (v3.8 o superior)
- Docker y Docker Compose
- FFmpeg (para procesamiento de video)
- Entorno virtual de Python (recomendado)

## Siguientes pasos

- [Instalación](instalacion.md): Guía completa para configurar el backend
- [Arquitectura](arquitectura.md): Estructura detallada del proyecto

