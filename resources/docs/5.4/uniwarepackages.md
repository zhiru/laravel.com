# Pacotes Uniware

- [Instalação](#)
    - [Log-Viewer](#log-viewer)
    - [Laravel Modules](#laravel-modules)
    - [Instalando o Laravel](#installing-laravel)
    - [Configuração](#configuration)
- [Configuração do Servidor](#web-server-configuration)
    - [URLs Amigáveis](#pretty-urls)

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

<a name="laravel-modules"></a>
## Instalação do Laravel Modules

Aqui você irá ver como instalar o Laravel Modules, no qual iremos usar para criar os módulos da aplicação de forma separada estruturalmente (diretórios).

Link para o GitHub Original [nWidart/laravel-modules](https://github.com/nWidart/laravel-modules)  
Link para documentação original e completa [laravel-modules](https://nwidart.com/laravel-modules/v1/introduction)

[![Latest Version on Packagist](https://img.shields.io/packagist/v/nwidart/laravel-modules.svg?style=flat-square)](https://packagist.org/packages/nwidart/laravel-modules)
![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)
[![Build Status](https://img.shields.io/travis/nWidart/laravel-modules/1.0.svg?style=flat-square)](https://travis-ci.org/nWidart/laravel-modules)
[![Scrutinizer Coverage](https://img.shields.io/scrutinizer/coverage/g/nWidart/laravel-modules.svg?maxAge=86400&style=flat-square)](https://scrutinizer-ci.com/g/nWidart/laravel-modules/?branch=master)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/25320a08-8af4-475e-a23e-3321f55bf8d2.svg?style=flat-square)](https://insight.sensiolabs.com/projects/25320a08-8af4-475e-a23e-3321f55bf8d2)
[![Quality Score](https://img.shields.io/scrutinizer/g/nWidart/laravel-modules.svg?style=flat-square)](https://scrutinizer-ci.com/g/nWidart/laravel-modules)
[![Total Downloads](https://img.shields.io/packagist/dt/nwidart/laravel-modules.svg?style=flat-square)](https://packagist.org/packages/nwidart/laravel-modules)

| **Laravel**  |  **laravel-modules** |
|---|---|
| 5.4  | ^1.0  |
| 5.5  | ^2.0  |

`nwidart/laravel-modules` é um pacote do Laravel criado para gerenciar grandes aplicações usando módulos. Módulo é um como se fosse um pacote do laravel, possui as Models, Views e Controllers (MVC). Esse pacote é suportado e testado no Laravel 5 em diante.

Esse pacote é uma re-publicação, re-organizado e atualizada versão do pacote [pingpong/modules](https://github.com/pingpong-labs/modules), no qual não é mantido mais.

Uma das grandes melhorias que o pacote original não tem são os **tests**.

Descubra por que você deveria usar este pacote no artigo: [Writing modular applications with laravel-modules](https://nicolaswidart.com/blog/writing-modular-applications-with-laravel-modules).

### Composer

Para instalar pelo composer, execute o seguinte comando:

``` bash
composer require nwidart/laravel-modules
```

### Adicione o Provedor de Serviços (Service Provider)

Após a instalação, adicione os seguintes Provedores em `config/app.php`.

``` php
// config\app.php
'providers' => [
  Nwidart\Modules\LaravelModulesServiceProvider::class,
],
```

Depois, adicione os seguintes dados no array `aliases` no mesmo arquivo:

``` php
// config\app.php
'aliases' => [
  'Module' => Nwidart\Modules\Facades\Module::class,
],
```

Feito os passos anteriores, publique o arquivo de configuração executando o seguinte comando:

``` bash
php artisan vendor:publish --provider="Nwidart\Modules\LaravelModulesServiceProvider"
```

### Auto-carregamento dos modulos (Autoloading)

Por padrão as classes dos módulos não são carregadas automaticamente. Você pode carregar os módulos usando `psr-4`. Por exemplo:

``` json
// composer.json
{
  "autoload": {
    "psr-4": {
      "App\\": "app/",
      "Modules\\": "Modules/"
    }
  }
}
```

**Dica: não esqueça de executar o comando `composer dump-autoload` depois de instaldo**