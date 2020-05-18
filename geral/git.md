---
title: GIT - Sistema de controle de versões distribuído
description: Comandos básicos GIT
published: true
date: 2020-05-18T01:44:57.992Z
tags: git, versionamento
---

# Git init

* Para inicializarmos o Git em nosso projeto e a partir de então o projeto começar a ser versionado pelo Git executar o seguinte comando

```git

git init

```

# Git clone

* Para baixar o repositório do servidor e clonar na máquina local executar este comando juntamente como o link do prepositório

```git
git clone myproject.git
```

# Git pull

* Para atualizarmos o repositório local executar

```git
git pull

```
# Git remote
* Para sabermos para onde o estão sendo enviadas as alterações, executar

```git
git remote -v

```
# Git add
* Para adicionarmos os arquivos que estão sendo alterados na área de pré commit (staging area), executar
```git
git add nome_do_arquivo

```

* Ou para adicionar todos os arquivos de uma só vez, executar
```git
git add .

```

# Git reset
* Para removermos algum arquivo que foi adicionado erroneamente, executar

```git
git reset nome_do_arquivo

```

* Ou para remover todos os arquivos, executar

```git
git reset HEAD .

```

# Git commit
* Para salvarmos todas as alterações que realizamos, exeutar
```git
git commit -m "mensagem_do_commit"

```
# Git status
* Para verificarmos como esta o status do nosso repositório local, executar
```git
git status

```

# Git diff
* Para sabermos quais alterações foram realizadas, executar
```git
git diff

```

# Git branch
* Para listar quais branch existem, executar
```git
git branch
```
* Para criar uma nova branch, executar
```git
git branch nome_da_branch
```

* Para criar uma branch e ao mesmo tempo entrar nessa branch, executar
```git
git checkout -b nome_da_nova_branch
```

# Git checkout 
* Para entrarmos em uma branch, executar
```git
git checkout nome_da_nova_branch
```

* Para deletar uma branch
```git
git branch -d nome_da_nova_branch
```

# Git push

* Para enviar uma branch para o servidor, executar

```git
git push origin nome_da_branch
```

# Git merge master

* Para fazermos o merge das branchs será necessário primeiro, entrar na branch master
```git
git checkout master
```
* E depois executar
```git
git merge nome_branch
```
# Git hist

* Para visualizar o histórico de mudanças, executar
```git
git hist --all
```



