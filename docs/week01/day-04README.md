```markdown
# 🚀 Dia 04 - Fundamentos de Sistemas Operacionais, Processos & Pensamento Investigativo

## 📌 Visão Geral
Estudo voltado ao entendimento da arquitetura do Linux, gerenciamento de processos via linha de comando, navegação na estrutura de diretórios (FHS) e a aplicação do **pensamento investigativo** para monitoramento de ameaças em Cybersecurity.

---

## 🔬 O Fluxo da Investigação em Cybersecurity

O uso da mentalidade investigativa exige compreender como as ações do nível mais alto (processos/usuários) impactam a base do sistema (hardware):


```

Hardware
│
▼
Kernel (Interface de baixo nível)
│
▼
Sistema Operacional (Gerenciador de recursos)
│
▼
Processos (Programas em execução)
│
▼
Comportamento Normal (Baseline)
│
▼
Identificação de Anomalias
│
▼
🔐 Cybersecurity (Detecção & Resposta)

```

---

## 🛠️ Diagnóstico do Sistema
* **Kernel em execução:** `6.12.94+deb13-amd64` (Debian 13 Trixie / 64-bits)
* **Comandos de verificação:** `uname -a` / `uname -r`

---

## ⚙️ Gerenciamento de Processos no Linux

Todo processo criado no sistema recebe um **PID** (*Process ID*). O ciclo de vida e controle segue o fluxo:


```

Criou o processo ──> Identificou o processo ──> Descobriu o PID ──> Enviou o sinal ──> Terminou o processo

```

### Prática Realizada no Terminal
Simulação de criação de processo em segundo plano, localização na tabela de processos e encerramento forçado:

```bash
# 1. Criação de um processo temporário de 60 segundos
sleep 60

# 2. Localização do processo e identificação do PID (em outro terminal)
ps aux | grep sleep

# 3. Envio do sinal de encerramento para o PID encontrado
kill <PID_DO_PROCESSO>

```

---

## 📁 Estrutura de Diretórios (FHS - Filesystem Hierarchy Standard)

Mapeamento das principais pastas raiz do ecossistema Linux:

* `/etc` — Arquivos de configuração do sistema e serviços.
* `/home` — Diretório pessoal dos usuários comuns.
* `/var` — Dados variáveis (logs de sistema, filas de impressão, bancos de dados).
* `/tmp` — Arquivos temporários (limpos na reinicialização).
* `/usr` — Programas, utilitários e recursos do usuário.
* `/root` — Diretório home exclusivo do usuário administrador (root).

---

## 🛡️ Relação: Sistemas Operacionais × Cybersecurity

Para identificar anomalias em um ambiente corporativo ou SOC, o analista deve dominar a baseline do sistema para diferi-la de desvios suspeitos.

### Cenários Práticos de Investigação:

* Processos não identificados executando a partir de pastas temporárias (`/tmp`).
* Picos anormais de consumo de CPU e Memória RAM.
* Usuários, serviços ou tarefas agendadas criados sem autorização.
* Modificações não autorizadas em arquivos críticos de configuração (`/etc`).
* Processos ocultos inicializando automaticamente na subida do sistema.

> **Regra de Ouro:** É impossível identificar um **comportamento suspeito** sem conhecer previamente o **comportamento normal** do sistema.

---

## 📊 Autoavaliação de Domínio (Dia 04)

| Tema | Nota | Status |
| --- | --- | --- |
| **Sistema Operacional** | `5/5` | Dominado |
| **Kernel** | `5/5` | Dominado |
| **Processos** | `5/5` | Dominado |
| **PID** | `5/5` | Dominado |
| **Memória** | `5/5` | Dominado |
| **Sistema de Arquivos** | `5/5` | Dominado |
| **Comandos Linux** | `4/5` | Em Prática |
| **Relação com Cybersecurity** | `5/5` | Dominado |

```

```