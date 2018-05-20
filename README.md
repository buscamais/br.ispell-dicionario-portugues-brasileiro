# br.ispell - Dicionário português brasileiro Ispell
> Este repositório é apenas cópia do br.ispell 3.0 beta4 (2003-03-25) que pode
ser obtida diretamente de <https://www.ime.usp.br/~ueda/br.ispell/beta.html>.
O principal motivo é servir de uma das referências para o
[fititnt/linguistic-datasets-portuguese](https://github.com/fititnt/linguistic-datasets-portuguese).

> O br.ispell também pode ser instalado até hoje (2018) como pacote de boa parte
das distribuições línux até a presente data como ortográfico que suporte
Ispell / Aspell. Porém pelas minhas buscas, todas as instalações que fazem uso
do br.ispell _apenas_ atualizaram arquivos que o tornam compatível com versões
mais recentes de sistemas operacionais, isto é, muito provavelmente desde
2003 e da versão 3.0 beta4 não houve qualquer atualização por parte da
comunidade no conteúdo.

> A seguir o conteúdo de [br.ispell/README]

----

Este é o anúncio da versão 3.0 (beta) do br.ispell, um pacote
para revisão ortográfica do português do Brasil com conteúdo
lexical, programas e documentação, estando esse conjunto
livremente disponível sob os termos da licença GNU GPL.

Nesta versão o pacote está ganhando diversos recursos
novos. Assim que eles estiverem melhor estabilizados, será feito
o release 3.0 de fato. Sugestões e críticas são bem-vindas, bem
como a participação nos trabalhos. Para tanto, envie email para
ueda@ime.usp.br e/ou para a lista criada pelo Cláudio (v. n. 9
abaixo). Saudações a todos,

Ricardo Ueda.

---

COMO OBTER A NOVA VERSÃO
------------------------

A versão 3.0 beta pode ser obtida a partir do endereço

    http://www.ime.usp.br/~ueda/br.ispell/beta.html

Nessa página deverão também ser publicadas notícias sobre os
progressos, até o release de fato da nova versão.

A extração dos arquivos e eventuais testes com o pacote podem ser
feitos tanto no Linux quanto no Windows, mas subentendem um certo
conhecimento do ambiente e das ferramentas do Unix, bem como a
instalação, no Windows, de ferramentas que não são nativas.


NOVIDADES DA VERSÃO 3.0
-----------------------

  1. Várias correções
  2. Suporte para aspell e myspell (OpenOffice)
  3. Revisão cuidadosa do conjugador de verbos
  4. Tentativa de padronização da flexão dos nomes
  5. Lematização e expansão de formas em perl
  6. Separação silábica e ordenação fonética
  7. Tentativa de anotação e classificação gramatical e semântica
  8. Sistema de manutenção online
  9. Lista de discussão

Dentre os novos recursos, alguns estão implementados na
ferramenta "fl" (arquivo "fl" do pacote). É um script (programa)
perl. O manual (man page) está incluído no próprio script, na
forma de comentário, no início do arquivo. Ele traz vários
exemplos práticos de uso (por exemplo separação silábica de uma
palavra dada, cálculo do infinitivo de um verbo, etc).


DETALHES SOBRE AS NOVIDADES
---------------------------

Alguns dos arquivos citados a seguir não estão presentes no
tarball distribuído, devendo ser gerados como segue:

    $ make br.aff
    $ make br.ispell

Isso leva uns 4 minutos numa máquina de 1GHz.


1. Várias correções
-------------------

A base para a versão 3.0 do br.ispell foi a versão 2.5, que não
chegou a ser distribuída. A versão 2.5 foi preparada por Imre
Simon, a partir da 2.4, através de um trabalho extenso de
revisão.


2. Suporte para aspell e myspell (OpenOffice)
---------------------------------------------

Os arquivos de que o myspell necessita são criados de forma
automática. Há mais detalhes sobre isso no Makefile. Há detalhes
sobre como usar esses arquivos em

  http://www.ime.usp.br/~ueda/br.ispell/index.html#OOo
  http://oobr.querencialivre.rs.gov.br/docajuda_dict.php

Obs. O Augusto Tavares Rosa Marcacini fez um porte independente
para o myspell, que pode ser encontrado em
http://dict.progbits.com/download_dictionary.html


3. Revisão cuidadosa do conjugador de verbos
--------------------------------------------

O conjugador de verbos foi revisado de forma cuidadosa por várias
pessoas (veja os créditos abaixo). Toda a morfologia conhecida
pelo conjugador pode agora ser exportada na forma de tabela de
afixos do ispell. Isso significa que (até certo ponto) o conteúdo
total do conjugador pode agora ser utilizado sem o conjugador,
isto é, sem necessidade de entender, utilizar ou manusear o
código do conjugador.


4. Tentativa de padronização da flexão dos nomes
------------------------------------------------

A flexão dos nomes (substantivos e adjetivos) foi revisada,
reorganizada e ampliada.

A flexão dos nomes apresenta uma uniformidade menor e portanto
uma complexidade maior do que a conjugação verbal. A conjugação
verbal do pacote br.ispell pode hoje ser considerada completa, ou
quase. A flexão dos nomes está tentando aproximar-se disso.

A atual tentativa de ajustes na flexão dos nomes baseia-se em
blocos de afixos unívocos (flags A-Z no arquivo br.aff.nv),
seqüencias de regras de afixos e listas dessas seqüencias. Essas
listas são citadas na documentação como "paradigmas de flexão
nominal", e o estado delas pode ser examinado na seção
"paradigmas nominais" do arquivo br.base. Cada lema da seção de
verbetes do arquivo br.base refere um paradigma de flexão através
da chave par=N.

As deficiências da atual tentativa estão principalmente na flexão
de grau.


5. Lematização e expansão de formas em perl
-------------------------------------------

O procedimento de expansão de formas do ispell e a sua inversão
foram implementados em perl. A razão principal disso é o fato do
ispell estar caindo em desuso em favor do aspell ou outros. Essa
implementação não é eficiente, mas permite que muitos testes de
volume possam ser feitos utilizando-se o formato da tabela de
afixos do ispell, que é bastante prático, sem necessidade de
instalar o ispell manualmente, ou mesmo de conhecê-lo. Em
particular, o infinitivo de um verbo pode agora ser calculado
através de qualquer uma das suas formas, visto que elas
encontram-se tabeladas como afixos do ispell (veja item 3 acima).

A implementação feita não é eficiente pela falta de um índice. No
atual estado o seu uso demanda paciência e cpu rápida. Além
disso, ela não inclui todos os recursos do ispell, mas apenas a
expansão de formas e o cálculo de raízes.


6. Separação silábica e ordenação fonética
------------------------------------------

O Osmar Ritz estava organizando um dicionário de nomes. Ao
desistir do projeto, ele enviou-me uma lista com cerca de 12000
nomes de pessoas.

Muitas entradas não estão conformes à ortografia usual ("Kaio",
"Aleksandro", etc). Na tentativa de normalizar a ortografia de
forma automática, arriscamos escrever um procedimento de
ordenação fonética simples baseado em separação silábica.

Essa tentativa está agora no ponto dos ajustes finos da
codificação da equivalência fonética de sílabas (ex. "tha" =
"ta"). Para examiná-la, observe no arquivo fl os exemplos de uso
e o código das funções "vf" e "silabas".

Além disso, o pacote agora calcula um silabário de forma
automática (veja a entrada "silabas" do Makefile). O pacote
inclui também cerca de 200 testes de separação silábica (arquivo
testesep) extraídos de livros de Hêndricas Nadólskis, Napoleão
Mendes de Almeida, Celso Luft, Osmar Barbosa, Celso Cunha e José
Oiticica.


7. Tentativa de anotação e classificação gramatical e semântica
---------------------------------------------------------------

A manutenção de um vocabulário flexionado ao longo do tempo exige
a anotação das entradas, e uma estruturação gramatical e/ou
semântica.

Desde o surgimento do pacote br.ispell, várias tentativas de
anotação e estruturação foram feitas. Agora todo o conteúdo nelas
acumulado foi convertido para um formato simples que suporta as
anotações mais comuns.

Esse formato imita mais ou menos um dicionário tradicional,
acrescentando informações de origem (autor) da anotação, flexão e
uma classificação semântica.

Para examinar esse formato, basta carregar num editor de textos o
arquivo br.base do pacote e navegar um pouco nele. As abreviações
estão descritas no arquivo fl, procedimento registre_abrevs. Se
houver necessidade, leia na documentação da ferramenta fl
(encontra-se no início do arquivo fl do pacote) a descrição
completa do formato.

Praticamente todas as entradas do arquivo br.base estão
flexionadas no padrão descrito acima (n. 4). Essa flexão foi
produzida manualmente ao longo dos anos. Um dos pontos fracos
dela, já citado acima, é a flexão de grau.

A classificação semântica adotada assemelha-se àquela dos livros
didáticos para aprendizado de línguas, isto é, é feita em torno
de temas do cotidiano como "frutas", "profissões", etc. Há
atualmente entre 200 e 300 classes. Uma grande quantidade de
lemas (certamente mais de 50%) não está classificada.

A classificação gramatical (isto é, nas classes "substantivo",
"adjetivo", "numeral", "verbo", etc) abrange 75% dos não verbos
(os verbos são tratados à parte pelo programa conjugue). Muitas
classificações estão, entretanto, incompletas (ex. "substantivo"
ao invés de "substantivo feminino"). A classificação gramatical
foi quase totalmente deduzida de forma automática a partir da
classificação semântica (veja a classificação por categoria na
seção "semântica" do arquivo br.base) e das próprias formas
(ex. -ção,s.f., -mente,adv., etc).


8. Sistema de manutenção online
-------------------------------

Foi criado um sistema de manutenção online. Está operando apenas
ao nível de formas flexionadas/conjugadas, mas isso deverá ser
melhorado em breve para que ele suporte a fatoração nos lemas. O
sistema está provisoriamente hospedado em

    http://www.claraocr.org/br.ispell

mas migrará para outro lugar assim que possível.

Esse sistema quer ser uma ferramenta para a manutenção
cooperativa e, até onde isso for possível, impessoal do
vocabulário no longo prazo.


9. Lista de discussão
---------------------

O Cláudio Ferreira Filho criou uma lista de discussão. Para
inscrever-se envie email para

    verificador-subscribe@br-pt.openoffice.org

Essa lista deverá tornar-se um apoio importante para usuários e
desenvolvedores.


CRÉDITOS
--------

A revisão feita por Imre Simon contou com conteúdo obtido junto
a Edleno Silva de Moura e Nivio Ziviani.

Vários problemas do conjugador foram reportados ou corrigidos por
Imre Simon, Raul Fernandes, Alexandre Hamada, e Augusto Tavares
Rosa Marcacini. Agradecimentos especiais para Alexandre Hamada.

Rodrigo Siqueira contribuiu listas extensas de palavras.

Raul Fernandes contribuiu um vocabulário médico extenso.

O suporte a OpenOffice contou com a ajuda de Olivier Hallot,
Cleber Gonçalves, Claudio Ferreira Filho, Winston Leibon e
Nicolau A. S. Rodrigues.

Osmar Ritz contribuiu outras listas temáticas além dos nomes de
pessoas.

Alguns ajustes ou novos recursos deveram-se a esclarecimentos
feitos por Maria Tereza Camargo Biderman.

Carlos E. Morimoto ofereceu-nos gentilmente as palavras do
dicionário http://www.guiadohardware.net/dicionario

Marcelo Finger emprestou a terceira edição do Cândido de
Figueiredo para testes de digitalização. Aliás, esse é um terreno
em que obtivemos progressos sensíveis.

As morfolimpíadas e as discussões de avaliação que surgiram por
iniciativa da Diana Santos têm sido um incentivo para os
trabalhos em torno do br.ispell.

Várias outras pessoas fizeram observações ou apontaram
problemas. Dentre elas gostaria de lembrar Leslie H. Watter,
E. A. Tacão, Wanderlei Cavassin, e André Uratsuka.

Agradecimentos relativos às versões anteriores podem ser
encontrados em http://www.ime.usp.br/~ueda/br.ispell

Se esqueci alguém, peço desculpas e também que me avisem!
