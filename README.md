# 🛡️ Cybersecurity Roadmap — 24 Semanas

> Jornada prática de transição de **Suporte N2 para Cibersegurança**, unindo fundamentos, laboratórios, investigação, documentação, evidências e projetos de portfólio.

[![GitHub](https://img.shields.io/badge/GitHub-Cybersecurity%20Roadmap-181717?logo=github)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)

---

## 🎯 Sobre o Projeto

Este repositório documenta minha jornada de desenvolvimento de competências em Cibersegurança, com foco em transformar conhecimento teórico em capacidade prática.
A proposta não é apenas consumir cursos. É seguir um ciclo contínuo:
Estudar → Executar → Investigar → Registrar evidências → Documentar → Refletir → Repetir
A experiência anterior em Suporte N2 faz parte dessa evolução: troubleshooting, análise de problemas, atendimento técnico e resolução de incidentes são utilizados como base para desenvolver uma visão cada vez mais orientada à segurança.

---

## 📍 Progresso atual

**Semana atual: 07 — Python**

| Semana | Tema | Status |
|---:|---|---|
| 01 | Fundamentos de Computação | ✅ Concluída |
| 02 | Virtualização + CyberLab | ✅ Concluída |
| 03 | Linux | ✅ Concluída |
| 04 | Redes | ✅ Concluída |
| 05 | Windows | ✅ Concluída |
| 06 | Active Directory | ✅ Concluída |
| **07** | **Python** | 🚧 Em andamento |
| 08 | Segurança de Redes | 📋 Planejada |
| 09 | Wireshark | 📋 Planejada |
| 10 | Web Security | 📋 Planejada |
| 11 | Vulnerabilidades | 📋 Planejada |
| 12 | Pentest | 📋 Planejada |
| 13 | SOC | 📋 Planejada |
| 14 | SIEM | 📋 Planejada |
| 15 | Threat Intelligence | 📋 Planejada |
| 16 | Incident Response | 📋 Planejada |
| 17 | DFIR | 📋 Planejada |
| 18 | Malware Analysis | 📋 Planejada |
| 19 | Cloud | 📋 Planejada |
| 20 | Cloud Security | 📋 Planejada |
| 21 | Automação | 📋 Planejada |
| 22 | Projetos | 📋 Planejada |
| 23 | Projeto Final | 📋 Planejada |
| 24 | Revisão + Portfólio | 📋 Planejada |

### Semanas

- [Week 01](./week-01/)
- [Week 02](./week-02/)
- [Week 03](./week-03/)
- [Week 04](./week-04/)
- [Week 05](./week-05/)
- [Week 06 — Active Directory](./week-06/)
- [Week 07 — Python](./week-07/)

---

## ⭐ Projetos em destaque

| Projeto | Foco | Documentação |
|---|---|---|
| 🖥️ Windows Server 2025 | AD DS, DNS, GPO e identidades | [Abrir projeto](./projects/windows-server-2025/README.md) |
| 🧪 CyberLab | Laboratório virtual isolado | [Abrir portfólio](./portfolio/cyberlab/README.md) |
| 🌐 Network Analysis | TCP/IP, Nmap, DNS, ARP e Wireshark | [Abrir portfólio](./portfolio/network-analysis/README.md) |
| 🐧 Linux Security | Usuários, permissões, processos, serviços e logs | [Abrir portfólio](./portfolio/linux-security/README.md) |
| 🔐 Account Security Hygiene | MFA, credenciais, sessões, IAM e redução de risco | [Abrir projeto](./projects/account-security-hygiene/README.md) |

---
## 🗺️ Roadmap

## 🧱 Fase 1 — Fundamentos

Semanas 01–04
Fundamentos de computação
Hardware e sistemas operacionais
Processos, memória e armazenamento
Virtualização
Linux e redes
Objetivo
Construir uma base sólida antes de avançar para temas específicos de segurança.
---
## 🏢 Fase 2 — Sistemas e Infraestrutura

Semanas 05–08
Windows e Active Directory
Usuários, permissões e GPO
Serviços de rede
DNS, DHCP e Firewall
Python
Segurança de redes
Objetivo
Entender como ambientes corporativos funcionam e onde estão seus principais pontos de controle e exposição.
---
## 🔎 Fase 3 — Segurança Ofensiva

Semanas 09–12
Wireshark e reconhecimento
Vulnerabilidades
Web Security
SQL Injection e XSS
Pentest e exploração controlada
Objetivo
Compreender técnicas ofensivas para desenvolver capacidade de identificação, análise e defesa.
> ⚠️ Todos os testes são realizados exclusivamente em ambientes próprios, autorizados e isolados.
---
## 🛡️ Fase 4 — Blue Team / SOC

Semanas 13–18
SOC
SIEM
Análise de logs
Monitoramento
Threat Intelligence
Incident Response
DFIR
Malware Analysis
Objetivo
Desenvolver habilidades de detecção, investigação, análise e resposta a incidentes.
---
## ☁️ Fase 5 — Cloud & Automação

Semanas 19–21
Cloud Fundamentals
Cloud Security
IAM
Segurança de workloads
Python
Automação de tarefas de segurança
Objetivo
Aplicar conceitos de segurança em ambientes modernos e automatizar tarefas repetitivas.
---
## 🚀 Fase 6 — Projetos & Portfólio

Semanas 22–24
Projetos práticos
Projeto final
Documentação
Revisão técnica
Organização do GitHub
Consolidação do portfólio profissional
Objetivo
Transformar o conhecimento acumulado durante a jornada em projetos demonstráveis.
---
## 🧪 CyberLab

Ambiente virtual utilizado nos exercícios práticos.

```text
                 CYBERLAB — INTERNAL NETWORK
                    10.10.10.0/24
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   Kali Linux          Debian 13       Windows Server 2025
  10.10.10.20/24      10.10.10.30/24      10.10.10.10/24
   Security Lab       Linux Services       AD DS / DNS / GPO
```

| Host | IP | Função |
|---|---|---|
| Kali Linux | 10.10.10.20/24 | Análise e testes controlados |
| Debian 13 | 10.10.10.30/24 | Serviços e administração Linux |
| Windows Server 2025 | 10.10.10.10/24 | Active Directory, DNS e GPO |

> Laboratório próprio e destinado exclusivamente a testes autorizados.

[Documentação do CyberLab](./portfolio/cyberlab/README.md)

---

## 🖼️ Evidências e documentação

- **[Evidências — índice de capturas](./evidence/README.md)**
- [Evidências Windows Server 2025 / Active Directory](./evidence/windows-server-2025/README.md)
- [Documentação complementar](./docs/README.md)
- [Anotações técnicas](./notes/)

---

## 🗂️ Projetos

- [Índice de projetos](./projects/README.md)
- [Windows Server 2025](./projects/windows-server-2025/README.md)
- [Account Security Hygiene](./projects/account-security-hygiene/README.md)

---

## 🛠️ Competências em desenvolvimento

### Sistemas
Linux · Debian · Kali Linux · Windows · Windows Server · Active Directory

### Redes
TCP/IP · IPv4 · ICMP · TCP/UDP · DNS · DHCP · ARP · Routing · Firewall · Nmap · Wireshark · SSH

### Segurança
Fundamentos de Cybersecurity · Hardening · IAM · MFA · Vulnerability Analysis · SOC/SIEM · Incident Response · DFIR · Threat Intelligence

### Automação e infraestrutura
Python · Shell · PowerShell · VirtualBox · Laboratórios virtualizados · Redes isoladas

---

## 🎓 Formação e certificações

- Graduação em Segurança da Informação
- Google Cybersecurity Professional Certificate
- Cisco Networking Academy — Introduction to Cybersecurity, Endpoint Security, Network Defense e Cyber Threat Management
- Cisco Academy — trilha profissionalizante Analista de Cibersegurança Júnior
- FIAP — Cyber Security
- FIAP — Cloud Fundamentals
- Solyd — Introdução ao Hacking e Pentest 2.0
- DIO.me — Segurança e boas práticas em projetos feitos com Vibe Coding
- ITIL 5 Foundation

---

## 🚀 Evolução profissional

Minha trajetória parte de **Suporte N2**, onde desenvolvi experiência em troubleshooting, análise de sistemas e redes, investigação de incidentes, atendimento técnico e documentação de soluções.

O Cybersecurity Roadmap amplia essa experiência para uma abordagem orientada à **Segurança da Informação**, com laboratórios, evidências e projetos práticos.

---

## 🔗 Links

- **GitHub:** [@thiagoalphabsb](https://github.com/thiagoalphabsb)
- **Cybersecurity Portfolio:** [cybersecurity-portfolio](https://github.com/thiagoalphabsb/cybersecurity-portfolio)
- **LinkedIn:** [Thiago Souza Silva](https://www.linkedin.com/in/thiago-souza-silva-5607223aa/)

---

> **Desenvolvido por Thiago S. Silva**  
> Cybersecurity Roadmap — Brasília, DF, Brasil
