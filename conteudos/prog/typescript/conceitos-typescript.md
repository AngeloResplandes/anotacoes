# Conceitos Essenciais

Este documento serve como um guia de referência rápida para os conceitos fundamentais do TypeScript, abordando desde a tipagem primitiva até usos mais avançados como `Interfaces` e `Types`.

## Índice

1.  [Tipos Primitivos](#1-tipos-primitivos-e-declaração-de-variáveis)
2.  [Tipos em Arrays](#2-tipos-em-arrays)
3.  [Tipos em Funções](#3-tipos-nos-parâmetros-e-retorno-de-funções)
4.  [Contextual Typing](#4-contextual-typing-em-funções-anônimas)
5.  [Tipos em Objetos](#5-tipos-em-objetos)
6.  [Union Types](#6-union-types-múltiplos-tipos)
7.  [Type e Interface](#7-type-e-interface-como-usar-e-diferenças)
8.  [Type Assertions](#8-type-assertions)
9.  [Tipos Literais](#9-tipos-literais)
10. [Inferência de Tipos Literais](#10-inferência-de-tipos-literais)
11. [Tipos para Funções](#11-criando-tipos-para-funções)

### 1. Tipos Primitivos e Declaração de Variáveis

Os tipos primitivos são a base do sistema de tipos do TypeScript. Ao declarar uma variável, você pode especificar o tipo de dado que ela irá armazenar, garantindo a segurança do tipo.

-   **`string`**: Para valores de texto.
-   **`number`**: Para valores numéricos (inteiros ou decimais).
-   **`boolean`**: Para valores lógicos `true` ou `false`.

```typescript
// Variáveis como let, var e const
let fullName: string = "Angelo Resplandes";
let age: number = 21;
let isAlive: boolean = true;
```

### 2. Tipos em Arrays

Você pode definir o tipo de dado que um array deve conter, garantindo que todos os seus elementos sejam consistentes.

A sintaxe é `tipo[]` ou a forma genérica `Array<tipo>`.

```typescript
// Arrays no typescript
let names: string[] = ["Angelo", "Vitória", "Luis", "João"];
let ages: number[] = [21, 30, 16, 11];
```

#### O tipo `any`

O tipo `any` desliga a verificação de tipos para uma variável, permitindo que ela receba qualquer valor. Use-o com moderação, pois ele remove as garantias de segurança do TypeScript.

```typescript
// O array 'lista' pode conter qualquer tipo de elemento
let lista: any[] = ["Carro", "Moto", 100, true];
```

### 3. Tipos nos Parâmetros e Retorno de Funções

Defina os tipos dos parâmetros que uma função aceita e o tipo do valor que ela retorna para criar funções mais previsíveis e seguras.

```typescript
// A função espera um parâmetro 'name' do tipo 'string'
// e explicitamente retorna uma 'string'.
function firstLetterUpperCase(name: string): string {
    let firstLetter = name.charAt(0).toUpperCase();
    return firstLetter + name.substring(1);
}

firstLetterUpperCase("angelo"); // Retorna "Angelo"
```

> Se uma função não retorna nenhum valor, seu tipo de retorno é `void`.

### 4. Contextual Typing em Funções Anônimas

O TypeScript consegue inferir os tipos dos parâmetros de funções anônimas com base no contexto em que são usadas (por exemplo, em um `forEach`).

```typescript
let names = ["angelo", "pedro", "vitória", 'cristina', 10];
// O TS infere que 'names' é do tipo (string | number)[]

// Não é preciso tipar 'nome', o TS infere pelo contexto do array 'names'.
names.forEach(function (nome) {
    // É necessário usar um "Type Guard" para tratar os tipos diferentes
    if (typeof nome === "string") {
        console.log(nome.toUpperCase());
    } else {
        console.log(nome);
    }
});
```

### 5. Tipos em Objetos

Defina a "forma" (shape) de um objeto, especificando suas propriedades e tipos.

```typescript
// Tipagem "inline" para o parâmetro 'usuario'
function message(usuario: { name: string, age: number }) {
    return console.log(`Olá ${usuario.name}, você tem ${usuario.age} anos de idade!`);
}

let u = {
    name: "Angelo",
    age: 21
};

message(u);
```

> Para definir **propriedades opcionais**, adicione `?` após o nome da propriedade: `age?: number`.

### 6. Union Types (Múltiplos Tipos)

Permite que uma variável ou parâmetro possa ter um de vários tipos definidos, usando o operador `|` (pipe).

```typescript
// Uso em variáveis
let age: string | number = 21;
age = "21"; // Válido

// Uso em funções
function mostrarIdade(idade: string | number) {
    if (typeof idade === "string") {
        console.log(idade.toUpperCase());
    } else {
        console.log(idade);
    }
}
```

### 7. Type e Interface: Como Usar e Diferenças

Ambos são usados para criar tipos nomeados para objetos, tornando o código mais legível e reutilizável.

#### `type` (Type Alias)

Um "apelido" flexível para qualquer tipo.

```typescript
type User = {
    nome: string,
    idade: number
};

function resumo(usuario: User) {
    return console.log(`Olá ${usuario.nome}, você tem ${usuario.idade} anos.`);
}
```

#### `interface`

Um "contrato" para a estrutura de objetos, com foco em extensibilidade.

```typescript
interface User {
    nome: string;
    idade: number;
}

function resumo(usuario: User) {
    return console.log(`Olá ${usuario.nome}, você tem ${usuario.idade} anos.`);
}
```

**Principal Diferença:** `Interfaces` podem ser estendidas e mescladas (declaration merging), sendo ideais para definir a forma de objetos e classes. `Types` são mais flexíveis e podem representar uniões, interseções e outros tipos complexos.

### 8. Type Assertions

Uma forma de informar ao compilador: "Eu sei o tipo deste valor, confie em mim". É útil ao interagir com o DOM ou APIs externas.

Use `as` para fazer a afirmação.

```typescript
// document.querySelector retorna um 'Element' genérico.
// Afirmamos que ele é um 'HTMLInputElement' para acessar a propriedade '.value'.
let campoIdade = document.querySelector("#idade") as HTMLInputElement;

console.log(campoIdade.value);
```

> **Atenção:** A asserção não realiza nenhuma conversão em tempo de execução. Se o tipo estiver errado, ocorrerá um erro.

### 9. Tipos Literais

Restringe uma variável a um conjunto específico de valores literais (strings, números, etc.), em vez de um tipo geral.

```typescript
function mostrarFrase(
    nome: string,
    alinhamento: "left" | "center" | "right" // 'alinhamento' só pode ser um desses três valores
) {
    return `<div style="text-align: ${alinhamento}">${nome}</div>`;
}

mostrarFrase("Angelo", "center");
// mostrarFrase("Angelo", "top"); // Erro do compilador!
```

### 10. Inferência de Tipos Literais

O TypeScript consegue inferir tipos literais com base no contexto, especialmente quando tipos explícitos são usados.

```typescript
function fazerRequisicao(url: string, method: "GET" | "POST") {
    // ...
}

type RequestDetails = {
    url: string,
    method: "GET" | "POST"
};

// Como 'req' tem o tipo 'RequestDetails', o TS sabe que 'req.method'
// é do tipo literal "GET" ou "POST", não apenas 'string'.
let req: RequestDetails = {
    url: "[http://google.com](http://google.com)",
    method: "GET"
};

fazerRequisicao(req.url, req.method); // Válido
```

### 11. Criando Tipos para Funções

Você pode criar um `type` para definir a assinatura de uma função. Isso é excelente para garantir consistência, especialmente com callbacks.

```typescript
// 'MathFunction' é um tipo para qualquer função que recebe
// dois números e retorna um número.
type MathFunction = (n1: number, n2: number) => number;

const somar: MathFunction = (n1, n2) => {
    return n1 + n2;
};

const subtrair: MathFunction = (n1, n2) => {
    return n1 - n2;
}
```