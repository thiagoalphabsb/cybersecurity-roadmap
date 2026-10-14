# 🌐 Laboratório Prático: Network Analysis & Investigação Defensiva (Blue Team / SOC)

> **Módulo / Categoria:** Análise de Tráfego, Engenharia de Redes & Segurança Defensiva[cite: 49]  
> **Escopo:** Investigação L2-L7, Correlação Host/Rede e Análise de Evidências[cite: 49]  
> **Status:** 🟢 Concluído[cite: 49]  

---

## 🎯 1. Apresentação & Objetivo do Projeto

Este laboratório documenta uma **investigação prática de segurança e comportamento de rede** realizada dentro do ambiente controlado **CyberLab**[cite: 49]. 

O objetivo principal foi realizar a **correlação sistemática** entre o tráfego de pacotes (L2-L4), registros de resolução de nomes (L7), regras de filtragem no firewall host-based e os processos ativos no sistema operacional[cite: 49].

### 🧠 A Mentalidade Investigativa (Cadeia de Custódia & Análise)
A análise foi estruturada para responder tecnicamente a incidentes de rede: *como mapear e provar a origem, o caminho e o processo responsável por uma conexão?*[cite: 25, 49]

```text
Nome (DNS) ➔ IP ➔ ARP (MAC) ➔ TCP/UDP ➔ Porta ➔ Firewall (nftables) ➔ Socket ➔ Processo (PID) ➔ Evento/Log

```

Cada etapa da cadeia fornece uma **evidência técnica verificável**, permitindo correlacionar um tráfego capturado no Wireshark diretamente a uma linha de processo executada no host.

---

## 🏗️ 2. Topologia do Ambiente de Laboratório

O ambiente foi configurado em subrede privada isolada (*Host-Only Network*) para garantir testes controlados sem impacto externo:

```text
                        CYBERLAB INTERNAL NETWORK
                             (10.10.10.0/24)
                                    │
                         Isolated Virtual Switch
                                    │
            ┌───────────────────────┴───────────────────────┐
            │                                               │
     CyberLab-Debian                                 CyberLab-Kali
    Debian GNU/Linux 13                                Kali Linux
      10.10.10.10/24                                 10.10.10.20/24
 (Servidor Target / Application Host)          (Estação de Auditoria / SOC / Wireshark)

```

---

## 🛠️ 3. Matriz de Ferramentas & Protocolos Investigados

| Ferramenta / Protocolo | Camada OSI | Aplicação Prática no SOC / Blue Team |
| --- | --- | --- |
| **`Wireshark`** | L2 – L7 | Captura e inspeção profunda de pacotes (*Deep Packet Inspection*), análise de handshakes TCP e requisições DNS.

 |
| **`nftables` (`nft`)** | L3 – L4 | Implementação de controle de acessos (Host-Based Firewall), validação de regras `DROP`/`ACCEPT` e auditoria via contadores.

 |
| **`Nmap`** | L4 – L7 | Mapeamento de superfície de ataque, identificação de portas abertas e *fingerprinting* de serviços.

 |
| **`ss` / `systemctl**` | Sistema Host | Mapeamento da cadeia `Socket → Porta → PID → Serviço Systemd` no Linux.

 |
| **`dig` / `nslookup**` | L7 (DNS) | Validação de infraestrutura de resolução de nomes e análise de registros `A`, `AAAA` e `MX`.

 |
| **`ip` (`addr` / `neigh`)** | L2 – L3 | Análise de tabelas ARP, correlação de IPs com endereços MAC físicos/virtuais e rotas.

 |

---

## 🔬 4. Casos Práticos & Correlação de Evidências

### Caso 01: Mapeamento L4/L7 e Resolução de Nomes

* **Cenário:** Identificação de portas abertas via Nmap e validação das consultas DNS na camada de aplicação.


* **Execução & Análise:** Identifiquei o serviço SSH aberto na porta `22/tcp` e validei a resolução de nomes via consultas `dig` e inspeção no Wireshark.


* **Evidências Visuais:**

### Figura 1: Mapeamento de superfície de ataque com Nmap na estação Kali
![Mapeamento de superfície de ataque com Nmap na estação Kali](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day01-nmap-kali.png)

### Figura 2: Análise de requisição e resposta de pacotes DNS no Wireshark
![Análise de requisição e resposta de pacotes DNS no Wireshark](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day04-wireshark-dns.png)

---

### Caso 02: Correlação Encadeada — Socket, Processo e Conexão TCP

* **Cenário:** Rastreamento completo entre o tráfego de rede e a estrutura interna do SO (Processos/PIDs).


* **Execução & Análise:** Relacionei a porta `22/tcp` ao processo `sshd` (PID 831) no Debian e analisei o estabelecimento de conexão TCP (*Three-Way Handshake*) no Wireshark[cite: 25, 32, 46].
* **Evidências Visuais:**

### Figura 3: Encadeamento entre Socket em escuta, PID do processo e status no Systemd
![Encadeamento entre Socket em escuta, PID do processo e status no Systemd](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day07-correlacao.png)

### Figura 4: Abertura de sessão TCP interceptada no Wireshark via filtro tcp.flags.syn == 1
![Abertura de sessão TCP interceptada no Wireshark via filtro tcp.flags.syn == 1](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day02-wiresharkSYN.png)

---

### Caso 03: Camada de Enlace (ARP) e Firewall Host-Based (`nftables`)

* **Cenário:** Mapeamento L2 na rede local e validação de controle de acessos com regras e contadores[cite: 25, 42, 45, 49].
* **Execução & Análise:** Rastreiei requisições ARP broadcast/unicast e implementei regras no `nftables` para bloquear o tráfego HTTP/8080, validando a retenção através dos contadores do firewall[cite: 25, 42, 45].
* **Evidências Visuais:**

### Figura 5: Intercepção do fluxo ARP Request/Reply entre Debian e Kali
![Intercepção do fluxo ARP Request/Reply entre Debian e Kali](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day07-ARP-wireshark.png)

### Figura 6: Regra de bloqueio em ação no nftables com contadores de pacotes descartados (counter drop)
![Regra de bloqueio em ação no nftables com contadores de pacotes descartados (counter drop)](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week04-day05-counter-drop.png)

---

## 📑 5. Relatório Sintético de Investigação de Redes

```text
===================================================================
                INVESTIGAÇÃO DE REDES — WEEK 04
===================================================================

1. HOST ANALISADO:
   IP: 10.10.10.10 | Sistema: Debian 13 (Trixie)

2. RECONHECIMENTO (Nmap v7.99):
   - Porta Encontrada: 22/tcp open (ssh)
   - Versão do Serviço: OpenSSH 10.0p2 Debian 7+deb13u4

3. MAPEAMENTO DE SERVIÇOS & PROCESSOS:
   - Serviço: SSH (Secure Shell)
   - Processos: sshd (daemon) / sshd-session
   - PIDs: 831 (daemon principal) / 3192 (sessão ativa)

4. TABELA ARP & MAC ADDRESS:
   - IP Origem (Kali Linux): 10.10.10.20
   - MAC Alvo: 08:00:27:EE:8E:5F (VirtualBox NIC)

5. RESOLUÇÃO DE NOMES (DNS):
   - Consulta: google.com (Tipo A) ➔ Resposta: 172.217.172.46
   - Servidor DNS Ativo: 10.1.1.12#53 (UDP)

6. ANÁLISE DE TRÁFEGO (Wireshark):
   - Three-Way Handshake TCP validado na porta 22 (SYN -> SYN/ACK -> ACK)
   - Tráfego criptografado SSHv2 capturado e isolado por filtro de porta

7. FILTRAGEM & FIREWALL (nftables v1.1.3):
   - Tabela isolada: `inet cyberlab`
   - Teste de Regra: `tcp dport 8080 counter drop` / `accept`
   - Validação: Bloqueio efetivo de requisições e contabilização precisa nos contadores do firewall.
===================================================================

```

---

## 📈 6. Evolução Técnica & Competências Desenvolvidas

Através deste laboratório, evoluí de uma compreensão teórica de redes para uma **abordagem prática e investigativa voltada para Operações de Segurança (SOC / Blue Team)**:

* **Desenvolvi capacidade de investigação correlacionada (L2 a L7):** Aprendi a não analisar eventos isolados. Agora relaciono endereços MAC (L2) e IPs (L3) a requisições de DNS, estabelecimentos de conexão TCP (L4) e o binário que os gerou no sistema operacional[cite: 25, 26, 49].
* **Aprimorei a análise de tráfego com Wireshark:** Evoluí na criação de filtros avançados para isolar *handshakes* TCP, analisar requisições DNS e validar a comunicação entre hosts sem depender exclusivamente da interface do sistema[cite: 25, 32, 35, 49].
* **Consolidei técnicas de mitigação e firewall com `nftables`:** Dominei a criação de tabelas, correntes e regras personalizadas de filtragem, utilizando contadores nativos para auditar e provar a eficácia de bloqueios em acessos não autorizados[cite: 25, 42, 49].
* **Fortaleci a mentalidade de resposta a incidentes:** Desenvolvi o hábito de estruturar diagnósticos baseados em evidências reproduzíveis, gerando relatórios técnicos que conectam a perspectiva de rede à perspectiva do host[cite: 20, 25, 49].

---

## 🔗 Projetos e Links Relacionados

* 🛡️ [Cybersecurity Portfolio Principal](https://github.com/thiagoalphabsb/cybersecurity-portfolio)
* 🧪 [CyberLab Infrastructure](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/portfolio/cyberlab/README.md)
* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)
