# Boas práticas com o GIT

Boas práticas podem variar de ambiente pra ambiente, porém esse modelo foi baseado nas regras de vários repositórios cujo fluxo de commits e pull requests são altos. O intuito é manter esse ~guia~ sempre atualizado, contando com a ajuda de toda a equipe, para deixar o mesmo sempre de acordo com as necessidades do time.

## Aumente a frequência de commits

*If you force good commit practices consistently, you will be able to drive the engineering culture and the code itself to a better state.*

Fazer commits mais cedo e com maior frequência ajuda a previnir a perda de dados, assim como também nos ajuda a identificar a partir de qual momento a feature quebrou na sua branch local. Ao se trabalhar com git podemos seguir as seguintes regras para commits:

+ Se é difícil dar nomes talvez seja melhor quebrar o commit antes.
+ Mais commits é melhor que menos commits.
+ É interessante colocar o número da issue no commit para ajudar a minerar o histórico
+ Commits não deveriam quebrar o build (serem atômicos).
+ Commits de funcionalidade não devem conter mudança de estilo, espaçamento, etc
+ Commits não deveriam necessitar mais de 5 a 10 minutos para serem compreendidos e revisados

## Crie mensagens de commit mais úteis

Quando executamos o git log ou usamos o gitk percebemos o quanto uma mensagem de commit mal elaborada/formatada pode atrapalhar nas pesquisas. Mensagens mais curtas e objetivas facilitam a leitura e agilizam o entendimento do commit.

### Exemplos:

Ruim:

```sh
'corrigindo erro'
'Removendo códigos inúteis'
```

Os commits acima não dizem a qual parte do sistema estão referidos, nem quais arquivos. Somos obrigados a checar todo o diff para exatamente o que e onde foram feitas alterações.

Bom:

```sh
'docs(README): atualiza o README para a versão 1.6.1'
'fix(Processos): corrige erro de translate3d no switch do style guide'          
```

Em ambos casos acima, conseguimos entender o tipo de alteração, em qual o módulo a tarefa foi executada e o que foi feito.

### Guia de commit message

Nos exemplos anteriores, o guia de contribuição do Google foi usado. Nele existe as seguintes regras com relação a commit messages:

+ Mensagens mais legíveis
+ Melhor tracking de alterações através do histórico do projeto
+ Máximo de 100 caracteres na commit message
+ Estrutura de commit message definida

#### Estrutura de Commit Message

Temos a seguinte estrutura:

```
<tipo>(<escopo>): <assunto>
```

A presença do tipo e assunto na mensagem de commit é obrigatório, enquanto o escopo é opcional.

Com relação ao tipo dos commits, temos os seguintes:

* build: Alterações que afetam diretamente o build system ou dependências externas
* ci: Alterações nos arquivos de configuração do CI  ou scripts (ex.: Travis, Circle, BrowserStack, SauceLabs, codacy)
* docs: Somente alterações na documentação do projeto
* feat: Nova feature
* fix: Bug fix
* perf: Alterações de código que tenham como finalidade, melhorar a performance do sistema
* refactor: Alterações de código que não corrigem bugs nem adicionam novas features
* style: Alterações que não alteram a razão do código (white-space, formatação, etc)
* test: Novos testes ou correções em testes já existentes

Em assunto, temos as seguintes regras:

+ Use verbos no imperativo: 'corrige' e não 'corrigido', 'corrigindo'
+ Não use letra maiúscula na primeira letra do assunto
+ Não encerre o assunto com ponto (.)
