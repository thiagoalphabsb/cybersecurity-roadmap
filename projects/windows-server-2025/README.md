# 🖥️ Windows Server 2025 — CyberLab Infrastructure

> Laboratório prático de implementação e administração do Windows Server 2025, utilizado como base para estudos de Active Directory, gestão de identidades, endpoints e segurança defensiva.

---

## 🎯 Objetivo

Implementar uma infraestrutura Windows Server 2025 virtualizada para simular um ambiente corporativo e servir como base para estudos práticos de Active Directory e Cybersecurity.

O laboratório foi construído utilizando Oracle VirtualBox em uma rede isolada para permitir experimentação e testes de segurança sem riscos.

---

## 🧪 Ambiente

| Componente | Configuração |
|---|---|
| **Hypervisor** | Oracle VirtualBox |
| **Sistema Operacional** | Windows Server 2025 |
| **Hostname** | DC01 |
| **Função** | Domain Controller (DC) |
| **Domínio** | corp.thiago.lab |
| **NetBIOS** | THIAGO |
| **Endereço IP** | 10.10.10.10/24 |
| **DNS Server** | 10.10.10.10 |
| **Nível Funcional** | Windows2025Forest |
| **Serviços Ativos** | AD DS, DNS Server, Global Catalog, Kerberos |

---

## 🌐 Topologia

```text
                    CyberLab Network
                           │
                 Isolated Virtual Switch
                           │
             ┌─────────────┴─────────────┐
             │                           │
          DC01                        Kali Linux
      Windows Server                 10.10.10.20
        10.10.10.10                      (Attacker / Tester)
             │
             ├── Active Directory DS
             ├── DNS Server
             ├── Kerberos Auth
             ├── Global Catalog
             └── Group Policy (GPO)

```

---

## 🚀 Implementação

### 1. Criação da Máquina Virtual

* Dimensionamento de CPU e RAM otimizado para o ambiente de laboratório;
* Disco rígido virtual alocado dinamicamente;
* Adaptadores de rede configurados na rede interna isolada do CyberLab;
* Isolamento total da rede de produção.

### 2. Instalação e Pós-Instalação do Windows Server 2025

* Definição do hostname padronizado (`DC01`);
* Atribuição de endereço IP estático e configuração do DNS local;
* Validação de conectividade interna via PowerShell (`Get-NetIPConfiguration`).

### 3. Promoção a Domain Controller (AD DS)

* Instalação da role **Active Directory Domain Services** via Server Manager;
* Promoção do servidor a Controller de Domínio e criação da nova floresta `corp.thiago.lab`.

---

## 🏢 Estrutura Organizacional (OUs)

```text
corp.thiago.lab
│
├── Empresa
│   ├── Users
│   │   ├── Security
│   │   ├── IT
│   │   └── Helpdesk
│   │
│   └── ...
│
├── CorpDevices
│   ├── Workstations
│   └── Servers
│
├── Groups
└── Admins

```

---

## 👥 Identidade e Acesso (IAM)

Criação de contas e grupos padronizados aplicando o modelo **Identity → Group → Role → Access**:

| Usuário | Função | Grupo de Segurança |
| --- | --- | --- |
| Ana Silva | Security Analyst | `GG-SOC-Analysts` |
| Carlos Souza | IT Support | `GG-IT-Support` |
| João Santos | Helpdesk | `GG-Helpdesk` |

---

## 🔐 Group Policy (GPO) & Baseline de Segurança

Implementação de políticas centralizadas de segurança em `GPO-Workstations-Security-Baseline`:

* Regras de complexidade e tamanho mínimo de senha;
* Política de expiração e reuso de credenciais;
* Bloqueio automático de conta (*Account Lockout Threshold*) após tentativas inválidas.

---

## 🛡️ Segurança, Auditoria e Investigação de Eventos

Análise e monitoramento dos logs de auditoria do Windows Event Viewer relacionados à autenticação e credenciais:

| Event ID | Descrição Técnica |
| --- | --- |
| **4624** | Logon realizado com sucesso |
| **4625** | Falha de autenticação (potencial brute force / password spraying) |
| **4648** | Logon utilizando credenciais explícitas (`runas`) |
| **4672** | Privilégios especiais atribuídos a novo logon |
| **4720** | Novo usuário criado |
| **4725** | Conta de usuário desabilitada |
| **4728** | Usuário adicionado a grupo de segurança |
| **4740** | Conta de usuário bloqueada |

### Exemplo de Consulta de Auditoria via PowerShell:

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    Id      = 4625
} -MaxEvents 10

```

---

## 🔎 Validação e Diagnóstico do Ambiente

Comandos executados para validação dos serviços essenciais do Active Directory:

```powershell
Get-ADDomain
Get-ADForest
Get-ADDomainController
Get-Service NTDS, DNS, Netlogon, KDC
dcdiag

```

---

## 🧠 Competências Desenvolvidas

* **Windows Server 2025 & AD DS:** Instalação, promoção de DC, topologia de floresta e domínio;
* **Gestão de Identidades (IAM):** Estruturação de OUs, grupos de segurança e Least Privilege;
* **Segurança Operacional:** Definição de baselines de GPO e auditoria de logs de segurança;
* **PowerShell:** Diagnóstico de AD DS e filtragem de eventos de segurança.

---

## 📸 Evidências Técnicas e Documentação

- 📸 **Evidências Visuais:** [Acessar evidências no GitHub (evidence/windows-server-2025)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/windows-server-2025)
- 📚 **Documentação Completa da Semana:** [Acessar documentação da Week 06 (week-06)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/week-06)
---

### Status do Projeto

**Status:** ✅ Concluído

**Ambiente:** CyberLab (Infraestrutura Híbrida)

```
