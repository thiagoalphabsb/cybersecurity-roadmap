# 🛡️ Week 06 — Active Directory para Cibersegurança

> **Cybersecurity Roadmap — Fase 2: Sistemas e Infraestrutura**

A Week 06 consolida o avanço do roadmap no ecossistema corporativo **Windows Server**, abordando a implementação do **Active Directory Domain Services (AD DS)**, gestão de identidades e acessos (IAM), arquitetura de Unidades Organizacionais (OUs), Group Policy Objects (GPO), hardening de baselines de segurança e resposta a incidentes defensivos via logs do PowerShell.

## 🎯 Objetivos

* Implementar e promover um Controlador de Domínio (DC) Windows Server 2025 (`corp.thiago.lab`).
* Entender a arquitetura de Florestas, Domínios e papéis FSMO.
* Gerenciar usuários, grupos globais de segurança e aplicar o Princípio do Menor Privilégio (*Least Privilege*).
* Estruturar a árvore corporativa de Unidades Organizacionais (OUs) e migração de objetos.
* Configurar diretivas de senhas e bloqueio de conta (*Default Domain Password Policy*).
* Criar e vincular Group Policy Objects (GPO) para aplicação de Security Baselines.
* Habilitar e configurar políticas locais de auditoria avançada (*auditpol*).
* Simular incidentes de autenticação e realizar parsing do Event ID 4625 via PowerShell.
* Emitir relatórios de incidentes e consolidar evidências de segurança do CyberLab.

## 📚 Progresso

| Dia | Tema | Status |
| :-: | :--- | :-: |
| Day 01 | Deploy e Pré-requisitos do Domain Controller | 🟢 Concluído |
| Day 02 | Promoção a DC e Validação da Floresta | 🟢 Concluído |
| Day 03 | Gestão de Identidades, Grupos e Privilégios (IAM) | 🟢 Concluído |
| Day 04 | Estruturação Corporativa de OUs e Migração de Objetos | 🟢 Concluído |
| Day 05 | Group Policy Objects (GPO), Hardening & Auditoria | 🟢 Concluído |
| Day 06 | Simulação de Incidente & Análise do Event ID 4625 via PowerShell | 🟢 Concluído |
| Day 07 | Resposta a Incidentes, Relatório SOC & Encerramento | 🟢 Concluído |

**Status da Week 06: 🟢 FINALIZADA**

---

# 🗓️ Day 01 & 02 — Deploy e Promoção do Domain Controller

Foram estudados:

* instalação da função AD DS e servidor DNS no Windows Server 2025 (`DC01`);
* promoção a controlador de domínio raiz do novo domínio `corp.thiago.lab`;
* validação de catálogo global (GC), partições de diretório e papéis FSMO.

### PowerShell praticado

```powershell
hostname
whoami

Get-ADForest
Get-ADDomain
Get-ADDomainController -Filter *

```

📄 Documentação técnica: [`docs/day-01-02-deploy-dc.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-06/day-02/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 👤 Day 03 — Usuários, Grupos e Privilégios (IAM)

Foram estudados:

* gestão de contas corporativas (`ana.silva`, `carlos.souza`, `joao.santos`);
* criação de grupos globais de segurança (`GG-SOC-Analysts`, `GG-IT-Support`, `GG-Helpdesk`);
* aplicação rigorosa do **Princípio do Menor Privilégio (*Least Privilege*)**;
* limitação de permissões ao grupo `Domain Admins`.

```powershell
Get-ADUser -Filter * | Select-Object Name, SamAccountName, Enabled
Get-ADGroup -Filter * | Select-Object Name, GroupScope, GroupCategory
Get-ADGroupMember "Domain Admins"
Get-ADPrincipalGroupMembership ana.silva | Select-Object Name

```

📄 Documentação técnica: [`docs/day-03-iam-users-groups.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-06/day-03/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🏢 Day 04 — Estrutura de OUs Corporativas

Foram estudados:

* diferença fundamental entre Unidade Organizacional (OU) e Grupos de Segurança;
* criação de uma árvore hierárquica corporativa limpa;
* prevenção de conflitos de nomenclatura com containers nativos (`CN=Users`, `CN=Computers`);
* migração de objetos com `Move-ADObject`.

### Arquitetura de OUs Implementada

```text
                    CORP.THIAGO.LAB
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
     CorpUsers        CorpDevices         Groups
         │                 │                 │
   ┌─────┼─────┐     ┌─────┴─────┐      ┌────┼────┐
Security IT Helpdesk Workstations Servers  SOC   IT  Helpdesk
   │     │     │                         (GG-Groups)
  Ana  Carlos João

```

```powershell
Get-ADOrganizationalUnit -Filter *
Move-ADObject -Identity "CN=Ana Silva,OU=Lab Users,DC=corp,DC=thiago,DC=lab" -TargetPath "OU=Security,OU=CorpUsers,DC=corp,DC=thiago,DC=lab"
Get-ADUser -Filter * | Select-Object Name, DistinguishedName

```

📄 Documentação técnica: [`docs/day-04-ou-structure.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-06/day-04/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🟣 Day 05 — Group Policy Objects (GPO), Hardening & Auditoria

Foram estudados:

* configuração da **Default Domain Password Policy** no nível de domínio;
* requisitos de complexidade, tamanho mínimo de 12 caracteres e histórico de senhas;
* política de bloqueio de contas por tentativas incorretas (*Account Lockout Policy*);
* criação e vinculação de GPO customizada (`GPO-Workstations-Security-Baseline`);
* habilitação de auditoria de eventos com `auditpol`.

```powershell
# Configuração da Política de Senhas e Lockout
Set-ADDefaultDomainPasswordPolicy `
  -Identity "corp.thiago.lab" `
  -MinPasswordLength 12 `
  -ComplexityEnabled $true `
  -MaxPasswordAge (New-TimeSpan -Days 90) `
  -MinPasswordAge (New-TimeSpan -Days 1) `
  -PasswordHistoryCount 5 `
  -LockoutThreshold 5 `
  -LockoutDuration (New-TimeSpan -Minutes 15) `
  -LockoutObservationWindow (New-TimeSpan -Minutes 15)

# GPO & Auditoria
New-GPO -Name "GPO-Workstations-Security-Baseline" -Comment "Baseline de Seguranca e Auditoria"
New-GPLink -Name "GPO-Workstations-Security-Baseline" -Target "OU=Workstations,OU=CorpDevices,DC=corp,DC=thiago,DC=lab"

auditpol /set /subcategory:"Logon" /success:enable /failure:enable
auditpol /set /subcategory:"User Account Management" /success:enable /failure:enable
auditpol /set /subcategory:"Security Group Management" /success:enable /failure:enable

gpupdate /force

```

📄 Documentação técnica: [`docs/day-05-gpo-security-baseline.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-06/day-05/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🔴 Day 06 — Simulação de Incidente & Análise do Event ID 4625

O Day 06 integrou os conceitos de auditoria em um cenário de simulação de ataque e investigação de logs pelo PowerShell.

### Simulação do Incidente (Failed Logon)

```powershell
$SecString = ConvertTo-SecureString "SenhaIncorreta123!" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential("corp\ana.silva", $SecString)
Start-Process powershell -Credential $cred -ErrorAction SilentlyContinue

```

### Análise de Log via PowerShell (Event ID 4625)

```powershell
$Event = Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 1
$XmlEvent = [xml]$Event.ToXml()

[PSCustomObject]@{
    DataHora        = $Event.TimeCreated
    UsuarioTentado  = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'TargetUserName'}).'#text'
    Dominio         = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'TargetDomainName'}).'#text'
    TipoLogon       = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'LogonType'}).'#text'
    IPOrigem        = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'IpAddress'}).'#text'
    NomeEstacao     = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'WorkstationName'}).'#text'
    CodigoStatus    = ($XmlEvent.Event.EventData.Data | Where-Object {$_.Name -eq 'Status'}).'#text'
}

```

📄 Documentação técnica: [`docs/day-06-incident-investigation.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

🖼️ Evidências do dia: [`evidence/week-06/day-06/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

# 🔎 Day 07 — Resposta a Incidentes & Consolidação SOC

O último dia consolidou as evidências, elaborou o relatório de segurança **INC-2026-001** e formalizou o encerramento da semana.

### 🧪 Relatório de Incidente SOC #001

```text
===============================================================================
RELATÓRIO DE INCIDENTE DE SEGURANÇA - INCIDENTE #001
===============================================================================
ID do Incidente:   INC-2026-001
Usuário Alvo:      ana.silva
Evento Auditado:   Event ID 4625 (An account failed to log on)
Severidade:        Média / Alerta de Autenticação

1. DETALHES DA INVESTIGAÇÃO:
   - Data/Hora:       08/10/2026 - 11:40:58 AM
   - Origem (IP/Host): ::1 / DC01
   - Tipo de Logon:   2 (Interactive / Local Console)
   - Código Status:   0xc000006d (Bad Credential)

2. AVALIAÇÃO DE RISCO:
   - Falha de autenticação provocada por digitação de senha incorreta.
   - Proteção de Account Lockout ativa garantindo o bloqueio da conta após 5 tentativas.

3. RECOMENDAÇÕES:
   - Notificar a usuária Ana Silva sobre o alerta gerado.
   - Verificar serviços/scripts locais utilizando credenciais antigas ou incorretas.
===============================================================================

```

📄 Documentação técnica: [`docs/day-07-week06-summary.txt`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

---

# 📸 Repositório de Evidências (`.png`)

Todas as capturas de tela dos testes, saídas do terminal e validações estão catalogadas no diretório oficial de evidências:

🔗 **[Acessar pasta de evidências no GitHub](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)**

---

# 🧠 Principais Aprendizados

* Instalação e promoção do Active Directory Domain Services (AD DS).
* Administração centralizada de identidades e grupos globais (IAM).
* Aplicação do Princípio do Menor Privilégio (*Least Privilege*).
* Design e organização de Unidades Organizacionais (OUs).
* Hardening do domínio via Default Domain Password Policy.
* Implementação e gerenciamento de Group Policy Objects (GPO).
* Configuração avançada de auditoria de eventos (*auditpol*).
* Simulação de falhas de autenticação e investigação do Event ID 4625.
* Coleta, parsing e análise de Event Logs diretamente via PowerShell.
* Emissão de relatórios e documentação de incidentes para SOC/Blue Team.

---

# 🔗 Relação com as Weeks Anteriores

### Week 04 — Redes

```text
IP / Subnet
 ↓
DNS Server
 ↓
Tráfego de Rede
 ↓
Firewall Rules

```

### Week 05 — Windows

```text
Usuário Local
 ↓
Processos / PID
 ↓
Serviços
 ↓
Windows Event Logs (4624 / 4625)

```

### Week 06 — Active Directory

```text
Controlador de Domínio (DC01)
 ↓
Identidades e Grupos de Segurança (IAM)
 ↓
Unidades Organizacionais (OUs)
 ↓
Group Policy Objects (GPO)
 ↓
Auditoria Centralizada & SOC

```

---

# 🛡️ Perspectiva Blue Team

A Week 06 reforçou que o Active Directory é a espinha dorsal da identidade corporativa e o alvo primário em ataques a redes corporativas.

> **Sem visibilidade de logs e baselines de segurança consolidados, a infraestrutura fica exposta a ataques como Password Spraying, Brute Force e movimentação lateral.**

A correlação entre OUs, políticas de senhas restritivas, auditorias de logon ativas e o monitoramento proativo via PowerShell permite identificar e conter anomalias antes que elas se tornem um comprometimento total do ambiente.

---

# 🏁 Status

**Week 06 — Active Directory: 🟢 CONCLUÍDA**

**Fase 2 — Sistemas e Infraestrutura: em andamento**

**Documentos:** [`docs/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/docs)

**Evidências:** [`evidence/`](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence)

---

## 👨‍💻 Projeto

**Cybersecurity Roadmap**

**Desenvolvido por Thiago S. Silva**

🔗 [GitHub — Cybersecurity Roadmap](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap)

```

```
