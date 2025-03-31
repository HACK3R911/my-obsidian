```go
package main

import "fmt"

func main() {
    i := 0
    fmt.Println("Start")
LOOP:
    if i > 50 {
        goto END
    }
    fmt.Println(i)
    i++
    goto LOOP
END:
}
```

Нельзя прыгать в другой блок кода, в функцию
после `goto`

Нельзя понять как работает программа лучше использовать циклы