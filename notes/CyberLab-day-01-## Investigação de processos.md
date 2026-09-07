## Investigação de processos

### Objetivo
Identificar processos ativos e observar consumo de CPU.

### Hipótese
Espero encontrar diversos processos executando
simultaneamente e diferentes níveis de consumo de CPU.

### Pergunta
Quais processos estavam utilizando mais CPU?
Debian PID 5155 e 1535

### Comando
ps aux --sort=-%cpu | head

### Resultado
ele me mostrou os processos que mais estão consumindo cpu. usuário Debian PID 5155 e 1535, print salvo 
em evidencias. 

### Interpretação
comando ps mostra os processos no momento o comando 
ps aux --sort=-%cpu | head
mostra especificamente os processos que mais estão usando recursos da cpu, junto com o | (pipe) o final 
head concatena outro comando para mostrar as linhas superiores.

### Limitações
ele só mostra os processos do momento usado o comando. 

### Conclusão
[1 ou 2 frases]

### Evidências
day-01-cyberlabs-command-ps.png
day-01-command-ps-aux-resultado.png


