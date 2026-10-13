## Investigação de processos

### Objetivo
Identificar processos ativos e observar o consumo de CPU.

### Hipótese
Esperava encontrar vários processos executando simultaneamente e diferentes níveis de consumo de CPU.

### Pergunta
Quais processos estavam utilizando mais CPU?

### Comando
```bash
ps aux --sort=-%cpu | head
```

### Resultado
O comando exibiu os processos com maior consumo de CPU no momento da consulta. Os processos e PIDs registrados pertencem ao ambiente de laboratório.

### Interpretação
`ps` mostra os processos no momento da execução. A combinação com `--sort=-%cpu` ordena pelo consumo de CPU, e `head` limita a saída às primeiras linhas.

### Limitações
A saída representa apenas o momento em que o comando foi executado.

### Evidências
As capturas associadas estão disponíveis no [índice de evidências](../evidence/README.md).
