# Inventario de Ativos - CyberLab v1.0

Data: 01/09/2026
Host Fisico: Windows 11 (VirtualBox)
Rede Interna Isolda: CYBERLAB-INTERNAL (10.10.10.0/24)

---

## Mapeamento Geral do Laboratorio

| Ativo | Funcao | Sistema Operacional | Kernel | IP NAT | IP Interno | Status |
|---|---|---|---|---|---|---|
| Debian | Servidor / SysAdmin | Debian GNU/Linux 13 | 6.12.94+deb13-amd64 | 10.0.2.15/24 | 10.10.10.10/24 (enp0s8) | Executando |
| Kali Linux | Security / Analise | Kali Linux Rolling | 6.19.14+kali-amd64 | 10.0.2.15/24 | 10.10.10.20/24 (eth1) | Desligado |

---

## Detalhamento dos Ativos

### Ativo 01: Debian (Servidor de Laboratorio)
* Hostname: debian
* Nome no VirtualBox: CyberLab-Linux
* Arquitetura: x86-64
* Recursos:
  - vCPU: 2 Processadores
  - RAM: 3.8 GiB (Total) | 2.8 GiB (Livre)
  - Disco: 30 GB VDI (/dev/sda1 com 28 GB formatados, 5.1 GB em uso)
* Configuracao de Rede:
  - Interface NAT (enp0s3): IP 10.0.2.15/24 | Gateway 10.0.2.2
  - Interface Interna (enp0s8): IP Estatico 10.10.10.10/24 (CYBERLAB-INTERNAL)
* Snapshot: BASE-LINUX-INSTALADO

### Ativo 02: Kali Linux (Analise e Testes)
* Hostname: kali
* Nome no VirtualBox: kali-linux-2026.2-virtualbox-amd64
* Arquitetura: x86-64
* Recursos:
  - RAM: ~2.0 GB
  - Disco: 79 GB VDI
* Configuracao de Rede:
  - Interface NAT (eth0): IP 10.0.2.15/24 | Gateway 10.0.2.2
  - Interface Interna (eth1): IP Estatico 10.10.10.20/24 (CYBERLAB-INTERNAL)
* Snapshot: CYBERLAB-CLEAN-01

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
   (Acesso a Internet)               (Acesso a Internet)
             |                                 |
     +-------v--------+               +--------v------+
     |   Debian       |               |   Kali        |
     |  10.10.10.10   |               |  10.10.10.20  |
     +-------+--------+               +--------+------+
             |                                 |
     Adapter 2 (enp0s8)                Adapter 2 (eth1)
             |                                 |
             +--------- Rede Interna ----------+
                      CYBERLAB-INTERNAL
                      (10.10.10.0/24)
