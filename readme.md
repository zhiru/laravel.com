## Laravel Documentação 

This is the source of the official Laravel.com website.

The site has two main sections. The front / marketing page which is located at `resources/views/marketing.blade.php` and the documentation pages.

### Documentation

The website's documentation is loaded from the `resources/docs` directory. You will need to clone each version of the documentation into this directory. For example, `resources/docs/5.4`, etc. All of the documentation is stored on GitHub at [laravel/docs](https://github.com/laravel/docs).

### Additional Information

Projeto com traduções da versão 5.4 do Laravel e alguns dos pacotes usados no projetos da Uniware


### Passos iniciais

#### Passo 1

Após clonar o projeto execute os seguintes comandos `composer install` enquanto o comando vai sendo executado você pode,
renomear o arquivo `.env.example` para `.env`, existe algumas pré-configurações que é bom ver neste arquivo.

#### Passo 2

Após finalizado o passo 1, execute o comando `npm install`.

#### Passo 3

Após finalizado o passo 2, execute o comando `gulp`.

### Observações

Caso não exista um vhost para este projeto é melhor criar para facilitar no acesso.