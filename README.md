# Taller de n8n + WordPress utilizando Docker
En este repositorio encontrarás un ejemplo de cómo integrar n8n con WordPress utilizando Docker. n8n es una herramienta de automatización de flujos de trabajo que permite conectar diferentes aplicaciones y servicios, mientras que WordPress es un sistema de gestión de contenido ampliamente utilizado.

## Requisitos previos
Antes de comenzar, asegúrate de tener instalado lo siguiente en tu máquina:
- Docker Desktop: [Instalación de Docker](https://www.docker.com/products/docker-desktop/)
- VS Code: [Instalación de VS Code](https://code.visualstudio.com/download)
- Necesitarás un terminal para activar los contenedores de Docker `PowerShell` o `CMD` en Windows, o `Terminal` en macOS/Linux.
- Clonar el proyecto desde GitHub utilizando el siguiente comando:
```bash
git clone https://github.com/taller-n8n-wordpress-docker.git
```

## Comandos para levantar los contenedores
Para levantar los contenedores de n8n y WordPress:
```bash
cd taller-n8n-wordpress-docker
docker-compose up -d
```

Para detener los contenedores:
```bash
docker-compose down
```

## Acceder a n8n y WordPress
- n8n estará disponible en [http://localhost:5678](http://localhost:5678)
- WordPress estará disponible en [http://localhost:8080](http://localhost:8080)

## Configuración de WordPress en el fichero `docker-compose.yml`
Necesitamos que se pueda acceder a `Contraseña de aplicación` dentro de WordPress para conectar n8n con WordPress.
Es necesario habilitar el modo depuración de WordPress porque no tenemos activo el HTTPS. 
Para ello en `WORDPRESS_CONFIG_EXTRA` y agregamos `define( 'WP_ENVIRONMENT_TYPE', 'local' );`.
```yaml
services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass123
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_CONFIG_EXTRA: |
        define( 'WP_DEBUG_LOG', true );
        define( 'WP_DEBUG_DISPLAY', false );
        @ini_set( 'display_errors', 0 );
        define( 'SCRIPT_DEBUG', true );
        define( 'WP_ENVIRONMENT_TYPE', 'local' );
```