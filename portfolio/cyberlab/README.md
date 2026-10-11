# 🧪 CyberLab — Laboratório de Cibersegurança & Infraestrutura Defensiva

> Ambiente virtualizado e isolado de simulação para práticas de Administração de Redes, Segurança Defensiva (Blue Team), Gestão de Identidades (IAM/AD) e Análise de Tráfego.

---

## 🏗️ Arquitetura & Topologia da Rede

O **CyberLab** foi construído utilizando o **Oracle VirtualBox** em uma rede interna virtualizada e totalmente isolada (*Host-Only Switch / Internal Network*), garantindo a execução de testes sem impacto em redes externas ou de produção.

```
                        CyberLab Internal Network
                             (10.10.10.0/24)
                                    │
                         Isolated Virtual Switch
                                    │
    ┌───────────────────────────────┼───────────────────────────────┐
    │                               │                               │
  DC01                        CyberLab-Debian                CyberLab-Kali
Windows Server 2025              Debian Linux                     Kali Linux
  10.10.10.10                     10.10.10.10                     10.10.10.20
(Active Directory / DNS)     (Servidor / Aplicação)      (Tester / Auditoria / SOC)

```
---

## 🖥️ Matriz de Ativos do Laboratório

Hostname / VMSistema OperacionalFunção / Papel no LabIP / MáscaraServiços Ativos / TecnologiasDC01Windows Server 2025Domain Controller (DC)10.10.10.10/24AD DS (corp.thiago.lab), DNS, Kerberos, GPO, PowerShellCyberLab-DebianDebian Linux 12Servidor Target / Serviços10.10.10.10/24SSH (Porta 22), Firewall (iptables/ufw), SyslogCyberLab-KaliKali LinuxAuditoria & Análise10.10.10.20/24Wireshark, Nmap, OpenSSH Client, Ferramentas de Análise

---

## 🎯 Objetivos Práticos do Laboratório

- Simulação Híbrida (Windows & Linux): Validar a convivência, conectividade e políticas de segurança entre ambientes heterogêneos.
- Gestão de Identidades & Acesso (IAM): Implementar e gerir a estrutura de Unidades Organizacionais (OUs), Grupos de Segurança e Contas no Active Directory (corp.thiago.lab).
- Segurança Operacional & Hardening: Aplicar baselines de segurança via GPO (GPO-Workstations-Security-Baseline) e políticas de auditoria local com auditpol.
- Análise de Tráfego & Protocolos: Capturar e inspecionar pacotes de rede (SSH, TCP 3-Way Handshake, ARP, DNS, SMB) utilizando o Wireshark.

---

## 🚀 Atividades & Atributos Implementados

1. Infraestrutura Linux & Análise de Serviços (Semanas 1-4)
- Enumeração de Rede: Mapeamento de portas abertas e serviços via Nmap (nmap -sV -p 22 10.10.10.10).

- Correlação Técnica: Análise da pilha de rede: IP → Porta → Socket → Serviço → Processo.

- Análise de Pacotes: Captura e inspeção do estabelecimento de sessão SSH e negociação de chaves via Wireshark (tcp.port == 22).

2. Infraestrutura Windows Server 2025 & Active Directory (Semanas 5-6)
- Domain Controller: Promoção da máquina DC01 e criação da floresta corp.thiago.lab.

- Estruturação de IAM: Modelagem de OUs (CorpDevices, Workstations, Empresa/Users) e criação de grupos globais (GG-SOC-Analysts, GG-IT-Support).

- Auditoria Avançada & GPO: Ativação de auditorias de evento (Logon, User Account Management, Security Group Management) e forçamento de políticas com gpupdate /force.

---

## 📸 Evidências Práticas

Análise de Tráfego com WiresharkConfiguração de GPO & Auditoria no ADCaptura e inspeção de pacotes SSH (tcp.port == 22) entre Kali e DebianCriação de GPO GPO-Workstations-Security-Baseline e comandos auditpol via PowerShell

📁 Acesse a pasta de evidências completas: Ver diretório de evidências

---

## 🧠 Competências Práticas Demonstradas

- Virtualização & Redes: VirtualBox, Switches Isolados, Sub-roteamento IPv4, Topologia Host-Only.

- Análise de Tráfego & Protocolos: Wireshark, Filtros Display/Capture, Nmap, Inspeção de Cabeçalhos TCP/IP.

- Windows Server & AD DS: Active Directory, DNS, Kerberos, Group Policy Management (GPMC), auditpol, PowerShell.

- Segurança Defensiva (Blue Team): Hardening de SO, Auditoria de Events IDs de Segurança (4624, 4625, 4740), Least Privilege.

---

## 🔮 Próximos Passos no Laboratório

[x] Redes & Linux Hardening

[x] Windows Server 2025 & Active Directory

[ ] Automação Defensiva com Python (Semana 07 — Em Andamento)

[ ] Integração com Sysmon & Elastic SIEM / Wazuh

[ ] Análise de Regras de Firewall e Deteção de Intrusões (IDS/IPS)

---

🔗 Links Relacionados

🛣️ Cybersecurity Roadmap (24 Semanas)

🛡️ Cybersecurity Portfolio Principal

🖥️ Laboratório Específico de Active Directory
