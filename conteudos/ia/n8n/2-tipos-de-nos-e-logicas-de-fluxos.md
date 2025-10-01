# 🪢 Tipos de nós e lógicas de fluxos

## Fluxo no n8n

```
[ Gatilho/Trigger ] --> [ Nó 1 (Ação) ] --> [ Nó 2 (Ação) ] --> [ Resultado ]
```

## Tipos de Nós

Nós são os blocos de construção de qualquer automação no n8n. Cada nó executa uma tarefa específica. Eles são divididos em três categorias principais.

### 1. Nós de Gatilho (Trigger Nodes)

São os nós que **iniciam** um fluxo de trabalho. Eles "escutam" um evento específico e disparam a automação quando ele ocorre.

  * **Webhook:** Inicia o fluxo ao receber uma requisição HTTP. Perfeito para integrações via API.
  * **Schedule (Cron):** Executa o fluxo em intervalos de tempo agendados (ex: a cada 5 minutos, toda segunda-feira às 9h).
  * **On App Event:** Dispara a automação com base em um evento de um aplicativo específico (ex: novo e-mail no Gmail, novo card no Trello).
  * **Manual:** Permite a execução manual do fluxo com um clique, ideal para testes.

### 2. Nós de Ação (Regular Nodes)

Estes nós realizam a maior parte do trabalho em um fluxo. Eles executam operações como ler, escrever ou modificar dados.

  * **Integrações de Apps:** Conectam-se a centenas de serviços para realizar ações (ex: enviar mensagem no Slack, criar linha no Google Sheets, adicionar lead no Salesforce).
  * **Manipulação de Dados:**
      * **Set:** Cria, renomeia ou define valores de campos.
      * **Function:** Permite escrever código JavaScript customizado para manipulações complexas.
      * **Edit Fields:** Permite selecionar, renomear e organizar os campos de dados que passam pelo fluxo.
  * **Comunicação:**
      * **HTTP Request:** Permite fazer chamadas para qualquer API REST, oferecendo máxima flexibilidade.

-----

## Lógicas de Fluxos de Trabalho

A verdadeira magia do n8n está em como você conecta os nós para criar lógicas que tomam decisões e se adaptam a diferentes cenários.

### 1. Ramificação (Branching)

Permite que seu fluxo siga caminhos diferentes com base em condições.

  * **IF:** Avalia uma condição e divide o fluxo em duas saídas: `true` (verdadeiro) e `false` (falso).
    ```
    (Entrada) --> [IF: "Status" é igual a "Aprovado"?] --(true)--> [Enviar E-mail de Parabéns]
                                                    |
                                                    --(false)--> [Enviar E-mail de Recusa]
    ```
  * **Switch:** Direciona o fluxo para uma de várias saídas com base no valor de um campo. É como ter vários "IFs" em um só nó.
    ```
                    | --(caso 1: "Marketing")--> [Adicionar Tag 'MKT']
                    |
    (Entrada) --> [Switch: "Departamento"] --(caso 2: "Vendas")--> [Notificar Time de Vendas]
                    |
                    | --(default)--> [Arquivar Registro]
    ```

### 2. Fusão (Merging)

Une diferentes ramificações de volta em um único fluxo.

  * **Merge:** Combina os dados de duas ou mais entradas para que as próximas etapas possam processá-los de forma unificada.

### 3. Laços (Looping)

Executa uma série de ações para cada item em uma lista de dados.

  * **Split in Batches:** Este nó é a forma padrão do n8n para criar laços. Ele recebe uma lista de itens e executa os nós seguintes uma vez para cada item (ou para cada lote de itens), permitindo processar múltiplos registros de forma eficiente.

    **Exemplo:** Você recebe 10 novos leads de um formulário. O `Split in Batches` pode processar um lead por vez, executando a mesma sequência de ações para cada um:

    1.  Adicionar o lead ao CRM.
    2.  Enviar um e-mail de boas-vindas.
    3.  Notificar a equipe no Slack.