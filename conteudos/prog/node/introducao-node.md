# Introdução ao Node

### 1. O que é Node?

**Conceito Principal:**
Node.js **não é uma linguagem de programação nem um framework**. É um **ambiente de execução (runtime environment)** de JavaScript construído sobre o motor V8 do Google Chrome. De forma simples, ele permite que você execute código JavaScript fora de um navegador, diretamente no servidor.

**Detalhes:**

  * **Acesso ao Sistema:** Diferente do JavaScript no navegador (que é limitado por segurança), o Node.js tem acesso total aos recursos do computador, como o sistema de arquivos (ler e escrever arquivos), a rede (criar servidores, fazer requisições), e outros processos do sistema operacional.
  * **Modelo Assíncrono e "Non-blocking I/O":** Esta é a sua característica mais importante. Node.js opera em uma única thread e usa um "loop de eventos" (event loop). Em vez de esperar uma operação demorada (como uma consulta ao banco de dados) terminar, ele a inicia e continua executando outras tarefas. Quando a operação termina, ele é notificado e processa o resultado. Isso o torna extremamente eficiente para lidar com muitas conexões simultâneas.

**Por que é importante?**
Permite que desenvolvedores usem uma única linguagem (JavaScript/TypeScript) para construir tanto o frontend quanto o backend de uma aplicação, unificando o desenvolvimento e facilitando o compartilhamento de código e conhecimento.

-----

### 2. Instalando Node e NPM

**Conceito Principal:**
É o processo de configurar seu computador com as ferramentas essenciais para começar a desenvolver com Node.js.

**Passos Chave:**

1.  **Baixar o Node.js:** A forma mais recomendada é ir ao [site oficial do Node.js](https://nodejs.org/).
2.  **Escolher a Versão:** Você verá duas opções:
      * **LTS (Long-Term Support):** Versão recomendada para a maioria dos usuários. É a mais estável e com suporte de longo prazo. Ideal para produção.
      * **Current:** A versão com os recursos mais recentes, mas que pode ser menos estável. Ideal para quem quer experimentar as novidades.
3.  **Instalação:** Baixe o instalador para o seu sistema operacional (Windows, macOS, Linux) e siga os passos.
4.  **NPM:** O **NPM (Node Package Manager)** é o gerenciador de pacotes do Node e é instalado automaticamente junto com ele.
5.  **Verificação:** Para confirmar que tudo foi instalado corretamente, abra seu terminal (ou prompt de comando) e digite:
    ```bash
    node -v  # Mostra a versão do Node.js
    npm -v   # Mostra a versão do NPM
    ```

-----

### 3. Criando um projeto em Node

**Conceito Principal:**
É o processo de inicialização formal de um novo projeto. O coração de todo projeto Node.js é o arquivo `package.json`.

**Passos Chave:**

1.  Crie uma nova pasta para o seu projeto: `mkdir meu-projeto-node`
2.  Entre na pasta: `cd meu-projeto-node`
3.  Inicie o projeto com o comando:
    ```bash
    npm init
    ```
4.  O terminal fará uma série de perguntas (nome do projeto, versão, descrição, etc.). Você pode respondê-las ou apenas pressionar Enter para aceitar os padrões.
      * **Dica:** Use `npm init -y` para pular todas as perguntas e criar um `package.json` com os valores padrão.

**O que é o `package.json`?**
É o arquivo de manifesto do seu projeto. Ele contém metadados (como nome e versão) e, mais importante, lista todas as dependências (pacotes de terceiros) e os scripts do projeto.

-----

### 4. Introdução ao Node Package Manager (NPM)

**Conceito Principal:**
NPM é duas coisas:

1.  **Uma ferramenta de linha de comando:** Para instalar e gerenciar pacotes no seu projeto.
2.  **Um registro online:** Um repositório gigantesco de pacotes de código aberto que você pode usar em seus projetos.

**Comandos Essenciais:**

  * `npm install <nome-do-pacote>`: Instala um pacote. Ex: `npm install express`.
      * Isso cria uma pasta `node_modules` (onde os pacotes são baixados) e adiciona o pacote ao `package.json` e ao `package-lock.json`.
  * `npm install`: Instala todas as dependências listadas no `package.json`.
  * `npm uninstall <nome-do-pacote>`: Remove um pacote.

**Dependências de Desenvolvimento vs. Produção:**

  * `npm install express`: Instala como uma dependência de produção (necessária para a aplicação rodar).
  * `npm install typescript -D` (ou `--save-dev`): Instala como uma dependência de desenvolvimento (ferramentas usadas apenas durante o desenvolvimento, como compiladores, testadores, etc.).

-----

### 5. Criando scripts NPM personalizados

**Conceito Principal:**
O NPM permite que você defina "atalhos" para comandos do terminal na seção `"scripts"` do seu `package.json`. Isso padroniza tarefas comuns e as torna mais fáceis de executar.

**Exemplo Prático:**
No seu `package.json`:

```json
"scripts": {
  "start": "node src/index.js",
  "dev": "nodemon src/index.js",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

Para executar esses scripts, você usa o comando `npm run <nome-do-script>`:

  * `npm run dev`
  * `npm start` (para `start`, `test`, `stop`, `restart`, o `run` é opcional).

**Por que é importante?**
Automatiza tarefas repetitivas e garante que todos na equipe (ou até mesmo você no futuro) rodem, testem e construam o projeto da mesma maneira.

-----

### 6. Trabalhando com Typescript no Node

**Conceito Principal:**
Usar TypeScript (um superset do JavaScript que adiciona tipagem estática) para escrever seu código backend. Isso ajuda a pegar erros durante o desenvolvimento, melhora a legibilidade do código e oferece um autocompletar poderoso no editor.

**Passos Chave para Configuração:**

1.  **Instalar dependências de desenvolvimento:**
    ```bash
    npm install -D typescript ts-node @types/node
    ```
      * `typescript`: O compilador do TypeScript.
      * `ts-node`: Permite executar código TypeScript diretamente, sem a necessidade de compilar para JavaScript primeiro (ótimo para desenvolvimento).
      * `@types/node`: Fornece as definições de tipo para os módulos nativos do Node.js.
2.  **Criar o `tsconfig.json`:** Este arquivo configura o compilador do TypeScript.
    ```bash
    npx tsc --init
    ```
3.  **Escrever código em `.ts`:** Crie seus arquivos com a extensão `.ts` (ex: `src/index.ts`).
4.  **Configurar scripts no `package.json`:**
    ```json
    "scripts": {
      "dev": "ts-node src/index.ts",
      "build": "tsc",
      "start": "node dist/index.js"
    }
    ```
      * `npm run dev`: Roda o projeto em modo de desenvolvimento.
      * `npm run build`: Compila seu código `.ts` para JavaScript na pasta `dist`.
      * `npm start`: Roda a versão compilada em JavaScript (para produção).

-----

### 7. Organização básica de pastas

**Conceito Principal:**
Estruturar seu projeto de forma lógica e escalável para que seja fácil de encontrar arquivos e entender a arquitetura da aplicação.

**Estrutura Comum:**

```
meu-projeto/
├── dist/             # Código compilado para produção (gerado pelo `tsc`)
├── node_modules/     # Dependências do projeto (gerenciado pelo NPM)
├── src/              # Código-fonte da sua aplicação (.ts ou .js)
│   ├── controllers/  # Lógica de requisição/resposta
│   ├── services/     # Lógica de negócio
│   ├── routes/       # Definição das rotas da API
│   └── index.ts      # Ponto de entrada da aplicação
├── .env              # Variáveis de ambiente
├── .gitignore        # Arquivos e pastas a serem ignorados pelo Git
├── package.json
├── package-lock.json
└── tsconfig.json
```

-----

### 8. Modo Watch do Node

**Conceito Principal:**
Reiniciar automaticamente o servidor toda vez que você salva uma alteração em um arquivo. Isso acelera drasticamente o desenvolvimento, pois você não precisa parar e iniciar o servidor manualmente a cada mudança.

**Ferramentas Populares:**

  * **`nodemon`:** Uma das ferramentas mais populares para isso.
      * Instalação: `npm install -D nodemon`.
      * Uso no `package.json`: `"dev": "nodemon src/index.ts"`
  * **Flag `--watch` nativa do Node:** Versões mais recentes do Node.js (v18.11+) incluem um modo watch nativo.
      * Uso: `node --watch src/index.js`
  * **`ts-node-dev`:** Uma ótima opção para projetos TypeScript, pois é otimizada para reiniciar rapidamente.
      * Instalação: `npm i -D ts-node-dev`
      * Uso: `"dev": "ts-node-dev --respawn src/index.ts"`

-----

### 9. Uso de variáveis de ambiente

**Conceito Principal:**
Configurar sua aplicação usando variáveis que existem fora do seu código-fonte. Isso é crucial para manter informações sensíveis (como senhas de banco de dados, chaves de API) seguras e para permitir configurações diferentes entre os ambientes (desenvolvimento, produção).

**Como usar (com o pacote `dotenv`):**

1.  Instale o pacote: `npm install dotenv`
2.  Crie um arquivo chamado `.env` na raiz do seu projeto.
3.  Adicione suas variáveis nesse arquivo:
    ```
    PORT=3333
    DB_PASSWORD="minhasenhasecreta"
    ```
4.  **IMPORTANTE:** Adicione o arquivo `.env` ao seu `.gitignore` para nunca enviar segredos para o repositório\!
5.  No ponto de entrada da sua aplicação (ex: `src/index.ts`), carregue as variáveis:
    ```typescript
    import dotenv from 'dotenv';
    dotenv.config();
    ```
6.  Acesse as variáveis em qualquer lugar do seu código através de `process.env`:
    ```typescript
    const port = process.env.PORT;
    const password = process.env.DB_PASSWORD;
    ```

-----

### 10. Criando um servidor HTTP básico

**Conceito Principal:**
O "Hello, World\!" do backend. É o primeiro passo para criar qualquer API ou aplicação web, demonstrando como fazer o Node.js "escutar" por requisições de rede e respondê-las.

**Exemplo com o módulo `http` nativo:**

```typescript
import http from 'http';

const server = http.createServer((request, response) => {
  response.writeHead(200, { 'Content-Type': 'application/json' });
  response.end(JSON.stringify({ message: 'Olá, mundo!' }));
});

server.listen(3000, () => {
  console.log('Servidor rodando na porta 3000! 🔥');
});
```

**Exemplo com Express.js (mais simples e prático):**

```typescript
import express from 'express';

const app = express();

app.get('/', (request, response) => {
  return response.json({ message: 'Olá, mundo!' });
});

app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000! 🔥');
});
```

Este exemplo com Express mostra por que os frameworks são tão usados: eles simplificam muito a criação de rotas e o gerenciamento de requisições e respostas.