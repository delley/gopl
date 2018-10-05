# echo3

O exemplo `echo3` exibe seus argumentos de linha de comando, porém, é uma versão mais simples e eficiente que usa a função **Join**, do pacote **strings**: 
 
```go
package main

import (
	"fmt"
	"os"
	"strings"
)

func main() {
	fmt.Println(strings.Join(os.Args[1:], " "))
}
```