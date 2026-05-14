# Concorrência II

## Tópicos Avançados em Concorrência

Esta seção aborda conceitos avançados de concorrência em Go, incluindo Channels, Select, e outros mecanismos para comunicação entre goroutines.

## Channels

Channels são o principal mecanismo de comunicação entre goroutines em Go. Eles permitem que goroutines enviem e recebam valores de forma segura, evitando problemas de concorrência como race conditions.

### Criando Channels

Para criar um channel, use a função `make()`:

```go
// Channel não-buferizado (unbuffered)
ch := make(chan int)

// Channel buferizado (buffered) com capacidade 3
chBuf := make(chan string, 3)
```

### Enviando e Recebendo Valores

- **Envio**: Use `ch <- valor`
- **Recebimento**: Use `valor := <-ch` ou `valor, ok := <-ch`

```go
ch := make(chan int)

go func() {
    ch <- 42  // Envia o valor 42
}()

valor := <-ch  // Recebe o valor
fmt.Println(valor)  // Imprime 42
```

### Channels Buferizados vs Não-Buferizados

- **Não-buferizados**: O envio bloqueia até que outra goroutine receba o valor.
- **Buferizados**: Permitem enviar valores até a capacidade do buffer sem bloquear.

```go
ch := make(chan int, 2)  // Buffer de 2
ch <- 1  // Não bloqueia
ch <- 2  // Não bloqueia
ch <- 3  // Bloqueia até que alguém receba
```

### Fechando Channels

Use `close(ch)` para indicar que não serão enviados mais valores. Receber de um channel fechado retorna o valor zero do tipo e `ok = false`.

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
close(ch)

for valor := range ch {
    fmt.Println(valor)  // Imprime 1 e 2
}
```

### Range sobre Channels

O `range` pode ser usado para iterar sobre valores de um channel até que ele seja fechado:

```go
ch := make(chan int)
go func() {
    for i := 1; i <= 5; i++ {
        ch <- i
    }
    close(ch)
}()

for valor := range ch {
    fmt.Println(valor)  // Imprime 1, 2, 3, 4, 5
}
```

### Channels Direcionais

Channels podem ser restritos a apenas envio ou recebimento:

```go
func enviar(ch chan<- int) {  // Apenas envio
    ch <- 42
}

func receber(ch <-chan int) {  // Apenas recebimento
    valor := <-ch
}
```

### Select Statement

O `select` permite aguardar múltiplas operações de channel simultaneamente, similar ao `switch`:

```go
select {
case msg := <-ch1:
    fmt.Println("Recebido de ch1:", msg)
case msg := <-ch2:
    fmt.Println("Recebido de ch2:", msg)
case ch3 <- "enviando":
    fmt.Println("Enviado para ch3")
default:
    fmt.Println("Nenhuma operação pronta")
}
```

O `select` bloqueia até que uma das operações esteja pronta. Se múltiplas estiverem prontas, uma é escolhida aleatoriamente.

### Padrões Comuns com Channels

- **Generator**: Função que retorna um channel para produzir valores
- **Fan-in/Fan-out**: Combinar ou dividir trabalho entre múltiplas goroutines
- **Pipeline**: Cadeia de operações onde cada etapa é uma goroutine

```go
// Exemplo de pipeline
func gerar(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        for _, n := range nums {
            out <- n
        }
        close(out)
    }()
    return out
}

func quadrado(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

// Uso: c := quadrado(gerar(1, 2, 3, 4))
```

Channels são fundamentais para escrever programas concorrentes eficientes e seguros em Go, permitindo comunicação clara entre goroutines sem compartilhamento de memória.