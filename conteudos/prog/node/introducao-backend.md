# Introdução ao backend

### 1. O que é backend?

**Conceito Principal:**
O backend (ou "back-end") é a parte de uma aplicação que o usuário não vê diretamente, mas que é responsável por fazer tudo funcionar. Pense nele como a "cozinha de um restaurante": enquanto o cliente (usuário) vê o salão e o cardápio (frontend), é na cozinha que os pedidos são processados, os pratos são preparados e os ingredientes são gerenciados no estoque.

**Detalhes:**

  * **Lógica de Negócio:** Contém as regras e os processos que definem como a aplicação funciona. Por exemplo, como calcular o frete de uma compra ou como validar se um usuário pode ter acesso a um certo conteúdo.
  * **Acesso a Dados:** É responsável por se comunicar com o banco de dados para salvar, buscar, atualizar e deletar informações (ex: dados de usuários, produtos, posts).
  * **Autenticação e Segurança:** Gerencia logins, senhas, permissões e protege a aplicação contra acessos não autorizados e ataques.
  * **Comunicação:** Disponibiliza dados para o frontend (o lado do cliente) através de APIs.

**Relevância para Node.js:**
Node.js é um **ambiente de execução** que permite que você escreva o código do backend usando a linguagem JavaScript. Em vez de rodar JavaScript no navegador (frontend), o Node.js o executa no servidor. Ele é muito popular para construir backends por ser rápido, eficiente com operações de entrada/saída (I/O), como consultas a banco de dados e requisições de rede.

-----

### 2. O que é cliente e servidor?

**Conceito Principal:**
Este é o modelo fundamental da web, conhecido como arquitetura cliente-servidor.

  * **Cliente (Client):** É o dispositivo que **solicita** informações ou serviços. Geralmente é o navegador web (Chrome, Firefox), um aplicativo de celular ou até mesmo outro backend. Ele é responsável por exibir a interface para o usuário.
  * **Servidor (Server):** É um computador (ou conjunto de computadores) que **aguarda e responde** às solicitações dos clientes. Ele hospeda o código do backend, o banco de dados e outros recursos necessários para atender a essas solicitações.

**O fluxo é simples:**

1.  O Cliente envia uma **requisição** (request) para o Servidor (ex: "me dê a lista de produtos").
2.  O Servidor processa essa requisição, busca os dados no banco de dados e prepara a resposta.
3.  O Servidor envia uma **resposta** (response) de volta para o Cliente (ex: uma lista de produtos em formato JSON).

**Relevância para Node.js:**
Uma aplicação Node.js **é o software que roda no servidor**. Usando o módulo `http` nativo do Node.js ou, mais comumente, frameworks como o **Express.js** ou **Fastify**, você cria um servidor que fica "escutando" por requisições de clientes em uma determinada porta (ex: porta 3000) e define o que fazer quando cada tipo de requisição chega.

-----

### 3. Entendendo o protocolo HTTP 1 e HTTP 2

**Conceito Principal:**
HTTP (HyperText Transfer Protocol) é o "idioma" ou o conjunto de regras que clientes e servidores usam para se comunicar na web. Ele define como as mensagens de requisição e resposta devem ser formatadas.

**Detalhes:**

  * **HTTP/1.1:** A versão mais clássica e difundida. Funciona bem, mas tem uma limitação importante: por padrão, ele só consegue lidar com uma requisição por vez em uma única conexão (problema conhecido como "Head-of-Line Blocking"). Para carregar vários recursos (imagens, scripts), o navegador precisa abrir múltiplas conexões, o que é menos eficiente.
  * **HTTP/2:** Uma evolução significativa que resolve os problemas do HTTP/1.1. Sua principal vantagem é o **multiplexing**, que permite que várias requisições e respostas sejam enviadas simultaneamente através de uma única conexão. Isso torna o carregamento de sites e a comunicação com APIs muito mais rápidos e eficientes.

**Relevância para Node.js:**
O Node.js possui módulos nativos para lidar com ambos os protocolos:

  * O módulo `http` cria servidores que se comunicam via HTTP/1.1.
  * O módulo `http2`, introduzido em versões mais recentes, permite criar servidores que suportam as melhorias do HTTP/2. A maioria dos frameworks modernos construídos sobre Node.js já oferece suporte ou pode ser configurada para usar HTTP/2.

-----

### 4. Métodos HTTP (Verbos)

**Conceito Principal:**
Os métodos HTTP são os "verbos" de uma requisição. Eles indicam a **ação** que o cliente deseja realizar sobre um determinado recurso no servidor.

**Principais Métodos:**

  * **`GET`**: Solicita a **leitura/busca** de um recurso. É usado para obter dados. (Ex: buscar um usuário, listar produtos).
  * **`POST`**: Envia dados para o servidor para **criar** um novo recurso. (Ex: cadastrar um novo usuário).
  * **`PUT`**: Envia dados para **substituir/atualizar** um recurso por completo. (Ex: atualizar todos os dados de um perfil de usuário).
  * **`PATCH`**: Envia dados para **atualizar parcialmente** um recurso. (Ex: atualizar apenas o nome de um usuário, sem alterar o resto).
  * **`DELETE`**: Solicita a **remoção** de um recurso. (Ex: deletar uma postagem).

**Relevância para Node.js:**
Em frameworks como o Express.js, você define "rotas" que correspondem a esses métodos e a um caminho (URL).

```javascript
// Exemplo em Express.js
app.get('/usuarios', (req, res) => { /* Lógica para listar usuários */ });
app.post('/usuarios', (req, res) => { /* Lógica para criar um usuário */ });
app.delete('/usuarios/:id', (req, res) => { /* Lógica para deletar um usuário pelo ID */ });
```

-----

### 5. Formas de fazer backend

**Conceito Principal:**
Refere-se às diferentes arquiteturas ou estilos que podem ser usados para estruturar uma aplicação de backend.

**Principais Formas:**

  * **Monolito (Monolithic):** A aplicação inteira (autenticação, produtos, pagamentos, etc.) é construída como uma única unidade de código. É mais simples de começar, mas pode se tornar complexa e difícil de manter e escalar à medida que cresce.
  * **Microsserviços (Microservices):** A aplicação é dividida em serviços menores e independentes, cada um com sua própria responsabilidade e, muitas vezes, seu próprio banco de dados. (Ex: um serviço para usuários, outro para pagamentos). Eles se comunicam entre si via rede (geralmente por APIs).
  * **Serverless (ou FaaS - Function as a Service):** Você escreve o código como funções independentes, e o provedor de nuvem (AWS, Google Cloud, Azure) gerencia toda a infraestrutura do servidor para você. Você não se preocupa com o servidor, apenas com a função.

**Relevância para Node.js:**
Node.js é extremamente versátil e se encaixa em todas essas arquiteturas:

  * É ótimo para construir **Monolitos** robustos com frameworks como Express.js.
  * Sua leveza, rapidez e ecossistema (NPM) o tornam uma das tecnologias mais populares para construir **Microsserviços**.
  * É a linguagem número um para **Serverless** (ex: AWS Lambda), pois suas funções iniciam muito rapidamente ("cold start" baixo).

-----

### 6. Entendendo o que é API e SDK

**Conceito Principal:**
São duas formas de permitir que sistemas diferentes conversem entre si.

  * **API (Application Programming Interface):** É um **contrato** ou uma "interface de comunicação". Pense nela como o **cardápio de um restaurante**: ele define quais pratos (operações) estão disponíveis, quais ingredientes (parâmetros) você pode escolher e o que você receberá de volta. Uma API de backend expõe um conjunto de *endpoints* (URLs) que o frontend pode chamar para obter ou manipular dados.
  * **SDK (Software Development Kit):** É um **kit de ferramentas** que facilita o uso de uma API. Em vez de você ter que montar as requisições HTTP manualmente, o SDK oferece um conjunto de funções e classes na sua linguagem de programação preferida que fazem esse trabalho por você. Por exemplo, em vez de fazer um `POST` manual para `/payments`, você poderia simplesmente chamar uma função como `pagseguroSDK.createPayment(...)`.

**Relevância para Node.js:**

  * O principal objetivo de um backend Node.js moderno é **construir APIs** (geralmente REST APIs ou GraphQL APIs) para serem consumidas por clientes (web ou mobile).
  * Ao mesmo tempo, seu backend Node.js também pode **consumir APIs** de terceiros (como de um sistema de pagamento ou de uma rede social) usando os **SDKs** que eles fornecem (ex: `aws-sdk`, `stripe-node`).

-----

### 7. Formatos de resposta

**Conceito Principal:**
É a estrutura dos dados que o servidor envia de volta ao cliente em uma resposta HTTP. O formato precisa ser algo que ambos os lados consigam entender e interpretar.

**Principais Formatos:**

  * **JSON (JavaScript Object Notation):** O padrão absoluto para APIs modernas. É um formato de texto leve, legível por humanos e facilmente interpretável por máquinas, especialmente em JavaScript.
  * **XML (eXtensible Markup Language):** Um formato mais antigo e verboso, baseado em tags (como o HTML). Ainda é usado em sistemas legados e em alguns serviços corporativos (ex: SOAP).
  * **HTML (HyperText Markup Language):** Quando o servidor gera a página web inteira e a envia para o navegador renderizar. É mais comum em aplicações tradicionais do que em APIs modernas (que costumam enviar apenas os dados em JSON).
  * **Texto Plano (Plain Text):** Para respostas muito simples, sem estrutura.

**Relevância para Node.js:**
Node.js e JavaScript são perfeitos para trabalhar com **JSON**, pois a sintaxe dos objetos JavaScript é praticamente idêntica à do JSON. Frameworks como o Express.js possuem métodos que facilitam o envio de respostas JSON:

```javascript
// Exemplo em Express.js
app.get('/user', (req, res) => {
    const user = { name: "Angelo", age: 21 };
    res.json(user); // Converte o objeto para JSON e envia a resposta
});
```