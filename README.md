# git-and-gitlab 
<b>[em construção]</b>
Esse projeto descreve o uso do [feature brach workflow](https://martinfowler.com/bliki/FeatureBranch.html) no GitLab na prática usando o Git no IntelliJ e no terminal, o uso de uma pipeline de CI (integração continua) descrita em arquivo .yml para compilar, testar e publicar ao fazer merge request com a branch `main` e
as funcionalidades e comandos mais utilizados durante o uso desse fluxo com o Git e GitLab no dia a dia. 

# Feature branch workflow
`Feature branch workflow` segundo [Martin Fowler](https://martinfowler.com/bliki/FeatureBranch.html) esse é um padrão de ramificação de código-fonte em que um desenvolvedor abre um branch quando começa a trabalhar em um novo recurso, faz todo o trabalho neste branch e integra as mudanças em um branch (main) quando o recurso é concluído.

# VCS - Version Control System
Controle de versões diferentes de um documento.
- São sistemas Gerenciadores de versões
- Mantém o registro de modificação do código
- Quem? O que? Quando? Por que? 
- Disponibilizar código mais recente

# GIT e GitHub
- DVCS - Distributed Version Control System 
- Cada cópia do repositório contém o histórico completo de todas as alterações
- Sistema Distribuido
- Git Open Source
- GitHub não é Open Source


Repositório remoto e repositório local (GitLab segue a mesma ideia)

![](/git-remote.png)

# Feature branch
![](/feature-branch.jpg)


# Fluxo de trabalho
![](/lifecycle-git.png)

# Comandos GIT
`git init` Cria um repositorio git (pasta .git)

### Git config
Usuário pode ser local ou global - opção --global

Identificando o usuario no repositorio local
`git config user.nome "ukaliko"´` 
`git config user.email "ukaliko@gmail.com"`

# Arquivo .gitignore
Armazena informações de padrão de arquivos e pastas que não serão versionados
- Formato expressões regulares

### Arquivos no .gitignore
Para evitar que um arquivo continue aparencendo na lista de arquivos versionados mesmo estando no .gitgnore.
usar `git rm --cached *.log` ou `git update-index --assume-unchanged *.log`

### Status do repositório Git
`git status` 

### Versionar as alterações feitas 
`git commit -m "digite a msg aqui"`

### Ver os logs dos commit no Git
`git log`

### Git config
Visualizando configurações do git (atalhos para comandos git)

`git config -l | grep alias`

`git config -l | grep core`

### Git acm (verificar alias)
Esse comando adiciona e faz o comit de uma vez só (Comando não encontrado non config do git)

`git acm "msg aqui"`

### Criando uma nova branch
Cria a branch e a seta como a default
`git checkout -b feature1`

### Mudando de branch
`git switch main`

Troca de branch criando a branch feature2 -c (cria a branch)
git switch -c feature2

### Visualizando a arvore de commit do git
git log --graph --oneline --all
ou
git log --graph --abbrev-commit --decorate --format=format:'%C(yellow)%h%C(reset)%C(auto)%d%C(reset) %C(normal)%s%C(reset) %C(dim white)%an%C(reset) %C(dim blue)(%ar)%C (reset)' --all

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

### commit Git no intelliJ
clicar na aba `Local change do Git` com o botão direito e selecionar `Commit Files...`

### para remover um branch remoto ou local
[Consultar esse link](https://receitasdecodigo.com.br/devops/git-remover-um-branch-local-ou-remoto)

### Desfazer um commit no intellij
Na aba Git clicar no commit e selecionar a opção `Undo commit...`

### Merge Request 
Solicitação feita pelo desenvolvedor, no gitLab ao um responsável pela organização e distribuição do código, onde o mesmo
vai rodar pode rodar pipeline de testes, deploy e build. 


### Mudar de branch
`git checkout feature2`

Traz o conteúdo da `main` para a branch `feature2`

### git Rebase 
- Reescreve a arvore de commit da branch features, movendo a ligação para o ultimo commit da main
- Mantém a estrura de commit limpa, usar sempre se ainda não fez nenhum commit para o main `rebase master > feature`

# Referências
- [Live conding Osnir Cunha da Inter](https://www.youtube.com/watch?v=vczVA6pUIpc)
- [PDF com os comando do Git](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
- [Comparando Workflows Git](https://www.atlassian.com/git/tutorials/comparing-workflows)
- [feature brach workflow](https://docs.gitlab.com/ee/gitlab-basics/feature_branch_workflow.html)

