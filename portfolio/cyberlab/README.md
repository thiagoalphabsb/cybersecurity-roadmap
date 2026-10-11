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

* **DC01** | `Windows Server 2025`
  * **Função:** Domain Controller (AD DS / `corp.thiago.lab`)
  * **IP:** `10.10.10.10/24`
  * **Serviços:** Active Directory, DNS, Kerberos, GPO, PowerShell

* **CyberLab-Debian** | `Debian Linux 12`
  * **Função:** Servidor Target / Testes de Aplicação
  * **IP:** `10.10.10.10/24`
  * **Serviços:** SSH (Porta 22), Firewall (`iptables`/`ufw`), Syslog

* **CyberLab-Kali** | `Kali Linux`
  * **Função:** Estação de Auditoria & Segurança
  * **IP:** `10.10.10.20/24`
  * **Serviços:** Wireshark, Nmap, OpenSSH Client

---

## 🎯 Objetivos Práticos do Laboratório

- Simulação Híbrida (Windows & Linux): Validar a convivência, conectividade e políticas de segurança entre ambientes heterogêneos.
- Gestão de Identidades & Acesso (IAM): Implementar e gerir a estrutura de Unidades Organizacionais (OUs), Grupos de Segurança e Contas no Active Directory (corp.thiago.lab).
- Segurança Operacional & Hardening: Aplicar baselines de segurança via GPO (GPO-Workstations-Security-Baseline) e políticas de auditoria local com auditpol.
- Análise de Tráfego & Protocolos: Capturar e inspecionar pacotes de rede (SSH, TCP 3-Way Handshake, ARP, DNS, SMB) utilizando o Wireshark.

---

## 🚀 Atividades & Atributos Implementados

### 1. Infraestrutura Linux & Análise de Serviços (Semanas 1–4)

* **Enumeração de Rede:** Mapeamento de portas abertas e serviços via Nmap:
  ```bash
  nmap -sV -p 22 10.10.10.10

  Correlação Técnica: Análise da pilha de rede: `IP` → `Porta` → `Socket` → `Serviço` → `Processo`.
  
* **Análise de Pacotes:** Captura e inspeção do estabelecimento de sessão SSH e negociação de chaves via Wireshark (`tcp.port == 22`).

### 2. Infraestrutura Windows Server 2025 & Active Directory (Semanas 5-6)

- Domain Controller: Promoção da máquina DC01 e criação da floresta corp.thiago.lab.

- Estruturação de IAM: Modelagem de OUs (CorpDevices, Workstations, Empresa/Users) e criação de grupos globais (GG-SOC-Analysts, GG-IT-Support).

- Auditoria Avançada & GPO: Ativação de auditorias de evento (Logon, User Account Management, Security Group Management) e forçamento de políticas com gpupdate /force.

---

📸 Evidências Práticas
Análise de Tráfego com Wireshark	Configuração de GPO & Auditoria no AD
![Análise Wireshark SSH](./assets/week04-day02-wireshark3way.jpg) <br><sub>Captura e inspeção de pacotes SSH (`tcp.port == 22`) entre Kali e Debian</sub>	![GPO Windows Server](./assets/10-day05-GPO-WSB.png) <br><sub>Criação de GPO `GPO-Workstations-Security-Baseline` e comandos `auditpol` via PowerShell</sub>
> 📁 **Acesse a pasta de evidências completas:** [Ver diretório de evidências](../../evidence/windows-server-2025)

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
