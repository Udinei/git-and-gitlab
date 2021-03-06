# git-and-gitlab 
<b>[em construção]</b>
Projeto da [Live Encoding do Osnir Cunha (Inter)](https://www.youtube.com/watch?v=vczVA6pUIpc) que descreve o uso do [feature brach workflow](https://martinfowler.com/bliki/FeatureBranch.html) no GitLab na prática usando o Git no IntelliJ e no terminal.

# Stack
- Java 15
- Spring boot
- Maven
- IDE Intellij
- Junit
- Git Bash (Windows)
- Conta no GitLab
 
# Assuntos abordados
- Comandos Git mais utilizados durante o versionamento de um documento usando Git e GitLab no dia a dia. 
- O uso de uma pipeline de CI (integração continua) descrita em arquivo `.yml` para compilar, testar e publicar ao fazer `merge request` com a branch `main`.
- Funcionalidades do GitLab no controle de versões
 
# O que é Feature branch workflow
`Feature branch workflow` segundo [Martin Fowler](https://martinfowler.com/bliki/FeatureBranch.html) esse é um padrão de ramificação de código-fonte em que um desenvolvedor abre um branch quando começa a trabalhar em um novo recurso, faz todo o trabalho neste branch e integra as mudanças em um branch (main) quando o recurso é concluído.

# O que é versionamento
Controle de versões diferentes de um documento.

### VCS - Version Control System
- São sistemas Gerenciadores de versões
- Mantém o registro de modificação do código
- Quem? O que? Quando? Por que? 
- Tem o objetivo de manter e disponibilizar código mais recente

### GIT e GitHub são DVCS - Distributed Version Control System 
- Cada cópia do repositório contém o histórico completo de todas as alterações
- Sistema Distribuido
- Git Open Source
- GitHub não é Open Source
- Otimizado para o desempenho

# Fluxo entre repositórios Remote/Local do Git
Repositório remoto e repositório local (GitLab segue a mesma ideia)

![](/images/fluxo-basic-git.png)


# Feature branch
O Git segue o conceito de branch sendo o branch(ramos, ramificações) `main` o branch principal do repositório, onde todo o código feitos em outras branch é juntado, formando assim um só código (no caso do software).

![](/images/git-branchs1.png)


# Fluxo de trabalho local do Git
Todos os documentos (arquivos) na área de trabalho, seguem o fluxo abaixo quando estão sendo monitorados pelo
sistema de versão do Git.
![](/lifecycle-git.png)


Fluxo de trabalho local
# Uso do git
O Git pode ser utilizado através de um terminal Linux, Windows (cmd ou gitbash) ou com uso de uma IDE no nosso caso IntelliJ

### Visualizando Help do Git
`git --help`

### Criando um repositorio git na área de trabalho
A área de trabalho é a pasta no seu computador local, que contém o documentos ou arquivos que deseja versionar
O comando abaixo cria o repositorio `.git` (uma pasta oculta), onde o Git armazena seus metadados de controle.

`git init` 

Comando para ver arquivos ocultos no windows:
No `cmd` na pasta onde esta o arquivo digite: `attrib *.*`

No terminal linux digite: `ls -a`

### Git config
Criando usuário do Git (pode ser local ou global --global)

Identificando o usuário no repositório do Git
- `git config user.nome "ukaliko"` 
- `git config user.email "ukaliko@gmail.com"`

# Arquivo .gitignore
Armazena informações de padrão de arquivos e pastas que não serão versionados
- Formato expressões regulares
Abaixo exemplo de arquuivo `.gitignore`
~~~
### Java ###
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

### Code-Java ###
.project
.classpath
factoryConfiguration.json

### Java-Web ###
## ignoring target file
target/
out/

# Eclipse
.classpath
.project
.settings/
# Intellij
.idea/
*.iml
*.iws
 
# Mac
.DS_Store
 
# Maven
log/
target/
~~~

As vezes alguns arquivos já informados no .gitignore insistem em ser versionados, para forçar que esses arquivos não sejam versionados execute o comando abaixo (exemplo arquivos de log):

`git rm --cached *.log` 

e

`git update-index --assume-unchanged *.log`

### git Status
Para visualizar Status do repositório local

`git status` 

### git commit 
Para versionar os arquivos novos ou que sofreram alterações 

`git commit -m "digite a msg aqui"`

### git log
Para ver os logs dos commit no Git

`git log`

### Git Alias
Alias são atalhos para comandos git, você pode visualizar essa lista de atablhos usando o comando abaixo:

`git config -l | grep alias`

`git config -l | grep core`

O comando `git acm` é um alias que adiciona as alterações e faz o commit em um único comando
se o comando não for encontrado no config do git, será necessário cria-lo ante de usar como abaixo:

`git acm "msg aqui"`

# Criando Branchs
### Criando uma novo branch chamada feature1 com a opção `-b` ex:

`git checkout -b feature1`

### Alternando entre commits 
o comando `git checkout nomeBranch` alterna entre versões de código já commitados no sistema local, usa o `hash do commit` para navegar entre as versões do código, usar o comando `git log` para obter o hash do commit ex: 

`git checkout 135deecb687f4d0fe5dcfc26e3f6c75f3167319e` 

Você pode vsualizar a árvore de commit do git com o comando abaixo:

`git log --graph --oneline --all`

ou de forma mais colorida usando o comando abaixo:

`git log --graph --abbrev-commit --decorate --format=format:'%C(yellow)%h%C(reset)%C(auto)%d%C(reset) %C(normal)%s%C(reset) %C(dim white)%an%C(reset) %C(dim blue)(%ar)%C (reset)' --all`

- [Git checkout](https://www.atlassian.com/br/git/tutorials/using-branches/git-checkout)
- [Saiba mais lendo esse artigo](https://bluecast.tech/blog/git-switch-branch/)

### Mudando de branch
O comando `git switch` troca de branch

`git switch main`

ou cria uma branch feature2 (e já muda para ela)

`git switch -c feature2`

ou ainda `git checkout` que também muda de branch

`git checkout nomeBranch`

# Atualizando branchs
O comando merge e rebase são responsaveis por atualizar as branch, sendo necessario estar na branch que deseja atualizar
e então executar um desses comandos, que possuem suas particularidades.

### git merge
`git merge main`

O comando acima, e o  `merge` da `master` para a `feature2` vai atualizar a branch `feature2` com os novos commits feitos na branch `main` e criando na branch `feature2` um novo commit ("G") como na imagem abaixo
![](/merge-feature2.png)


### git rebase
`git rebase main`

O comando acima, é o comando `rebase` da `master` para a `feature1` que atualiza a branch `feature1`, com os novos commits feitos na branch `main`, refazendo a linha base ou seja reescrevendo a árvore de commits da `master` para `feature1` e não cria nenhum novo commit na branch `feature1`, ficando assim de forma linear e limpa a árvore de commits da branch `feature1`.
Esse comando deve ser usado se a branch `feature1` ainda não foi comitada na `main` caso contrário o melhor é usar o `merge`
![](/rebase-feature1.png)

# Removendo branchs
### Local
Para remover um branch `local` use o comando abaixo:

`git branch -d feature3`

### Remoto
Para remover um branch `remoto` use o comando abaixo:

`git push origin --delete feature3`

[Leia mais sobre o comando delete branch nesse link](https://receitasdecodigo.com.br/devops/git-remover-um-branch-local-ou-remoto)


# GitLab
- Gerenciamento de repósitorios
- Similar ao GitHub e Bitbucket
- Open Source
- Organização de repósitorio em grupos
- suporta CI/CD

### Criando uma conta no GitLab
- Acessar o site do GitLab em https://gitlab.com/
- Criar seu usuario no GitLab
- Criar um o grupo "DIO-GIT_AND_LAB"
- Criar o projeto sitema-vendas

Como o repositório git já foi criado localmente usar a opção `Push an existing Git repository` sugerida pelo GitLab logo após a criação do projeto.
~~~
cd existing_repo
git remote rename origin old-origin
git remote add origin git@gitlab.com:dio-git_and_lab/sistema-vendas.git
git push -u origin --all
git push -u origin --tags
~~~
### Conectando o repositorio local ao repositorio remoto
No IntelliJ - No menu "Git" 
![](/images/menu-git-intellij.png)

usar a opção "Manage Remotes..."
e informar somente o endereço do repositorio "git@gitlab.com:dio-git_and_lab/sistema-vendas.git"
como na imagem abaixo:

![](/images/conect-remote-gitlab.png)


### Como usar a mesma chave SSH do git no GitLab
 Se você tem já tem um par de chaves SSH existente, você não precisa criar uma nova (a menos que queira) você pode utilizar a essa mesma chave SSH do Git no GitLab.
[Consulte esse link para saber mais sobre esse assunto](https://docs.gitlab.com/ee/ssh/README.html#see-if-you-have-an-existing-ssh-key-pair)

# Atualizando as informações
Traz as referência de "origin/main" (uma cópia da branch "main" do repositório remoto) para o repositório local.
`git fetch` 
[Mais detalhes sobre o comando fetch](https://metring.com.br/para-que-serve-o-git-fetch-vs-pull)

Atualiza o repositório remoto com informações do repositório local
`git push -u origin --all` - as opções `-u origin --all` podem ser executadas somente da primeira vez, que fizer o push

# Integrando branchs com Merge request no GitLab
Atualizando a branch main com dados de feature2

### Habilitando no Intellij a aba Local change
Na aba local change é possivel visualizar todas as modificações feitas na brach (como um git status)

Settings -> Version Control -> Commit -> Use non-modal commit interface (deselecionar essa opção)

### Adicionando o arquivo ao controle de versão usando o intellij
Na aba Local Change clicar no arquivo criado com o botão direito e selecionar Add to VCS (equivalente ao `git add`) 

### Commit Git no intelliJ
clicar na aba `Local change do Git` com o botão direito e selecionar `Commit Files...`


### Desfazer um commit no intellij
Na aba Git clicar no commit e selecionar a opção `Undo commit...`

### Merge Request 
Solicitação feita pelo desenvolvedor, dentro do GitLab ao um responsável pela organização e distribuição do código, onde o mesmo
vai rodar pode rodar pipeline de testes, deploy e build. 

### Agrupando commits
Para agrupar commits utilizar o comando `squash`

### Usando arquivos .yml para fazer pipeline no GitLab
Arquivos .YAML usa um padrão de dados hierárquicos, que pode ser usado em conjunto com qualquer linguagens de programação, e é usualmente utilizado para armazenar arquivos de configuração. Nesse caso o conteúdo do arquivo .gitlab-ci.yml abaixo, é lido automaticamente pelo GitLab que executa os comandos nele contido, que é uma sequencia de comandos para compilar, testar e construir toda a aplicação assim que for feito um `Merge Request` com a branch `main`.

Abaixo o conteúdo do arquivo `.gitlab-ci.yml`
~~~
# Esse arquivo adiciona as configurações de pipeline para o CI (Continuos Integrations)
# passagem de parametros para as Variaveis do Maven
variables:
  MAVEN_OPTS: "-Dhttps.protocols=TLSv1.2 -Dmaven.repo.local=$CI_PROJECT_DIR/.m2/repository -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=WARN -Dorg.slf4j.simpleLogger.showDateTime=true -Djava.awt.headless=true"
  MAVEN_CLI_OPTS: "--batch-mode --errors --fail-at-end --show-version -DinstallAtEnd=true"

# imagem do maven que sera utilizada
image: maven:3.6.3-jdk-11

# faz cache do repositorio do maven no repositorio
cache:
  paths:
    - .m2/repository

#  A pipeline tera os 3 estagios abaixo
stages:
  - compile
  - test
  - publish

# 1 stage - compila a app
compilation:
  stage: compile
  script: # empacota app package e pula os tests
    - mvn $MAVEN_CLI_OPTS package -DskipTests

# 2 stage - faz os testes
unit-tests:
  stage: test
  script:
    - mvn $MAVEN_CLI_OPTS clean verify
  artifacts:
    when: always
    reports: # sempre salva os relatorios de testes do maven no endereco abaixo
      junit:
        - target/surefire-reports/TEST-*.xml
        - target/failsafe-reports/TEST-*.xml

#  sempre que for feito um merge com a branch main, publica com a geração do .jar
artifact-publish:
  stage: publish
  script:
    - mvn $MAVEN_CLI_OPTS clean install -DskipTests
  only: # somente roda esse stage quando o branche que tem o arquivo de CI for integrado com o master
    refs:
      - main
  artifacts:
    paths: [ "target/*.jar" ]
    expire_in: 3 days

~~~

# Referências
- [Live encoding Osnir Cunha](https://www.youtube.com/watch?v=vczVA6pUIpc)
- [Linkdin Osnir Cunha](https://linkdin.com/in/osnircunha)
- [PDF com os comando do Git](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
- [Comparando Workflows Git](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [feature brach workflow](https://docs.gitlab.com/ee/gitlab-basics/feature_branch_workflow.html)

