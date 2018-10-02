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

### Post the announcement to the Rails blog.

If you used Markdown format for your email, you can just paste it into the
blog.

* http://weblog.rubyonrails.org

### Post the announcement to the Rails Twitter account.

## Time between release candidate and actual release

Check the rails-core mailing list and the GitHub issue list for regressions in
the RC.

If any regressions are found, fix the regressions and repeat the release
candidate process. We will not release the final until 72 hours after the
last release candidate has been pushed. This means that if users find
regressions, the scheduled release date must be postponed.

When you fix the regressions, do not create a new branch. Fix them on the
stable branch, then cherry pick the commit to your release branch. No other
commits should be added to the release branch besides regression fixing commits.

## Day of release

Many of these steps are the same as for the release candidate, so if you need
more explanation on a particular step, see the RC steps.

Today, do this stuff in this order:

* Apply security patches to the release branch
* Update CHANGELOG with security fixes
* Update RAILS_VERSION to remove the rc
* Build and test the gem
* Release the gems
* If releasing a new stable version:
  - Trigger stable docs generation (see below)
  - Update the version in the home page
* Email security lists
* Email general announcement lists

### Emailing the Rails security announce list

Email the security announce list once for each vulnerability fixed.

You can do this, or ask the security team to do it.

Email the security reports to:

* rubyonrails-security@googlegroups.com
* oss-security@lists.openwall.com

Be sure to note the security fixes in your announcement along with CVE numbers
and links to each patch. Some people may not be able to upgrade right away,
so we need to give them the security fixes in patch form.

* Blog announcements
* Twitter announcements
* Merge the release branch to the stable branch
* Drink beer (or other cocktail)

## Misc

### Fixing the CI

There are two simple steps for fixing the CI:

1. Identify the problem
2. Fix it

Repeat these steps until the CI is green.
