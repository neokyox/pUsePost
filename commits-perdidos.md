# Lidando com commits perdidos

Em alguns momentos podemos, devido ao exercício de forças ocultas, podemos perder algumas alterações de forma misteriosa. Mas desde que tenha sido feito o commit, as alterações podem ser recuperadas de algumas formas:

## Utilizando reflog

reflog é onde devemos buscar primeiro pelo commit perdido, pois mostra cada commit que modificou o repositório.

```shell
git log -g # Mostra o log de commits de forma detalhada, com data, sha1, autor e mensagem completa.
git reflog show # Mostra o log de forma simples e abreviada, contendo apenas o sha1, ação e short-message.
gitk --all --date-order $(git log -g --pretty=%H) # Mostra as alterações na tree em modo visual, com labels e dados ordenados por data
```

## Achados e perdidos

Commits e arquivos modificados as vezes podem se perder em resets, rebases e merges. Essas informações ficam 'penduradas' e fora do alcance de qualquer referencia, mas podem ser achadas utilizando o fsck.

```shell
git fsck | grep "dangling commit" | awk '{print $3;}' # Verifica a existência de commits pendurados no database local
gitk --all --date-order $(git fsck | grep "dangling commit" | awk '{print $3;}') # O mesmo do anterior, porém em modo visual
```

## Stash

Existe também a possibilidade de ter ocorrido um stash ao invés de um commit. Nesse caso podemos checar da seguinte maneira:

```shell
git stash show # Mostra os arquivos contidos no stash
git stash list # Lista os stashes existentes
gitk --all --date-order $(git stash list | awk -F: '{print $1};') # Lista os stashes existentes em modo gráfico
```

## Extravio

Tem certeza que fez o commit na branch correta? Podemos procurar o arquivo utilizando o comando:

```shell
git log -S --all --author=(seu usuário) --since=YYYY-MM-DD # Mostra todos os commits do seu usuário a partir da data X
gitk --all --author=(seu usuário) --date-order # Mostra todos os commits do seu usuário em modo gráfico
```