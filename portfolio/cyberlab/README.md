# 🧪 CyberLab — Laboratório de Cibersegurança

## 🏗️ Arquitetura do CyberLab

O ambiente é composto pelas seguintes máquinas virtuais conectadas em rede virtualizada via VirtualBox:

| VM / Hostname | Sistema Operacional | Função / Papel no Lab | IP / Subrede |
|---|---|---|---|
| **CyberLab-Kali** | Kali Linux | Pentest, análise de vulnerabilidades, auditoria | Host-Only / Internal |
| **CyberLab-Debian** | Debian Linux | Servidor de aplicação, firewall, testes de serviços | Host-Only / Internal |
| **CyberLab-Win2025** | Windows Server 2025 | Domain Controller (AD DS), DNS, GPO, testes de identidade | Host-Only / Internal |

---

## 🎯 Objetivos do Laboratório

- Simular cenários de ataques e defesas em redes híbridas (Linux + Windows).
- Praticar administração de identidades com Active Directory e integração com Linux/SSH.
- Analisar tráfego de protocolos Windows (SMB, Kerberos, LDAP, NTLM) via Wireshark.
## Ambiente

- Debian
- Kali Linux
- Windows Server 2025
- VirtualBox
- Rede interna do laboratório
- SSH
- Nmap
- Ferramentas nativas de Linux

## Atividades realizadas

### Preparação do ambiente

Configuração das máquinas virtuais, interfaces de rede e comunicação entre os hosts.

Topologia utilizada durante os laboratórios:

- Kali Linux → 10.10.10.20/24
- Debian → 10.10.10.10/24

### Enumeração

O Nmap foi utilizado para identificar portas TCP acessíveis no host Debian. Durante a evolução do laboratório, a porta **22/tcp** foi identificada como aberta e associada ao serviço SSH.

### Correlação técnica

A investigação foi além da identificação da porta, relacionando:

**IP → porta → socket → serviço → processo**

## Competências demonstradas

- Virtualização
- Linux
- TCP/IP
- IPv4
- SSH
- Nmap
- Enumeração
- Análise de serviços
- Investigação técnica
- Documentação de evidências

## Evidências

[Evidence](../../evidence/)

## Resultado

O CyberLab tornou-se a base prática para os exercícios posteriores de redes, serviços, firewall, análise de tráfego e segurança.

## Próximos passos

- Windows e Active Directory
- Vulnerability Management
- SOC
- SIEM
- Incident Response
- DFIR
- Cloud Security
