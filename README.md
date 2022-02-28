
# Makefile for CraftCMS 3 Development

### Este Makefile provee un entorno de desarrollo basado en Webpack, Babel, PostCSS, y SASS, sobre Laravel Mix optimizado para desarrollo en CraftCMS 3. 

### Incluye:
* Make command para descargar y configurar una [instancia local de CraftCMS 3](https://craftcms.com/).
* Make command para descargar y configurar la [base de código de template para CraftCMS 3](https://github.com/anuarhdz/craftcms-template).
* Make command para configurar y ejecutar [Laravel Mix](https://laravel-mix.com), [Webpack](https://webpack.js.org/), Babel, SASS y otros.



## Requerimientos

Este repositorio asume que cuentas con los siguientes requerimientos:

* Servidor local configurado para trabajar con virtual hosts. Si trabajas con MAMP, XAMPP o algún software parecido, verifica que [Composer use la misma versión e instalación de PHP de tu servidor local](https://craftcms.com/knowledge-base/mamp-with-composer-and-mysql-on-the-command-line/). 
* PHP 7.2.5+ o superior.
* Composer instalado globalmente.
* NodeJS / NPM.
* Git clone - SSH.

### Mi local development setup

Al momento de crear este makefile, mi entorno de desarrollo local se basa en:

* macOS Monterey 12.1 - Macbook Air (M1, 2020)
* PHP 8.1.2
* Laravel Valet 2.18.9 - Laravel V8
* NVM 0.38.0
* Node 14.17.3
* NPM 6.14.13

### CraftCMS 3 Setup

Este setup de CraftCMS 3 instala automáticamente algunos plugins al ejecutar `make init`:
* [Craft Mix](https://github.com/mister-bk/craft-plugin-mix) (Requerido)
* [Minify](https://github.com/nystudio107/craft-minify) (Requerido)
* [Redactor](https://github.com/craftcms/redactor) (Opcional)
* [SEO](https://github.com/ethercreative/seo) (Opcional)


## Instalación

Descarga el código de este repositorio o ejecuta el siguiente comando en terminal: `git clone git@github.com:anuarhdz/makefile.git ./your/project/path && cd /your/project/path`. A continuación, continua con los comandos del makefile.

**Nota:** Para más información de los comandos de la terminal sugeridos, consulte la [referencia de comandos](#referencia-de-comandos-de-la-terminal).

## Referencia de comandos de la terminal

Es requerido ejecutar los comandos `make init`, `make template` y `make webpack` (o `make webpack-ssl`) la configuración inicial por cada proyecto a configurar.

## Instalación con un solo comando

Al ejecutar `make` o `make all` en el directorio donde previamente clonó o descargó este repositorio, se ejecutarán uno a uno cada uno de los comandos de configuración de este setup. En algunos pasos se requerirá que capture información (Craft CMS 3 setup), por lo que la captura de dicha info es importante para que los comandos de make se ejecuten adecuadamente. 

Si desea configurar este entorno de desarrollo paso a paso, a continuación se describe la función de cada comando:

1. `make init` hace el setup de CraftCMS 3 y plugins recomendados mediante [Composer](https://getcomposer.org). Debe tener lista una base de datos compatible. **Continue hasta la finalización de la instalación de CraftCMS mediante terminal.**

2. `make template` configura el boilerplate adaptado al workflow de desarrollo sobre CraftCMS, es decir, la base de código de JS, SASS, imágenes, fonts y favicon, así como la estructura de un template de Twig.

3. `make webpack-mix` instala todas las dependencias de `npm` y dejará la base de código lista para funcionar.

**Nota:** Verifique que su archivo `.env` contenga la variable `PRIMARY_SITE_URL` con su virtual host como valor. Si no lo tiene, añadalo. Es importante para el correcto funcionamiento del entorno. 

**Los siguientes comandos serán utilizados durante el desarrollo:**

4. `make mix-dev` creando una instancia de Browsersync de su virtual host.

5. `make mix-staging` compilará assets para staging.

6. `make mix-prod` compilará assets para production.

**Organización del setup**

El setup completo del entorno debe verse de la siguiente forma:

```shell
├── .babelrc
├── .env
├── .env.example
├── .gitignore
├── Makefile
├── README.md
├── bootstrap.php
├── composer.json
├── composer.lock
├── config
│   ├── app.php
│   ├── db.php
│   ├── general.php
│   ├── htmlpurifier
│   ├── license.key
│   ├── mix.php
│   ├── project
│   ├── redactor
│   └── routes.php
├── craft
├── modules
│   └── Module.php
├── node_modules
│   └── ...
├── package-lock.json
├── package.json
├── src
│   ├── css
│   │    ├── main.scss
│   │    ├── base
│   │    │   ├── base.scss
│   │    │   ├── mixins.scss
│   │    │   ├── variables.scss
│   │    │   └── resets
│   │    │         ├── normalize.scss
│   │    │         ├── reset.local.scss
│   │    │         └── typography.scss
│   │    ├── components
│   │    │   ├── header.scss
│   │    │   ├── loading.scss
│   │    │   └── footer.scss
│   │    ├── layout
│   │    │   └── containers.scss
│   │    ├── pages
│   │    │   └── ...
│   │    ├── shared
│   │    │   └── buttons.scss
│   │    │   └── typography.scss
│   │    └── utils
│   │        └── ...
│   ├── favicon
│   ├── fonts
│   ├── images
│   └── js
│        └──main.js
│        └──stickyNav.js
│    
│  
├── storage
│   ├── .gitignore
│   ├── config-deltas
│   ├── logs
│   └── runtime
├── templates
│   ├── _components
│   │    └── ...
│   ├── _critical
│   │    └── ...
│   ├── _layouts
│   │    └── ...
│   ├── _meta
│   │    └── ...
│   ├── _snippets
│   │    └── ...
│   └── index.twig
├── vendor
│   └── ...
├── web
│   ├── .htaccess
│   ├── assets
│   ├── cpresources
│   ├── index.php
│   └── web.config
└── webpack.mix.js
```
La carpeta raíz del proyecto debe contener la instalación de CraftCMS con la distribución de nombres original. Además, contendrá el directorio `./src` donde se crearán los archivos de desarrollo, así como assets y fonts.

Deberá configurar su servidor local para que su virtual host apunte a `./web` como cualquier instalación de CraftCMS. 

## Flujo de trabajo de desarrollo en proyectos con CraftCMS 3

Este boilerplate contempla algunos escenarios especificos durante el proceso de desarrollo en CraftCMS 3. 

* Desarrollo desde cero.
* Continuación de desarrollo luego de un `git pull`.

## Desarrollo desde cero en CraftCMS 3

* Ejecute en el orden establecido los comandos mencionados en la sección [Referencia de comandos de la terminal](#referencia-de-comandos-de-la-terminal).

## Development continuation from `git pull`

Si configurará por primera vez un proyecto desde `git pull`:

1. Haga pull del repositorio del proyecto en su servidor local. 
2. Importe su backup de la base de datos.
3. Configure el archivo `.env` en el directorio raíz del proyecto. [Puede usar este ejemplo como base](https://gist.github.com/anuarhdz/c802cf373fcc5f8de2f2e480190a4e02).
4. Configure el archivo `general.php` dentro de `./config`. [Puede usar este ejemplo como base](https://gist.github.com/anuarhdz/ec96fc0a20a64aff81d73e7ed28de530).
5. Ejecute `composer update` en la carpeta raíz del proyecto.
6. Ejecute `php craft setup/welcome` o `./craft setup/welcome` en la carpeta raíz del proyecto para configurar CraftCMS en base al `.env`. 
7. Verifique que su archivo `.env` contenga la variable `PRIMARY_SITE_URL` con su virtual host como valor. Si no lo tiene, añadalo. Es importante para el correcto funcionamiento del entorno. 
8. Ejecute `make setupnpm` para instalar todas las dependencias de npm y webpack / laravel mix. Luego de este paso, podrá usar los comandos `make work`, `make staging` o `make prod` para desarrollar. 


## Critical CSS

Para crear una base CSS crítica correcta, indique cada una de las URL del sitio y el nombre de la plantilla que muestra esa página en el CMS.

```
.criticalCss({
    enabled: mix.inProduction(),
    paths: {
        base: SITE_URL_PROXY,
        templates: './templates/_critical/',
        suffix: '-critical.min'
    },
    urls: [
        {
            url: '/',
           template: 'index'
        }
    ],
    options: {
        minify: true,
        width: 1440,
        height: 1200,
    },
})
```
Todo el CSS crítico solicitado se calculará y compilará ejecutando el comando `make mix-prod`.



---

MIT License

Copyright (c) 2022 Anuar Reyes

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
