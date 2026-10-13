# 📚 Documentação Técnica — Cybersecurity Roadmap

> Índice central dos registros técnicos, anotações de laboratório e relatórios que complementam cada semana do **Cybersecurity Roadmap**. A organização abaixo apresenta o foco de estudo, os documentos disponíveis e as evidências práticas relacionadas.

---

## 🎯 Visão geral

Esta pasta reúne materiais de apoio produzidos durante os laboratórios. Para acompanhar o roteiro completo de cada semana, acesse também o README principal da respectiva semana. As evidências visuais ficam organizadas separadamente em `evidence/`.

## 🧭 Sumário

1. [Semana 01 — Fundamentos, Linux e CyberLab](#-semana-01--fundamentos-linux-e-cyberlab)
2. [Semana 02 — Virtualização e provisionamento do CyberLab](#-semana-02--virtualização-e-provisionamento-do-cyberlab)
3. [Semana 03 — Linux e segurança defensiva](#-semana-03--linux-e-segurança-defensiva)
4. [Semana 04 — Redes e análise prática](#-semana-04--redes-e-análise-prática)
5. [Semana 05 — Windows para Cibersegurança](#-semana-05--windows-para-cibersegurança)
6. [Semana 06 — Active Directory](#-semana-06--active-directory)
7. [Semana 07 — Python](#-semana-07--python)
8. [Materiais complementares e projetos](#-materiais-complementares-e-projetos)

---

## 🖥️ Semana 01 — Fundamentos, Linux e CyberLab

**Foco:** fundamentos de computação, comandos Linux, configuração do ambiente de laboratório e primeiros registros técnicos.

**Roteiro da semana:** [Week 01 — Fundamentos de Computação, Linux e CyberLab](../week-01/README.md)  
**Evidências:** [Abrir evidências da Semana 01](../evidence/week01/)

### Documentos disponíveis

- [Comandos do Dia 02](./week01/comandos-dia-02.md)
- [Configuração do ambiente](./week01/configuration.md)
- [Comandos aprendidos no CyberLab — Dia 01](./week01/cyberlab-day-01-comandos-aprendidos.md)
- [Inventário](./week01/inventario.md)
- [Lições aprendidas](./week01/lessons-learned.md)
- [Guia de MFA](./week01/mfa-guide.md)
- [Processo de revisão](./week01/review-process.md)
- [Checklist de segurança](./week01/security-checklist.md)
- [Relatório de incidente 001](./week01/RELATORIO-INCIDENTE-001.txt)

Também estão disponíveis registros operacionais adicionais: [README do Dia 04](./week01/day-04README.md), [README do Dia 05](./week01/day-05-README.md), [README do Dia 07](./week01/day-07-README.md) e [registro de comandos do CyberLab](./week01/cyberlab-day-01-comandos-aprendidos.md).

---

## 🧪 Semana 02 — Virtualização e provisionamento do CyberLab

**Foco:** criação e configuração das máquinas virtuais, rede isolada, snapshots e validação da comunicação entre Debian e Kali.

**Roteiro da semana:** [Week 02 — Virtualização e Provisionamento do CyberLab](../week-02/README.md)  
**Evidências:** [Abrir evidências da Semana 02](../evidence/week02/) · [Relatório de evidências da Semana 02](../evidence/week02/README.md)

### Documentos disponíveis

- [Week 02 — Dias 01 e 02](./week02/week%2002%20-%20day%2001%20e%2002.txt)
- [Week 02 — Dia 03](./week02/week%2002%20-%20day%2003.txt)
- [Week 02 — Dia 04](./week02/week%2002%20-day%2004.md)
- [Week 02 — Dias 06 e 07](./week02/week-02-day06-07.md)

As evidências incluem provisionamento das VMs, snapshot Debian, comunicação interna, análise de handshake TCP/SSH, captura no Wireshark e reconhecimento com Nmap.

---

## 🐧 Semana 03 — Linux e segurança defensiva

**Foco:** usuários e grupos, permissões POSIX, privilégios sudo, processos, serviços, logs e investigação de arquivos.

**Roteiro da semana:** [Week 03 — Linux](../week-03/README.md)  
**Evidências:** [Abrir evidências da Semana 03](../evidence/week03/) · [Relatório de evidências Linux](../evidence/week03/README.md)

### Documentos disponíveis

- [Investigação de permissões e arquivos](./week03/week-03-day-01-investigacao-permissoes-arquivos.md)
- [Investigação de processos](./week03/week-03-day-01-investigacao-processos.md)
- [Registro do Dia 01](./week03/week-03-day-01.txt)
- [Registro dos Dias 02 e 03](./week03/week-03-day-02%2603.txt)

---

## 🌐 Semana 04 — Redes e análise prática

**Foco:** endereçamento IP e conectividade, TCP e sockets, ARP, DNS, firewall Linux com nftables, captura de tráfego e correlação de eventos.

**Roteiro da semana:** [Week 04 — Redes](../week-04/README.md)  
**Evidências:** [Abrir evidências da Semana 04](../evidence/week04/)

### Documentos disponíveis

- [Registro do Dia 01](./week04/Week04-day01.txt)
- [Registro do Dia 02](./week04/Week04-day02.txt)
- [Registro do Dia 03](./week04/Week04-day03.txt)
- [Registro do Dia 05](./week04/week04-day05.txt)
- [Registro do Dia 06](./week04/week04-day06.txt)
- [Registro do Dia 07](./week04/week04-day07.txt)
- [Investigação integrada da Semana 04](./week04/week04-investigacao.txt)

O arquivo [week_04_day_04.txt](./week01/week_04_day_04.txt) está atualmente na pasta `docs/week01`, mas seu nome indica conteúdo do Dia 04 da Semana 04 (DNS). Ele foi mantido no local atual para que este índice reflita a estrutura existente sem mover arquivos adicionais.

---

## 🪟 Semana 05 — Windows para Cibersegurança

**Foco:** administração e investigação defensiva em Windows, PowerShell, usuários e privilégios, processos, serviços, Event Logs, conexões de rede e firewall.

**Roteiro da semana:** [Week 05 — Windows para Cibersegurança](../week-05/README.md)  
**Evidências:** ainda não há uma pasta dedicada `evidence/week05`; consulte os registros e o README da semana.

### Documentos disponíveis

- [Dia 01 — Fundamentos de Windows](./week05/week_05_day_01.txt)
- [Dia 02 — Usuários, grupos e privilégios](./week05/week_05_day_02.txt)
- [Dia 03 — Processos, serviços e persistência](./week05/week_05_day_03.txt)
- [Dia 04 — Logs e investigação](./week05/week_05_day_04.txt)
- [Dia 05 — Rede, firewall e conexões](./week05/week_05_day_05.txt)
- [Dia 06 — Laboratório integrado de investigação](./week05/week_05_day_06.txt)
- [Dia 07 — Revisão e consolidação](./week05/week_05_day_07.txt)

---

## 🏢 Semana 06 — Active Directory

**Foco:** implantação do Windows Server 2025, promoção a controlador de domínio, usuários e grupos (IAM), estrutura de OUs, GPOs, hardening, auditoria e simulação de incidente com análise de eventos de autenticação.

**Roteiro da semana:** [Week 06 — Active Directory para Cibersegurança](../week-06/README.md)  
**Evidências:** [Windows Server 2025 e Active Directory](../evidence/windows-server-2025/)

### Documentos disponíveis

Os documentos desta semana estão atualmente em `docs/week01`, pois seus nomes não seguiam os prefixos usados na organização anterior. Os links abaixo apontam para os caminhos reais no repositório.

- [Deploy do Domain Controller — Dias 01 e 02](./week01/dia-01-02-deploy-dc.txt)
- [IAM — usuários e grupos](./week01/dia-03-iam-users-groups.txt)
- [Estrutura de OUs](./week01/dia-04-ou-structure.txt)
- [GPO e baseline de segurança](./week01/dia-05-gpo-security-baseline.txt)
- [Investigação de incidente](./week01/dia-06-incident-investigation.txt)
- [Resumo da Semana 06](./week01/dia-07-week06-summary.txt)
- [Registro complementar do Dia 04](./week01/day-04README.md)
- [Registro complementar do Dia 05](./week01/day-05-README.md)
- [Registro complementar do Dia 07](./week01/day-07-README.md)

---

## 🐍 Semana 07 — Python

**Foco:** introdução à automação e programação aplicada à cibersegurança, desenvolvendo fundamentos para scripts e tarefas de segurança defensiva.

**Roteiro da semana:** [Week 07 — Python](../week-07/README.md)  
**Documentos e evidências:** os registros diários estão em andamento; acompanhe o README da semana para a evolução das atividades.

---

## 🔗 Materiais complementares e projetos

- [README principal do Cybersecurity Roadmap](../README.md)
- [Índice geral de evidências](../evidence/README.md)
- [Projetos e laboratórios](../portfolio/README.md)
- [CyberLab Infrastructure](../portfolio/cyberlab/README.md)
- [Linux Security](../portfolio/linux-security/README.md)
- [Network Analysis](../portfolio/network-analysis/README.md)
- [Higiene de segurança de contas](../portfolio/account-security-hygiene/README.md)

---

## 🗂️ Convenção de organização

- `docs/weekXX/` — notas, relatórios e registros textuais da semana.
- `evidence/weekXX/` — capturas de tela e relatórios que demonstram a execução prática.
- `week-XX/README.md` — roteiro principal, objetivos, progresso e resumo da semana.
- `portfolio/` — projetos apresentados como entregáveis técnicos.

> **Nota de manutenção:** alguns documentos antigos estão em uma pasta diferente da semana indicada no nome ou no conteúdo. Os links deste índice preservam os caminhos atuais e identificam essas exceções explicitamente. A estrutura pode ser normalizada em uma etapa posterior, sem perder o histórico dos registros.

---

**Desenvolvido por Thiago S. Silva**