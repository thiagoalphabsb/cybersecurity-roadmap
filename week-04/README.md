# 🌐 Week 04 — Redes (Fundamentos \& Análise Prática)

## 🎯 Visão Geral da Semana

A **Week 04** consolida a base de comunicação e infraestrutura dentro da **Fase 1 (Fundamentos)** do **Cybersecurity Roadmap**.

O objetivo desta semana é integrar os conhecimentos de Linux e virtualização adquiridos nas semanas anteriores, analisando como os dados trafegam pela rede a partir de uma perspectiva defensiva (*Blue Team*).

**Metodologia de Estudo:**

> \*\*Estudar → Executar → Documentar → Explicar → Repetir\*\*

\---

## 📅 Progresso Diário

|Dia|Conteúdo / Foco Prático|Status|
|:-:|-|:-:|
|**Dia 01**|Fundamentos de Redes, configuração de IP estático, tabela de rotas, conectividade ICMP e reconhecimento (`nmap`, `ss`)|🟢 Concluído|
|**Dia 02**|Camada de Transporte (TCP vs. UDP), mapeamento encadeado (`IP → Porta → Serviço → Processo → systemd`), Handshake TCP e análise no Wireshark|🟢 Concluído|
|**Dia 03**|Camada de Enlace e resolução de endereço local: ARP, MAC Address, tabela de vizinhos (`ip neigh`) e captura de pacotes no Wireshark|🟢 Concluído|
|**Dia 04**|DNS, resolução de nomes, tipos de registros (`dig`, `nslookup`) e análise de consultas no Wireshark|🟡 A iniciar|
|**Dia 05**|Serviços Web e acesso remoto: HTTP, HTTPS, SSH e análise de cabeçalhos (`curl`, `ssh`)|⚪ A iniciar|
|**Dia 06**|Laboratório integrado de análise de tráfego (*Network Traffic Analysis*) e projeto da semana|⚪ A iniciar|
|**Dia 07**|Consolidação do relatório, revisão geral e atualização do repositório|⚪ A iniciar|

\---

## 🧠 Resumo do Conteúdo Desenvolvido

### 🔹 Dia 01 — Fundamentos de Redes e Reconhecimento

**Laboratório**

Configuração de interfaces e atribuição de IP estático no Debian (`10.10.10.10/24`) e Kali Linux (`10.10.10.20/24`), conectados à rede isolada `CYBERLAB-INTERNAL`.

**Comandos praticados**

```bash
ip addr
ip route
ip route get
ping -c 4
ss -tuln
nmap -n
```

**Aprendizado principal**

O funcionamento do `ping` (ICMP) permite validar a conectividade da camada de rede. Porém, uma análise de segurança precisa avançar para a verificação de portas abertas e serviços disponíveis nas camadas superiores.

\---

### 🔹 Dia 02 — TCP, UDP, Portas e Serviços

**Laboratório**

Mapeamento do socket em escuta (`LISTEN`) até o processo daemon e a unidade do `systemd`, seguido de inspeção externa com Nmap e captura do Three-Way Handshake TCP (`SYN → SYN/ACK → ACK`) via Wireshark durante uma sessão SSH.

**Comandos praticados**

```bash
sudo ss -tulnp
ss -tan
sudo ss -tnp
ps -p <PID>
systemctl status ssh
nmap -n -sV -p 22
ssh debian@10.10.10.10
```

**Cadeia de investigação**

```text
10.10.10.20 (Kali)
        ↓
     TCP/22
        ↓
       SSH
        ↓
   sshd (PID)
        ↓
systemd (ssh.service)
        ↓
   ESTABLISHED
```

\---

### 🔹 Dia 03 — ARP, MAC Address e Descoberta na Rede

**Laboratório**

Inspeção dos endereços físicos (**MAC Address**) e análise da tabela de vizinhos (**cache ARP**).

Também foi realizada a simulação de invalidação da tabela com `ip neigh del`, seguida de redescoberta por meio de Broadcast/Unicast e análise dos cabeçalhos dos pacotes **ARP Request** e **ARP Reply** no Wireshark.

**Comandos praticados**

```bash
ip link
ip neigh
sudo ip neigh del <IP> dev <interface>
ping -c 1
```

**Filtro utilizado no Wireshark**

```text
arp
```

**Cadeia de investigação atualizada**

```text
MAC → IP → TCP/UDP → Porta → Serviço → Processo
```

\---

## 📸 Evidências do Laboratório

### 📍 Dia 01 — Fundamentos \& Conectividade

* [Configuração de IP e Rotas no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ipdebian.png)
* [Configuração de IP e Rotas no Kali Linux](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ipkali.png)
* [Teste de Conectividade ICMP Bidirecional](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-pingvms.jpg)
* [Sockets em Escuta no Debian (`ss -tuln`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ss-tuln-debian.png)
* [Varredura Nmap Simples a partir do Kali](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-nmap-kali.png)

### 📍 Dia 02 — TCP, Sockets \& Handshake

* [Sockets e Processos no Debian (`ss -tulnp` / `ss -tan`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-sstul.png)
* [Status do Serviço SSH no systemd (`systemctl status ssh`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-sshstatus.png)
* [Scanner de Portas com Nmap no Kali](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-nmapscankali.png)
* [Conexão TCP Estabelecida no Debian (`sudo ss -tnp`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-tnp.png)
* [Filtro da Flag SYN no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-wiresharkSYN.jpg)
* [Captura da Sessão SSH e Handshake no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-wireshark3way.jpg)

### 📍 Dia 03 — ARP \& Camada de Enlace

* [Mapeamento de MAC e Tabela ARP no Debian (`ip link` / `ip neigh`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-ipneigh-debian.png)
* [Mapeamento de MAC e Tabela ARP no Kali (`ip link` / `ip neigh`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-ipneigh-kali.png)
* [Limpeza de Cache e Redescoberta ARP (`ip neigh del` + `ping`)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-arp-del-ping.png)
* [Captura dos Pacotes ARP Request e Reply no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-wireshark-arp.png)

\---

## 📌 Status da Semana

**Status:** 🟡 Em Andamento

**Projeto:** Cybersecurity Roadmap

**Semana:** 04 — Redes

> \*Desenvolvido por Thiago S. Silva\*

