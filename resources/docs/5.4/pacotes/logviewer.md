# Pacotes

- [Instalação](#)
    - [Log-Viewer](/docs/{{version}}/pacotes/logviewer)
    - [Laravel Modules](/docs/{{version}}/pacotes/laravelmodules)
    - [Stolz Assets](/docs/{{version}}/pacotes/stolzassets)
    - [Collective HTML](/docs/{{version}}/pacotes/collectivehtml)
    - [Kodeine Laravel Acl](#kodeine-laravel-acl)
    - [Faker](#faker)
    - [Laravel DataTables](#laravel-datatables)
    - [Intervention Image](#intervention-image)

<a name="log-viewer"></a>
## Instalação do Log-Viewer

Aqui você irá ver como instalar o Log-Viewer, para ter uma forma melhor de ver os logs/erros gerados no projeto.

Link para documentação original [Log-viewer](https://github.com/ARCANEDEV/LogViewer)
  
### Requisitos do Servidor

O pacote LogViewer tem alguns requisitos:

    - PHP >= 5.6.4

### Requisitos da aplicação

LogViewer supora somente o modo diario de log, então tenha certeza que esteja configurado para `daily` ao invés de `single`:

```php
// config\app.php
return [
    ...

    /*--------------------------------------------------------------------------
     | Logging Configuration
     |--------------------------------------------------------------------------
     | Available Settings: "single", "daily", "syslog", "errorlog"
     */
    'log' => 'daily',

    ...
];
```

Laravel usa por padrão [Biblioteca Monolog](https://github.com/Seldaek/monolog). This gives you a variety of powerful log handlers/formatters to utilize.
 
### Compatibilidade das versões

| LogViewer                             | Laravel                                                                                                             |
|:--------------------------------------|:--------------------------------------------------------------------------------------------------------------------|
| ![LogViewer v4.2.x](https://img.shields.io/badge/version-4.2.*-blue.svg?style=flat-square) | ![Laravel v5.0](https://img.shields.io/badge/v5.0-supported-brightgreen.svg?style=flat-square) ![Laravel v5.1](https://img.shields.io/badge/v5.1-supported-brightgreen.svg?style=flat-square) ![Laravel v5.2](https://img.shields.io/badge/v5.2-supported-brightgreen.svg?style=flat-square) ![Laravel v5.3](https://img.shields.io/badge/v5.3-supported-brightgreen.svg?style=flat-square) |
| ![LogViewer v4.3.x](https://img.shields.io/badge/version-4.3.*-blue.svg?style=flat-square) | ![Laravel v5.4](https://img.shields.io/badge/v5.4-supported-brightgreen.svg?style=flat-square)

### Composer

Você pode instalar esse pacote pelo [Composer](http://getcomposer.org/) usando este comando: `composer require arcanedev/log-viewer`.

### No Laravel

#### Configuração
Assim que o pacote estiver instalado, você tem que  registrar no Provedor de Serviços (Service Provider) no `config/app.php` no array `providers`:

```php
// config\app.php
'providers' => [
    ...
    Arcanedev\LogViewer\LogViewerServiceProvider::class,
],
```
> Não precisa registrar a facade LogViewer, é realizado automagicamente :P

#### Comandos Artisan 

Para publicar os arquivos de traduções, use este comando:

```bash
php artisan log-viewer:publish
```
###### Para Forçar a publicação

```bash
php artisan log-viewer:publish --force
```

###### Publicar somente o arquivo de configuração

```bash
php artisan log-viewer:publish --tag=config
```

> Para forçar a publicação adicione a flag `--force`.

###### Publicar somente as traduções

```bash
php artisan log-viewer:publish --tag=lang
```

> Para forçar a publicação adicione a flag `--force`.

###### Requisitos da aplicação e checar os arquivos de log

```bash
php artisan log-viewer:check
```
## Feito !

Acesse `http://{your-project}/log-viewer` (Veja [Configuration](https://github.com/ARCANEDEV/LogViewer/wiki/3.-Configuration) para alterar a URI e outras coisas).
