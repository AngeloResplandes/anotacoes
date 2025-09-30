# 🚶🏻‍♂️ Primeiros Passos

## 1 - Introdução ao Go

### Go CLI
* `go mod init NomePasta` - Criando go.mod
* `go run main.go` - Compila e executa o projeto
* `go build main.go` - Compila o projeto
* `go build -o "app" main.go` - Compila o projeto e nomeia como app.exe
* `go get` - Instala algum package
* `go install` - Compila e instala um package
* `go test` - Roda algum teste relacionado ao projeto
* `go mod tidy` - Atualiza as dependencias

### Estrutura básica de um programa
* Todo programa Go começa na função `main`:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

### Variáveis
* Em Go, variáveis podem ser declaradas de forma explícita ou inferida:

```go
package main

import "fmt"

func main() {
    var nome string = "Ângelo" // declaração explícita
    idade := 21                // inferência de tipo
    fmt.Println(nome, idade)
}

```

### Constantes
* Usadas para valores que não mudam:

```go
package main

import "fmt"

const PI = 3.14

func main() {
    fmt.Println("Valor de PI:", PI)
}

```

## 2 - Tipos Primitivos

### Inteiros
```go
var a int = 10
var b int = -5
fmt.Println(a, b)
```

### Floats
```go
var preco float64 = 19.90
fmt.Println("Preço:", preco)
```

### Booleanos
```go
ativo := true
fmt.Println("Está ativo?", ativo)
```

### Strings
```go
nome := "GoLang"
fmt.Println("Nome:", nome)
```

## 3 - Tipos Compostos

### Array
* Tamanho fixo:

```go
var numeros [3]int = [3]int{1, 2, 3}
fmt.Println(numeros)
```

### Slice
* Flexível (mais usado que array):

```go
frutas := []string{"maçã", "banana", "laranja"}
frutas = append(frutas, "uva")
fmt.Println(frutas)
```

### Map
* Estrutura de chave-valor:

```go
notas := map[string]float64{
    "Maria": 9.5,
    "João":  8.3,
}
fmt.Println(notas["Maria"])
```

## 4 - Fluxo de Controle

### If e Else
* Condicional (se e senão)

```go
idade := 18
if idade >= 18 {
    fmt.Println("Maior de idade")
} else {
    fmt.Println("Menor de idade")
}
```

### Switch Case
* Interruptor

```go
dia := 3
switch dia {
case 1:
    fmt.Println("Domingo")
case 2:
    fmt.Println("Segunda")
default:
    fmt.Println("Outro dia")
}
```

### For
* Laço de reptição

```go
for i := 0; i < 5; i++ {
    fmt.Println("i =", i)
}
```

### Range 
* Itera sobre coleções:

```go
frutas := []string{"maçã", "banana", "uva"}
for i, fruta := range frutas {
    fmt.Println(i, fruta)
}
```

## 5 - Estruturas

### Structs
* Agrupamento de dados:

```go
type Pessoa struct {
    Nome  string
    Idade int
}

p := Pessoa{"Maria", 30}
fmt.Println(p.Nome, p.Idade)
```

### Funções

```go
func soma(a int, b int) int {
    return a + b
}

fmt.Println(soma(3, 5))
```

### Métodos
* Funções associadas a tipos:

```go
type Retangulo struct {
    Largura, Altura float64
}

func (r Retangulo) Area() float64 {
    return r.Largura * r.Altura
}

ret := Retangulo{10, 5}
fmt.Println("Área:", ret.Area())
```

## 6 - Avançado

### Ponteiros
* Referência a endereços de memória:

```go
x := 10
p := &x  // ponteiro para x
*p = 20  // altera x através do ponteiro
fmt.Println("x =", x) // 20
```

### Concorrência com Goroutines
* Executam funções de forma paralela:

```go
func falar(texto string) {
    for i := 0; i < 3; i++ {
        fmt.Println(texto)
        time.Sleep(time.Millisecond * 500)
    }
}

go falar("Olá")
go falar("Mundo")
time.Sleep(time.Second * 2)
```

### Goroutines sem ordem definida

```go
func tarefa(id int) {
    fmt.Println("Tarefa", id, "iniciada")
    time.Sleep(time.Duration(id) * time.Second)
    fmt.Println("Tarefa", id, "finalizada")
}

for i := 1; i <= 3; i++ {
    go tarefa(i)
}
time.Sleep(time.Second * 5)
```

### Channels
* Comunicação entre goroutines:

```go
canal := make(chan string)

go func() {
    canal <- "Mensagem 1"
    canal <- "Mensagem 2"
}()

fmt.Println(<-canal)
fmt.Println(<-canal)
```