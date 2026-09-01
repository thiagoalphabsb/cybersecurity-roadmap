# 📓 Diário de Aprendizagem & Revisão — Dia 01

**Data:** 31/08/2026  
**Módulo:** Fundamentos de Computação, Sistema Operacional & Virtualização  

---

## 📊 1. Autoavaliação do Dia

| Tópico | Nota (0–5) | Nível de Domínio |
| :--- | :---: | :--- |
| **CPU** | **5/5** | Domínio completo do fluxo de execução |
| **RAM** | **5/5** | Compreensão total do papel de memória volátil |
| **Armazenamento** | **5/5** | Entendimento de persistência (SSD/HDD) |
| **Processos** | **5/5** | Entendimento de programas em execução |
| **Arquivos** | **5/5** | Estrutura e organização no SO |
| **Virtualização** | **4/5** | Entendimento de Hypervisor, Host e Guest |

---

## 🧠 2. O Que Aprendi
Compreendi o ciclo fundamental de funcionamento de um sistema computacional:
* **Fluxo de Execução:** Um programa permanece "adormecido" no armazenamento (SSD/HDD). Ao ser iniciado, é carregado na memória RAM, transformando-se em um **processo ativo**.
* **Ciclo da CPU:** A CPU busca (*fetch*), decodifica (*decode*) e executa (*execute*) as instruções diretamente da memória RAM, devido à sua altíssima velocidade.
* **Virtualização:** Conceitos de abstração de hardware por meio de *hypervisors* (VirtualBox) e gerenciamento de Máquinas Virtuais (Host vs. Guest).

---

## 🛠️ 3. O Que Consegui Executar

Comandos validados na máquina virtual Debian (VirtualBox):

| Comando | Função / Utilidade | O que observei no laboratório |
| :--- | :--- | :--- |
| `pwd` | Print Working Directory | Confirmação do caminho do laboratório atual |
| `ls -la` | Listagem detalhada | Mapeamento de arquivos ocultos e permissões |
| `ps` | Process Status simples | Processos vinculados à sessão atual |
| `ps aux` | Process Status detalhado | Mapeamento completo de todos os processos do sistema |
| `ps aux --sort=-%cpu \| head` | Filtro de processos | Identificação do *top process* com maior consumo de CPU |
| `df -h` | Disk Free (humano) | Leitura do espaço disponível nas partições de disco |
| `free -h` | Free Memory (humano) | Consumo e disponibilidade da memória RAM do sistema |

---

## 📁 4. Evidências Produzidas
As evidências e capturas de tela geradas durante a prática foram salvas na pasta `./evidence/`:

* `day-01-command-ps-aux-resultado.png`
* `day-01-commands-ls_-la-resultado-permissoesarquivos.png`
* `day-01-cyberlabs-command-ps.png`

---

## ❓ 5. Principais Dúvidas & Pontos de Atenção
1. **Uso composto de comandos (Pipes e Redirecionamentos):** Aprofundar o entendimento de como encadear múltiplos comandos usando `|`, `grep`, `head`, etc.
2. **Permissões de Arquivos e Diretórios:** Detalhar a interpretação da notação Octal e dos grupos de permissões (`rwx` para Usuário, Grupo e Outros).

---

## 🧑‍💻 6. Como Isso se Conecta à Cybersecurity?
Saber como os componentes de hardware e o SO funcionam em nível fundamental é indispensável para o trabalho de **Investigação e Detecção (SOC / DFIR)**:
* **Análise de Processos:** Permite identificar comportamentos anômalos, como malwares tentando se disfarçar de processos legítimos do sistema.
* **Monitoramento de Recursos:** Picos atípicos no consumo de CPU, RAM ou uso de disco podem indicar sequestro de recursos (ex: *cryptojacking*) ou vazamento/extração de dados.

---

## 📝 7. Conclusão do Dia
Os fundamentos apresentados foram assimilados com facilidade devido ao conhecimento prévio de computação. As prioridades identificadas para os próximos laboratórios são o domínio prático no encadeamento de comandos e a interpretação avançada da matriz de permissões Linux.
