# Introdução Java

### Variáveis

Em Java, variáveis são espaços na memória usados para armazenar dados. Toda variável precisa ser declarada com um tipo antes de ser usada.

**Sintaxe básica:**
```java
tipo nomeDaVariavel = valor;
```

**Exemplos:**
```java
int idade = 25;
String nome = "João";
double salario = 3500.50;
boolean ativo = true;
```

**Regras para nomes de variáveis:**
- Devem começar com letra, underscore (_) ou cifrão ($)
- Podem conter letras, números, underscore e cifrão
- São case-sensitive (idade ≠ Idade)
- Não podem usar palavras reservadas do Java
- Convenção: usar camelCase (minhaVariavel)

### Tipagem de Dados

Java é uma linguagem **fortemente tipada** e **estaticamente tipada**, o que significa:

- **Fortemente tipada:** Não permite conversões automáticas que possam causar perda de dados
- **Estaticamente tipada:** O tipo da variável é definido em tempo de compilação e não muda

**Características:**
- Toda variável deve ter seu tipo declarado
- O tipo não pode ser alterado após a declaração
- Oferece segurança e previne erros em tempo de compilação

**Exemplo:**
```java
int numero = 10;
numero = "texto"; // ERRO! Não é possível atribuir String a int
```

### Dados Primitivos

Java possui 8 tipos de dados primitivos, que são os blocos fundamentais de construção:

**1. Tipos Inteiros:**
- `byte`: 8 bits (-128 a 127)
  ```java
  byte idade = 25;
  ```
- `short`: 16 bits (-32.768 a 32.767)
  ```java
  short ano = 2024;
  ```
- `int`: 32 bits (-2³¹ a 2³¹-1)
  ```java
  int populacao = 1000000;
  ```
- `long`: 64 bits (-2⁶³ a 2⁶³-1)
  ```java
  long distancia = 9876543210L; // L no final
  ```

**2. Tipos de Ponto Flutuante:**
- `float`: 32 bits (precisão simples)
  ```java
  float preco = 19.99f; // f no final
  ```
- `double`: 64 bits (precisão dupla)
  ```java
  double pi = 3.14159265359;
  ```

**3. Tipo Caractere:**
- `char`: 16 bits (caractere Unicode)
  ```java
  char letra = 'A';
  char simbolo = '\u0041'; // Unicode
  ```

**4. Tipo Lógico:**
- `boolean`: true ou false
  ```java
  boolean ativo = true;
  boolean maior = (10 > 5); // true
  ```

**Tabela Resumo:**
| Tipo    | Tamanho | Valor Padrão | Intervalo                    |
|---------|---------|--------------|------------------------------|
| byte    | 1 byte  | 0            | -128 a 127                   |
| short   | 2 bytes | 0            | -32.768 a 32.767             |
| int     | 4 bytes | 0            | -2³¹ a 2³¹-1                 |
| long    | 8 bytes | 0L           | -2⁶³ a 2⁶³-1                 |
| float   | 4 bytes | 0.0f         | ~±3.4E+38 (6-7 dígitos)      |
| double  | 8 bytes | 0.0d         | ~±1.8E+308 (15 dígitos)      |
| char    | 2 bytes | '\u0000'     | 0 a 65.535                   |
| boolean | 1 bit   | false        | true ou false                |

### Dados não Primitivos

Dados não primitivos (ou tipos de referência) são objetos criados a partir de classes. Eles armazenam referências (endereços de memória) aos objetos, não os valores diretamente.

**Principais características:**
- São criados pelo programador (exceto String)
- Podem ser nulos (`null`)
- Têm métodos associados
- Valor padrão é `null`
- Armazenados no heap

**Exemplos principais:**

**1. String:**
```java
String nome = "Maria";
String sobrenome = new String("Silva");
String completo = nome + " " + sobrenome; // Concatenação

// Métodos úteis
int tamanho = nome.length(); // 5
String maiuscula = nome.toUpperCase(); // "MARIA"
char primeira = nome.charAt(0); // 'M'
```

**2. Arrays:**
```java
int[] numeros = {1, 2, 3, 4, 5};
String[] nomes = new String[3];
nomes[0] = "Ana";
nomes[1] = "Bia";
nomes[2] = "Carlos";

int tamanho = numeros.length; // 5
```

**3. Classes Wrapper:**
Classes que "envolvem" tipos primitivos, tornando-os objetos:
```java
Integer numero = 100;        // int
Double decimal = 3.14;       // double
Boolean ativo = true;        // boolean
Character letra = 'A';       // char

// Conversões
int primitivo = numero.intValue();
String texto = numero.toString();
```

**4. Classes Personalizadas:**
```java
public class Pessoa {
    String nome;
    int idade;
    
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }
}

Pessoa pessoa = new Pessoa("João", 30);
```

**Diferenças entre Primitivos e Não Primitivos:**
| Aspecto           | Primitivos      | Não Primitivos           |
|-------------------|-----------------|--------------------------|
| Armazenamento     | Stack           | Heap (referência no Stack)|
| Valor padrão      | 0, false, etc.  | null                     |
| Tamanho           | Fixo            | Variável                 |
| Métodos           | Não possuem     | Possuem métodos          |
| Comparação        | == (valor)      | == (referência)          |
| Pode ser null     | Não             | Sim                      |

### Condicionais If, Else e Else if