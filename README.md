# MGRun

[![License](https://img.shields.io/badge/license-PolyForm%20Perimeter%201.0.0-5351FB)](LICENSE.md)

**MGRun** é um wrapper leve e multiplataforma em Go para execução de comandos do sistema, projetado para simplificar o uso de `exec` com **captura de saída em tempo real**, **callbacks** e **controle seguro de concorrência**.

Ideal para aplicações CLI, ferramentas de automação, instaladores, utilitários desktop e sistemas que precisam acompanhar a execução de comandos enquanto eles ainda estão rodando.

---

## ✨ Recursos

* 🌍 **Multiplataforma**
  Abstrai automaticamente a execução entre:

  * PowerShell (Windows)
  * SH (Linux e macOS)

* 📡 **Streaming em tempo real**
  Receba cada linha de `stdout` e `stderr` via callbacks enquanto o processo executa.

* 🧵 **Thread-safe**
  Leitura concorrente segura das streams e controle confiável do processo.

* 🏠 **Ambiente herdado**

  * Executa comandos a partir do diretório *Home* do usuário
  * Herda variáveis de ambiente do sistema
  * Permite adicionar variáveis customizadas

* 🔁 **Código de saída acessível**
  Obtenha o *exit code* após a finalização do processo.

---

## 📦 Instalação

```bash
go get github.com/profmugomes/mgrun
```

---

## 🚀 Exemplo de uso

```go
package main

import (
	"fmt"
	"os"

	"github.com/profmugomes/mgrun"
)

func main() {
	sRun := mgrun.New("ls -a")

	// Definir diretório de execução (opcional)
	pathHome, _ := os.UserHomeDir()
	sRun.SetDir(pathHome)

	// Variáveis de ambiente extras (opcional)
	sRun.AddEnv("EXEMPLO", "Valor")

	// Callback para stderr
	sRun.OnStderr(func(line string) {
		fmt.Printf("[STDERR]: %s\n", line)
	})

	// Callback para stdout
	sRun.OnStdout(func(line string) {
		fmt.Printf("[STDOUT]: %s\n", line)
	})

	// Executa o comando
	if err := sRun.Run(); err != nil {
		fmt.Printf("Erro na execução: %v\n", err)
	}

	fmt.Printf("Exit Code: %d\n", sRun.ExitCode())
}
```

---

## 🧩 Compatibilidade

* Go 1.26.5+
* Linux, Windows ou macOS

---

## 👤 Autor

**Murilo Gomes Julio**

🔗 [https://www.profmugomes.com.br](https://www.profmugomes.com.br)

📺 [https://youtube.com/@profmugomes](https://youtube.com/@profmugomes)

---

## License

Copyright (c) 2025-2026 Murilo Gomes Julio. All Rights Reserved.

This project is licensed under the PolyForm Perimeter License 1.0.1.

### Summary

This software is available for commercial and noncommercial use, subject to the terms of the PolyForm Perimeter License 1.0.1.

You may:

* ✔ Use the software for commercial and noncommercial purposes.
* ✔ Inspect and study the source code.
* ✔ Modify the software.
* ✔ Create derivative works based on the software.
* ✔ Redistribute the software and permitted modifications.

You may not:

* ✖ Provide a product that competes with the software.

See the full license terms at LICENSE.md.

This summary is provided for convenience only and does not replace or modify the full license terms.