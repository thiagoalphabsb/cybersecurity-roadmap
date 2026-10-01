# 🛡️ Cybersecurity Roadmap — 24 Semanas

> **Jornada prática de transição de Suporte N2 para Cibersegurança**, unindo fundamentos, laboratório, investigação, documentação, evidências e projetos práticos.

[![GitHub](https://img.shields.io/badge/GitHub-Cybersecurity%20Roadmap-181717?logo=github)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)

---

## 🎯 Sobre o Projeto

Este repositório documenta minha jornada de desenvolvimento de competências em **Cibersegurança**, com foco em transformar conhecimento teórico em capacidade prática.

A proposta não é apenas consumir cursos. É seguir um ciclo contínuo:

**Estudar → Executar → Investigar → Registrar evidências → Documentar → Refletir → Repetir**

A experiência anterior em **Suporte N2** faz parte dessa evolução: troubleshooting, análise de problemas, atendimento técnico e resolução de incidentes são utilizados como base para desenvolver uma visão cada vez mais orientada à segurança.

---

## 🔐 Cybersecurity Portfolio

Além do roadmap de estudos, este repositório possui um **portfólio profissional com projetos práticos selecionados**, organizados para demonstrar competências técnicas desenvolvidas durante a jornada.

### 👉 [Acessar o Cybersecurity Portfolio](./portfolio/README.md)

### Projetos em destaque

| Projeto | Competências demonstradas | Status |
|---|---|---|
| 🖥️ [CyberLab](./portfolio/cyberlab/README.md) | Linux, VirtualBox, SSH, Nmap, redes e investigação | 🟢 Concluído |
| 🌐 [Network Analysis](./portfolio/network-analysis/README.md) | TCP/IP, Wireshark, Nmap, DNS, ARP e firewall | 🟢 Concluído |
| 🐧 [Linux Security Fundamentals](./portfolio/linux-security/README.md) | Usuários, permissões, processos, serviços e logs | 🟢 Concluído |
| 🔐 [Account Security Hygiene](./portfolio/account-security-hygiene/README.md) | MFA, credenciais, sessões, least privilege e IAM | 🟢 Concluído |

O portfólio será ampliado conforme novos projetos forem desenvolvidos ao longo das próximas semanas.

---

## 📊 Progresso Atual

**Semana atual: 05 — Windows**

| Semana | Tema | Status |
|---|---|---|
| **01** | Fundamentos de Computação | 🟢 Concluída |
| **02** | Virtualização + CyberLab | 🟢 Concluída |
| **03** | Linux | 🟢 Concluída |
| **04** | Redes | 🟢 Concluída |
| **05** | Windows | 🔵 Em andamento |
| 06 | Active Directory | ⚪ Planejada |
| 07 | Python | ⚪ Planejada |
| 08 | Segurança de Redes | ⚪ Planejada |
| 09 | Wireshark | ⚪ Planejada |
| 10 | Web Security | ⚪ Planejada |
| 11 | Vulnerabilidades | ⚪ Planejada |
| 12 | Pentest | ⚪ Planejada |
| 13 | SOC | ⚪ Planejada |
| 14 | SIEM | ⚪ Planejada |
| 15 | Threat Intelligence | ⚪ Planejada |
| 16 | Incident Response | ⚪ Planejada |
| 17 | DFIR | ⚪ Planejada |
| 18 | Malware Analysis | ⚪ Planejada |
| 19 | Cloud | ⚪ Planejada |
| 20 | Cloud Security | ⚪ Planejada |
| 21 | Automação | ⚪ Planejada |
| 22 | Projetos | ⚪ Planejada |
| 23 | Projeto Final | ⚪ Planejada |
| 24 | Revisão + Portfólio | ⚪ Planejada |

> **Legenda:** 🟢 Concluído · 🔵 Em andamento · ⚪ Planejado

---

# 🗺️ Roadmap

## 🧱 Fase 1 — Fundamentos

**Semanas 01–04**

- Fundamentos de computação
- Hardware e sistemas operacionais
- Processos, memória e armazenamento
- Virtualização
- Linux e redes

### Objetivo

Construir uma base sólida antes de avançar para temas específicos de segurança.

---

## 🏢 Fase 2 — Sistemas e Infraestrutura

**Semanas 05–08**

- Windows e Active Directory
- Usuários, permissões e GPO
- Serviços de rede
- DNS, DHCP e Firewall
- Python
- Segurança de redes

### Objetivo

Entender como ambientes corporativos funcionam e onde estão seus principais pontos de controle e exposição.

---

## 🔎 Fase 3 — Segurança Ofensiva

**Semanas 09–12**

- Wireshark e reconhecimento
- Vulnerabilidades
- Web Security
- SQL Injection e XSS
- Pentest e exploração controlada

### Objetivo

Compreender técnicas ofensivas para desenvolver capacidade de identificação, análise e defesa.

> ⚠️ Todos os testes são realizados exclusivamente em ambientes próprios, autorizados e isolados.

---

## 🛡️ Fase 4 — Blue Team / SOC

**Semanas 13–18**

- SOC
- SIEM
- Análise de logs
- Monitoramento
- Threat Intelligence
- Incident Response
- DFIR
- Malware Analysis

### Objetivo

Desenvolver habilidades de detecção, investigação, análise e resposta a incidentes.

---

## ☁️ Fase 5 — Cloud & Automação

**Semanas 19–21**

- Cloud Fundamentals
- Cloud Security
- IAM
- Segurança de workloads
- Python
- Automação de tarefas de segurança

### Objetivo

Aplicar conceitos de segurança em ambientes modernos e automatizar tarefas repetitivas.

---

## 🚀 Fase 6 — Projetos & Portfólio

**Semanas 22–24**

- Projetos práticos
- Projeto final
- Documentação
- Revisão técnica
- Organização do GitHub
- Consolidação do portfólio profissional

### Objetivo

Transformar o conhecimento acumulado durante a jornada em projetos demonstráveis.

---

# 🧪 CyberLab

O **CyberLab** é o ambiente virtual utilizado para realizar os experimentos práticos da jornada.

### Ambiente

- **Debian 13** — servidor/host de testes
- **Kali Linux** — estação de análise e testes
- **VirtualBox** — virtualização
- **Rede interna isolada**
- **SSH**
- **Nmap**
- **Wireshark**
- Ferramentas nativas de Linux e redes

### Topologia atual

```text
┌───────────────────────────────┐
│        CYBERLAB - INTERNAL    │
│                               │
│  Kali Linux                   │
│  10.10.10.20/24               │
│       │                       │
│       │  Rede isolada         │
│       │                       │
│  Debian 13                    │
│  10.10.10.10/24               │
│                               │
└───────────────────────────────┘
```

O laboratório permite praticar enumeração, análise de serviços, redes, Linux, segurança e investigação sem afetar ambientes externos.

👉 [Documentação completa do CyberLab](./portfolio/cyberlab/README.md)

---

# 📁 Evidências

As atividades práticas são acompanhadas por evidências técnicas sempre que aplicável.

👉 [Abrir pasta de evidências](./evidence/)

As evidências são utilizadas como parte do processo de validação do aprendizado, acompanhadas de contexto e documentação.

---

# 🔬 Metodologia de Investigação

Ao longo do projeto, procuro evoluir de uma abordagem baseada apenas em comandos para uma abordagem baseada em **hipóteses e evidências**.

Um modelo recorrente é:

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
```

Exemplo:

```text
IP
 ↓
Porta
 ↓
Socket
 ↓
Processo
 ↓
Serviço
 ↓
Firewall
 ↓
Tráfego
```

Essa forma de raciocínio aproxima os exercícios de situações reais de troubleshooting, análise e investigação de segurança.

---

# 🧰 Ferramentas e Tecnologias

### Sistemas

- Linux
- Debian
- Kali Linux
- Windows
- Windows Server

### Redes

- TCP/IP
- IPv4
- ICMP
- TCP / UDP
- DNS
- DHCP
- ARP
- MAC
- Routing
- Firewall

### Segurança

- Nmap
- Wireshark
- SSH
- nftables
- SIEM
- Threat Intelligence
- Incident Response
- DFIR

### Desenvolvimento e Automação

- Python
- Shell
- Scripts de automação

### Infraestrutura

- VirtualBox
- Ambientes virtuais
- Redes isoladas
- CyberLab

---

# 📚 Formação, Certificações & Cursos

## 🎓 Formação

**Graduação:** Segurança da Informação

## 🛡️ Cisco Networking Academy

- Introduction to Cybersecurity
- Endpoint Security
- Network Defense
- Cyber Threat Management
- Trilha profissionalizante — Analista de Cibersegurança Júnior

## 🎓 FIAP

- Cyber Security
- Cloud Fundamentals
- Python Development
- Linux Fundamentos

## 🔴 Solyd

- Introdução ao Hacking e Pentest 2.0

## 🔵 DIO.me

- Segurança e boas práticas em projetos feitos com Vibe Coding

## 📋 Outros

- ITIL 5 Foundation

---

# 💼 Evolução Profissional

Minha trajetória parte da experiência em **Suporte N2**, onde troubleshooting, análise de problemas, sistemas operacionais, redes e atendimento técnico fazem parte da rotina.

A jornada em Cibersegurança busca transformar essa experiência em uma nova perspectiva:

```text
Suporte N2
    ↓
Troubleshooting
    ↓
Análise de sistemas e redes
    ↓
Fundamentos de Segurança
    ↓
Laboratórios práticos
    ↓
Investigação baseada em evidências
    ↓
Projetos de Cibersegurança
    ↓
SOC / Blue Team / Segurança da Informação
```

O objetivo é demonstrar não apenas o que foi estudado, mas **como o conhecimento é aplicado para investigar, solucionar problemas e construir soluções de segurança**.

---

# 🗂️ Estrutura do Repositório

```text
cybersecurity-roadmap/
│
├── README.md
│
├── portfolio/
│   ├── README.md
│   ├── cyberlab/
│   ├── network-analysis/
│   ├── linux-security/
│   └── account-security-hygiene/
│
├── week-01/
├── week-02/
├── week-03/
├── week-04/
├── week-05/
├── ...
├── week-24/
│
├── projects/
├── evidence/
├── resources/
├── notes/
└── docs/
```

### Organização

- **README.md** → visão geral do projeto
- **portfolio/** → projetos selecionados para apresentação profissional
- **week-XX/** → documentação detalhada de cada semana
- **projects/** → projetos práticos
- **evidence/** → evidências dos laboratórios
- **resources/** → materiais de referência
- **notes/** → anotações técnicas
- **docs/** → documentação complementar

---

# 🧠 Competências em Desenvolvimento

Ao longo da jornada, o objetivo é consolidar competências em:

- 🐧 Linux
- 🪟 Windows
- 🌐 Redes e TCP/IP
- 🔍 Análise de tráfego
- 🛡️ Fundamentos de Cybersecurity
- 🔎 Vulnerability Analysis
- 🧪 Pentest em laboratório
- 🛡️ Blue Team
- 🖥️ SOC
- 📊 SIEM
- 🚨 Incident Response
- 🔬 DFIR
- ☁️ Cloud Security
- 🐍 Python
- ⚙️ Automação
- 📝 Documentação técnica
- 🔎 Investigação baseada em evidências

---

# 📈 Evolução

Este repositório será atualizado continuamente durante a jornada, registrando:

- problemas encontrados;
- hipóteses levantadas;
- comandos utilizados;
- configurações;
- resultados;
- evidências;
- aprendizados;
- decisões técnicas;
- projetos desenvolvidos.

> **O objetivo não é demonstrar que sei tudo. É demonstrar que sei aprender, investigar, resolver problemas e evoluir tecnicamente.**

---

# 🔗 Contato & Links

**GitHub:** [@thiagoalphabsb](https://github.com/thiagoalphabsb)

**Cybersecurity Roadmap:** [github.com/thiagoalphabsb/cybersecurity-roadmap](https://github.com/thiagoalphabsb/cybersecurity-roadmap)

**Cybersecurity Portfolio:** [./portfolio/README.md](./portfolio/README.md)

**LinkedIn:** [linkedin.com/in/thiago-souza-silva-5607223aa](https://www.linkedin.com/in/thiago-souza-silva-5607223aa/)

---

> **“O objetivo não é apenas aprender Cibersegurança. É construir evidências de que consigo aplicar o conhecimento.”**

**Desenvolvido por Thiago S. Silva**
