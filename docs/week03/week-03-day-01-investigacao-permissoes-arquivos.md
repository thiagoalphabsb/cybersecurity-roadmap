## Investigação de permissões de arquivos

### Objetivo
Identificar permissões apresentadas nos arquivos e compreender as diferenças entre os tipos de acesso.

### Hipótese
Os arquivos e diretórios apresentam permissões diferentes conforme usuário, grupo e demais usuários.

### Conceitos
- `r` — leitura (*read*)
- `w` — escrita (*write*)
- `x` — execução (*execute*)

### Comando
```bash
ls -la
```

### Resultado
O comando apresentou permissões, proprietário, grupo e nomes de arquivos e diretórios no caminho consultado.

### Interpretação
As permissões indicam os acessos concedidos ao proprietário, ao grupo e aos demais usuários. Para diretórios, o significado de `x` está relacionado à possibilidade de atravessar/acessar o diretório.

### Limitações
A saída mostra os arquivos e diretórios do local em que o comando foi executado.

### Evidências
As capturas associadas estão disponíveis no [índice de evidências](../evidence/README.md).
