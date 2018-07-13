# SISTEMA ESCOLAR
### En este apartado encontrara todo el proceso de creación del sistema denominado "SISTEMA ESCOLAR", incluyendo todos los pasos utilizados en la codificación y demas recursos utilizados.

> “Hablar es barato. Enséñame el código.”

## Consideraciones a tener en cuenta:

El desarrollo que a continuación llevaremos acabo utilizando lo siguiente:

Diversos marcos de trabajo implementan el patrón de arquitectura Modelo-Vista-Controlador (MVC). Cada marco de trabajo tiene sus detalles finos. Veamos a grandes rasgos la forma en que Laravel hace su implementación de MVC.

Laravel es un marco de trabajo o framework para PHP que ha adquirido una gran popularidad por su arquitectura y estabilidad, y cuyas herramientas están cuidadosamente ensambladas para agilizar el trabajo de desarrollo. Su filosofía propone que los desarrolladores se conviertan en artesanos web trabajando con finura y con clase. Al tomar lo mejor de los demás marcos de trabajo, su estructura se vuelve ágil, su sintaxis elocuente, y sus herramientas para generar código, fundamentales para el desarrollo. Todo ello convierta a Laravel en una excelente opción tanto para el desarrollador novato como para el veterano.

### Qué es Composer y cómo usarlo

¿Así que no sabes qué es Composer? A mi también me pasó cuando empecé a estudiar Laravel, no entendía que era Composer, no entendía porqué necesitaba instalar eso en mi computadora, para qué era necesario, que era eso de “vendor”, ¿Composer.json? En este primer post te explicaré todos esos puntos que una vez trataron de complicarme la existencia.

El asunto está así: PHP ha tenido algunos cuantos problemas en el mundo de la descarga de paquetes/librerías, para hacer eso tenías que ir a la web (si es que tenía) de alguna librería y buscar la sección de “Descargas” para poder utilizarla; sin contar con el hecho que para hacer eso en algunas ocasiones necesitabas registrarte a la página; programadores PHP se quejaban de que no existía algo como npm para Node.js o bundler para Ruby. Bien, ahora existe, se llama Composer y podría considerarse una de las maravillas del mundo de PHP.

#### Composer es un manejador de dependencias.

– ¿Manejador de qué?

Composer es un manejador de dependencias, no un gestor de paquetes. Pero es cierto que trata con paquetes y librerías, la instalación siempre es local para cualquier proyecto, las librerías se instalan en un directorio por defecto (normalmente es /vendor). Composer es capaz de instalar las librerías que requiere tu proyecto con las versiones que necesiten. ¿Y si mis librerías dependen de otras? También es capaz de resolver eso y descargar todo lo necesario para que funcione y así quitarnos del dolor de cabeza de hacer todo eso de forma manual.

#### ¿Qué problemas resuelve Composer?

Tienes un proyecto que depende de ciertas librerías desarrolladas por terceros, y a su vez, éstas librerías también dependen de otras (tú no tienes porqué conocer estas librerías), lo que hace Composer en este caso es averiguar que librerías deben instalarse; es decir, resuelve todas las dependencias indirectas y descarga automáticamente la versión correcta de cada paquete.

[En https://packagist.com puedes ver todo los paquetes privados (de pago) que hay disponibles con Composer](https://packagist.com/)

[y en https://packagist.org los que son gratuitos.](https://packagist.org/)

#### ¿Cómo instalo Composer?

La instalación de Composer es muy sencilla, si estás en Linux o Mac es sólo ejecutar dos comandos en la terminal:

```bash
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```
El primer comando descarga Composer a tu computador y el segundo lo mueve al directorio para que lo puedas ejecutar globalmente usando $ composer desde cualquier carpeta, de lo contrario necesitarías siempre referenciar al archivo con la ruta completa, por ejemplo algo como: ~/Downloads/composer.phar.

Y si estás en Windows, tienes un [instalador de Composer ejecutable](https://getcomposer.org/Composer-Setup.exe). No, no es un virus. Aquí tienes las instrucciones detalladas para [instalar Composer en tu plataforma favorita](https://getcomposer.org/doc/00-intro.md).

#### Comandos disponibles con Composer

Si eres un programador Ruby entonces debes de estar familiarizado con el archivo Gemfile, o si eres de Node.js con package.json; bueno, estos son los comandos que puedes utilizar con composer:

```bash
$ composer about
$ composer archive
$ composer browse
$ composer clear-cache
$ composer config --list
$ composer create project laravel/laravel
$ composer depends vendor/package
$ composer diagnose
$ composer dump-autoload --optimization
$ composer global
$ composer help
$ composer init
$ composer install
$ composer licenses
$ composer list
$ composer remove
$ composer require vendor/package
$ composer run-script
$ composer search my keywords
$ composer self-update
$ composer show
$ composer status
$ composer update
$ composer validate
```
Ahora explicaré brevemente algunos comandos.

```bash
$ composer init
```

Al ejecutar este comando solicitará cierta información que servirá para crear el archivo composer.json, este lo explicaré en el siguiente tutorial, solo mencionaré que la información requerida es básica para el archivo, como el nombre del paquete, descripción, autor(es), página del proyecto, y las dependencias. No te preocupes, te explicaré detalladamente qué es cada uno de estos datos.

```bash
$ composer install
```

Este comando procesa el archivo composer.json y resuelve las dependencias, normalmente las instala en un directorio llamado /vendor, pero podemos especificar cualquier otro.

```bash
$ composer update
```

Actualiza las dependencias de tu proyecto a la última versión y también actualiza el archivo composer.lock Esto se puede hacer de varias maneras, imagina que solo quieres actualizar un dependencia en específico, para hacer eso tienes que indicar el nombre del paquete, de la siguiente manera:

```bash
$ composer update vendor/package another-vendor/another-package vendor-x/package-x
```

Esto solo actualizará las dependencias especificadas, si quieres actualizar todas las dependencias de un cierto paquete puede ahorrar muchos carateres utilizando un comodín *, de la siguiente manera:

```bash
$ composer update vendor-x/*
```

El comando require instala las dependencias especificadas, este lo explicaré más detalladamente en el siguiente tutorial, la sintaxis es la siguiente:

```bash
$ composer require vendor/package:*
```

El comando search busca el paquete indicado en Packagist, solo tienes que pasarle el nombre del paquete.

```bash
$ php composer search monolog
```

El comando show muestra los paquetes disponibles y también puedes ver los detalles de un paquete en específico. Basta con pasarle un argumento, este tiene que ser el nombre del paquete:

```bash
$ php composer show vendor/package
```

Desplegará información como: el nombre del paquete, versiones, el tipo de paquete, el código fuente, el zip del código fuente, licencia, etc.

El comando depends muestra la lista de paquetes de los cuales depende el paquete indicado. Sí, me estoy refiriendo a las librerías de terceros. Muestra los paquetes de tipo require y require-dev

```bash
$ php composer depends vendor/package
```

Para asegurarnos que nuestro archivo composer.json está escrito correctamente y que alguno no tendrá errores al descargarlo y tampoco tener problemas al instalar las dependencias, como algún caracter mal escrito, podemos utilizar el comando validate para verificar que todo está correctamente bien.

```bash
$ php composer validate
```

Si a menudo realizas cambios en tus dependencias y las has instalado mediante el código fuente del repositorio, el comando status te permite comprobar si has hecho cambios en alguna de ellas, así como el git status nos indica qué archivos hemos modificado, este comando funciona de la misma manera:

```bash
$ php composer status -v
```

Si añadimos la opción -v nos brinda información más detallada sobre los cambios producidos.
You have changes in the following dependencies:
vendor/seld/jsonlint:
M README.mdown

El comando self-update actualiza el propio Composer a la versión más reciente, no tienes que realizar ningún otro paso más escribir en la consola lo siguiente:

```bash
$ php composer self-update
```

Y listo, tendrás disponible la versión más actualizada del manejador. ¿Lindo, no?

El comando config te permite editar varias opciones de Composer, tanto en el archivo local del proyecto como en el archivo global.

```bash
$ php composer config --list
```

El comando create-project crea un nuevo proyecto, es necesario pasar como parámetros el vendor y package correspondiente. Esto es lo mismo que descargar el proyecto y después ejecutar el archivo composer.json que venga en él, el siguiente ejemplo crea un proyecto de laravel.

```bash
$ php composer create-project laravel/laravel mi-proyecto
```

Ahora, si necesitas actualizar tu archivo autoloader porque tienes nuevas clases puedes hacerlo con el comando dump-autoload, es como ejecutar install o update, pero la ventaja es que puedes especificar que se cree un arreglo de todas las clases del proyecto con sus respectivos archivos, de la siguiente manera:

```bash
$ php composer dump-autoload --optimize
```

El comando run-script permite ejecutar manualmente alguno de los scripts definidos por algún paquete.

```bash
$ php composer run-script nombre-script --no-dev
```

Hemos agregado –no-dev para desactivar el modo de desarrollo.

Utiliza el comando help para ver información sobre el comando solicitado.

```bash
$ php composer help install
```

El comando remove sirve para eliminar alguna dependencia que ya no utilicemos, de la siguiente manera:

```bash
$ php composer remove vendor/package
```


> “Los que pueden, lo hacen; los que no, sólo saben quejarse.”

**_[@intelguasoft](https://twitter.com/Intelguasoft)_**