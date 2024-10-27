<a id="readme-top"></a>
# Documentação do QuickStatements (QS) 3.0

<details>
 <summary>Traduções:</summary>
 <ul>
  <li><a href="translations/qts-index-fr.md">Francês</li>
  <li><a href="translations/qts-index-pt.md">Português</li>
   <li><a href="translations/qts-index-es.md">Espanhol</li>
 </ul>
</details>

## Índice
<!-- TABELA DE CONTEÚDOS -->
<details>
  <summary>Índice</summary>
  <ol>
    <li><a href="#overview">Visão Geral do QuickStatements</a></li>
    <li><a href="#a-brief-on-wikidata">Um Resumo sobre o Wikidata</a>
      <ul>
        <li><a href="#structure-of-wikidata">Estrutura do Wikidata</a></li>
        <li><a href="#lda">Rótulos, descrições e apelidos</a></li>
        <li><a href="#wiki-statements">Declarações do Wikidata</a></li>
        <li><a href="#syntax-and-command-structure">Sintaxe e Estrutura de Comando</a></li>
      </ul>
    </li>
    <li><a href="#qs-v3-docs">Documentação do QuickStatements 3.0</a>
      <ul>
        <li><a href="#prerequisites">Começando: Pré-requisitos</a></li>
        <li><a href="#qs-3.0-homepage">Visão Geral da Página Inicial do QuickStatements 3.0</a></li>
        <li><a href="#what-is-a-batch">Guias: O que é um Lote?</a>
          <ul>
            <li><a href="#create-new-batch">Criando um Novo Lote</a></li>
            <li><a href="#details-of-a-batch">Detalhes de um Lote</a></li>
          </ul>
        </li>
        <li><a href="#batch-details">Visualizando Detalhes e Histórico de Lotes</a></li>
        <li><a href="#batches-per-user">Ver todos os Lotes Criados por um Usuário</a></li>
        <li><a href="#writing-batch-commands">Escrevendo Comandos de Lote</a>
          <ul>
            <li><a href="#create-new-item">Criar um Novo Item</a>
            <li><a href="#add-statements">Adicionar Declarações</a>
            <li><a href="#add-qualifiers">Adicionar Qualificadores</a> 
            <li><a href="#add-references">Adicionar Referências</a>
            <li><a href="#modify-lda">Modificar Rótulos, Descrições e Apelidos</a>
            <li><a href="#remove-items">Remover Declarações ou Itens</a>
            <li><a href="#import-data">Importando Dados CSV/TSV</a>                                                                  </ul>
        </li>
        <li><a href="#best-practices">Melhores Práticas</a></li>
        <li><a href="#error-handling">Tratamento de Erros</a></li>
        <li><a href="#recommendations">Recomendações</a></li>
        <li><a href="#conclusion">Conclusão</a></li>
      </ul>
    </li> 
  </ol>
</details>

## Visão Geral

**QuickStatements (QS)** é uma ferramenta poderosa projetada por [Magnus Manske](https://en.wikipedia.org/wiki/User:Magnus_Manske) para realizar edições em massa no Wikidata. Ela permite que os usuários adicionem, modifiquem ou removam grandes quantidades de dados de maneira eficiente, utilizando uma sintaxe simples, semelhante a uma linha de comando. Seja para adicionar novos itens, declarações ou atualizar propriedades em várias entidades, o QuickStatements é uma ferramenta essencial para os editores do Wikidata que precisam fazer alterações em larga escala de maneira rápida e confiável.

Esta documentação fornece uma introdução aos recursos, ao uso e às melhores práticas do QuickStatements 3.0. _[Clique](#qs-v3-docs)_ para começar. No entanto, para compreender completamente as funcionalidades do QuickStatements 3.0, é importante entender primeiro o principal componente do QuickStatements⎯```Wikidata.```

#

<a id="a-brief-on-wikidata"></a>
<details>
 <summary> Um resumo sobre o Wikidata</summary>
Wikidata é um banco de dados secundário gratuito, colaborativo, multilíngue, gerido pela Fundação Wikimedia. Ele serve como um armazenamento central de dados estruturados usados em vários projetos Wikimedia, como a Wikipédia, e também fornece dados para usuários e organizações externas. O principal objetivo do Wikidata é permitir que humanos e máquinas compreendam e consultem informações de forma fácil.

Algumas características principais incluem:

- **Suporte multilíngue:** Os dados são armazenados de maneira que possam ser acessados em qualquer idioma.
- **Dados abertos:** Os dados do Wikidata estão disponíveis sob a Dedicação ao Domínio Público (CC0) da Creative Commons.
- **Edição colaborativa:** Qualquer pessoa com uma conta pode editar o Wikidata, tornando-o um recurso conduzido pela comunidade.
- **Ligação de dados:** O Wikidata se integra a outros projetos Wikimedia, servindo como a fonte de dados consistente e atualizada.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="structure-of-wikidata"></a>
## Estrutura do Wikidata
A estrutura do Wikidata baseia-se em um modelo simples, mas poderoso de **itens**, **propriedades** e **valores**. Esses três componentes formam a base de como os dados são armazenados, vinculados e recuperados.

- **Itens (números Q):** Cada item é um conceito único representado por um **QID** (por exemplo, Douglas Adams é representado por Q42). Esses itens armazenam dados e vinculam-se a outros itens.

- **Propriedades (números P):** As propriedades descrevem atributos específicos de um item e são identificadas por **PIDs** (por exemplo, data de nascimento é representada por **P569**). As propriedades podem descrever relações entre itens ou entre um item e um valor de dados.

- **Valores:** São os dados reais (por exemplo, a data **1952-03-11** como valor para **P569** no item **Q42** para a data de nascimento de Douglas Adams).

Juntos, itens, propriedades e valores criam **declarações**, que são os blocos de construção do Wikidata.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="lda"></a>
## Rótulos, Descrições e Apelidos
Cada item no Wikidata pode ter múltiplos **rótulos**, **descrições** e **apelidos** em diferentes idiomas:

- **Rótulos:** Um rótulo é o nome principal de um item (por exemplo, “Douglas Adams” para **Q42**). Um item pode ter um rótulo diferente em cada idioma.

- **Descrições:** As descrições fornecem contexto sobre o item para diferenciá-lo de itens semelhantes (por exemplo, “Autor e roteirista britânico” para **Q42**).

- **Apelidos:** Os apelidos são nomes alternativos para um item usados para fins de pesquisa. Por exemplo, **Q42** (Douglas Adams) pode ter um apelido como "Douglas Noel Adams."

Esses três componentes ajudam a garantir que os itens sejam fáceis de encontrar, distinguir e acessar em uma variedade de idiomas e contextos.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="wiki-statements"></a>
## Declarações do Wikidata
**Declarações** são as unidades de conhecimento principais no Wikidata, usadas para descrever itens por meio de uma combinação de uma propriedade e um valor. Uma declaração conecta um item aos seus dados associados:

- **Propriedade:** Define o aspecto do item que você está descrevendo (por exemplo, data de nascimento, ocupação, nacionalidade).
- **Valor:** Fornece a informação específica (por exemplo, uma data, uma string ou uma referência a outro item).
Uma declaração também pode ter **qualificadores** e **referências** para fornecer mais contexto ou citar a fonte dos dados.

Por exemplo:

- **Item:** Douglas Adams (Q42)
- **Propriedade:** Data de nascimento (P569)
- **Valor:** 11 de março de 1952
- **Qualificador:** Fonte (S854) – Link para uma página da web ou banco de dados que forneça prova da declaração.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="syntax-and-command-structure"></a>
## Sintaxe e Estrutura de Comando

Cada comando do QuickStatements segue um formato simplificado com colunas que especificam o **Item**, **Propriedade**, **Valor** e opcionais **Qualificadores**, **Referências**, etc.

| Campo        | Descrição                                                                                      |
|--------------|------------------------------------------------------------------------------------------------|
| `Q####`      | Refere-se a um item (por exemplo, `Q42` para Douglas Adams).                                    |
| `P####`      | Refere-se a uma propriedade (por exemplo, `P31` para "instância de").                           |
| Valor        | O valor associado à propriedade. Pode ser uma referência a um item (por exemplo, `Q####`), string, número, etc. |
| Qualificador | Informação adicional adicionada a uma afirmação para dar mais contexto (por exemplo, tempo, lugar).|
| Referências  | Dados para apoiar uma afirmação (por exemplo, uma URL, data de publicação).                     |
| Rótulos      | Nomes ou títulos de itens em diferentes idiomas.                                                |
| Descrições   | Breves resumos que descrevem os itens.                                                          |
| Apelidos     | Nomes alternativos ou termos pelos quais um item é conhecido.                                   |

</details>

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#

<a id="qs-v3-docs"></a>
## Documentação do QuickStatements 3.0

Esta documentação fornece uma introdução aos recursos do QuickStatements 3.0, que é uma atualização que melhora a funcionalidade, o desempenho e a experiência do usuário da plataforma QuickStatements para melhorar a estabilidade do sistema.

#

### Pré-requisitos
Para criar e executar lotes, você deve garantir o seguinte:
- **Conta do Wikidata**: Você deve estar logado no Wikidata para usar o QuickStatements.
- **Dados Estruturados**: Seus dados devem estar bem estruturados em formato CSV/TSV ou semelhante para serem facilmente importados e processados.
- **Usuário Autoconfirmado**: Para ser um usuário autoconfirmado, você deve ter pelo menos 4 dias na plataforma e deve ter feito 50 edições para ser considerado um.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="qs-3.0-homepage"></a>
## Visão Geral da Página Inicial do QuickStatements 3.0
A página inicial do **QuickStatements 3.0** é projetada para facilitar o acesso a recursos principais para gerenciar e executar edições em lote. Abaixo está um detalhamento dos elementos visíveis:

<p align="center">
  <img src="https://github.com/user-attachments/assets/339297cb-b5e4-46ca-82d1-799ea0b964dd" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Página Inicial do QuickStatements 3.0</p>
</p>

#### menu de navegação:
1. **Novo lote:** Um link que leva você a um formulário onde pode criar um novo lote de edições para serem carregadas no Wikidata.

2. **Últimos lotes:** Este link fornece acesso ao histórico de lotes submetidos recentemente. Os usuários podem rastrear o status e os detalhes de suas operações de lote anteriores.

3. **Git:** Links para o [repositório GitHub do QuickStatements](https://github.com/WikiMovimentoBrasil/quickstatements3), onde os usuários podem visualizar o código, relatar problemas ou contribuir para o desenvolvimento da plataforma.
  
4. **Login:** Permite que os usuários façam login em suas contas do Wikidata. Após o login, os usuários podem acessar recursos como enviar e rastrear seus lotes.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#### Interface Principal:
5. **“Bem-vindo ao QuickStatements 3.0”:** Um cabeçalho que dá boas-vindas aos usuários à interface principal.

#### Botões de Ação Principais:

6. **Novo lote:** Clicar neste botão inicia a criação de um novo lote. Os usuários podem inserir dados e comandos para processar e carregar várias edições no Wikidata em massa.
  
#### Seção de Pesquisa de Lotes:
7. **ID do Lote:** Os usuários podem inserir um ID de lote específico para recuperar informações detalhadas sobre aquele lote em particular. Clicar no botão ```Ver detalhes do lote``` exibe o status, progresso e resultados do lote.

8. **Nome de usuário:** Os usuários podem inserir um nome de usuário específico do Wikidata para recuperar uma lista de todos os lotes associados a esse usuário. Clicar em ```Ver lotes por usuário``` exibirá todos os lotes enviados por aquele usuário.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#
  
<a id="what-is-a-batch"></a>
### O que é um Lote no QuickStatements?
Um **lote** refere-se a um conjunto de comandos ou operações que são executados juntos para realizar edições em massa. Cada lote pode incluir várias declarações ou afirmações que você deseja adicionar, modificar ou remover de itens no Wikidata.

#

<a id="create-new-batch"></a>
#### A. Criando um novo Lote no QuickStatements
Para criar um novo lote no QuickStatements, siga estas etapas:
1. Clique no botão ```Novo Lote``` localizado na página inicial

<p align="center">
  <img src="https://github.com/user-attachments/assets/76fe5cb2-584a-45c9-a4d2-9e2815ac015c" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Clique em Novo Lote</p>
</p>

2. Um formulário aparecerá onde você pode inserir seus comandos ou carregar seu arquivo de dados. Os formatos disponíveis incluem tanto o formato QuickStatements V1 quanto o formato CSV/TSV.
<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Detalhes de um Lote no QuickStatements

<p align="center">
  <img src="https://github.com/user-attachments/assets/e81cd5a6-e029-454c-b4d6-67b7e607b920" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Detalhes de um Novo Lote</p>
</p>

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

Um novo lote consiste em:
1. **Formato de comando:** Seu formato de comando pode estar em formato V1 ou formato CSV.
     - **Formato V1:** Formato baseado em comandos, onde cada linha representa um comando separado por tabulação.
     - **Formato CSV:** Consiste em uma primeira linha⎯o cabeçalho⎯que define o conteúdo de cada coluna. As linhas subsequentes fornecem informações que serão aplicadas ao Wikibase de acordo com o conteúdo do cabeçalho de cada coluna.
  
Exemplo de sintaxe V1:
```
CREATE
LAST Len Doctor Worm
LAST Den 1998 song performed by They Might Be Giants
LAST P2650 Q12830
```
Exemplo de sintaxe CSV:
```
qid,Len,Den,P260
Q128309,Doctor Worm,1998,song performed by They Might Be Giants
```

QuickStatements também podem ser executados via URL:
```
See example: https://quickstatements.toolforge.org/#/v1=Q37887397%7CP214%7C%2296480189%22%7CS143%7CQ565
Qid: Q37887397
Property: P214
Senwiki : S143
Value: Q565
```

2. **Nome personalizado do lote:** Este é um rótulo ou identificador que você pode atribuir a um lote específico de edições para facilitar o gerenciamento e a referência. Por padrão, os lotes recebem nomes genéricos, geralmente apenas um ID de lote. No entanto, você tem a opção de fornecer um nome personalizado quando criar ou carregar um lote. Este nome personalizado facilita o reconhecimento ou a lembrança do que um determinado lote foi destinado a fazer, especialmente quando se lida com vários lotes ao longo do tempo.

3. **Comandos:** Estes são as instruções que você insere para realizar operações específicas em itens do Wikidata. Esses comandos permitem adicionar, modificar ou remover dados de itens no Wikidata. Os comandos são escritos em um formato específico, e cada linha geralmente representa uma ação a ser executada em um item do Wikidata.
<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Visualizando Detalhes e Histórico de Lotes
Você pode rastrear o progresso e o status de um lote específico inserindo o **ID do Lote** no campo apropriado e clicando no botão **Ver detalhes do lote**. Isso exibe informações como o número de edições feitas, o sucesso ou falha das operações e quaisquer erros que ocorreram.

#

<a id="batches-per-user"></a>
#### C. Ver todos os Lotes por Usuário no QuickStatements
Para visualizar o histórico de edições em lote por um usuário específico:
1. Insira o ```nome de usuário``` do usuário no campo nome de usuário (nome de usuário pode ser encontrado no login do wiki).
2. Clique em ```Ver lotes por usuário``` para listar todos os lotes que o usuário enviou. A lista incluirá:
   - **IDs dos Lotes**
   - **Descrições (se você adicionou nomes personalizados)**
   - **Status (por exemplo, em andamento, concluído ou falhado)**
   - **Datas**
   - **Número de edições no lote**

> [!NOTE]
> Cada lote tem uma URL única associada. Você pode adicionar esta URL aos favoritos ou compartilhá-la para acessar ou monitorar um lote posteriormente.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#

<a id="writing-batch-commands"></a>
#### D. Escrevendo Comandos de Lote no QuickStatements

<a id="create-new-item"></a>
#### 1. Criar um Novo Item

Este comando criará um novo item com um rótulo e descrição.
```
CREATE
LAST  Len  "Élément Exemple"
LAST  Den  "Ceci est un exemple d'élément à des fins de démonstration."
LAST  P31  Q5  # Ajoute une revendication selon laquelle l'élément est une instance d'un humain
```

<a id="add-statements"></a>

#### 2. Adicionar Declarações (Afirmações)
Adicionando declarações a um item existente (por exemplo, Douglas Adams - Q42). 
```
Q42  P569  1952-03-11  # Ajoute la date de naissance (P569) pour Douglas Adams
Q42  P19  Q84          # Ajoute le lieu de naissance (P19) comme Cambridge (Q84)
```

<a id="add-qualifiers"></a>

#### 3. Adicionar Qualificadores
Você pode adicionar qualificadores às declarações existentes para fornecer mais detalhes.
```
Q42  P69  Q3918  P580  1971  P582  1974  # Ajoute l'éducation (P69) au St John's College (Q3918) avec des dates de début (P580) et de fin (P582)
```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="add-references"></a>
#### 4. Adicionar Referências
Adicionando referências a uma declaração existente:
```
Q42  P69  Q3918  S854  "https://exemple.com/education"  # Ajoute une référence URL pour la revendication d'éducation
```

<a id="modify-lda"></a>
5. Modificar Rótulos, Descrições e Apelidos
Modifique rótulos, descrições e apelidos em diferentes idiomas:
```
Q42  Len  "Douglas Adams"  # Change l'étiquette anglaise en "Douglas Adams"
Q42  Ade  "Douglas Adams"  # Change l'étiquette allemande en "Douglas Adams"
Q42  Aen  "Douglas Noel Adams"  # Ajoute un alias en anglais
Q42  Den  "Auteur et scénariste britannique"  # Modifie la description anglaise
```

<a id="remove-items"></a>
6. Remover Declarações ou Itens
Remova declarações ou exclua itens inteiramente:
```
-Q42  P19  # Supprime la déclaration du lieu de naissance (P19) pour Q42
-Q100000  # Supprime entièrement l'élément Q100000
```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<a id="import-data"></a>
7. Importando Dados CSV/TSV
Você pode preparar seus dados no formato CSV ou TSV, onde cada linha representa uma operação. Um formato de exemplo:
```
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,+1856-01-01T00:00:00Z/9
```

Carregue o arquivo através da interface web para processar o lote.
<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#

### Melhores Práticas
- **Teste com Lotes Pequenos:** Sempre teste seus comandos com um pequeno conjunto de itens antes de realizar edições em larga escala para evitar alterações indesejadas.
- **Use Referências:** Certifique-se de que as declarações estejam devidamente referenciadas com fontes para melhorar a qualidade dos dados.
- **Monitore o Progresso:** Após o envio, acompanhe o progresso do seu lote e verifique se há erros.

#

### Tratamento de Erros

Quando ocorre um erro durante a execução, o QuickStatements indicará qual comando falhou. Problemas comuns incluem:

- IDs de itens ou propriedades incorretos.
- Erros de sintaxe em formatos de data ou campos de dados ausentes.
- Permissões ou limitação de velocidade pelo Wikidata para edições em grande escala. Nesses casos, revise os comandos que falharam e corrija os problemas antes de executá-los novamente.
  
<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#          

### Conclusão
O QuickStatements é uma ferramenta essencial para edições em massa no Wikidata, permitindo que os usuários gerenciem grandes conjuntos de dados de forma eficiente. Seguindo este guia, você pode criar, atualizar e gerenciar itens com facilidade, melhorando a qualidade e a precisão do Wikidata.

Para casos de uso mais avançados, consulte a [documentação do Wikidata](https://www.wikidata.org/wiki/Help:QuickStatements) para obter mais detalhes e atualizações.
# 

### Références
Esta documentação foi inspirada em muitas fontes, no entanto, o [Diátaxis](https://developers.google.com/tech-writing/overview) foi o guia mais significativo para escrever isto, pois fornece uma abordagem sistemática para entender as necessidades dos usuários da documentação. O [Curso de Redação Técnica do Google](https://developers.google.com/tech-writing/overview) também foi fundamental.

## 💚️ OBRIGADO MENTORES  💙
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :---------------------: | :-----------------------: | :--------------------: |
<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->

