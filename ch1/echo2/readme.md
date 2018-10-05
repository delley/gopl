# echo2

O exemplo `echo2` exibe seus argumentos de linha de comando, porém, neste exemplo é utilizado o loop **for** associado com o **range**: 
 
```go
package main

import (
	"fmt"
	"os"
)

func main() {
	s, sep := "", ""
	for _, arg := range os.Args[1:] {
		s += sep + arg
		sep = " "
	}
	fmt.Println(s)
}
```