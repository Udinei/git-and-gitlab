# git-and-gitlab 
<b>[em construção]</b>
Projeto da [Live Encoding do Osnir Cunha (Inter)](https://www.youtube.com/watch?v=vczVA6pUIpc) que descreve o uso do [feature brach workflow](https://martinfowler.com/bliki/FeatureBranch.html) no GitLab na prática usando o Git no IntelliJ e no terminal.

# Stack
- Java 15
- Spring boot
- Maven
- IDE Intellij
- Junit
- Git 
- GitLab
 
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
Visualizando configurações do git (atalhos para comandos git)

`git config -l | grep alias`

`git config -l | grep core`

### Git acm (necessário ter criado o alias)
Esse comando adiciona e faz o comit de uma vez só (Comando não encontrado non config do git)

`git acm "msg aqui"`

### Git checkout
`git checkout` alterna entre versões de código já existentes no sistema local, usa o `hash do commit` para navegar
entre as versões do código, usuar o comando `git log` para obter o hash do commit
`git checkout 135deecb687f4d0fe5dcfc26e3f6c75f3167319e` 

ou cria uma nova branch com a opção `-b` ex:
`git checkout -b feature1`

- [Git checkout](https://www.atlassian.com/br/git/tutorials/using-branches/git-checkout)
- [Saiba mais lendo esse artigo](https://bluecast.tech/blog/git-switch-branch/)

### Mudando de branch
`git switch main`

ou troca de branch criando a branch feature2 -c (cria a branch)

`git switch -c feature2`

### Visualizando a arvore de commit do git
`git log --graph --oneline --all`

ou

`
git log --graph --abbrev-commit --decorate --format=format:'%C(yellow)%h%C(reset)%C(auto)%d%C(reset) %C(normal)%s%C(reset) %C(dim white)%an%C(reset) %C(dim blue)(%ar)%C (reset)' --all`

# Atualizando branchs

### git merge
`merge` da `master` para a `feature2` Atualiza a branch feature2, com os novos commits feitos na branch(main), merge cria um novo commit ("G") na branch feature2
![](/merge-feature2.png)


### git rebase
`rebase` da `master` para a `feature1` Atualiza a branch feature1, com os novos commits feitos na branch(main), refazendo a linha base ou seja reescrevendo a árvore de commits da `master` para `feature1` que agora fica de forma linear e limpa.
![](/rebase-feature1.png)

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

### Para remover um branch remoto ou local
[Consultar esse link](https://receitasdecodigo.com.br/devops/git-remover-um-branch-local-ou-remoto)

### Desfazer um commit no intellij
Na aba Git clicar no commit e selecionar a opção `Undo commit...`

### Merge Request 
Solicitação feita pelo desenvolvedor, dentro do GitLab ao um responsável pela organização e distribuição do código, onde o mesmo
vai rodar pode rodar pipeline de testes, deploy e build. 

### Mudar de branch
`git checkout feature2`

Traz o conteúdo da `main` para a branch `feature2`

### Atualizando branch com rebase 
Comando que atualiza a branch atual com os dados vindos da main, reescrevendo a árvore de commit
`git rebase master feature`
- Reescreve a árvore local, não cria um novo commit, apenas atualiza os dados local com os dados vindos da `main`
- Mantém a estrura de commit limpa, usar sempre que ainda não fez nenhum commit para o main

### Agrupando commits com squash

# Referências
- [Live conding Osnir Cunha](https://www.youtube.com/watch?v=vczVA6pUIpc)
- [Linkdin Osnir Cunha](https://linkdin.com/in/osnircunha)
- [PDF com os comando do Git](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
- [Comparando Workflows Git](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [feature brach workflow](https://docs.gitlab.com/ee/gitlab-basics/feature_branch_workflow.html)

