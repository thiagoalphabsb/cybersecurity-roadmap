# Inventário de Ativos — CyberLab v2.0

Data de Atualização: 11/10/2026
Host Físico: Windows 11 (Oracle VirtualBox)
Rede Interna Isolada: CYBERLAB-INTERNAL (10.10.10.0/24)

---

## Mapeamento Geral do Laboratório

| Ativo / Hostname | Função / Papel | Sistema Operacional | Kernel / Build | IP NAT | IP Interno | Status |
|---|---|---|---|---|---|---|
| **DC01** | Domain Controller (AD DS / DNS) | Windows Server 2025 Datacenter | Build 26100 (x86-64) | - | 10.10.10.10/24 | Executando |
| **CyberLab-Debian** | Servidor / SysAdmin / Target | Debian GNU/Linux 13 | 6.12.94+deb13-amd64 | 10.0.2.15/24 | 10.10.10.10/24 (enp0s8) | Executando |
| **CyberLab-Kali** | Security / Auditoria / SOC | Kali Linux Rolling | 6.19.14+kali-amd64 | 10.0.2.15/24 | 10.10.10.20/24 (eth1) | Executando |

---

## Detalhamento dos Ativos

### Ativo 01: DC01 (Controlador de Domínio Windows Server 2025)
* **Hostname:** `DC01`
* **Nome no VirtualBox:** `BASE-WINDOWS-SERVER-2025`
* **Domínio AD:** `corp.thiago.lab` (NetBIOS: `THIAGO`)
* **Arquitetura:** x86-64
* **Recursos:**
  - **vCPU:** 2 Processadores
  - **RAM:** 4.0 GiB
  - **Disco:** 50 GB VDI
* **Configuração de Rede:**
  - **Interface Interna:** IP Estático `10.10.10.10/24` (CYBERLAB-INTERNAL)
  - **DNS Server:** `10.10.10.10`
* **Serviços Ativos:** AD DS, DNS Server, Kerberos, Global Catalog, Group Policy Management
* **Snapshot:** `BASE-WIN2025-ADDS-CONFIGURED`

### Ativo 02: Debian (Servidor de Aplicação / Target)
* **Hostname:** `debian`
* **Nome no VirtualBox:** `CyberLab-Linux`
* **Arquitetura:** x86-64
* **Recursos:**
  - **vCPU:** 2 Processadores
  - **RAM:** 3.8 GiB (Total) | 2.8 GiB (Livre)
  - **Disco:** 30 GB VDI (`/dev/sda1` com 28 GB formatados)
* **Configuração de Rede:**
  - **Interface NAT (enp0s3):** IP `10.0.2.15/24` | Gateway `10.0.2.2`
  - **Interface Interna (enp0s8):** IP Estático `10.10.10.10/24` (CYBERLAB-INTERNAL)
* **Serviços Ativos:** OpenSSH Server (Porta 22/tcp), UFW Firewall, Syslog
* **Snapshot:** `BASE-LINUX-INSTALADO`

### Ativo 03: Kali Linux (Estação de Auditoria e Testes)
* **Hostname:** `kali`
* **Nome no VirtualBox:** `kali-linux-2026.2-virtualbox-amd64`
* **Arquitetura:** x86-64
* **Recursos:**
  - **RAM:** ~2.0 GB
  - **Disco:** 79 GB VDI
* **Configuração de Rede:**
  - **Interface NAT (eth0):** IP `10.0.2.15/24` | Gateway `10.0.2.2`
  - **Interface Interna (eth1):** IP Estático `10.10.10.20/24` (CYBERLAB-INTERNAL)
* **Ferramentas Principais:** Wireshark, Nmap, OpenSSH Client, PowerShell Core
* **Snapshot:** `CYBERLAB-CLEAN-01`

---

## Topologia da Rede Isolada

```text
                  +------------------------+
                  |      Windows Host      |
                  |   Oracle VirtualBox    |
                  +-----------+------------+
                              |
             +----------------+----------------+
             |                                 |
     Adapter 1 (NAT)                   Adapter 1 (NAT)
   (Acesso à Internet)               (Acesso à Internet)
             |                                 |
     +-------v--------+               +--------v------+
     | CyberLab-Debian|               | CyberLab-Kali |
     |  10.10.10.10   |               |  10.10.10.20  |
     +-------+--------+               +--------+------+
             |                                 |
     Adapter 2 (enp0s8)                Adapter 2 (eth1)
             |                                 |
             +------------+--------------------+
                          |
             +------------v--------------------+
             |        DC01 (WinServer)         |
             |          10.10.10.10            |
             |       (corp.thiago.lab)         |
             +---------------------------------+
                      Rede Interna
                 CYBERLAB-INTERNAL
                  (10.10.10.0/24)
