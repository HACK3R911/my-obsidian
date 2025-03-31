#errors #panic #recover

## Что такое ошибка?

Ошибка - это хорошо разработанная абстрактная концепция, которая возникает, когда происходит исключение. То есть всякий раз, когда происходит что-то непредвиденное, возникает ошибка. Ошибки встречаются в каждом языке, что, по сути, означает, что это концепция в сфере программирования.

## Зачем нам нужна ошибка?

Ошибки - это часть любой программы. Ошибка говорит о том, что произошло что-то непредвиденное. Ошибки также помогают поддерживать стабильность и ремонтопригодность кода. Без ошибок программы, которые мы используем сегодня, будут чрезвычайно глючными из-за недостатка тестирования.

## Ошибки в Golang

В Golang поддержка ошибок реализована очень просто. Функции Go возвращают ошибки в качестве второго возвращаемого значения. Это стандартный способ реализации и использования ошибок в Go. Это означает, что ошибку можно проверить непосредственно перед тем, как перейти к следующим шагам.

## Простые методы создания ошибок

Существует множество методов создания ошибок. Здесь мы рассмотрим простые, которые можно создать без особых усилий.
### 1. Использование функции New

В пакете ошибок Golang есть функция New(), с помощью которой можно легко создавать ошибки. Ниже она показана в действии.

```go
package main
 
import (
    "fmt"
    "errors"
)
 
func e(v int) (int, error) {
    if v == 0 {
        return 0, errors.New("Zero cannot be used")
    } else {
        return 2*v, nil
    }
}
 
func main() {
    v, err := e(0)
     
    if err ! = nil {
        fmt.Println(err, v)      // Zero cannot be used 0
    }   
}
```

### 2. Использование функции Errorf

В пакете fmt есть метод Errorf(), который позволяет форматировать ошибки, как показано ниже.

```go
fmt.Errorf("Error: Zero not allowed! %v", v)    // Error: Zero not allowed! 0
```
## Проверка на ошибку

Для проверки ошибки мы просто получаем второе значение функции, а затем сверяем его с nil. Поскольку нулевое значение ошибки - это nil. Поэтому мы проверяем, является ли ошибка нулем. Если да, то ошибки нет, а во всех остальных случаях ошибка произошла.

```go
package main
 
import (
    "fmt"
    "errors"
)
 
func e(v int) (int, error) {
    return 42, errors.New("42 is unexpected!")
}
 
func main() {
    _, err := e(0)
     
    if err != nil {   // check error here
        fmt.Println(err)      // 42 is unexpected!
    }   
}
```
## Паника и выздоровление(panic and recover)

Паника возникает, когда происходит неожиданная ошибка. Это останавливает выполнение функции. Восстановление(recover) является ее противоположностью. Он позволяет восстановить выполнение после остановки. Приведенный ниже код иллюстрирует эту концепцию.

```go
package main
 
import (
    "fmt"
)
 
func f(s string) {
    panic(s)      // throws panic
}
 
func main() {
        // defer makes the function run at the end
    defer func() {      // recovers panic
        if e := recover(); e != nil {
                    fmt.Println("Recovered from panic")
	            }
    }()
     
    f("Panic occurs!!!") // throws panic 
     
    // output:
    // Recovered from panic
}
```
## Создание пользовательских ошибок

Как мы видели ранее, для создания новых ошибок можно использовать функции errors.New() и fmt.Errorf(). Но есть и другой способ сделать это. Это реализация интерфейса ошибок.

```go
type CustomError struct {
    data string
}
 
func (e *CustomError) Error() string {
    return fmt.Sprintf("Error occured due to... %s", e.data)
}
```
## Возвращение ошибок наряду со значениями

Возвращать ошибки в Go довольно просто. Go поддерживает несколько возвращаемых значений. Поэтому мы можем вернуть любое значение и ошибку одновременно, а затем проверить ошибку. Вот как это можно сделать.

```go
package main

import (
    "fmt"
    "errors"
)
 
func returnError() (int, error) {  // declare return type here
    return 42, errors.New("Error occured!")  // return it here
}
 
func main() {
    v, e := returnError()
    if e != nil {
        fmt.Println(e, v)  // Error occured! 42
    }
}
```
## Игнорирование ошибок в Golang

В Go есть оператор skip (-), который позволяет пропускать возвращаемые ошибки вообще. Здесь поможет простое использование оператора skip.

```go
package main
 
import (
    "fmt"
    "errors"
)
 
func returnError() (int, error) {  // declare return type here
    return 42, errors.New("Error occured!")  // return it here
}
 
func main() {
    v, _ := returnError()   // skip error with skip operator
     
    fmt.Println(v)    // 42
}
```