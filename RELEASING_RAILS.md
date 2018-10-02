# Criando uma _Release_ do Rails

Neste documento, vamos cobrir os passos necessários para criar uma _release_ do Rails.
Cada seção contém passos a serem tomados antes da _release_. As datas sugeridas
em cada cabeçalho são justamente isso: sugestões.
Porém, elas deveriam realmente serem consideradas como período mínimo.

## 10 Dias antes da _release_

As tarefas de hoje são, em sua maioria, de coordenação. Aqui estão algumas coisas que devem ser feitas por você hoje:

### O CI está verde? Se não, deixe-o verde (Veja "Consertando o CI")

Não crie uma release com um CI vermelho. Você pode ver o status
do CI [aqui](http://travis-ci.org/rails/rails).

### O Sam Ruby está feliz? Se não estiver, deixe-o feliz.

Sam Ruby mantém uma [suíte de testes](https://github.com/rubys/awdwr)
que garante que os exemplos de código de seu livro ([Agile Web Development with Rails](https://pragprog.com/titles/rails5/agile-web-development-with-rails-5th-edition))
todos funcionem. Esses são testes de sistema valiosos para o Rails.
Você pode checar o status destes testes aqui:
[http://intertwingly.net/projects/dashboard.html](http://intertwingly.net/projects/dashboard.html)

Não gere uma _release_ tendo testes AWDwR no vermelho.

### Temos alguma dependência no Git? Se sim, contate estes autores.

Possuir dependências no Git significa que nós dependemos de código sem _release_.
Obviamente o Rails não pode de forma alguma ter uma _release_ que depende de código não finalizado.
Contate os autores dessas _gems_ em particular e negocie uma data para a _release_ que funcione para eles.

### Contate o time de segurança (ambos tenderlove ou rafaelfranca)

Deixe-os a par dos seus planos para a _release_. Podem existir
problemas de segurança a serem resolvidas, e isso pode impactar na data da sua _release_.

### Notifique os implementadores

Os implementadores do Ruby apostam alto na certeza que o Rails funciona.
Seja gentil e avise que o Rails vai possuir uma nova _release_ logo.

Isso é apenas necessário para _releases_ de pequeno e grande impacto,
_releases_ de solução de bugs não possuem tanto problema e supostamente devem ser retro-compativeis.

Envie um email informando sobre a _release_ que está por vir para essas listas:

* team@jruby.org
* community@rubini.us
* rubyonrails-core@googlegroups.com

Os implementadores irão te amar e te ajudar.

## 3 Dias antes da _release_

Aqui é quando você deve liberar a candidata para _release_ (_release candidate_).
Aqui estão as suas tarefas para hoje:

### O CI está verde? Se não, deixe-o verde.

### O Sam Ruby está feliz? Se não, deixe-o feliz.

### Contate o time de segurança. Emails  de CVE devem ser enviados neste dia.

### Crie uma _branch_ para a _release_.

Da _branch_ estável, crie uma _branch_ para a _release_.
Por exemplo, se você vai criar a _release_ do Rails 3.0.10, faça o seguinte:

```
[aaron@higgins rails (3-0-stable)]$ git checkout -b 3-0-10
Switched to a new branch '3-0-10'
[aaron@higgins rails (3-0-10)]$
```

### Atualize cada CHANGELOG.

Muitas vezes commits são feitos sem a atualização do CHANGELOG.
Você deve revisar os commits desde a ultima release, e preencher qualquer
informação perdida para cada CHANGELOG.

Você pode revisar os commits para a _release_ dessa forma:s:

```
[aaron@higgins rails (3-0-10)]$ git log v3.0.9..
```

Se você estiver fazendo uma _release_ de uma _branch_ estável,
você também deve se assegurar de que todas as entradas do CHANGELOG na _branch_ estável
também estão sincronizadas com a _branch_ master.

### Coloque a nova versão no arquivo RAILS_VERSION.

Inclua um número para o _Release Candidate_ se for apropriado.Ex.: `6.0.0.rc1`.

### Teste e dê um build na gem.
Rode `rake verify` para gerar as gems e instalá-las localmente. `verify` também gera uma aplicação Rails com uma migração e o inicia para realizar um teste de aceitação de build no seu browser.

Isso vai impedir que você pareça um bobo de subir uma RC para rubygems.org e depois perceber que ela está quebrada.

### Faça uma Release para RubyGems e para o NPM.

IMPORTANTE: O cliente do Action Cable e os adaptadores UJS da Action View são lançados como
pacotes do NPM, logo você deve possuir o Node.js instalado, ter uma conta no NPM 
(npmjs.com), e ser um package owner dos pacotes `actioncable` e `rails-ujs` (você pode conferir isso com o commando `npm owner ls actioncable` e `npm owner ls rails-ujs`) para
realizar uma release completa. Não realize a release até estar tudo certo com o NPM!

O comando de release irá criar a tag de release. Caso você não tenha configurado a assinatura de commits, use https://git-scm.com/book/tr/v2/Git-Tools-Signing-Your-Work como guia.
Você pode gerar chaves com a suite GPG a partir daqui: https://gpgtools.org.

Rode `rake changelog:header` para colocar um cabeçalho com uma nova versão em cada
CHANGELOG. Não faça um commit disso, a task de release vai cuidar disso.

Rode `rake release`. Isso irá popular as gemspecs e o package.json do NPM com a atual RAILS_VERSION, faça o commit dessas mudanças, use uma tag disso, e publique as gems para a rubygems.org.

### Envie anúncios sobre a release do RAILS

Escreva um anúncio de release que inclui versão, mudanças, e links para o GitHub onde as pessoas podem achar a lista de commits específicos. Aqui seguem as listas de email onde vocês devem anúnciar:

* rubyonrails-core@googlegroups.com
* rubyonrails-talk@googlegroups.com
* ruby-talk@ruby-lang.org

Use o formato Markdown para fazer seu anúncio.
Lembre-se de pedir à comunidade para
reportar issues com sua versão candidata de release para a lista de email rails-core.

NOTA:  Para releases de patch, existe uma task `rake announce` para gerar o anúncio da release.
Ele suporta múltiplas releases de patch tambem:

```
VERSIONS="5.0.5.rc1,5.1.3.rc1" rake announce
```

IMPORTANTE: Caso qualquer usuário experimente regressão quando usar a versão de candidata à release você *deve* adiar a release. Releases com correções de bugs *não devem* quebrar aplicações existentes.

### Publique o anúncio no blog do Rails.

Se você usou o formato Markdown no seu email, você pode simplesmente colar o conteúdo no blog.

* http://weblog.rubyonrails.org

### Publique o anúncio para a conta do Rails no Twitter.

## Tempo entre a candidata à release e a atual release

Confira a lista de email rails-core e a lista de issues no GitHub por retrocessos na RC.

Caso seja encontradas quaisquer regressões, corrija-as e repita o processo de candidatura de release.
Nós não faremos a release final até passarem 72 horas após a submissão da última candidata à release.
Isso significa que caso usuários encontrarem retrocessos, a data marcada para a release deve ser adiada.

Quando você consertar as regressões, não crie uma nova branch. Conserte-os em uma branch estável, então faça um cherry-pick no commit para a sua branch de release.
Nenhum outro commit deve ser adicionado na branch de release exceto os de conserto de regressão.

## O dia da release

Muitos desses passos são os mesmos usados para uma candidata à release, logo se você precisar de mais explicação em um passo específico,
veja os passos de uma RC.

Hoje, faça as coisas nesta ordem:

* Aplique correções de segurança na branch de release
* Atualize o CHANGELOG com correções de segurança
* Atualize a RAILS_VERSION removendo o RC
* Construa e teste a gem
* Faça a publicação (release) das gems
* Caso esteja fazendo a release de uma nova versão estável:
  - Rode a geração da documentação estável (veja abaixo)
  - Atualize a versão na página inicial
* Envie um email para as listas de segurança
* Envie um email para as listas de anúncios gerais

### Enviando emails para a lista de anúncios de segurança

Mande um email para a lista de anúncios de segurança para cada vulnerabilidade consertada.

Você pode fazer isso ou pedir para o time de segurança para fazê-lo.

Mande email com relatórios de segurança para:

* rubyonrails-security@googlegroups.com
* oss-security@lists.openwall.com

Tenha certeza de documentar os consertos de segurança junto com os números de CVE e
links para cada mudança. Algumas pessoas podem não realizar a atualização logo em seguida,
logo devemos dar a eles as mudanças de segurança na forma de patch.

* Anúncios de blog
* Anúncios no Twitter
* Realize o merge da branch de release para a branch estável.
* Beba uma cerveja (ou algum coquetel)

## Diversos

### Consertando o CI

Existem dois passos simples para arrumar o CI:

1. Identifique o problema
2. Resolva o problema

Repita esses passos até o CI ficar verde.
