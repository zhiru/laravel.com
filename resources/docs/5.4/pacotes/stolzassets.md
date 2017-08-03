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

**Nota:** *Esse recurso só está disponível para o Laravel> = 5.0*.

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

Se você usa uma quantidade muito grande de assets, tenha certeza que sua conexão é rapida o suficiente e que se computador consegue lidar com vários downloads e compreesões de arquivos, antes do tempo máximo de execução do php.

<a id="stolz-assets-faq_config_on_the_fly"></a>
#### Posso usar várias instancias da biblioteca?

Sim você pode, mas não há motivos para o mesmo. talvez seja melhor usar [multitenancy](#stolz-assets-multitenancy) (*Disponível apenas para Laravel> = 5.0*). 

<a id="stolz-assets-faq_instances"></a>
#### Posso alterar as configurações me tempo de execução (on the fly)?

Sim você pode. Existe um método publica chamado `config()`. Isto permite que você use a mesma instancia da biblioteca, mas para configurações diferentes:

	echo Assets::add('jquery-cdn')->js();
	echo Assets::reset()->add(['custom.js', 'main.js'])->config(['pipeline' => true])->js();

Se você deseja que suas configurações diferentes sejam permanentes, use então o [multitenancy](#stolz-assets-multitenancy).

<a id="stolz-assets-faq_filter"></a>
#### Posso filtrar ou usar pré-processadores nos meus assets?

A Biblioteca não inclui nenhum pacote de funcionalidade de filtros/pré-processadores, mas oferece um meio para o caso de ser customziado quando o pipeline estiver ativado. Simplismente use a configuração [fetch_command](https://github.com/Stolz/Assets/blob/master/API.md#fetch_command) para aplicar um filtro customizado [filter](https://github.com/Stolz/Assets/issues/23).

<a name="collective-html"></a>
## Instalação Laravel Collective/HTML

- [Instalação](#collective-html-instalacao)
- [Criando um Form](#collective-html-criando-um-form)
- [Proteção CSRF](#collective-html-protecao-csrf)
- [Criando um Form relacionado a uma Model](#collective-html-form-model-binding)
- [Funções de acesso a dados da Model](#collective-html-form-form-model-accessors)
- [Labels](#collective-html-labels)
- [Campos Text, Text Area, Password e Hidden](#collective-html-text)
- [Campos Checkbox and Radio](#collective-html-checkboxes-and-radio-buttons)
- [Input de Arquivo](#collective-html-file-input)
- [Input de Número](#collective-html-number)
- [Input de Datas](#collective-html-date)
- [Lista de Drop-Down (Select)](#collective-html-drop-down-lists)
- [Buttons](#collective-html-buttons)
- [Macros Customizados](#collective-html-custom-macros)
- [Componentes Customizados](#collective-html-custom-components)
- [Gerando URLs](#collective-html-generating-urls)

<a name="collective-html-instalacao"></a>
### Instalação

Begin by installing this package through Composer. Edit your project's `composer.json` file to require `laravelcollective/html`.

    composer require "laravelcollective/html":"^5.4.0"

Next, add your new provider to the `providers` array of `config/app.php`:

```php
  'providers' => [
    // ...
    Collective\Html\HtmlServiceProvider::class,
    // ...
  ],
```

Finally, add two class aliases to the `aliases` array of `config/app.php`:

```php
  'aliases' => [
    // ...
      'Form' => Collective\Html\FormFacade::class,
      'Html' => Collective\Html\HtmlFacade::class,
    // ...
  ],
```

> Looking to install this package in <a href="http://lumen.laravel.com" target="\_blank">Lumen</a>? First of all, making this package compatible with Lumen will require some core changes to Lumen, which we believe would dampen the effectiveness of having Lumen in the first place. Secondly, it is our belief that if you need this package in your application, then you should be using Laravel anyway.

<a name="collective-html-criando-um-form"></a>
## Opening A Form

#### Opening A Form

```php
{!! Form::open(['url' => 'foo/bar']) !!}
	//
{!! Form::close() !!}
```

By default, a `POST` method will be assumed; however, you are free to specify another method:

```php
echo Form::open(['url' => 'foo/bar', 'method' => 'put'])
```

> **Note:** Since HTML forms only support `POST` and `GET`, `PUT` and `DELETE` methods will be spoofed by automatically adding a `_method` hidden field to your form.

You may also open forms that point to named routes or controller actions:

```php
echo Form::open(['route' => 'route.name'])

echo Form::open(['action' => 'Controller@method'])
```

You may pass in route parameters as well:

```php
echo Form::open(['route' => ['route.name', $user->id]])

echo Form::open(['action' => ['Controller@method', $user->id]])
```

If your form is going to accept file uploads, add a `files` option to your array:

```php
echo Form::open(['url' => 'foo/bar', 'files' => true])
```

<a name="collective-html-protecao-csrf"></a>
## CSRF Protection

#### Adding The CSRF Token To A Form

Laravel provides an easy method of protecting your application from cross-site request forgeries. First, a random token is placed in your user's session. If you use the `Form::open` method with `POST`, `PUT` or `DELETE` the CSRF token will be added to your forms as a hidden field automatically. Alternatively, if you wish to generate the HTML for the hidden CSRF field, you may use the `token` method:

```php
echo Form::token();
```

#### Attaching The CSRF Filter To A Route

```php
Route::post('profile',
    [
        'before' => 'csrf',
        function()
        {
            //
        }
    ]
);
```

<a name="collective-html-form-model-binding"></a>
## Form Model Binding

#### Opening A Model Form

Often, you will want to populate a form based on the contents of a model. To do so, use the `Form::model` method:

```php
echo Form::model($user, ['route' => ['user.update', $user->id]])
```

Now, when you generate a form element, like a text input, the model's value matching the field's name will automatically be set as the field value. So, for example, for a text input named `email`, the user model's `email` attribute would be set as the value. However, there's more! If there is an item in the Session flash data matching the input name, that will take precedence over the model's value. So, the priority looks like this:

1. Session Flash Data ([Old Input](https://laravel.com/docs/requests#old-input))
2. Data From Current [Request](https://laravel.com/docs/requests) (via `Request::input` method)
3. Explicitly Passed Value
4. Model Attribute Data

This allows you to quickly build forms that not only bind to model values, but easily re-populate if there is a validation error on the server!

> **Note:** When using `Form::model`, be sure to close your form with `Form::close`!

<a name="form-model-accessors"></a>
#### Form Model Accessors

Laravel's [Eloquent Accessor](http://laravel.com/docs/5.2/eloquent-mutators#accessors-and-mutators) allow you to manipulate a model attribute before returning it. This can be extremely useful for defining global date formats, for example. However, the date format used for display might not match the date format used for form elements. You can solve this by creating two separate accessors: a standard accessor, *and/or* a form accessor.

To define a form accessor, create a `formFooAttribute` method on your model where `Foo` is the "camel" cased name of the column you wish to access. In this example, we'll define an accessor for the `date_of_birth` attribute. The accessor will automatically be called by the HTML Form Builder when attempting to pre-fill a form field when `Form::model()` is used.

```php
<?php

namespace App;

use Carbon\Carbon;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * Get the user's first name.
     *
     * @param  string  $value
     * @return string
     */
    public function getDateOfBirthAttribute($value)
    {
        return Carbon::parse($value)->format('m/d/Y');
    }

    /**
     * Get the user's first name for forms.
     *
     * @param  string  $value
     * @return string
     */
    public function formDateOfBirthAttribute($value)
    {
        return Carbon::parse($value)->format('Y-m-d');
    }
}
```

<a name="labels"></a>
## Labels

#### Generating A Label Element

```php
echo Form::label('email', 'E-Mail Address');
```

#### Specifying Extra HTML Attributes

```php
echo Form::label('email', 'E-Mail Address', ['class' => 'awesome']);
```

> **Note:** After creating a label, any form element you create with a name matching the label name will automatically receive an ID matching the label name as well.

<a name="text"></a>
## Text, Text Area, Password & Hidden Fields

#### Generating A Text Input

```php
echo Form::text('username');
```

#### Specifying A Default Value

```php
echo Form::text('email', 'example@gmail.com');
```

> **Note:** The *hidden* and *textarea* methods have the same signature as the *text* method.

#### Generating A Password Input

```php
echo Form::password('password', ['class' => 'awesome']);
```

#### Generating Other Inputs

```php
echo Form::email($name, $value = null, $attributes = []);
echo Form::file($name, $attributes = []);
```

<a name="checkboxes-and-radio-buttons"></a>
## Checkboxes and Radio Buttons

#### Generating A Checkbox Or Radio Input

```php
echo Form::checkbox('name', 'value');

echo Form::radio('name', 'value');
```

#### Generating A Checkbox Or Radio Input That Is Checked

```php
echo Form::checkbox('name', 'value', true);

echo Form::radio('name', 'value', true);
```

<a name="number"></a>
## Number

#### Generating A Number Input

```php
echo Form::number('name', 'value');
```

<a name="date"></a>
## Date

#### Generating A Date Input

```php
echo Form::date('name', \Carbon\Carbon::now());
```

<a name="file-input"></a>
## File Input

#### Generating A File Input

```php
echo Form::file('image');
```

> **Note:** The form must have been opened with the `files` option set to `true`.

<a name="drop-down-lists"></a>
## Drop-Down Lists

#### Generating A Drop-Down List

```php
echo Form::select('size', ['L' => 'Large', 'S' => 'Small']);
```

#### Generating A Drop-Down List With Selected Default

```php
echo Form::select('size', ['L' => 'Large', 'S' => 'Small'], 'S');
```

#### Generating a Drop-Down List With an Empty Placeholder

This will create an `<option>` element with no value as the very first option of your drop-down.

```php
echo Form::select('size', ['L' => 'Large', 'S' => 'Small'], null, ['placeholder' => 'Pick a size...']);
```

#### Generating A Grouped List

```php
echo Form::select('animal',[
	'Cats' => ['leopard' => 'Leopard'],
	'Dogs' => ['spaniel' => 'Spaniel'],
]);
```

#### Generating A Drop-Down List With A Range

```php
echo Form::selectRange('number', 10, 20);
```

#### Generating A List With Month Names

```php
echo Form::selectMonth('month');
```

<a name="buttons"></a>
## Buttons

#### Generating A Submit Button

```php
echo Form::submit('Click Me!');
```

> **Note:** Need to create a button element? Try the *button* method. It has the same signature as *submit*.

<a name="custom-macros"></a>
## Custom Macros

#### Registering A Form Macro

It's easy to define your own custom Form class helpers called "macros". Here's how it works. First, simply register the macro with a given name and a Closure:

```php
Form::macro('myField', function()
{
	return '<input type="awesome">';
});
```

Now you can call your macro using its name:

#### Calling A Custom Form Macro

```php
echo Form::myField();
```

<a name="custom-components"></a>
##Custom Components

#### Registering A Custom Component

Custom Components are similar to Custom Macros, however instead of using a closure to generate the resulting HTML, Components utilize [Laravel Blade Templates](http://laravel.com/docs/5.2/blade). Components can be incredibly useful for developers who use [Twitter Bootstrap](http://getbootstrap.com/), or any other front-end framework, which requires additional markup to properly render forms.

Let's build a Form Component for a simple Bootstrap text input. You might consider registering your Components inside a Service Provider's `boot` method.

```php
Form::component('bsText', 'components.form.text', ['name', 'value', 'attributes']);
```

Notice how we reference a view path of `components.form.text`. Also, the array we provided is a sort of method signature for your Component. This defines the names of the variables that will be passed to your view. Your view might look something like this:

```php
// resources/views/components/form/text.blade.php
<div class="form-group">
    {{ Form::label($name, null, ['class' => 'control-label']) }}
    {{ Form::text($name, $value, array_merge(['class' => 'form-control'], $attributes)) }}
</div>
```

> Custom Components can also be created on the `Html` facade in the same fashion as on the `Form` facade.

##### Providing Default Values

When defining your Custom Component's method signature, you can provide default values simply by giving your array items values, like so:

```php
Form::component('bsText', 'components.form.text', ['name', 'value' => null, 'attributes' => []]);
```

#### Calling A Custom Form Component

Using our example from above (specifically, the one with default values provided), you can call your Custom Component like so:

```php
{{ Form::bsText('first_name') }}
```

This would result in something like the following HTML output:

```php
<div class="form-group">
    <label for="first_name">First Name</label>
    <input type="text" name="first_name" value="" class="form-control">
</div>
```

<a name="generating-urls"></a>
##Generating URLs

#### link_to

Generate a HTML link to the given URL.

```php
echo link_to('foo/bar', $title = null, $attributes = [], $secure = null);
```

#### link_to_asset

Generate a HTML link to the given asset.

```php
echo link_to_asset('foo/bar.zip', $title = null, $attributes = [], $secure = null);
```

#### link_to_route

Generate a HTML link to the given named route.

```php
echo link_to_route('route.name', $title = null, $parameters = [], $attributes = []);
```

#### link_to_action

Generate a HTML link to the given controller action.

```php
echo link_to_action('HomeController@getIndex', $title = null, $parameters = [], $attributes = []);
```