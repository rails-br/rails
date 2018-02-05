# Welcome to Rails

Rails é um _framework_ para aplicações web que inclui tudo que é necessário para criar aplicações
web com suporte a banco de dados, de acordo com o padrão
[Model-View-Controller (MVC)](http://en.wikipedia.org/wiki/Model-view-controller).

Entender o padrão MVC é a chave para entendermos o Rails. O MVC divide a sua aplicação em três camadas,
cada uma com uma responsabilidade específica.

A _Camada Model_ representa sua modelo de domínio (como Conta, Produto, Pessoa, Post, etc.) e
encapsula a lógica de negócio que é específica a sua aplicação. No Rails, as classes modelo
com suporte ao banco de dados se derivam da superclasse `ActiveRecord::Base`. A Active Record
lhe permite apresentar os dados das linhas do banco como objetos e "embeleze" esses dados com
métodos de lógica de negócio. You can read more about Active Record in its [README](activerecord/README.rdoc).
Although most Rails models are backed by a database, models can also be ordinary
Ruby classes, or Ruby classes that implement a set of interfaces as provided by
the Active Model module. You can read more about Active Model in its [README](activemodel/README.rdoc).

A _Camada Controller_ é responsável pelo tratamento de requisições HTTP recebidas e 
prover uma resposta adequada. Normalmente isso significa retornar HTML, mas as _controllers_ do _Rails_
também podem gerar XML, JSON, PDFs, visualizações específicas para dispositivos móveis, e outros.
As _Controllers_ carregam e manipulam as _Models_, e renderizam os  _templates_ da _View_ 
com a finalidade de gerar a resposta HTTP apropriada.
No _Rails_, requisições recebidas são direcionadas pela _ActionDispatch_ para uma 
_controller_ apropriada, e as classes _controller_ são derivadas da `ActionController::Base`.
A _ActionDispatch_ e a _ActionController_ são empacotadas juntas no _ActionPack_.
Você pode ler mais sobre a _ActionPack_ no seu [README](actionpack/README.rdoc).

The _View layer_ is composed of "templates" that are responsible for providing
appropriate representations of your application's resources. Templates can
come in a variety of formats, but most view templates are HTML with embedded
Ruby code (ERB files). Views are typically rendered to generate a controller response,
or to generate the body of an email. In Rails, View generation is handled by Action View.
You can read more about Action View in its [README](actionview/README.rdoc).

Active Record, Active Model, Action Pack, and Action View can each be used independently outside Rails.
In addition to that, Rails also comes with Action Mailer ([README](actionmailer/README.rdoc)), a library
to generate and send emails; Active Job ([README](activejob/README.md)), a
framework for declaring jobs and making them run on a variety of queueing
backends; Action Cable ([README](actioncable/README.md)), a framework to
integrate WebSockets with a Rails application;
Active Storage ([README](activestorage/README.md)), a library to attach cloud
and local files to Rails applications;
and Active Support ([README](activesupport/README.rdoc)), a collection
of utility classes and standard library extensions that are useful for Rails,
and may also be used independently outside Rails.

## Iniciando

1. Instale o Rails no terminal de comando, se ainda não o tiver:

        $ gem install rails

2. No terminal de comando, crie uma nova aplicação Rails:

        $ rails new myapp

   onde "myapp" é o nome da aplicação.

3. Mude o diretório para `myapp` e inicie o servidor web:

        $ cd myapp
        $ rails server

   Rode com `--help` ou `-h` para opções.

4. Usando um navegador, vá para `http://localhost:3000` e você verá:
"Yay! You’re on Rails!"

5. Siga as diretrizes para começar a desenvolver a sua aplicação. Você talvez ache as
   seguintes fontes úteis:
    * [Iniciando com o Rails](http://guides.rubyonrails.org/getting_started.html)
    * [Guias do Ruby on Rails](http://guides.rubyonrails.org)
    * [A documentação da API](http://api.rubyonrails.org)
    * [Tutorial do Ruby on Rails](https://www.railstutorial.org/book)

## Contribuindo

[![Code Triage Badge](https://www.codetriage.com/rails/rails/badges/users.svg)](https://www.codetriage.com/rails/rails)

Nós o encorajamos a contribuir ao Ruby on Rails! Por favor veja o [Guia de Contribuição ao Ruby on Rails](http://edgeguides.rubyonrails.org/contributing_to_ruby_on_rails.html) para diretrizes de como proceder. [Junte-se a nós!](http://contributors.rubyonrails.org)

Tentando reportar uma possível vulnerabilidade de segurança no Rails? Por favor confira a nossa [política de segurança](http://rubyonrails.org/security/) para diretrizes de como proceder.

Todo mundo que interage no Rails e nos códigos, issues, salas de bate-papo, e listas de email de seus sub-projetos é esperado que siga o [code of conduct](http://rubyonrails.org/conduct/) do Rails.

## Status de Código

[![Status da Build](https://travis-ci.org/rails/rails.svg?branch=master)](https://travis-ci.org/rails/rails)

## Licença

Ruby on Rails será lançado sob a [Licença MIT](https://opensource.org/licenses/MIT).
