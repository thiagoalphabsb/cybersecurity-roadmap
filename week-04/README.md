# 🌐 Week 04 — Redes (Fundamentos \& Análise Prática)

## 🎯 Visão Geral da Semana

A **Week 04** consolida a base de comunicação e infraestrutura dentro da **Fase 1 (Fundamentos)** do **Cybersecurity Roadmap**.

O objetivo desta semana foi integrar os conhecimentos de Linux e virtualização adquiridos nas semanas anteriores, analisando como os dados trafegam pela rede a partir de uma perspectiva defensiva (**Blue Team / SOC**).

**Metodologia de estudo:** `Estudar → Executar → Documentar → Explicar → Repetir`

\---

## 📅 Progresso Diário

|Dia|Conteúdo / Foco Prático|Status|
|:-:|-|:-:|
|**Dia 01**|Fundamentos de Redes, IP estático, tabela de rotas, conectividade ICMP e reconhecimento com `nmap` e `ss`|🟢 Concluído|
|**Dia 02**|TCP vs. UDP, mapeamento `IP → Porta → Serviço → Processo → systemd`, Three-Way Handshake e Wireshark|🟢 Concluído|
|**Dia 03**|ARP, MAC Address, tabela de vizinhos com `ip neigh` e análise de pacotes no Wireshark|🟢 Concluído|
|**Dia 04**|DNS, resolução de nomes, registros `A`, `AAAA`, `MX`, `dig`, `nslookup` e Wireshark|🟢 Concluído|
|**Dia 05**|Firewall Linux com `nftables`, tabela isolada `inet cyberlab`, regras `DROP`/`ACCEPT` e contadores|🟢 Concluído|
|**Dia 06**|Laboratório integrado de análise de tráfego, monitoramento SSH, investigação via `/proc`, handshake TCP e investigação de conexões|🟢 Concluído|
|**Dia 07**|Consolidação da Week 04, revisão do fluxo investigativo e documentação do laboratório|🟢 Concluído|

\---

## 🧠 Cadeia Investigativa Consolidada

Ao longo da semana, a análise evoluiu de um simples reconhecimento de portas para uma correlação técnica entre rede, sistema operacional, serviços, processos e mecanismos de controle.

```text
Nome
  ↓
DNS
  ↓
IP
  ↓
ARP
  ↓
MAC
  ↓
TCP / UDP
  ↓
Porta
  ↓
Firewall (nftables)
  ↓
Serviço / Socket
  ↓
Processo (PID)
  ↓
Logs / Evidências
```

Essa cadeia representa uma abordagem prática de investigação: cada camada fornece uma evidência que pode ser correlacionada com as demais.

\---

## 🔬 Destaques dos Laboratórios Práticos

### 🔹 Endereçamento e Conectividade — Dias 01 e 03

Configuração e análise da rede isolada `CYBERLAB-INTERNAL`:

```text
Debian → 10.10.10.10/24
Kali   → 10.10.10.20/24
```

Foram analisados:

* interfaces de rede;
* endereçamento IP;
* tabela de rotas;
* conectividade ICMP;
* tabela de vizinhos;
* resolução ARP;
* endereços MAC;
* pacotes ARP Request/Reply.

### 🔹 Camada de Transporte — Dia 02

Foram identificados sockets nos estados `LISTEN` e `ESTABLISHED`, correlacionando:

```text
IP → Porta → Serviço → Processo → systemd
```

Também foi analisado o **TCP Three-Way Handshake**:

```text
SYN → SYN/ACK → ACK
```

A comunicação SSH foi observada no sistema operacional e no Wireshark.

### 🔹 DNS — Dia 04

Foram realizadas consultas e análises utilizando:

* `dig`;
* `nslookup`;
* `getent hosts`;
* registros `A`;
* registros `AAAA`;
* registros `MX`;
* consultas DNS direcionadas;
* análise de pacotes DNS no Wireshark.

### 🔹 Firewall Linux — Dia 05

Foi utilizado `nftables` em uma tabela isolada:

```text
inet cyberlab
```

O laboratório demonstrou, de forma controlada, a diferença entre:

* serviço em `LISTEN`;
* tráfego permitido;
* tráfego bloqueado por `DROP`;
* tráfego novamente permitido por `ACCEPT`.

Também foram utilizados `counter` para observar a quantidade de pacotes atingindo a regra de firewall.

### 🔹 Análise de Tráfego e Investigação — Dias 06 e 07

A etapa final integrou os conhecimentos anteriores por meio da:

* observação de sessões SSH;
* identificação de conexões TCP;
* correlação entre porta, socket e processo;
* inspeção de `/proc/PID/exe`;
* análise do Three-Way Handshake;
* análise de DNS;
* reconhecimento com Nmap;
* observação de ARP;
* correlação entre firewall e tráfego;
* documentação de uma investigação técnica.

\---

## 🛠️ Principais Ferramentas Utilizadas

|Ferramenta / Comando|Aplicação|
|-|-|
|`ip addr`|Identificação e análise de endereços IP|
|`ip route`|Análise de rotas|
|`ip neigh`|Tabela de vizinhos / ARP|
|`ping`|Teste de conectividade ICMP|
|`ss`|Análise de sockets e conexões|
|`nmap`|Reconhecimento e identificação de portas/serviços|
|`systemctl`|Análise de serviços gerenciados pelo systemd|
|`dig`|Investigação de DNS|
|`nslookup`|Consulta de registros DNS|
|`nft` / `nftables`|Filtragem e controle de tráfego|
|`Wireshark`|Captura e análise de pacotes|
|`/proc`|Investigação de processos no Linux|

\---

## 📄 Documentos \& Relatórios da Semana

* 📘 [Dia 01 — Fundamentos de Redes e Reconhecimento](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/Week04-day01.txt)
* 📘 [Dia 02 — TCP, UDP, Portas e Serviços](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/Week04-day02.txt)
* 📘 [Dia 03 — ARP, MAC Address e Descoberta na Rede Local](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/Week04-day03.txt)
* 📘 [Dia 04 — DNS, Resolução de Nomes e Análise de Consultas](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/week_04_day_04.txt)
* 📘 [Dia 05 — Firewall Linux com nftables](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/week04-day05.txt)
* 📘 [Dia 06 — Monitoramento de Tráfego e Investigação de Conexões](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/week04-day06.txt)
* 📘 [Dia 07 — Consolidação da Week 04](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/docs/week04-day07.txt)
* 📑 [Relatório de Investigação da Week 04](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/notes/week04-investigacao.txt)



\---

## 📸 Evidências Globais da Week 04

### 📍 Dia 01 — Fundamentos \& Conectividade

* [Configuração de IP e Rotas no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ipdebian.png)
* [Configuração de IP e Rotas no Kali Linux](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ipkali.png)
* [Teste de Conectividade ICMP Bidirecional](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-pingvms.jpg)
* [Sockets em Escuta no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-ss-tuln-debian.png)
* [Varredura Nmap a partir do Kali](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day01-nmap-kali.png)

### 📍 Dia 02 — TCP, Sockets \& Handshake

* [Sockets e Processos no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-sstul.png)
* [Status do Serviço SSH no systemd](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-sshstatus.png)
* [Scanner de Portas com Nmap no Kali](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-nmapscankali.png)
* [Conexão TCP Estabelecida no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-tnp.png)
* [Filtro da Flag SYN no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-wiresharkSYN.jpg)
* [Captura da Sessão SSH e Handshake no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day02-wireshark3way.jpg)

### 📍 Dia 03 — ARP \& Camada de Enlace

* [Mapeamento de MAC e Tabela ARP no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-ipneigh-debian.png)
* [Mapeamento de MAC e Tabela ARP no Kali](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidenceweek04-day03-ipneigh-kali.png)
* [Limpeza de Cache e Redescoberta ARP](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-arp-del-ping.png)
* [Captura dos Pacotes ARP Request e Reply no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day03-wireshark-arp.png)

### 📍 Dia 04 — DNS \& Resolução de Nomes

* [Configuração do Resolv e Resolução no Debian](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day04-resolv-conf.png)
* [Consultas de Registros A, AAAA e MX via nslookup](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day04-nslookup-records.png)
* [Consultas DNS via dig](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day04-dig-queries.png)
* [Análise da Captura de Pacotes DNS no Wireshark](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day04-wireshark-dns.png)

### 📍 Dia 05 — Firewall Linux \& nftables

* [Estado Inicial do nftables](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidenceweek04-day05-nft-initial.png)
* [Servidor Temporário Python em Execução — 0.0.0.0:8080](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-python-listen.png)
* [Teste de Conectividade Antes do Bloqueio](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-baseline-kali.png)
* [Criação da Tabela cyberlab e Regra DROP](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-nft-drop-rule.png)
* [Porta Filtrada no Nmap e Timeout no Curl](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-nmap-filtered.png)
* [Contador de Pacotes da Regra DROP](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-counter-drop.png)
* [Regra ACCEPT e Conexão Permitida](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week04-day05-nft-accept-rule.png)
* [Limpeza da Tabela cyberlab](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/week04-day05-cleanup.png)

### 📍 Dia 06 e Dia 07 — Consolidação da Semana

* [Análise e Captura de Pacotes ARP no Wireshark](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/week04-day07-ARP-wireshark.png)
* [Correlação de Sockets, Processos e systemd no Debian](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/week04-day07-correlacao.png)
* [Consultas DNS no Terminal via dig](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/week04-day07-DNS.png)
* [Reconhecimento de Portas e Detecção de Versão com Nmap](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/week04-day07-reconhecimento.png)

\---

## 🎓 Competências Desenvolvidas

Ao concluir a Week 04, foram praticadas as seguintes competências:

* fundamentos de redes TCP/IP;
* endereçamento IPv4;
* análise de rotas;
* ICMP;
* ARP e MAC Address;
* TCP e UDP;
* portas e sockets;
* serviços e processos Linux;
* systemd;
* SSH;
* DNS;
* Nmap;
* Wireshark;
* firewall Linux com nftables;
* análise de regras `DROP` e `ACCEPT`;
* utilização de contadores para auditoria;
* investigação de conexões;
* correlação de evidências de rede e host;
* documentação técnica de laboratório.

\---

## 🔎 Perspectiva de Segurança

A Week 04 reforçou uma abordagem de investigação baseada em evidências.

Em vez de analisar uma porta ou um pacote de forma isolada, o laboratório permitiu correlacionar:


Quem?
  ↓
Qual host?
  ↓
Qual IP?
  ↓
Qual MAC?
  ↓
Qual protocolo?
  ↓
Qual porta?
  ↓
Qual serviço?
  ↓
Qual processo?
  ↓
Qual regra de firewall?
  ↓
Qual tráfego foi observado?
  ↓
Qual evidência sustenta a conclusão?


Essa abordagem aproxima o laboratório de situações reais de **monitoramento, análise e investigação defensiva**.

\---

## 🏁 Conclusão da Week 04

A Week 04 foi concluída com sucesso, consolidando os fundamentos de redes necessários para avançar no **Cybersecurity Roadmap**.

O principal resultado não foi apenas conhecer comandos individuais, mas compreender como diferentes fontes de informação podem ser correlacionadas durante uma investigação:


Nmap
  +
ss
  +
ip
  +
systemctl
  +
nftables
  +
Wireshark
  +
/proc
  =
Visão integrada do ambiente


Com isso, o laboratório evoluiu de uma simples configuração de rede para uma análise prática de comunicação, serviços, processos, filtragem e evidências.

\---

**Status:** 🟢 Concluído

**Projeto:** Cybersecurity Roadmap

**Semana:** 04 — Redes (Fundamentos \& Análise Prática)

*> Desenvolvido por Thiago S. Silva*

*---*

