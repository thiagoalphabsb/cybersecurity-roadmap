# 🛡️ Cybersecurity Roadmap — 24 Semanas

> Jornada prática de transição de **Suporte N2 para Cibersegurança**, unindo fundamentos, laboratórios, investigação, documentação, evidências e projetos de portfólio.

[![GitHub](https://img.shields.io/badge/GitHub-Cybersecurity%20Roadmap-181717?logo=github)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)

---

## 👋 Sobre o projeto

Este repositório documenta minha evolução prática em **Cibersegurança**, transformando conhecimento teórico em capacidade técnica reproduzível.

Minha experiência em **Suporte N2** é parte importante dessa evolução: troubleshooting, análise de sistemas e redes, atendimento técnico e investigação de incidentes formam a base do raciocínio que estou levando para Segurança da Informação.

O ciclo de estudo é:

**Estudar → Executar → Investigar → Registrar evidências → Documentar → Refletir → Repetir**

O objetivo não é apenas concluir conteúdos, mas construir evidências de que consigo **aplicar conhecimento, investigar problemas e documentar soluções**.

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

### 📚 Semanas

Cada semana possui uma página própria com objetivos, atividades, resultados, aprendizados e evidências quando aplicável.

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

## 🧪 CyberLab

O CyberLab é o ambiente virtual utilizado para os exercícios práticos.

### Topologia atual

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

> Todo o laboratório é próprio, virtualizado, isolado e destinado exclusivamente a testes autorizados.

**Documentação:** [CyberLab](./portfolio/cyberlab/README.md)

---

## 🖼️ Evidências

As evidências visuais ficam centralizadas em [evidence/](./evidence/).

A organização atual mantém os arquivos existentes e adiciona índices por contexto, evitando renomeações indiscriminadas que poderiam quebrar referências.

- [Índice de evidências](./evidence/README.md)
- [Windows Server 2025 / Active Directory](./evidence/windows-server-2025/README.md)

As capturas devem sempre estar acompanhadas de contexto: **objetivo, procedimento, resultado e conclusão**.

---

## 📄 Documentação

A documentação complementar está em [docs/](./docs/).

- [Índice de documentação](./docs/README.md)
- Relatórios de incidentes e troubleshooting
- Registros de atividades práticas
- Procedimentos e anotações técnicas

Sempre que possível, a documentação utiliza Markdown para facilitar navegação, versionamento e integração com evidências.

---

## 🗂️ Estrutura do repositório

```text
cybersecurity-roadmap/
├── README.md
├── week-01/ ... week-07/
├── portfolio/
│   ├── cyberlab/
│   ├── network-analysis/
│   ├── linux-security/
│   └── account-security-hygiene/
├── projects/
│   ├── windows-server-2025/
│   └── account-security-hygiene/
├── evidence/
│   └── windows-server-2025/
└── docs/
```

### Regra de organização

- **week-XX/** → documentação da jornada semanal.
- **portfolio/** → apresentação profissional dos projetos.
- **projects/** → documentação técnica completa dos projetos.
- **evidence/** → provas visuais e técnicas.
- **docs/** → documentação complementar, relatórios e registros.
- Arquivos novos devem usar **nomes previsíveis, sem espaços e com hífens**.

---

## 🔎 Metodologia de investigação

Durante os laboratórios, procuro seguir uma abordagem semelhante ao troubleshooting profissional:

```text
Evento
  ↓
Evidência
  ↓
Hipótese
  ↓
Validação
  ↓
Correlação
  ↓
Conclusão
  ↓
Documentação
```

Isso aproxima o estudo de situações reais de suporte, operações e segurança.

---

## 🛠️ Competências em desenvolvimento

### Sistemas
- Linux
- Debian
- Kali Linux
- Windows
- Windows Server
- Active Directory

### Redes
- TCP/IP
- IPv4
- ICMP
- TCP / UDP
- DNS
- DHCP
- ARP
- Routing
- Firewall
- Nmap
- Wireshark
- SSH

### Segurança
- Fundamentos de Cybersecurity
- Hardening
- IAM
- MFA
- Segurança de contas
- Vulnerability Analysis
- SOC / SIEM
- Incident Response
- DFIR
- Threat Intelligence

### Automação
- Python
- Shell
- PowerShell
- Scripts de automação

### Infraestrutura
- VirtualBox
- Laboratórios virtualizados
- Redes isoladas
- CyberLab

---

## 🎓 Formação e certificações

- Graduação em Segurança da Informação
- Google Cybersecurity Professional Certificate
- Cisco Networking Academy
  - Introduction to Cybersecurity
  - Endpoint Security
  - Network Defense
  - Cyber Threat Management
  - Trilha profissionalizante — Analista de Cibersegurança Júnior
- FIAP — Cyber Security
- FIAP — Cloud Fundamentals
- Solyd — Introdução ao Hacking e Pentest 2.0
- DIO.me — Segurança e boas práticas em projetos feitos com Vibe Coding
- ITIL 5 Foundation

---

## 🚀 Evolução profissional

Minha trajetória parte de **Suporte N2**, onde desenvolvi experiência prática em:

- Troubleshooting;
- análise de sistemas e redes;
- investigação de incidentes;
- atendimento técnico;
- identificação de causas;
- documentação de soluções.

O Cybersecurity Roadmap amplia essa experiência para uma abordagem orientada à **Segurança da Informação**, com laboratórios, evidências e projetos reproduzíveis.

> O objetivo não é demonstrar que já sei tudo. É demonstrar que sei **aprender, investigar, executar, resolver problemas e evoluir tecnicamente**.

---

## 🔗 Links

- **GitHub:** [@thiagoalphabsb](https://github.com/thiagoalphabsb)
- **Cybersecurity Portfolio:** [cybersecurity-portfolio](https://github.com/thiagoalphabsb/cybersecurity-portfolio)
- **LinkedIn:** [Thiago Souza Silva](https://www.linkedin.com/in/thiago-souza-silva-5607223aa/)

---

> **Desenvolvido por Thiago S. Silva**  
> Cybersecurity Roadmap — Brasília, DF, Brasil
