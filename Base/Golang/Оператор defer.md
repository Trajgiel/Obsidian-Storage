2025-11-09 20:32
Tags: #golang 

---
Оператор **defer** позволяет выполнить определенную операцию после выполнения других действий (даже если сработает `panic`), при этом не важно, где в реальности вызывается эта функция.
```go
func main() {
    defer finish() // Отложенный вызов функции finish
    fmt.Println("1 Program has been started")
    fmt.Println("2 Program is working")
}

func finish() {
    fmt.Println("3 Program has been finished")
}

// 1 Program has been started
// 2 Program is working
// 3 Program has been finished
```

---

Если несколько функций вызываются с оператором `defer`, то те функции, которые были отложены раньше, выполнятся позже всех.
```go
func main() {
    defer finish() // Этот вызов отложен
    defer fmt.Println("1 Program has been started") // Этот вызов отложен
    fmt.Println("2 Program is working")
}

func finish() {
    fmt.Println("3 Program has been finished")
}

// 2 Program is working
// 1 Program has been started
// 3 Program has been finished
```

---

_Дополнение:_ Команда `defer` помещает вызов функции в стек. Поэтому вызовы функций выполняются в очередности **LIFO** (Last-In, First-Out), то есть последняя отложенная функция будет выполнена первой.

**Важно:** Оператор `defer` запоминает значения переменных, переданных в функцию, на момент объявления `defer`, а не на момент её вызова. Это означает, что значение переменной будет захвачено сразу, как только вы объявите отложенный вызов.
```go
a := 5
defer myFunc(a) // Когда вызовется myFunc, будет значение 5, а не 7
a = 7
```

---
### Links
[[Base/Golang/Golang]]