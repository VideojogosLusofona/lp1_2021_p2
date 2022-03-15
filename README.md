# Projeto 1 de Linguagens de Programação | 2021/2022
## Introdução

Os grupos devem implementar o jogo **Snakes & Ladders** na forma de uma 
aplicação de consola .NET Core. O jogo deve ser PvP (_Player vs Player_), sem 
qualquer tipo de inteligência artificial.

## Regras do Jogo

O jogo **Snakes & Ladders** é um jogo simples que depende exclusivamente dos 
dados. O jogo consiste numa "corrida" onde o objetivo do jogo é ser o primeiro 
a chegar à ultima casa do tabuleiro. A implementação será uma variação deste
jogo.

![Possível tabuleiro inicial](img/SnakesBoard.png "Tabuleiro de Jogo")

O tabuleiro consiste numa sequencia de 100 "casas" no qual as casas podem ter 
vários tipos, que afecta a posição do jogador no tabuleiro (ver secção *Tipo Casas*). 
O movimento consiste avançar o "pião" - que representa cada jogador - o numero de 
casas equivalente ao que foi obtido no lançamento dos dados. 

![Como se avança no tabuleiro](img/SnakesMovement.png "Tabuleiro de Jogo")

### Mecânicas do Tabuleiro

Nesta implementação do **Snakes and Ladders** o jogo irá começar sempre com um 
tabuleiro aleatório onde o posicionamento dos differentes tipos de casas irá seguir 
uma heurística específica definido em baixo. 

O tabuleiro é uma matriz de 10x10, i.e. 10 casas por linha e coluna, onde cada jogador 
percorre uma linha até ao fim, para chegar a coluna seguinte (ou seja uma progressão 
horizontal). 

### Regras de Jogo

O jogo é jogado com 2 a 4 jogadores. 

A cada turno um jogador lança um dado de 6 lados, e avança o número de casas 
equivalente ao valor obtido. Se o jogador cai numa **casa especial**, a regra associada 
a essa casa é ativada immediatamente. Após o efeito da casa especial ter sido aplicada, 
a vez de jogar é passada para o jogador seguinte.

Casos Especiais:

* Se o jogador calha numa casa onde já existir outro jogador, o oponente é forçado a 
retroceder uma casa. Caso essa casa é especial, aplica-se na mesma a regra dessa casa 
de forma normal. 

* Caso o jogador ultrapassar o número necessário para chegar a ultima casa (e ganhar 
o jogo), este terá que retroceder o número de casas equivalente a diferença entre o 
número que saiu nos dados e o valor exato necessário. 
  * Ex: Falta duas casas para o João ganhar. Lançou 5 no dado, este irá retroceder 
  3 (5-2) casas contando a partir da ultima casa do tabuleiro. 

## Tipos de Casas

Existem 8 tipos de casas differentes aos quais têm heuristicas especificas de como 
podem ser posicionadas no tabuleiro (i.e. seguir estas regras para a criação do 
tabuleiro). 

* **Normal** - Casa normal sem regras especiais.
* **Snakes** - Esta casa faz com que o jogador retroceda immediatamente para uma casa 
que esteja no minímo a uma linha abaixo da casa corrente. Só pode existir no máximo 
10 casas deste tipo e no minimo 5 num tabuleiro.
* **Ladders** - Esta casa faz com que o jogador avance immediatemente para uma casa 
que esteja no minímo a uma linha acima da casa corrente. Só pode existir no máximo 
10 casas deste tipo e no minimo 5 num tabuleiro.
* **Cobra** - Esta casa obriga o jogador a voltar ao início do tabuleiro. Só pode 
existir uma casa deste tipo e este não pode estar nas duas primeiras linhas inicias. 
* **Boost** - Esta casa obriga o jogador a avançar duas casas. Só pode existir 5 
casas deste tipo no tabuleiro, e esta não pode existir na ultima linha.
* **U-Turn** - Esta casa obriga o jogador a retroceder duas casas. Só pode existir 
5 casas deste tipo no tabuleiro, e esta não pode existir na primeira linha. 
* **Extra Die** - Esta casa oferece um dado extra ao jogador, dado a possibilidade 
de usá-la a qualquer altura do jogo. Só pode existir 2 casas deste tipo. 
**Importante**: Um jogador nunca pode ter mais do que 1 dado extra de reserva. 
* **Cheat Die** - Esta casa oferece um dado "especial" oferencendo a possibilidade 
de substituir o valor de um dado por um escolhido pelo jogador (valores de 1 a 6). 
Só pode existir duas casas deste tipo no tabuleiro. 

## Visualização 

Toda a parte visual é feita na consola, e a cada turno é necessário mostrar o estado 
do tabuleiro aos jogadores, mostrando a posição corrente de todos os jogadores, as 
casas especiais e os dados extra e cheat-die que o jogador tenha.

# Funcionamento da Aplicação

O funcionamento exato da aplicação é da responsabilidade de cada grupo. No
entanto, quando a aplicação começa, **deve ser claro como cada jogador joga**,
ou seja, o jogo deve ter instruções muito claras sobre que teclas fazem o quê.
Por outras palavras, os grupos devem ter em conta as regras importantes do
_game design_, pois serão tidas em conta na avaliação do projeto.

A aplicação deve funcionar em Windows, macOS e Linux. A melhor estratégia para
garantir que assim seja é testar o jogo em Linux (e.g., numa máquina virtual).
Algumas instruções incompatíveis com macOS e Linux são, por exemplo:

* [Console.Beep()](https://docs.microsoft.com/dotnet/api/system.console.beep)
* [Console.SetBufferSize()](https://docs.microsoft.com/dotnet/api/system.console.setbuffersize)
* [Console.SetWindowPosition()](https://docs.microsoft.com/dotnet/api/system.console.setwindowposition)
* [Console.SetWindowSize()](https://docs.microsoft.com/dotnet/api/system.console.setwindowsize)
* Entre outras.

As instruções que só funcionam em Windows têm a seguinte indicação na sua
documentação:

![The current operating system is not Windows.](img/notsupported.png "The current operating system is not Windows.")

### Organização do código e estrutura de classes

O projeto deve estar devidamente organizado, fazendo uso de classes, _structs_
e enumerações. Cada classe, _struct_ ou enumeração deve ser colocada num
ficheiro com o mesmo nome. Por exemplo, uma classe chamada `Piece` deve ser
colocada no ficheiro `Piece.cs`. A estrutura de classes deve ser bem pensada e
organizada de uma forma lógica, e [cada classe deve ter uma responsabilidade
específica e bem definida][SRP].

## Objetivos e critério de avaliação

Este projeto tem os seguintes objetivos:

* **O1** - Programa deve funcionar como especificado e deve ter em conta as
  regras básicas do _game design_.
* **O2** - Projeto e código bem organizados, nomeadamente:
  * Estrutura de classes bem pensada (ver secção [Organização do código e
    estrutura de classes](#organizacao-do-codigo-e-estrutura-de-classes)).
  * Código devidamente comentado e indentado.
  * Inexistência de código "morto", que não faz nada, como por exemplo
    variáveis, propriedades ou métodos nunca usados.
  * Projeto compila e executa sem erros e/ou *warnings*.
* **O3** - Projeto adequadamente documentado com [comentários de documentação
  XML][XML]. A documentação gerada em formato HTML em [Doxygen] ou [DocFX],
  deve estar incluída no `zip` do projeto, mas **não** integrada no repositório
  Git.
* **O4** - Repositório Git deve refletir boa utilização do mesmo, nomeadamente:
  * Devem existir *commits* de todos os elementos do grupo, _commits_ esses
    com mensagens que sigam as melhores práticas para o efeito (como indicado
    [aqui](https://chris.beams.io/posts/git-commit/),
    [aqui](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53),
    [aqui](https://github.com/erlang/otp/wiki/writing-good-commit-messages) e
    [aqui](https://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)).
  * Ficheiros binários não necessários, como por exemplo todos os que são
    criados nas pastas `bin` e `obj`, bem como os ficheiros de configuração
    do Visual Studio (na pasta `.vs` ou `.vscode`), não devem estar no
    repositório. Ou seja, devem ser ignorados ao nível do ficheiro
    `.gitignore`.
  * *Assets* binários necessários, como é o caso da imagem do diagrama UML,
    devem ser integrados no repositório em modo Git LFS.
* **O5** - Relatório em formato [Markdown] (ficheiro `README.md`),
  organizado da seguinte forma:
  * Título do projeto.
  * Autoria:
    * Nome dos autores (primeiro e último) e respetivos números de aluno.
    * Informação de quem fez o quê no projeto. Esta informação é
      **obrigatória** e deve refletir os *commits* feitos no Git.
    * Indicação do repositório Git utilizado. Esta indicação é
      opcional, pois podem preferir manter o repositório privado após a
      entrega.
  * Arquitetura da solução:
    * Descrição da solução, com breve explicação de como o código foi
      organizado, bem como dos algoritmos não triviais que tenham sido
      implementados.
    * Um diagrama UML de classes simples (i.e., sem indicação dos
      membros da classe) descrevendo a estrutura de classes.
  * Referências, incluindo trocas de ideias com colegas, código aberto
    reutilizado (e.g., do StackOverflow) e bibliotecas de terceiros
    utilizadas. Devem ser o mais detalhados possível.
  * **Nota:** o relatório deve ser simples e breve, com informação mínima e
    suficiente para que seja possível ter uma boa ideia do que foi feito.
    Atenção aos erros ortográficos e à correta formatação [Markdown], pois
    ambos serão tidos em conta na nota final.

O projeto tem um peso de 5 valores na nota final da disciplina e será avaliado
de forma qualitativa. Isto significa que todos os objetivos têm de ser
parcialmente ou totalmente cumpridos. A cada objetivo, O1 a O5, será atribuída
uma nota entre 0 e 1. A nota do projeto será dada pela seguinte fórmula:

*N = 5 x O1 x O2 x O3 x O4 x O5 x D*

Em que *D* corresponde à nota da discussão e percentagem equitativa de
realização do projeto, também entre 0 e 1. Isto significa que se os alunos
ignorarem completamente um dos objetivos, não tenham feito nada no projeto ou
não comparerecem na discussão, a nota final será zero.

# Entrega

O projeto deve ser entregue por **grupos de 2 a 3 alunos** via Moodle até às
23h de 16 de maio de 2021. Um (e apenas um) dos elementos do grupo deve ser
submeter um ficheiro `zip` com a solução completa, nomeadamente:

* Pasta escondida `.git` com o repositório Git local do projeto.
* Documentação HTML gerada com [Doxygen] ou [DocFX]. Esta documentação
  **não** deve ser incluída no repositório Git, pelo que a respetiva pasta deve
  estar explicitamente ignorada a nível do ficheiro `.gitignore`.
* Ficheiro da solução (`.sln`).
* Pasta do projeto, contendo os ficheiros `.cs` e o ficheiro do projeto
  (`.csproj`).
* Ficheiro `README.md` contendo o relatório do projeto em formato [Markdown].
* Ficheiro de imagem contendo o diagrama UML. Este ficheiro deve ser incluído
  no repositório em modo Git LFS.
* Outros ficheiros de configuração, como por exemplo `.gitignore`,
  `.gitattributes`, `Doxyfile` ou `docfx.json`.

Não serão avaliados projetos sem estes elementos e que não sejam entregues
através do Moodle.

# Honestidade académica

Nesta disciplina, espera-se que cada aluno siga os mais altos padrões de
honestidade académica. Isto significa que cada ideia que não seja do
aluno deve ser claramente indicada, com devida referência ao respectivo
autor. O não cumprimento desta regra constitui plágio.

O plágio inclui a utilização de ideias, código ou conjuntos de soluções
de outros alunos ou indivíduos, ou quaisquer outras fontes para além
dos textos de apoio à disciplina, sem dar o respectivo crédito a essas
fontes. Os alunos são encorajados a discutir os problemas com outros
alunos e devem mencionar essa discussão quando submetem os projetos.
Essa menção **não** influenciará a nota. Os alunos não deverão, no
entanto, copiar códigos, documentação e relatórios de outros alunos, ou dar os
seus próprios códigos, documentação e relatórios a outros em qualquer
circunstância. De facto, não devem sequer deixar códigos, documentação e
relatórios em computadores de uso partilhado, e muito menos usar
repositórios Git públicos (embora os mesmos possam ser tornados públicos
12h após a data limite de submissão).

Nesta disciplina, a desonestidade académica é considerada fraude, com
todas as consequências legais que daí advêm. Qualquer fraude terá como
consequência imediata a anulação dos projetos de todos os alunos envolvidos
(incluindo os que possibilitaram a ocorrência). Qualquer suspeita de
desonestidade académica será relatada aos órgãos superiores da escola
para possível instauração de um processo disciplinar. Este poderá
resultar em reprovação à disciplina, reprovação de ano ou mesmo suspensão
temporária ou definitiva da ULHT.

*Texto adaptado da disciplina de [Algoritmos e
Estruturas de Dados][aed] do [Instituto Superior Técnico][ist]*

## Licenças

* Este enunciado é disponibilizado através da licença [CC BY-NC-SA 4.0].

## Metadados

* Autores: [Phil Lopes] e [Nuno Fachada]
* Curso:  [Licenciatura em Videojogos][lamv]
* Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[lamv]:https://www.ulusofona.pt/licenciatura/videojogos
[Phil Lopes]:https://github.com/worshipcookies
[Nuno Fachada]:https://github.com/fakenmc
[ULHT]:https://www.ulusofona.pt/
[aed]:https://fenix.tecnico.ulisboa.pt/disciplinas/AED-2/2009-2010/2-semestre/honestidade-academica
[ist]:https://tecnico.ulisboa.pt/pt/
[Markdown]:https://guides.github.com/features/mastering-markdown/
[Doxygen]:https://www.stack.nl/~dimitri/doxygen/
[DocFX]:https://dotnet.github.io/docfx/
[KISS]:https://en.wikipedia.org/wiki/KISS_principle
[XML]:https://docs.microsoft.com/dotnet/csharp/codedoc
[SRP]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[2º projeto de LP1 2018/19]:https://github.com/VideojogosLusofona/lp1_2018_p2_solucao
