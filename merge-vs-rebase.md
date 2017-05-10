# Merge vs. Rebase

Esse é um assunto um tanto quanto controverso. 

## Visão conceitual

A primeira coisa a se entender é que git rebase e git merge são comandos desenvolvidos para integrar alterações de uma branch para outra. Mas os comandos fazem isso de forma diferente.

Consideremos que você começou a trabalhar em uma nova feature, então algum dev do time atualizou a master com novos commits e eles são relevantes para sua tarefa, para inserir esses commits na sua branch você tem duas opções: *merge* ou *rebase*.

### Opção 1: Merge

A opção mais fácil, basta executar o seguinte comando:

```sh
git checkout feature
git merge master
# Podemos fazer em uma única linha também
git merge master feature
```

Isso cria um novo commit de merge no topo da branch feature, de forma simples.

Por outro lado, isso significa que a branch feature vai ter um commit de merge extra a cada vez que precisar ser atualizada. Se a master é bem ativa, você pode acabar poluindo o histórico

### Opção 2: Rebase

Como uma alternativa ao merge, você pode utilizar o rebase da seguinte maneira:

```sh
git checkout feature
git rebase master
```

Isso move toda a branch feature para o topo da branch da master, incorporando todos os commits até aquele ponto. Mas ao contrário do merge, o rebase reescreve todo o histórico do projeto criando novos commits para cada commit da branch original.

O maior benefício do rebase é manter um histórico mais limpo e linear por eliminar commits de merge requeridos pelo git merge.

Já um dos pontos negativos é: rebase exige um conhecimento mais elevado sobre git. O mau uso do mesmo pode quebrar todo o repositório.

## Políticas de uso

### Always Rebase

Consideremos o *Always Rebase* com o seguinte exemplo: Quando o desenvolvimento de uma feature está completa, fazemos o rebase / squash dos itens da branch reduzindo os mesmos a um número significante de commits e evitando criar um commit de merge - podemos usar o --ff ou cherry-pick na branch destino.

Enquando a branch de feature estiver em desenvolvimento e precisamos manter a mesma atualizada, usamos o rebase - ao invés de pull ou merge - para não poluir o histórico.

#### Prós

+ Histórico de código linear e legível. Commits limpos e claros ajudam a manter a saúde do histórico
+ Podemos usar o histórico e as mensagens de commit como changelog automático. Por esse motivo é importante não poluir o histórico com commits nebulosos
+ Manipular um commit é mais fácil (ex.: reverter)

#### Contras

- Squash de uma branch a meros commits pode ocultar contexto de alguma alteração
- Rebase e pull requests não combinam muito bem, pois acaba ocultando algumas 'minor changes' durante o processo
- Rebase pode ser perigoso. Reescrever o histórico de branches compartilhadas tende a quebrar o fluxo de trabalho.

Nota: Quando o histórico de uma branch utilizada por vários desenvolvedores é reescrito, ocorre uma quebra geral em todas a branchs em desenvolvimento derivada da mesma.
### Always Merge


Consideremos o *Always Merge* no exemplo a seguir: Quando uma branch de uma feature é finalizada, fazemos um merge para a branch destino (master, develop ou rc).

Tenha certeza de fazer o merge com o comando --no-ff, que obriga o git a manter uma mensagem de commit em todos os casos

#### Prós

+ 'Traceability': mantemos informações históricas da branch de feature que foi feito o merge e agrupa todos os commits na descrição

#### Contras

- Histórico imensamente poluído por centenas de commits de merge e o visual chart do repositório pode ter uma série de linhas coloridas que não adicionam praticamente nenhum tipo de informação, exigindo um conhecimento de como usar o git log para explorar o histórico de forma eficaz
- Debugs usando git bisect tornam-se mais difíceis devido ao commits de merge

### Utilizando o rebase como ferramenta de limpeza

*Rebase as Cleanup* e *Always Rebase* são coisas completamente diferentes.