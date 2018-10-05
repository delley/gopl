# dup2

O exemplo `dup2` exibe a contagem e o texto das linhas que aparecem mais de uma vez. Ele lê de `stdin` ou de uma lista de arquivos passados como argumento na linha de comando:
 
```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	counts := make(map[string]int)
	files := os.Args[1:]
	if len(files) == 0 {
		countLines(os.Stdin, counts)
	} else {
		for _, arg := range files {
			f, err := os.Open(arg)
			if err != nil {
				fmt.Fprintf(os.Stderr, "dup2: %v\n", err)
				continue
			}
			countLines(f, counts)
			f.Close()
		}
	}

	for line, n := range counts {
		if n > 1 {
			fmt.Printf("%d\t%s\n", n, line)
		}
	}
}

func countLines(f *os.File, counts map[string]int) {
	input := bufio.NewScanner(f)
	for input.Scan() {
		counts[input.Text()]++
	}
	// Nota: estamos ignorando potenciais erros de input.Err()
}
```

Para testar esse programa no linux, utilize o seguinte comando:

```shell
go run main.go dados1.txt dados2.txt
```