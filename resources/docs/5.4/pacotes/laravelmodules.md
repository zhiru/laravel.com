# Pacotes

- [Instalação](#)
    - [Log-Viewer](/docs/{{version}}/pacotes/logviewer)
    - [Laravel Modules](/docs/{{version}}/pacotes/laravelmodules)
    - [Stolz Assets](/docs/{{version}}/pacotes/stolzassets)
    - [Collective HTML](/docs/{{version}}/pacotes/collectivehtml)
    - [Kodeine Laravel Acl](/docs/{{version}}/pacotes/laravelacl)
    - [Faker](/docs/{{version}}/pacotes/faker)
    - [Laravel DataTables](/docs/{{version}}/pacotes/laraveldatatables)
    - [Intervention Image](/docs/{{version}}/pacotes/interventionimage)

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