# Pacotes Uniware

- [Instalação](#)
    - [Log-Viewer](#log-viewer)
    - [Laravel Modules](#laravel-modules)
    - [Stolz Assets](#stolz-assets)
    - [Collective HTML](#collective-html)
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

<a name="stolz-assets"></a>
## Instalação do Stolz/Assets

Aqui você irá ver como instalar o Stolz/Assets, que é um gerenciador de Assets ultra simples.

Link para documentação original [Stolz/Assets](https://github.com/Stolz/Assets)

<a id="stolz-assets-instalacao"></a>
### Instalação

Na raiz do seu projeto execute:

	composer require stolz/assets

Então edite o arquivo `config/app.php` e adicione o provedor de serviço (Service Provider) no array `providers`.

	// config/app.php
	'providers' => [
		//...
		'Stolz\Assets\Laravel\ServiceProvider',
		//...
	],


Não precisa adicionar o Facade, o pacote irá vincular para você no IoC.

<a id="stolz-assets-comousar"></a>
### Como usar

<a id="stolz-assets-views"></a>
#### Na suas Views/Layouts

Para gerar as tags CSS `<link rel="stylesheet">`

	echo Assets::css();

Para gerar as tags JavaScript `<script>`

	echo Assets::js();

<a id="stolz-assets-rotascontroladores"></a>
#### Nas suas Rotas/Controladores

Basicamente tudo que o você tem que fazer para adicionar um asset, não importa se é uma coleção de CSS, de JS ou os dois, exemplo: 

	Assets::add('filename');

> Para usos mais avançados continue lendo, porém alguns métodos não estão documentados aqui. Para **uma lista completa de todos os métodos disponíveis** por favor leia o arquivo [`API.md`](https://github.com/Stolz/Assets/blob/master/API.md)

Adicione mais de um asset de uma vez

	Assets::add(['another/file.js', 'one/more.css']);

Adicione um asset do seu pacote local

	Assets::add('twitter/bootstrap:bootstrap.min.css');

Nota-se que todos seus arquivos que serão usados como assets, os caminhos relativo dos diretórios (configurado nas suas opções `css_dir` e `js_dir`), ou seja, você não precisa ficar informando os caminhos/diretórios todas as vezes como `js/file.js` e `css/file.css`, bastaria apenas `file.js` e `file.css`.

Talvez você queira adicionar assets do mesmo jeito:

	Assets::add('//cdn.example.com/jquery.js');
	Assets::add('http://example.com/style.css');

Se seus assets não tem extensão ou a auto-detecção falhe, então use as funções canônicas *(Eles aceitam arrays de assets também)* 

	Assets::addCss('CSSfile.foo');
	Assets::addJs('JavaScriptFile.bar');

Se em algum momento você decidir que precisa resetar seus assets, use:

	Assets::reset();    // Reseta os dois CSS e JS
	Assets::resetCss(); // Reseta somente CSS
	Assets::resetJs();  // Reseta somente JS

Todos os métodos enquanto não gerarem a saída, aceitam encadeamento:

	Assets::reset()->add('collection')->addJs('file.js')->css();

<a id="stolz-assets-configuração"></a>
#### Configurações

Para publicar as configurações, execute o comando:

	php artisan vendor:publish

Isto irá criar o arquivo `config/assets.php` que você irá usar para configurar este pacote. Com comentários em todas as opções sendo auto explicativo.

Se você não está usando [uma interface não estática](#stolz-assets-naoestatica) somente informe um array associativo de configurações para o construtor da classe.

<a id="stolz-assets-colecoes"></a>
#### Coleções

Uma coleção é o nome de um grupo de assets, isto é, um grupot de arquivos de JavaScript e CSS. Qualquer coleção pode incluir mais coleções, permitindo definições de dependencias e agrupamento/ninho de coleções. Coleções podem ser criadas durante o momento de execução ou pelo arquivo config.

Para registrar uma coleção no momento de execução da aplicação para uso posterior, use:

	Assets::registerCollection($collectionName, ['some', 'awesome', 'assets']);

Para pré-configurar uma coleção pelo arquivo de configuração:

	// ... File: config/assets.php ...
	'collections' => [
		'one'	=> 'one.css',
		'two'	=> ['two.css', 'two.js'],
		'external'	=> ['http://example.com/external.css', 'https://secure.example.com/https.css', '//example.com/protocol/agnostic.js'],
		'mix'	=> ['internal.css', 'http://example.com/external.js'],
		'nested' => ['one', 'two'],
		'duplicated' => ['nested', 'one.css','two.css', 'three.js'],
	],

Abaixo segue exemplos de coleções em diferentes cenários:

Usando `Assets::add('dois');` irá resultar em

	<!-- CSS -->
	<link type="text/css" rel="stylesheet" href="css/two.css" />
	<!-- JS -->
	<script type="text/javascript" src="js/two.js"></script>

Usando `Assets::add('externo');` irá resultar em

	<!-- CSS -->
	<link type="text/css" rel="stylesheet" href="http://example.com/external.css" />
	<link type="text/css" rel="stylesheet" href="https://secure.example.com/https.css" />
	<!-- JS -->
	<script type="text/javascript" src="//example.com/protocol/agnostic.js"></script>

Usando `Assets::add('mixado');` irá resultar em

	<!-- CSS -->
	<link type="text/css" rel="stylesheet" href="css/internal.css" />
	<!-- JS -->
	<script type="text/javascript" src="http://example.com/external.js"></script>

Usando `Assets::add('aninhado');` irá resultar em

	<!-- CSS -->
	<link type="text/css" rel="stylesheet" href="css/one.css" />
	<link type="text/css" rel="stylesheet" href="css/two.css" />
	<!-- JS -->
	<script type="text/javascript" src="js/two.js"></script>

Usando `Assets::add('duplicado');` irá resultar em

	<!-- CSS -->
	<link type="text/css" rel="stylesheet" href="css/one.css" />
	<link type="text/css" rel="stylesheet" href="css/two.css" />
	<!-- JS -->
	<script type="text/javascript" src="js/two.js"></script>
	<script type="text/javascript" src="js/three.js"></script>

Note que neste último exemplo de coleção tem assets "duplicados", porém ele foi exibido uma unica vez.

<a id="stolz-assets-pipeline"></a>
#### Pipeline

Para habilitar pipeline use a opção `pipeline` no arquivo de configuração

	'pipeline' => true,

Uma vez habilitado todos seus assets serão concatenados e minificados em um único arquivo, melhorando a velocidade de carregamento e reduzindo o número de requisições que seu navegador irá fazer.

Este proceso pode demorar alguns segundos dependendo da quantidade de assets e de sua conexão, porém somente é usada na primeira vez que você carregar a página, quando nunca foi usado antes. As próximas vezes subsequentes na mesma página (ou qualquer página que você use os mesmo assets) que é carregada. Os arquivos prévios em pipeline serão carregados muito mais rápidos e com menos consumo de banda.

**Nota:** Por razões óbvias, usar o pipeline é recomendado somente para o ambiente de produção.

Se seus assets mudaram desde a última vez que foram gerados pelo pipeline, use o comando a seguir para remover o cache e o arquivo do pipeline

	php artisan asset:flush

Alternativamente, você pode setar a configuração do `pipeline` em um valor em string como `true`, que irá gerar um hash que será usado como validador. Se vocẽ setar como `auto` o hash será calculado automaticamente baseado na última modificação que você fez nos seus assets. 

Exemplo:

	'pipeline' => 'version 1.0',

Finalmente, se você usa NGINX com [gzip_static](http://nginx.org/en/docs/http/ngx_http_gzip_static_module.html) 
habilitado, adicione a seguinte configuração para automaticamente criar uma versão gzipada dos seus assets em pipeline:

	'pipeline_gzip' => true,

<a id="stolz-assets-options"></a>
#### Outras opções de configuração

Para uma **Lista completa com todas as opções** por favor leia [`API.md`](https://github.com/Stolz/Assets/blob/master/API.md)

`// config/assets.php`
- `'autoload' => [],`

    Acima você verá quais assets (Arquivos CSS, JavaScript ou coleções) vão ser carregadas por padrão.

`// config/assets.php`    
- `'css_dir' => 'css',`
- `'js_dir' => 'js',`

	Substitua a URL/Pasta padrão para seus assets. **Não use barras invertidas!** Eles serão vinculados a todos os seus assets locais. Tanto caminhos relativos como absolutos são aceitos.

`// config/assets.php`
- `'pipeline_dir' => 'min',`

	Substitua a pasta padrão para os assets que irão ser canalizados/unificados. **Não use barras invertidas!**

É possível **configurar ou realizar qualquer alteração enquanto é executado (on the fly)** passando um array de configurações par ao método `config()`. 
Usado quando alguns dos seus assets usam um diretório base diferente ou se você quer mudar e usar outros assets do que o padrão que será canalizado, exemplo:

	echo Assets::reset()->add('do-not-pipeline-this.js')->js(),
	     Assets::reset()->add('please-pipeline-this.js')->config(['pipeline' => true])->js();

<a id="stolz-assets-multitenancy"></a>
#### Múltiplas Configurações "Multitenancy"

**Nots:** *Esse recurso só está disponível para o Laravel> = 5.0*.

"Multitenancy" pode ser alcançado usando o agrupador de configurações. Um grupo é um container de configurações isolado. Cada grupo é totalmente independente do outro grupo, tendo suas próprias configurações. Não se esqueça que é sua responsabilidade que cada grupo seja carregado na ordem correta.

Por padrão cada grupo é definido como o grupo `default`. Se nenhum grupo foi definido por padrão então este será usado. Para definir um grupo somente crie um array com o nome do grupo e as configurações do memso como um array, sendo o nome do grupo como index. Por exemplo:

	// ... File: config/assets.php ...

	// Grupo por padrão
	'default' => [
		'pipeline' => true,
		'js_dir' => 'js',
		// ... mais opções do grupo padrão
	],

	// Outro grupo
	'groupo1' => [
		'pipeline' => false,
		'public_dir' => '/foo',
		// ... mais opções do grupo1
	],

	// Outro grupo
	'groupo2' => [
		'pipeline' => false,
		'css_dir' => 'css/admin',
		// ... mais opções do grupo2
	],

Para escolher qual grupo você irá interagir, use o método `group()`. Se não há um grupo definido, por padrão será usado o "default".

	Assets::add('foo.js')->js(); // Usa o grupo default
	Assets::group('group1')->add('bar.css')->css(); // Usa o grupo "grupo1".

Atente-se o método `group()` faz parte da Facade, ou seja, não aceita encadeiamento de métodos, sempre tem que ser usado no começo da interação com a bilbioteca.

----

<a id="stolz-assets-naoestatica"></a>
### Interface não estática

Você pode usar a biblioteca sem usar métodos estáticos. A assinatura de todos os métodos é a mesma descrita acima, mas usando o instanciamento da classe ao invés:

	// Carrega a biblioteca com o composer
	require __DIR__ . '/vendor/autoload.php';

	// Seta as opções de configuração
	$config = [
		'collections' => [...],
		'autoload' => [...],
		'pipeline' => true,
		'public_dir' => '/absolute/path/to/your/webroot/public/dir'
		...
	];

	// Instancia a biblioteca
	$assets = new \Stolz\Assets\Manager($config);

	// Adiciona alguns assets
	$assets->add('style.css')->add('script.js');

	// Gera as tags HTML
	echo $assets->css(),$assets->js();

----

<a id="stolz-assets-exemplos"></a>
## Exemplos de coleções

	// jQuery (CDN)
	'jquery-cdn' => ['//ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js'],

	// jQuery UI (CDN)
	'jquery-ui-cdn' => [
		'jquery-cdn',
		'//ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/jquery-ui.min.js',
		// Uncomment to load all languages '//ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/i18n/jquery-ui-i18n.min.js',
		// Uncomment to load a single language '//ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/i18n/jquery.ui.datepicker-es.min.js',
		// Uncomment to load a theme' //ajax.googleapis.com/ajax/libs/jqueryui/1.11.4/themes/smoothness/jquery-ui.min.css',
	],

	// Zurb Foundation (CDN)
	'foundation-cdn' => [
		'jquery-cdn',
		'//cdn.jsdelivr.net/foundation/5.5.1/css/normalize.css',
		'//cdn.jsdelivr.net/foundation/5.5.1/css/foundation.min.css',
		'//cdn.jsdelivr.net/foundation/5.5.1/js/foundation.min.js',
		'app.js'
	],

	// Twitter Bootstrap (CDN)
	'bootstrap-cdn' => [
		'jquery-cdn',
		'//netdna.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css',
		'//netdna.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap-theme.min.css',
		'//netdna.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js'
	],

	// Flags of all countries in one sprite (CDN)
	'flags-16px' => ['//cloud.github.com/downloads/lafeber/world-flags-sprite/flags16.css'],
	'flags-32px' => ['//cloud.github.com/downloads/lafeber/world-flags-sprite/flags32.css'],

<a id="stolz-assets-faq_folders"></a>
#### Onde eu devia copiar meus arquivos de assets?

Você deve copiar as sub pastas que você especificou na oções `css_dir` e `js_dir` da configuração. As duas configurações são relativas ao caminho da pasta "raiz/public". Paraca cada pacote de assets vale o mesmo, mas relativo a pasta do `pacote` com sua pasta "raiz/public".  

Exemplo, assumindo este cenário:

- Você está usando as configurações padrões.
- Por exemplo a pasta raiz/public do é `/caminho-do-seu-projeto/public`  
- Sua pasta raiz/public contém:
    - /caminho-do-seu-projeto/public/css/foo.css
    - /caminho-do-seu-projeto/public/js/bar.js
    - /caminho-do-seu-projeto/public/packages/vendor1/pacotex/css/lorem.css
    - /caminho-do-seu-projeto/public/packages/vendor2/pacotey/js/ipsum.js

Então eles devem ser carregadas no seu assets como:

	Assets::add([
		'foo.css',
		'bar.js',
		'vendor1/pacotex:lorem.css',
		'vendor2/pacotey:ipsum.js'
	]);

<a id="stolz-assets-faq_base"></a>
#### Por que meus assets funcionam na página principal mas não nas páginas internas?

Se seus assets funcionando por exemplo para a url <http://example.com> mas não para <http://example.com/some/other/place> você provavelmente está usando links relativos. Se você está usando links relativos para sua URI raiz você terá que usar a tag [`<base>`](http://www.w3.org/TR/html4/struct/links.html#h-12.4), apontando para sua URI raiz. Esse comportamento não é relacionado a biblioteca ou ao framework, mas ao [pardão do HTML](http://www.w3.org/TR/html401/struct/links.html#h-12.4.1). Por favor tenha certeza que você entende sobre [a semantica dos links relativos](http://tools.ietf.org/html/rfc3986#section-4) antes de reportar um bug.

<a id="stolz-assets-faq_pipeline"></a>
#### O pipeline não está funcionando

Tenha certeza que sua opção `public_dir` na configuração esteja apontando para o caminho **absoluto** baseado na pasta "raiz"/public e que o usuário que vai executar a biblioteca tenha permissões de escrita para esta pasta.

If you use a massive amount of assets make sure your connection is fast enough and your computer is powerful enough to download and compress all the assets before the PHP maximum execution time is reached.

<a id="stolz-assets-faq_config_on_the_fly"></a>
#### Posso usar várias instancias da biblioteca?

Sim você pode, mas não há motivos para o mesmo. talvez seja melhor usar [multitenancy](#stolz-assets-multitenancy) (*Disponível apenas para Laravel> = 5.0*). 
Yes you can but there is no need. You better use the 

<a id="stolz-assets-faq_instances"></a>
#### Posso alterar as configurações me tempo de execução (on the fly)?

Sim você pode. Existe um método publica chamado `config()`. Isto permite que você use a mesma instancia da biblioteca, mas para configurações diferentes:

	echo Assets::add('jquery-cdn')->js();
	echo Assets::reset()->add(['custom.js', 'main.js'])->config(['pipeline' => true])->js();

Se você deseja que suas configurações diferentes sejam permanentes, use então o [multitenancy](#stolz-assets-multitenancy).

<a id="stolz-assets-faq_filter"></a>
#### Posso filtrar ou usar pré-processadores nos meus assets?

A Biblioteca não inclui nenhum pacote de funcionalidade de filtros/pré-processadores, mas oferece um meio para o caso de ser customziado quando o pipeline estiver ativado. Simplismente use a configuração [fetch_command](https://github.com/Stolz/Assets/blob/master/API.md#fetch_command) para aplicar um filtro customizado [filter](https://github.com/Stolz/Assets/issues/23).