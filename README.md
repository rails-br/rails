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
prover uma resposta adequada. Normalmente isso significa retornar HTML, mas as _controllers_ do Rails
também podem gerar XML, JSON, PDFs, visualizações específicas para dispositivos móveis, e outros.
As _Controllers_ carregam e manipulam as _Models_, e renderizam os  _templates_ da _View_ 
com a finalidade de gerar a resposta HTTP apropriada.
No Rails, requisições recebidas são direcionadas pela _Action Dispatch_ para uma 
_controller_ apropriada, e as classes _controller_ são derivadas da `ActionController::Base`.
A _Action Dispatch_ e a _Action Controller_ são empacotadas juntas no _Action Pack_.
Você pode ler mais sobre a _Action Pack_ no seu [README](actionpack/README.rdoc).

A camada _View_ é composta de "_templates_" que são resonsáveis por prover
representações apropriadas dos recursos em sua aplicação.
_Templates_ podem ser feitos em formatos variados, mas a maioria dos _templates_ são HTML com código Ruby embutido (arquivos ERB).
As _Views_ são tipicamente renderizadas para gerar uma resposta da _controller_, ou para gerar o conteúdo de um email.
No Rails, a geração de _views_ é feita pela _Action View_.
Você pode ler mais sobre a _Action View_ no [README](actionview/README.rdoc).


_Active Record_, _Active Model_, _Action Pack_, e _Action View_ podem, cada uma delas, ser utilizadas de forma independente ao Rails.
Além disso, o Rails também possui: _Action Mailer_ ([README](actionmailer/README.rdoc)), uma biblioteca
para gerar e enviar emails; _Active Job_ ([README](activejob/README.md)), um _framework_ para declarar _jobs_ e fazê-los rodar em uma variedade de filas no background;
_Action Cable_ ([README](actioncable/README.md)), um _framework_ para integrar WebSockets com uma applicação Rails;
_Active Storage_ ([README](activestorage/README.md)), uma biblioteca para anexar arquivos locais ou da nuvem em aplicações Rails;
e _Active Support_ ([README](activesupport/README.rdoc)), uma coleção de classes de utilidade e extensões da biblioteca padrão que são úteis ao Rails, mas que podem ser usadas independentemente fora do Rails.

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
