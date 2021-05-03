# git-and-gitlab
Trabalhando com Git e GitLab na prática usando o IntelliJ. As principais funcionalidades, e como trabalhar com o Git e GitLab no dia a dia. 

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
Gerenciamento de repósitorios
Similar ao GitHub e Bitbucket
Open Source
Organização de repósitorio em grupos
CI/CD

Mudar para a branch feature2
git checkout feature2

git merge master(main)

Traz o conteudo da main para a branch feature2

### git Rebase 
Reescreve a arvore de commit da branch features, movendo a ligação para o ultimo commit da main
Mantem a estrura de commit limpa, usar sempre se ainda não fez nenhum commit para o main
rebase master > feature




