# Lidando com commits perdidos

Em alguns momentos, devido ao exercício de forças ocultas, podemos perder algumas alterações de forma misteriosa. Mas, desde que tenha sido feito o commit, as alterações podem ser recuperadas de algumas formas, tais como:

## Utilizando reflog

reflog é onde devemos buscar primeiro pelo commit perdido, pois mostra cada commit que modificou o repositório.

```shell
# Mostra o log de commits de forma detalhada, com data, sha1, autor e mensagem completa.
git log -g

# Mostra o log de forma simples e abreviada, contendo apenas o sha1, ação e short-message.
git reflog show

# Mostra as alterações na tree em modo visual, com labels e dados ordenados por data
gitk --all --date-order $(git log -g --pretty=%H)
```

## Achados e perdidos

Commits e arquivos modificados as vezes podem se perder em resets, rebases e merges. Essas informações ficam 'penduradas' e fora do alcance de qualquer referência, mas podem ser achadas utilizando o fsck.

```shell
# Verifica a existência de commits pendurados no database local
git fsck | grep "dangling commit" | awk '{print $3;}'

# O mesmo do anterior, porém em modo visual
gitk --all --date-order $(git fsck | grep "dangling commit" | awk '{print $3;}')
```

## Stash

Existe também a possibilidade de ter ocorrido um stash ao invés de um commit. Nesse caso podemos checar da seguinte maneira:

```shell
# Mostra os arquivos contidos no stash
git stash show

# Lista os stashes existentes
git stash list

# Lista os stashes existentes em modo gráfico
gitk --all --date-order $(git stash list | awk -F: '{print $1};')
```

## Extravio

Tem certeza que fez o commit na branch correta? Podemos procurar o arquivo utilizando o comando:

```shell
# Mostra todos os commits do seu usuário a partir da data X
git log -S --all --author=(seu usuário) --since=YYYY-MM-DD

# Mostra todos os commits do seu usuário em modo gráfico
gitk --all --author=(seu usuário) --date-order
```