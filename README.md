# DIVIDI --- Dividir ficou mais fácil!

O **DIVIDI** é uma aplicação web para organizar despesas compartilhadas
entre amigos, familiares, casais ou pessoas que dividem uma casa, viagem
ou atividade. O sistema reúne grupos, gastos registrados e saldos
estimados de cada participante.

> **Estado atual:** protótipo funcional executado no navegador. Os dados
> são armazenados localmente por meio do `localStorage`. Esta versão não
> possui login, banco de dados em nuvem ou sincronização entre
> dispositivos.

## 1. Objetivo

Facilitar o controle de despesas compartilhadas e deixar mais claro: -
quais gastos foram registrados; - a qual grupo cada despesa pertence; -
quem realizou o pagamento; - como o valor foi dividido; - quanto cada
participante tem a pagar ou a receber.

## 2. Funcionalidades

### Visão geral

Apresenta o total de despesas, quantidade de grupos, valores estimados a
receber e a pagar pelo participante "Você", lista de grupos e últimas
movimentações.

### Cadastro de grupos

Permite criar grupos para organizar despesas por contexto, como casa
compartilhada, viagem, casal ou amigos. O formulário solicita o nome do
grupo e os participantes, separados por vírgula. O participante "Você" é
incluído automaticamente caso não esteja na lista. Nomes repetidos são
eliminados.

### Registro de despesas

Cada despesa possui descrição, valor em reais, grupo, pagador, tipo de
divisão e data/hora de registro. Há duas opções: - **Todos do grupo:**
divide o valor igualmente entre todos os participantes; - **Somente quem
pagou:** atribui o custo apenas à pessoa que pagou.

O formulário exige os campos e não aceita valores iguais ou inferiores a
zero.

### Consulta de despesas

Exibe as despesas em uma tabela com descrição, data, grupo, pagador,
valor e tipo de divisão. As movimentações mais recentes aparecem
primeiro.

### Acertos

Mostra o saldo estimado de cada participante em cada grupo: - saldo
positivo: valor a receber; - saldo negativo: valor a pagar; - saldo
próximo de zero: situação equilibrada.

## 3. Como são calculados os saldos

Para cada despesa, o sistema identifica quem participa da divisão. Se a
opção for "Todos do grupo", o valor é dividido pelo número de
participantes. Se for "Somente quem pagou", apenas o pagador assume o
custo.

O sistema subtrai de cada participante sua parte e adiciona o valor
integral ao saldo de quem pagou.

**Exemplo:** em um grupo com três pessoas, uma despesa de R\$ 90,00
dividida entre todos representa R\$ 30,00 para cada pessoa. Se uma delas
pagou tudo, seu saldo nessa despesa será +R\$ 60,00 e o das outras duas
será -R\$ 30,00 cada.

Os saldos são calculados por grupo. A visão geral também apresenta uma
posição líquida simplificada de "Você", somando os efeitos das despesas
dos grupos em que participa.

> Os saldos são estimativas baseadas nos registros. O sistema não
> realiza transferências, não confirma pagamentos e não liquida
> automaticamente as dívidas.

## 4. Tecnologias utilizadas

O protótipo atual utiliza tecnologias nativas da web, sem framework ou
biblioteca externa obrigatória.

  -----------------------------------------------------------------------
  Tecnologia                          Utilização
  ----------------------------------- -----------------------------------
  **HTML5**                           Estrutura das páginas, menus,
                                      tabelas, formulários, cartões e
                                      janelas modais.

  **CSS3**                            Identidade visual, cores,
                                      espaçamentos, cartões, tabelas e
                                      adaptação a diferentes telas.

  **JavaScript**                      Navegação, cadastro de grupos e
                                      despesas, cálculos, validações e
                                      atualização da interface.

  **Web Storage (`localStorage`)**    Armazenamento local dos grupos e
                                      despesas no navegador.

  **DOM**                             Acesso e atualização dos elementos
                                      HTML por JavaScript.
  -----------------------------------------------------------------------

### HTML5

Organiza o conteúdo por meio de elementos como formulários, campos,
botões, tabelas, navegação e seções.

### CSS3

Define a identidade visual, com predominância de roxo e branco e
detalhes em verde. Utiliza *media queries*: em telas maiores há menu
lateral; em telas menores, uma navegação inferior. Os cartões,
formulários e tabelas também se ajustam à largura disponível.

### JavaScript

Controla o funcionamento da aplicação: carrega e salva dados, cria
grupos, cadastra despesas, atualiza as opções dos formulários, calcula
totais e saldos, ordena movimentações, alterna seções e exibe mensagens.

### localStorage

É um recurso do navegador para guardar informações localmente. O DIVIDI
utiliza a chave `dividi-data` e armazena os dados em formato JSON. As
informações permanecem disponíveis no mesmo navegador e perfil, desde
que os dados do site não sejam apagados.

**Importante:** `localStorage` não é um banco de dados online. Os dados
não são compartilhados automaticamente com outros usuários, computadores
ou celulares.

## 5. Organização do código

A versão atual está concentrada em um único arquivo:

``` text
DIVIDI/
└── index.html
```

Dentro dele estão: - **HTML:** estrutura e conteúdo da interface; -
**CSS:** estilos dentro da seção `<style>`; - **JavaScript:**
funcionalidades dentro da seção `<script>`.

Em uma evolução, o código poderá ser separado:

``` text
DIVIDI/
├── index.html
├── css/
│   └── style.css
└── js/
    └── app.js
```

## 6. Como executar

Como o protótipo usa HTML, CSS e JavaScript nativos, não é necessário
instalar Node.js, React ou configurar um servidor para um teste local
simples.

1.  Obtenha o arquivo HTML do projeto.
2.  Se necessário, renomeie-o para `index.html`.
3.  Abra o arquivo em um navegador atualizado, como Chrome, Edge,
    Firefox ou Safari.
4.  Acesse as seções pelo menu.
5.  Crie um grupo antes de cadastrar uma despesa.

O site também pode ser publicado em um serviço de hospedagem de páginas
estáticas para receber um endereço público.

## 7. Compatibilidade e responsividade

A interface se adapta a computadores, tablets e celulares. Por ser uma
aplicação web, pode ser aberta em navegadores Android e iPhone, sem
instalação de aplicativo nativo.

Como os dados são locais, abrir o site em outro dispositivo não
transfere os registros feitos no primeiro.

## 8. Dados de demonstração

Na primeira execução, o protótipo apresenta dados de exemplo:

**Grupos** - Casa compartilhada --- Você, Ana e Bruno; - Viagem de fim
de semana --- Você, Mariana, Lucas e Pedro.

**Despesas** - Compras do mercado --- R\$ 240,00, pagas por Ana; -
Combustível --- R\$ 180,00, pago por Você; - Pizza de sexta --- R\$
96,00, paga por Bruno.

Novos grupos e despesas podem ser adicionados. A interface atual não
oferece funções para editar ou excluir registros.

## 9. Limitações atuais

-   Não possui cadastro, login ou autenticação.
-   Não possui banco de dados remoto.
-   Não sincroniza informações entre dispositivos.
-   Não permite que várias pessoas atualizem o mesmo grupo em tempo
    real.
-   Não possui convites por link ou e-mail.
-   Não oferece edição ou exclusão de grupos e despesas.
-   Não processa pagamentos nem realiza transferências.
-   Os cálculos seguem regras simplificadas de divisão igualitária.
-   Os dados podem ser perdidos se o armazenamento do navegador for
    apagado ou se outro perfil/dispositivo for utilizado.

## 10. Melhorias futuras

1.  Cadastro e autenticação de usuários;
2.  Banco de dados em nuvem;
3.  Compartilhamento de grupos por convite;
4.  Sincronização entre celulares e computadores;
5.  Edição e exclusão de grupos e despesas;
6.  Registro e confirmação de acertos;
7.  Histórico por pessoa e período;
8.  Gráficos de gastos mensais e por categoria;
9.  Categorias de despesas, como alimentação, transporte e moradia;
10. Notificações sobre novos gastos e valores pendentes.

## 11. Tecnologias que podem ser adotadas futuramente

As opções abaixo são possibilidades para uma próxima versão; **não fazem
parte da implementação atual**.

  -----------------------------------------------------------------------
  Tecnologia                          Possível finalidade
  ----------------------------------- -----------------------------------
  **React**                           Construir a interface em
                                      componentes e facilitar a evolução
                                      das telas.

  **Tailwind CSS**                    Padronizar e agilizar a criação dos
                                      estilos.

  **Supabase**                        Oferecer banco de dados em nuvem e
                                      autenticação.

  **Git e GitHub**                    Controlar versões do código e
                                      colaborar no desenvolvimento.

  **Vercel**                          Hospedar a aplicação e
                                      disponibilizar um endereço público.
  -----------------------------------------------------------------------

A adoção dessas ferramentas dependerá do planejamento e da implementação
das próximas etapas.

## 12. Segurança e privacidade

Nesta versão, os dados ficam no navegador e não há contas nem controle
de acesso. Portanto, o protótipo não deve ser usado para armazenar
informações financeiras sensíveis ou dados pessoais de terceiros.

Em uma versão colaborativa online, será necessário implementar
autenticação, regras de autorização, proteção das informações e
políticas adequadas de privacidade.

## 13. Considerações finais

O DIVIDI apresenta uma solução simples para organizar despesas
compartilhadas. O protótipo demonstra o fluxo principal: criar grupos,
registrar gastos, visualizar movimentações e consultar saldos estimados.

A implementação atual com HTML, CSS e JavaScript permite testar a
proposta sem configuração complexa. A integração futura com banco de
dados e autenticação poderá transformar o protótipo em um sistema
colaborativo, com informações sincronizadas entre os participantes.

------------------------------------------------------------------------

**Projeto:** DIVIDI\
**Slogan:** Dividir ficou mais fácil!\
**Tipo:** Aplicação web responsiva --- protótipo acadêmico\
**Idioma da interface:** Português (Brasil)
