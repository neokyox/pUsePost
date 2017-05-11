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

git add

git commit 

git push

git status

git checkout

