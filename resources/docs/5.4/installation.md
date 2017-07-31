# Instalação

- [Instalação](#installation)
    - [Requisitos do Servidor](#server-requirements)
    - [Instalando o Laravel](#installing-laravel)
    - [Configuração](#configuration)
- [Configuração do Servidor](#web-server-configuration)
    - [URLs Amigáveis](#pretty-urls)

<a name="installation"></a>
## Instalação

<a name="server-requirements"></a>
### Requisitos do Servidor

O framework Laravel possui alguns requisitos de sistema. Claro, todos esses requisitos são satisfeitos pela máquina virtual [Laravel Homestead](/docs/{{version}}/homestead), por isso é altamente recomendável que você use Homestead como seu ambiente local de desenvolvimento Laravel.

Contudo, se você não estiver usando o Homestead, você irá precisar ter certeza que o servidor atende os seguintes requisitos:

<div class="content-list" markdown="1">
- PHP >= 5.6.4
- Extensão PHP OpenSSL
- Extensão PHP PDO
- Extensão PHP Mbstring
- Extensão PHP Tokenizer
- Extensão PHP XML
</div>

<a name="installing-laravel"></a>
### Instalando o Laravel

Laravel usa o [Composer](https://getcomposer.org) para gerenciar suas dependencias. Então, antes de usar o laravel tenha certeza de que o composer esteja instalado em sua máquina. 


#### Através do Instalador do Laravel

Primeiro, faça download do instalador do Laravel usando o Composer:

    composer global require "laravel/installer"

Tenha certeza de inserir `$HOME/.composer/vendor/bin` no diretório (ou diretório equivalente do seu SO) no $PATH para que `laravel` seja um comando executável e possa ser localizado pelo seu sistema.

Uma vez instalado, o comando `laravel new` irá criar uma instalação limpa do Laravel no diretórios especificado. 
Para conhecimento, o comando `laravel new blog` irá criar uma pasta chamada `blog` contendo a instalação do Laravel com todas as dependencias iniciais:

    laravel new blog

####  Através do Composer Create-Project

Alternativamente, você queira instalar o Laravel diretamente pelo composer usando o`create-project` no seu terminal:

    composer create-project --prefer-dist laravel/laravel blog

#### Servidor de desenvolvimento Local

Se você instalou o PHP localmente e você gostaria de usar o servidor de desenvolvimento embutido do PHP para atender seu aplicativo, você pode usar o comando `serve` Artisan. Este comando iniciará um servidor de desenvolvimento em `http://localhost:8000`:

    php artisan serve

Claro, opções de desenvolvimento local mais robustas estão disponíveis via [Homestead](/docs/{{version}}/homestead) e [Valet](/docs/{{version}}/valet).

<a name="configuration"></a>
### Configuração

#### Diretório público

Depois de instalar o Laravel, você deve configurar o caminho padrão para a pasta public do seu projeto. O `index.php` neste diretório serve como o controlador frontal para todos os pedidos HTTP que entram no seu aplicativo.

#### Arquivos de Configuração

Todas as configurações do Laravel ficam armazenadas na pasta `config`. ada opção está documentada, então fique à vontade para examinar os arquivos e familiarizar-se com as opções disponíveis.

#### Permissões dos Diretórios

Depois de instalar o Laravel, vocẽ talvez precise configurar algumas permissões. Os diretórios `storage` e `bootstrap/cache` precisam ter a permissão de escrita ou o Laravel não irá funcionar. Se vocẽ estiver usando o [Homestead](/docs/{{version}}/homestead) essas permissões já estarão configuradas.

#### Chave da Aplicação

A próxima coisa que você deve fazer após instalar o Laravel é setar a chave da aplicação a uma string randomica. Se você instalou o Laravel via Composer ou pelo Instalador do Laravel, está chave já foi setada para você pelo comando `php artisan key:generate`.

Tipicamente, as strings deve ser de 32 caracteres. A Chave pode ser no arquivo ambiente `.env`. se você não renomeou o arquivo `.env.example` para `.env`, você deve fazer isso agora. **Se a chave da aplicação não estiver setada, seus usuários e sessões e outros dados criptografados não estarão seguros!**

#### Configuração Adicional

Laravel precisa praticamente de nenhuma outra configuração fora da caixa. Você é livre para começar a desenvolver! No entanto, talvez você queira revisar o arquivo `config/app.php` e sua documentação. Ele contém várias opções tais como `timezone` e `locale` que talvez vocẽ queira alterar de acordo com sua aplicação.

Talvez você também queira configurar algums componentes adicionais do Laravel, tais como:

<div class="content-list" markdown="1">
- [Cache](/docs/{{version}}/cache#configuration)
- [Banco de Dados](/docs/{{version}}/database#configuration)
- [Sessão](/docs/{{version}}/session#configuration)
</div>

<a name="web-server-configuration"></a>
## Configurações do Servidor Web

<a name="pretty-urls"></a>
### URLs Amigáveis

#### Apache

Laravel inclui um arquivo `public/.htaccess` que é usado para prover URLs sem o `index.php` controlador frontal de caminhos. Antes de acessar a sua aplicação com o Apache, tenha certeza que o módulo `mod_rewrite` esteja habilitado para que o arquivo `.htaccess` seja visualizado/lido pelo servidor.

Se o `.htaccess` que está incluído no Laravel não funcione para sua aplicação no Apache, tente esta alternativa:

    Options +FollowSymLinks
    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]

#### Nginx

Se você estiver usando Nginx, siga as instruções de diretivas na configuração da sua aplicação, redirecionando todas as requisições 
para o controloador frontal `index.php` que está dentro da `public/`:

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

Claro, caso esteja usando [Homestead](/docs/{{version}}/homestead) ou [Valet](/docs/{{version}}/valet), as URLs Amigáveis já estarão automaticamente configuradas.
