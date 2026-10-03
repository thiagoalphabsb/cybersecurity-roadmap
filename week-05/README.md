# 🪟 Week 05 — Windows para Cibersegurança

> \*\*Cybersecurity Roadmap — Fase 2: Sistemas e Infraestrutura\*\*

A Week 05 marca a entrada do roadmap no ambiente **Windows**, consolidando conhecimentos de administração, análise e investigação de endpoints antes da evolução para **Active Directory**, na Week 06.

## 🎯 Objetivos

* Conhecer o Windows sob uma perspectiva de segurança.
* Utilizar PowerShell para coleta e investigação.
* Identificar usuários, grupos e privilégios.
* Investigar processos e serviços.
* Correlacionar serviços com processos e PIDs.
* Analisar conexões de rede.
* Relacionar conexões a processos.
* Conhecer o Windows Defender Firewall.
* Investigar Windows Event Logs.
* Analisar eventos de autenticação `4624` e `4625`.
* Integrar evidências em uma investigação de endpoint.

## 📚 Progresso

|Dia|Tema|Status|
|-|-|-|
|Day 01|Fundamentos de Windows para Cybersecurity|🟢 Concluído|
|Day 02|Usuários, grupos e privilégios|🟢 Concluído|
|Day 03|Processos, serviços e persistência|🟢 Concluído|
|Day 04|Windows Event Logs e investigação|🟢 Concluído|
|Day 05|Rede, firewall e investigação de conexões|🟢 Concluído|
|Day 06|Laboratório integrado de investigação Windows|🟢 Concluído|
|Day 07|Security Review + consolidação|🟢 Concluído|

**Status da Week 05: 🟢 FINALIZADA**

\---

# 🗓️ Day 01 — Fundamentos de Windows para Cybersecurity

Foram estudados:

* identificação do sistema operacional;
* hardware e recursos;
* processos;
* serviços;
* configuração de rede;
* conexões TCP;
* Windows Defender;
* Windows Event Logs;
* coleta inicial de informações para investigação.

### PowerShell praticado

```powershell
Get-ComputerInfo
hostname
whoami

Get-CimInstance Win32\_ComputerSystem
Get-CimInstance Win32\_Processor

Get-Process
Get-Service

ipconfig /all
Get-NetIPConfiguration
Get-NetRoute
Get-NetTCPConnection

Get-MpComputerStatus

Get-WinEvent -LogName System -MaxEvents 10
Get-WinEvent -LogName Application -MaxEvents 10
Get-WinEvent -LogName Security -MaxEvents 10
```

**Aprendizado:** o Windows passou a ser tratado como um endpoint de investigação, e não somente como sistema operacional de uso diário.

\---

# 👤 Day 02 — Usuários, grupos e privilégios

Foram estudados:

* identidade do usuário;
* SID;
* grupos locais;
* grupo de administradores;
* privilégios do token;
* UAC;
* princípio do menor privilégio.

```powershell
whoami
whoami /user
whoami /groups
whoami /priv

Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember -Group "Administrators"
```

### Comparação com Linux

|Linux|Windows|
|-|-|
|Usuário|Usuário local|
|Grupo|Grupo local|
|`sudo`|UAC / elevação|
|`/etc/passwd`|Contas locais|
|`/etc/group`|Grupos locais|
|Privilégios|Token / privilégios|

**Aprendizado:** investigar um endpoint exige saber não apenas qual usuário está conectado, mas também quais grupos e privilégios estão disponíveis.

\---

# ⚙️ Day 03 — Processos, serviços e persistência

Foram estudados:

* processos;
* PID;
* caminho do executável;
* command line;
* serviços Windows;
* estado do serviço;
* Start Mode;
* relação serviço → processo;
* Scheduled Tasks.

```powershell
Get-Process

Get-Process |
Sort-Object CPU -Descending

Get-Process |
Sort-Object WorkingSet64 -Descending

Get-Process -Name explorer |
Select-Object Name,Id,Path,StartTime
```

### Serviços

```powershell
Get-Service

Get-CimInstance Win32\_Service |
Select-Object Name,DisplayName,State,StartMode,ProcessId,PathName
```

### Persistência

```powershell
Get-ScheduledTask
Get-ScheduledTaskInfo
```

### Cadeia investigativa

```text
SERVIÇO
   ↓
PID
   ↓
PROCESSO
   ↓
EXECUTÁVEL
```

\---

# 📋 Day 04 — Windows Event Logs e Investigação

Foram estudados:

* Windows Event Logs;
* logs System, Application e Security;
* Event ID;
* eventos de autenticação;
* logon bem-sucedido;
* falha de autenticação;
* construção de linha do tempo.

### Principais logs

```text
System
Application
Security
```

```powershell
Get-WinEvent -ListLog \*
Get-WinEvent -LogName System -MaxEvents 20
Get-WinEvent -LogName Application -MaxEvents 20
Get-WinEvent -LogName Security -MaxEvents 20
```

### Event ID 4624

Representa um **logon bem-sucedido**.

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624
} -MaxEvents 10
```

### Event ID 4625

Representa uma **tentativa de logon malsucedida**.

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4625
} -MaxEvents 10
```

Foram analisados elementos como horário, usuário, domínio, tipo de logon, origem e motivo da falha.

**Aprendizado:** sair de “existe um evento?” para “o que aconteceu, quando aconteceu, com qual usuário e de onde veio?”.

\---

# 🌐 Day 05 — Rede, Firewall e Investigação de Conexões

Foram estudados:

* interfaces de rede;
* IPv4;
* gateway;
* DNS;
* rotas;
* conexões TCP;
* PID associado à conexão;
* processo associado à conexão;
* Windows Defender Firewall;
* regras de entrada e saída.

```powershell
ipconfig /all
Get-NetIPConfiguration
Get-NetAdapter
Get-NetRoute -AddressFamily IPv4
```

### Conexões

```powershell
Get-NetTCPConnection

Get-NetTCPConnection -State Established

Get-NetTCPConnection -State Established |
Select-Object LocalAddress,LocalPort,RemoteAddress,RemotePort,State,OwningProcess
```

### Correlação

```text
IP LOCAL
   ↓
PORTA
   ↓
IP REMOTO
   ↓
PORTA REMOTA
   ↓
PID
   ↓
PROCESSO
   ↓
EXECUTÁVEL
```

### Firewall

```powershell
Get-NetFirewallProfile

Get-NetFirewallRule |
Select-Object DisplayName,Enabled,Direction,Action
```

**Aprendizado:** uma conexão passou a ser investigada pela relação entre IP, porta, PID, processo, executável e usuário.

\---

# 🕵️ Day 06 — Laboratório Integrado de Investigação Windows

O Day 06 integrou os conhecimentos anteriores em um cenário de investigação de uma conexão de rede suspeita.

### Cadeia investigativa

```text
CONEXÃO
 ↓
PORTA
 ↓
PROCESSO
 ↓
EXECUTÁVEL
 ↓
USUÁRIO
 ↓
PRIVILÉGIOS
 ↓
SERVIÇO
 ↓
FIREWALL
 ↓
EVENTOS
```

### Identificação do processo

```powershell
Get-Process -Id PID |
Select-Object Name,Id,Path,StartTime
```

### Investigação detalhada

```powershell
Get-CimInstance Win32\_Process -Filter "ProcessId = PID" |
Select-Object ProcessId,Name,ExecutablePath,CommandLine
```

### Proprietário do processo

```powershell
Get-CimInstance Win32\_Process -Filter "ProcessId = PID" |
Invoke-CimMethod -MethodName GetOwner
```

### Serviço relacionado

```powershell
Get-CimInstance Win32\_Service |
Where-Object ProcessId -eq PID |
Select-Object Name,DisplayName,State,StartMode,ProcessId,PathName
```

### Privilégios

```powershell
whoami /groups
whoami /priv
```

### Eventos

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624,4625
} -MaxEvents 20
```

\---

# 🔎 Day 07 — Security Review + Consolidação

O último dia consolidou os conhecimentos da Week 05.

A revisão envolveu:

```text
HOST
 ↓
USUÁRIO
 ↓
GRUPOS / PRIVILÉGIOS
 ↓
PROCESSO
 ↓
SERVIÇO
 ↓
CONEXÃO
 ↓
FIREWALL
 ↓
EVENT LOG
 ↓
INVESTIGAÇÃO
```

Foram revisados:

```powershell
Get-ComputerInfo
hostname
whoami

Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember -Group "Administrators"

whoami /groups
whoami /priv

Get-Process
Get-Service

Get-NetTCPConnection
Get-NetRoute

Get-NetFirewallProfile
Get-NetFirewallRule

Get-WinEvent
```

O Day 07 também consolidou a investigação final de endpoint, relacionando conexão, processo, usuário, privilégios, serviço, firewall e eventos.

\---

# 🧠 Principais aprendizados

* PowerShell para coleta de informações.
* Usuários e grupos.
* Privilégios e UAC.
* Processos e PID.
* Serviços.
* Scheduled Tasks.
* Conexões TCP.
* Associação de conexão com processo.
* Windows Defender Firewall.
* Windows Event Logs.
* Eventos 4624 e 4625.
* Correlação de evidências.
* Investigação de endpoint.

\---

# 🔗 Relação com as Weeks anteriores

### Week 03 — Linux

```text
Usuário
 ↓
Privilégio
 ↓
Processo
 ↓
Serviço
 ↓
Log
```

### Week 04 — Redes

```text
DNS
 ↓
IP
 ↓
ARP
 ↓
MAC
 ↓
TCP/UDP
 ↓
Porta
 ↓
Firewall
 ↓
Serviço
 ↓
Processo
 ↓
Log
```

### Week 05 — Windows

```text
Usuário
 ↓
Grupos / Privilégios
 ↓
Processo
 ↓
Serviço
 ↓
Conexão
 ↓
Firewall
 ↓
Event Log
```

O objetivo foi perceber que os mesmos princípios de investigação aparecem em diferentes sistemas operacionais e camadas da infraestrutura.

\---

# 🛡️ Perspectiva Blue Team

A Week 05 reforçou uma mentalidade essencial para defesa:

> \*\*Uma evidência isolada raramente conta toda a história.\*\*

Uma conexão pode ser legítima. Um processo pode ser legítimo. Um usuário pode ser legítimo. Um serviço pode ser legítimo.

A correlação entre esses elementos, junto com horário, origem, privilégios e eventos, permite construir uma investigação mais consistente.

### Metodologia consolidada

```text
OBSERVAR
   ↓
COLETAR
   ↓
IDENTIFICAR
   ↓
CORRELACIONAR
   ↓
ANALISAR
   ↓
DOCUMENTAR
```

\---

# 🚀 Próxima etapa — Week 06

Com a base de Windows consolidada, o próximo passo é entrar no cenário corporativo:

```text
WINDOWS
   ↓
ACTIVE DIRECTORY
   ↓
DOMÍNIO
   ↓
USUÁRIOS
   ↓
GRUPOS
   ↓
GPO
   ↓
AUTENTICAÇÃO
   ↓
PRIVILÉGIOS
   ↓
AUDITORIA
   ↓
SEGURANÇA
```

A **Week 06 — Active Directory** vai conectar o conhecimento de Windows com o funcionamento de uma infraestrutura corporativa e preparar o CyberLab para investigações mais próximas de ambientes reais.

\---

# 🏁 Status

**Week 05 — Windows: 🟢 CONCLUÍDA**

**Fase 2 — Sistemas e Infraestrutura: em andamento**

**Próxima etapa: Week 06 — Active Directory**

\---

## 👨‍💻 Projeto

**Cybersecurity Roadmap**

**Desenvolvido por Thiago S. Silva**

🔗 [GitHub — Cybersecurity Roadmap](https://github.com/thiagoalphabsb/cybersecurity-roadmap)

