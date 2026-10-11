# 📁 Projetos & Laboratórios Práticos — Cybersecurity Roadmap

> Repositório central de projetos defensivos, investigações técnicas, análises de infraestrutura e laboratórios práticos desenvolvidos durante a execução do **Cybersecurity Roadmap (24 Semanas)**.

---

## 🧭 Visão Geral & Organização

Cada subpasta dentro deste diretório representa um laboratório de aplicação técnica estruturado com metodologia defensiva, documentação reproduzível, procedimentos e evidências visuais.

```text
projects/
├── 🟢 Concluídos        --> CyberLab, Windows Server 2025, Account Security Hygiene
├── 🟡 Em Andamento      --> Network Assessment, Linux Troubleshooting
└── 🔴 Planejados (SOC)  --> SOC Investigation, DFIR, Web Security, Capstone
```

---

## 🛠️ Status dos Projetos

### 🟢 Concluídos (Validados & Documentados)

| Projeto / Subpasta | Domínio Técnico | Descrição & Entregas Principais | Link do Projeto |
| :--- | :--- | :--- | :---: |
| **`cyberlab`** | Infraestrutura & Redes | Laboratório virtual isolado híbrido (Linux/Windows) para testes de conectividade, captura de tráfego e análise de serviços. | [Acessar](./cyberlab) |
| **`windows-server-2025`** | AD DS, GPO & IAM | Provisionamento de Domain Controller (`DC01`), estrutura de OUs, modelo de acessos e aplicação de GPO de baseline e auditoria. | [Acessar](./windows-server-2025) |
| **`account-security-hygiene`** | IAM & Gestão de Riscos | Framework de higiene cibernética cobrindo autenticação multifator (MFA), auditoria de credenciais e matriz de risco. | [Acessar](./account-security-hygiene) |

---

### 🟡 Em Andamento (Fase de Execução & Documentação)

| Projeto / Subpasta | Domínio Técnico | Foco de Estudo & Objetivos | Link do Projeto |
| :--- | :--- | :--- | :---: |
| **`network-assessment`** | Análise de Redes & PCAP | Inspeção profunda de pacotes via Wireshark, análise de handshakes TCP/IP, protocolos (DNS/ARP/SSH) e varreduras com Nmap. | [Acessar](./network-assessment) |
| **`linux-troubleshooting`** | Admin Linux & Hardening | Investigação de falhas em ambiente Debian/Kali, análise de processos, permissões, logs do sistema e regras de firewall (`iptables`/`ufw`). | [Acessar](./linux-troubleshooting) |

---

### 🔴 Planejados / Próximas Entregas (Futuros Módulos do Roadmap)

| Projeto / Subpasta | Domínio Técnico | Escopo do Projeto & Entregas Esperadas | Link do Projeto |
| :--- | :--- | :--- | :---: |
| **`soc-investigation`** | Operações SOC & SIEM | Análise e triagem de alertas de segurança, correlação de logs de Event Viewer/Sysmon e construção de linha do tempo de incidentes. | [Acessar](./soc-investigation) |
| **`web-security`** | Segurança Web & APIs | Análise defensiva de mecanismos de autenticação, proteção contra vulnerabilidades web (OWASP Top 10) e sanitização de dados. | [Acessar](./web-security) |
| **`dfir`** | Resposta a Incidentes | Coleta e preservação de evidências digitais, análise forense inicial de memória/disco e investigação de IoCs. | [Acessar](./dfir) |
| **`capstone`** | Projeto Integrador Final | Simulação completa de ataque e defesa (*End-to-End*) consolidando todas as competências do roadmap de 24 semanas. | [Acessar](./capstone) |

---

## 📄 Padronização dos Laboratórios

Todos os projetos deste repositório seguem a estrutura padronizada de documentação:

```markdown
1. 🎯 Objetivo & Escopo do Laboratório
2. 🖥️ Ambiente & Ferramentas (VMs, IPs, Softwares)
3. 🛠️ Procedimento & Comandos Executados
4. 📸 Evidências Visuais (Screenshots com legendas técnicas)
5. 🔍 Conclusões & Aplicação em Cenário Real (SOC / Blue Team)
```

---

## 🔗 Navegação do Repositório

- 🛣️ [Voltar para a Raiz do Cybersecurity Roadmap](https://github.com/thiagoalphabsb/cybersecurity-roadmap)
- 🛡️ [Acessar o Portfólio Principal no GitHub](https://github.com/thiagoalphabsb/Cybersecurity-Portfolio)
