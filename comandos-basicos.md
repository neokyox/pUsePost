# Comandos básicos

Segue uma pequena lista de comandos GIT e suas aplicações.

## Adicionando seu usuário e e-mail

É importante configurar seu usuário e e-mail do git, pois a cada commit essas informações são usadas para identificar o autor.

```sh
# Configurar seu usuário:
git config --global user.name "Usuário"
# Configurar seu E-mail
git config --global user.email "E-mail"

# Conferindo os dados inseridos:
$ git config --global --list
```

## Clonar um repositório

git clone né.

## Branches

Branches são utilizadas para desenvolver funcionalidades isoladas umas das outras.

```sh
# Cria uma nova branch e muda para a mesma:
git checkout -b <nome-da-branch>

# Muda de uma branch para outra:
git checkout <nome-da-branch>

# Lista todas as branches no seu repositório e também indica sua branch atual:
git branch

# Deleta uma branch:
git branch -d <nome-da-branch>

# Faz o push da branch para o repositório remoto:
git push origin <nome-da-branch>

# Faz o push de todas as branchs para o repositório remoto:
git push --all origin

# Deleta a branch no repositório remoto:
git push origin :<nome-da-branch>
```

## Commits

```sh
# Mostra os arquivos alterados desde seu último commit
git status

# Adiciona um arquivo específico
git add <arquivo>

# Adiciona todos os arquivos do diretório
git add .

# Cria um commit
git commit -m 'primeiro commit'

# Envia o commit para o repositório remoto
git push
```

## Consultando o histórico

```sh
# Consultando histórico via bash
git log

# Consultando histórico de forma resumida
git log --pretty=oneline

# Consultando via GUI
gitk
```