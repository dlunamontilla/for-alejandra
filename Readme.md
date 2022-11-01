# Instalación de proyectos

## Instalación de Goffice

Ver [reporte técnico de actividades](docs/Report.md "Ir a reporte técnico de actividades")

## Instalación del proyecto

Antes de empezar a instalar el proyecto, se debe clonar.

### Clonación del proyecto

Para clonar el proyecto debe escribir la siguiente línea en la terminal:

```bash
git clone git@github.com:goffice24/goffice-new.git
```

Si utilizas SSH.

Si utilizas HTTPS, debes escribir lo siguiente:

```bash
git clone https://github.com/goffice24/goffice-new.git
```

### Instalación de dependencias

Para instalar las dependencias se recomienda utilizar **PHP 7** y `composer 1.8.6`, de lo contrario, devolverá excepciones.

> **Importante:** no es compatible con PHP 8.

Para instalar las dependencias debe escribir la siguiente línea:

```bash
composer install
```

### ¿Qué hacer en caso de que su versión de composer no sea la indicada?

Debe seguir [este enlace](https://getcomposer.org/download/1.8.6/composer.phar "Descargar composer 1.8.6") para proceder a descargarlo y colocarlo en su proyecto local para correrlo de la siguiente forma:

```bash
php composer.phar install
```

De esa forma habrá instalado todas las dependencias.

## Configurar la basse de datos

Copie el archivo `.env.example` a `.env` y actualilice los parámetros de conexión.

## Correr el proyecto

.
Para correr el proyecto, solo debe escribir el siguiente comando:

```php
composer run server
```

> **Importante:** el comando anterior solo va a correr la versión de PHP que tiene instalado en su computador. Tome en cuenta que debe correr el proyecto con **PHP 7**

Después de que el proyecto esté corriendo, puede abrirlo mediante el siguiente enlace:

-   [Host local](http://localhost:8000 "Va a correr en localhost con el puerto 8000").
