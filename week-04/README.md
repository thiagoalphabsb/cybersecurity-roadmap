---

```markdown
# 🌐 Week 04 — Redes (Fundamentos & Análise Prática)

## 🎯 Visão Geral da Semana

A **Week 04** consolida a base de comunicação e infraestrutura dentro da **Fase 1 (Fundamentos)** do **Cybersecurity Roadmap**[cite: 17, 20]. O objetivo desta semana é integrar os conhecimentos de Linux e virtualização adquiridos nas semanas anteriores[cite: 17, 18], analisando como os dados trafegam pela rede a partir da perspectiva defensiva (*Blue Team*)[cite: 18, 21].

**Metodologia de Estudo:** `Estudar → Executar → Documentar → Explicar → Repetir`[cite: 17, 20]

---

## 📅 Progresso Diário

| Dia | Conteúdo / Foco Prático | Status |
| :---: | :--- | :---: |
| **Dia 01** | Fundamentos de Redes, Configuração de IP Estático, Tabela de Rotas, Conectividade ICMP e Reconhecimento (`nmap`, `ss`) | 🟢 Concluído |
| **Dia 02** | Camada de Transporte (TCP vs. UDP), Mapeamento Encadeado (`IP → Porta → Serviço → Processo → systemd`), Handshake TCP e Análise no Wireshark | 🟢 Concluído |
| **Dia 03** | Camada de Enlace & Resolução de Endereço Local: ARP, MAC Address, Tabela de Vizinhos (`ip neigh`) e Captura de Pacotes no Wireshark | 🟢 Concluído |
| **Dia 04** | DNS, Resolução de Nomes, Tipos de Registros (`dig`, `nslookup`) e Análise de Consultas no Wireshark | 🟡 A iniciar (Amanhã) |
| **Dia 05** | Serviços Web & Acesso Remoto: HTTP, HTTPS, SSH & Análise de Cabeçalhos (`curl`, `ssh`) | ⚪ A iniciar |
| **Dia 06** | Laboratório Integrado de Análise de Tráfego (`Network Traffic Analysis`) & Projeto da Semana | ⚪ A iniciar |
| **Dia 07** | Consolidação do Relatório, Revisão Geral e Atualização do Repositório | ⚪ A iniciar |

---

## 🧠 Resumo do Conteúdo Desenvolvido

### 🔹 Dia 01 — Fundamentos de Redes e Reconhecimento
* **Laboratório:** Configuração de interfaces e atribuição de IP estático no Debian (`10.10.10.10/24`) e Kali Linux (`10.10.10.20/24`) conectados à rede isolada `CYBERLAB-INTERNAL`[cite: 19, 20].
* **Comandos Praticados:** `ip addr`, `ip route`, `ip route get`, `ping -c 4`, `ss -tuln`, `nmap -n`.
* **Aprendizado Principal:** O funcionamento do `ping` (ICMP) valida a conectividade da camada de rede, mas a análise de segurança precisa avançar para a verificação de portas abertas e serviços da camada de aplicação[cite: 18, 21].

### 🔹 Dia 02 — TCP, UDP, Portas e Serviços
* **Laboratório:** Mapeamento do socket em escuta (`LISTEN`) até o processo daemon e a unidade do `systemd`, seguido de inspeção externa com Nmap e captura do Three-Way Handshake TCP (SYN → SYN/ACK → ACK) via Wireshark durante uma sessão SSH[cite: 18, 21].
* **Comandos Praticados:** `sudo ss -tulnp`, `ss -tan`, `sudo ss -tnp`, `ps -p <PID>`, `systemctl status ssh`, `nmap -n -sV -p 22`, `ssh debian@10.10.10.10`.
* **Cadeia de Investigação:**
  ```text
  10.10.10.20 (Kali) → TCP/22 → SSH → sshd (PID) → systemd (ssh.service) → ESTABLISHED

```

### 🔹 Dia 03 — ARP, MAC Address e Descoberta na Rede

* **Laboratório:** Inspeção dos endereços físicos (**MAC Address**) e análise da tabela de vizinhos (**Cache ARP**). Simulação de invalidação de tabela (`ip neigh del`), redescoberta via Broadcast/Unicast e análise do cabeçalho dos pacotes ARP Request e Reply no Wireshark.


* **Comandos Praticados:** `ip link`, `ip neigh`, `sudo ip neigh del <IP> dev <interface>`, `ping -c 1`, filtro `arp` no Wireshark.


* **Cadeia de Investigação Atualizada:**
```text
MAC → IP → TCP/UDP → Porta → Serviço → Processo

```



---

## 📸 Evidências do Laboratório

### 📍 Dia 01 — Fundamentos & Conectividade

* [Configuração de IP e Rotas no Debian](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day01-ipdebian.png&utm_source=gemini)
* [Configuração de IP e Rotas no Kali Linux](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day01-ipkali.png&utm_source=gemini)
* [Teste de Conectividade ICMP Bidirecional](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day01-pingvms.jpg&utm_source=gemini)
* [Sockets em Escuta no Debian (`ss -tuln`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day01-ss-tuln-debian.png&utm_source=gemini)
* [Varredura Nmap Simples a partir do Kali](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day01-nmap-kali.png&utm_source=gemini)

### 📍 Dia 02 — TCP, Sockets & Handshake

* [Sockets e Processos no Debian (`ss -tulnp` / `ss -tan`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-sstul.png&utm_source=gemini)
* [Status do Serviço SSH no Systemd (`systemctl status ssh`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-sshstatus.png&utm_source=gemini)
* [Scanner de Portas com Nmap no Kali](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-nmapscankali.png&utm_source=gemini)
* [Conexão TCP Estabelecida no Debian (`sudo ss -tnp`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-tnp.png&utm_source=gemini)
* [Filtro da Flag SYN no Wireshark](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-wiresharkSYN.jpg&utm_source=gemini)
* [Captura da Sessão SSH e Handshake no Wireshark](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day02-wireshark3way.jpg&utm_source=gemini)

### 📍 Dia 03 — ARP & Camada de Enlace

* [Mapeamento de MAC e Tabela ARP no Debian (`ip link` / `ip neigh`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day03-ipneigh-debian.png&utm_source=gemini)
* [Mapeamento de MAC e Tabela ARP no Kali (`ip link` / `ip neigh`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day03-ipneigh-kali.png&utm_source=gemini)
* [Limpeza de Cache e Redescoberta ARP (`ip neigh del` + `ping`)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day03-arp-del-ping.png&utm_source=gemini)
* [Captura dos Pacotes ARP Request e Reply no Wireshark](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/evidence/week04-day03-wireshark-arp.png&utm_source=gemini)

---

**Status:** 🟡 Em Andamento

**Projeto:** Cybersecurity Roadmap

**Semana:** 04 — Redes

> *Desenvolvido por Thiago S. Silva*
> 

```

---
