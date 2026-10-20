# 🛡️ Week 07 — Linux Fundamentals & Hardening para Cibersegurança

> **Cybersecurity Roadmap — Fase 2: Sistemas e Infraestrutura**

A Week 07 consolida a expansão do roadmap no ecossistema **Linux**, abordando desde os fundamentos do sistema operacional, estrutura da árvore de diretórios (FHS), gerenciamento de usuários, grupos e permissões avançadas (POSIX & SUID/SGID/Sticky Bit), até o hardening de serviços essenciais como **SSH**, configuração de **Firewall (UFW/IPTables)**, auditoria de logs defensivos (`/var/log`) e resposta a incidentes via Bash.

## 🎯 Objetivos

* Dominar a navegação CLI, manipulação de arquivos e a estrutura do Linux Filesystem Hierarchy Standard (FHS).
* Gerenciar identidades, grupos e aplicar permissões numéricas/simbólicas e atributos especiais (SUID, SGID, Sticky Bit).
* Administrar processos, monitorar consumo de recursos e gerenciar serviços do sistema via `systemctl` e `journalctl`.
* Realizar o hardening do serviço OpenSSH (desabiltar root login, autenticação via chave pública, alteração de porta).
* Configurar e aplicar políticas defensivas de firewall utilizando UFW e regras do IPTables.
* Analisar e correlacionar logs de autenticação e sistema (`/var/log/auth.log` / `/var/log/secure`) em busca de anomalias.
* Simular ataques de força bruta contra SSH e analisar tentativas de acesso indevido.
* Desenvolver scripts em Bash para automação de checagem de integridade e resposta a incidentes no ecossistema Linux.

## 📚 Progresso

| Dia | Tema | Status |
| :-: | :--- | :-: |
| Day 01 | Arquitetura Linux, FHS e Comandos Essenciais de CLI | 🟢 Concluído |
| Day 02 | Gestão de Usuários, Grupos e Permissões Avançadas (SUID/SGID) | 🟢 Concluído |
| Day 03 | Gerenciamento de Processos, Serviços e Logs do Sistema | 🟢 Concluído |
| Day 04 | Hardening de OpenSSH e Autenticação por Par de Chaves | 🟢 Concluído |
| Day 05 | Segurança de Rede no Host: UFW & IPTables Rules | 🟢 Concluído |
| Day 06 | Simulação de Brute Force SSH & Análise de Logs via Bash | 🟢 Concluído |
| Day 07 | Resposta a Incidentes Linux, Relatório SOC & Encerramento | 🟢 Concluído |

**Status da Week 07: 🟢 FINALIZADA**

---

# 🗓️ Day 01 & 02 — Estrutura Linux, Permissões e SUID/SGID

Foram estudados:

* navegação no sistema de arquivos segundo o padrão **FHS** (`/etc`, `/var`, `/home`, `/root`, `/proc`);
* criação, modificação e gerenciamento de usuários (`useradd`, `usermod`) e grupos (`groupadd`);
* aplicação de permissões de arquivos/diretórios em notação octal e simbólica (`chmod`, `chown`);
* identificação e riscos de permissões especiais (**SUID**, **SGID** e **Sticky Bit**) em binários do sistema.

### Bash praticado

```bash
uname -a
whoami

# Gestão de permissões e busca por binários SUID inseguros
ls -la /etc/passwd /etc/shadow
chmod 750 /var/www/html
find / -perm -4000 -type f 2>/dev/null
```

📄 Documentação técnica: [`docs/day-01-02-linux-basics-permissions.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-07/day-02/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 👤 Day 03 — Processos, Serviços e Logs (`systemd`)

Foram estudados:

* monitoramento de processos ativos e consumo de memória/CPU (`ps aux`, `top`, `htop`);
* gerenciamento de serviços do sistema através do daemon `systemd` (`systemctl`);
* inspeção centralizada de logs com `journalctl` e análise do diretório `/var/log/`.

```bash
ps aux | grep sshd
systemctl status ssh
journalctl -u ssh --since "1 hour ago"
tail -f /var/log/auth.log
```

📄 Documentação técnica: [`docs/day-03-processes-and-logs.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-07/day-03/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🏢 Day 04 — SSH Hardening & Key-based Authentication

Foram estudados:

* geração de pares de chaves criptográficas RSA/Ed25519 para acesso seguro sem senha (`ssh-keygen`);
* transferência e provisionamento de chaves públicas (`ssh-copy-id`);
* hardening do arquivo de configuração do OpenSSH (`/etc/ssh/sshd_config`);
* desabilitação do login do superusuário `root` e restrição de autenticação via senha.

### Configuração de Hardening Aplicada (`sshd_config`)

```text
Port 2222
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
AllowUsers secops
```

```bash
ssh-keygen -t ed25519 -C "secops@cyberlab"
ssh-copy-id -i ~/.ssh/id_ed25519.pub secops@192.168.1.50
sshd -t
systemctl restart ssh
```

📄 Documentação técnica: [`docs/day-04-ssh-hardening.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-07/day-04/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🟣 Day 05 — Firewall no Host: UFW & IPTables Rules

Foram estudados:

* aplicação da filosofia de **Deny All / Allow by Exception** para portas de rede local;
* configuração simplificada de firewall utilizando **UFW (Uncomplicated Firewall)**;
* inspeção e criação de regras avançadas via **IPTables** (tabelas e chains `INPUT`, `FORWARD`, `OUTPUT`).

```bash
# Habilitação do UFW com política padrão DROP
ufw default deny incoming
ufw default allow outgoing
ufw allow 2222/tcp comment 'SSH Custom Port'
ufw allow 80/tcp comment 'HTTP Web Server'
ufw enable
ufw status verbose

# Inspeção via IPTables
iptables -L -v -n
```

📄 Documentação técnica: [`docs/day-05-firewall-ufw-iptables.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-07/day-05/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🔴 Day 06 — Simulação de Incidente: Brute Force SSH & Log Analysis

O Day 06 abordou uma simulação controlada de ataques de força bruta contra o serviço SSH e a criação de scripts de Parsing de Logs em Bash para identificação dos endereços IP invasores.

### Simulação do Incidente (Failed Password Attempts)

```bash
# Simulação de múltiplas tentativas incorretas de acesso
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.50:2222 -t 4
```

### Análise e Extraction de IPs Invasores via Bash

```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr
```

📄 Documentação técnica: [`docs/day-06-ssh-incident-investigation.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-07/day-06/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🔎 Day 07 — Resposta a Incidentes & Consolidação SOC Linux

O último dia consolidou a automação defensiva, bloqueio ativo dos atacantes e elaborou o relatório de segurança **INC-2026-002**.

### 🧪 Relatório de Incidente SOC #002

```text
===============================================================================
RELATÓRIO DE INCIDENTE DE SEGURANÇA - INCIDENTE #002
===============================================================================
ID do Incidente:   INC-2026-002
Serviço Alvo:      OpenSSH Daemon (Porta 2222/TCP)
Evento Auditado:   Failed Password / SSH Brute Force Attack
Severidade:        Alta / Tentativa de Intrusão

1. DETALHES DA INVESTIGAÇÃO:
   - Data/Hora:       15/10/2026 - 14:22:10 UTC
   - Origem (IP):     192.168.1.105
   - Contagem Falhas: 142 tentativas de login com usuários inválidos (root, admin, user)
   - Status:          Bloqueado via Firewall / Nenhuma credencial foi comprometida

2. AVALIAÇÃO DE RISCO:
   - Tentativa automatizada de adivinhação de senhas via força bruta.
   - Mitigado com sucesso devido à restrição de acesso por chaves criptográficas e alteração da porta padrão.

3. RECOMENDAÇÕES:
   - Incluir o IP 192.168.1.105 na lista de bloqueio permanente do IPTables.
   - Implementar o utilitário `Fail2ban` para bloqueio automatizado de ataques de força bruta.
===============================================================================
```

📄 Documentação técnica: [`docs/day-07-week07-summary.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

---

# 📸 Repositório de Evidências (`.png`)

Todas as capturas de tela dos testes, comandos e relatórios estão catalogadas no diretório oficial de evidências:

🔗 **[Acessar pasta de evidências no GitHub](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)**

---

# 🧠 Principais Aprendizados

* Compreensão do Linux Filesystem Hierarchy Standard (FHS) e permissões POSIX.
* Identificação e mitigação de permissões especiais arriscadas (SUID/SGID).
* Gerenciamento e análise de processos/daemons via `systemd` e `journalctl`.
* Hardening rigoroso de serviços expostos (OpenSSH).
* Implementação de controle de acesso à rede com UFW e regras do IPTables.
* Monitoramento de logs do sistema em tempo real e extração de indicadores de comprometimento (IoCs) via Bash (`grep`, `awk`, `sed`, `uniq`).
* Automação básica de mitigação e resposta rápida a incidentes de rede e SO.

---

# 🔗 Relação com as Weeks Anteriores

### Week 05 — Windows Server

```text
Event Viewer
 ↓
Event ID 4625
 ↓
PowerShell Parsing
 ↓
Group Policy Objects (GPO)
```

### Week 06 — Active Directory

```text
Domain Controller
 ↓
IAM & Least Privilege
 ↓
Unidades Organizacionais
 ↓
Centralized Audit Baseline
```

### Week 07 — Linux Fundamentals & Hardening

```text
Linux Kernel & FHS
 ↓
POSIX Permissions & SUID Audit
 ↓
SSH Hardening & Key Auth
 ↓
UFW / IPTables Defense
 ↓
Auth Logs (`/var/log/auth.log`) & Incident Response via Bash
```

---

# 🛡️ Perspectiva Blue Team

A Week 07 provou que o Linux é a fundação da infraestrutura moderna, servidores web e cloud.

> **Garantir a segurança de um ambiente Linux exige entender profundamente permissões de arquivos, visibilidade constante de logs do sistema e restrição estrita de serviços expostos à rede.**

A combinação de autenticação baseada unicamente em chaves criptográficas, redução da superfície de ataque com firewalls de host e análise automatizada de logs permite interceptar atividades maliciosas rapidamente, impedindo a movimentação lateral ou elevação de privilégios.

---

# 🏁 Status

**Week 07 — Linux Fundamentals & Hardening: 🟢 CONCLUÍDA**

**Fase 2 — Sistemas e Infraestrutura: em andamento**

**Documentos:** [`docs/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

**Evidências:** [`evidence/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

## 👨‍💻 Projeto

**Cybersecurity Roadmap**

**Desenvolvido por Thiago S. Silva**

🔗 [GitHub — Cybersecurity Roadmap](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap)