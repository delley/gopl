# dup3

O exemplo `dup3` exibe a contagem e o texto das linhas que aparecem mais de uma vez. Ele usa a função `ReadFile` para lê arquivos passados como argumento na linha de comando e por isso não lê de `stdin`:
 
```go
package main

import (
	"fmt"
	"io/ioutil"
	"os"
	"strings"
)

func main() {
	counts := make(map[string]int)
	for _, filename := range os.Args[1:] {
		data, err := ioutil.ReadFile(filename)
		if err != nil {
			fmt.Fprintf(os.Stderr, "dup3: %v\n", err)
			continue
		}
		for _, line := range strings.Split(string(data), "\n") {
			counts[line]++
		}
	}

	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}
```

Para testar esse programa no linux, utilize o seguinte comando:

```shell
go run main.go dados1.txt dados2.txt
```