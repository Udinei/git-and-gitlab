# git-and-gitlab
Esse projeto descreve o uso do fluxo git flow. Trabalhando com Git e GitLab na prática usando o IntelliJ e as principais funcionalidades e os comandos mais utilizados durante o uso desse fluxo com o Git e GitLab no dia a dia. 

# VCS - Version Control System
Controle de versões diferentes de um documento.
- São sistemas Gerenciadores de versões
- Mantém o registro de modificação do código
- Quem? Oque? Quando? Por que? 
- Disponibilizar código mais recente

# DVCS - Distributed Version Control System 
Cada cópia do repositório contém o histórico completo de todas as alterações
- GIT 
- Sistema Distribuido
- Open Source

# GIT
Repositório remoto e repositorio local

![](/git-remote.png)

# Feature branch
![](/feature-branch.jpg)


# Fluxo de trabalho
![](/lifecycle-git.png)

# Comandos GIT
git init - Cria um repositorio git (pasta .git)
git status - Verificando o status do repositorio

### Git config
Usuario pode ser local ou global - opção --global

Identificando o usuario no repositorio local
`git config user.nome "ukaliko"´` 
`git config user.email "ukaliko@gmail.com"`

### Arquivo .gitignore
Armazena informações de padrão de arquivos e pastas que não serão versionadas
- Formato expressões regulares

### Status  do repositório
git status

### git commit
git commit -m "Adiciona o .gitignore com exclusao da target"

### git log
git log

### git config
Visualizando configurações do git (atalhos para comandos git)
git config -l | grep alias
git config -l | grep core

### git acm (verificar alias)
Esse comando adiciona e faz o comit de uma vez só (Comando não encontrado non config do git)
git acm "Adiciona Intellij ao gitignore"

### criando uma nova branch
Cria a branch e a seta como a default
git checkout -b feature1

### git switch
Alternando emtre branch
git switch main

Troca de branch criando a branch feature2 -c (cria a branch)
git switch -c feature2

### Visualizando a arvore de commit do git
git log --graph --oneline --all
ou
git log --graph --abbrev-commit --decorate --format=format:'%C(yellow)%h%C(reset)%C(auto)%d%C(reset) %C(normal)%s%C(reset) %C(dim white)%an%C(reset) %C(dim blue)(%ar)%C (reset)' --all

# Atualizando branch
### git merge
Atualizando a branch feature2, com os novos comits feitos na master(main)
cria um novo commit na branch
merge - main > feature2

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

# Fazendo um Merge request entre as branches



### Mudar para a branch feature2
git checkout feature2

git merge master(main)

Traz o conteudo da main para a branch feature2

### git Rebase 
Reescreve a arvore de commit da branch features, movendo a ligação para o ultimo commit da main
Mantem a estrura de commit limpa, usar sempre se ainda não fez nenhum commit para o main
rebase master > feature




