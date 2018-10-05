# dup1

O exemplo `dup1` exibe o texto de toda linha que aparece mais de uma vez na entrada-padrão, precedida por sua contagem:
 
```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	counts := make(map[string]int)
	input := bufio.NewScanner(os.Stdin)

	for input.Scan() {
		counts[input.Text()]++
	}
	// Nota: ignorando erros em potencial de input.Err()
	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}
```

Para testar esse programa no linux, utilize o seguinte comando:

```shell
cat dados.txt | go run main.go
```