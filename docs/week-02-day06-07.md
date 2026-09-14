# 🚀 Week 02 — Virtualização + CyberLab

### ❓ Pergunta Investigativa

**Se existe um Echo Request saindo do Kali e um Echo Reply retornando do Debian, o que isso prova sobre a comunicação entre os dois hosts?**

> Prova que a conectividade na Camada 3 (Rede) está totalmente funcional bidirecionalmente, os pacotes são roteados corretamente e ambos os hosts estão ativos na mesma sub-rede isolada.

\---

# Dia 06 — Análise de Tráfego de Rede com Wireshark

## 🎯 Objetivo

Realizar captura e análise de tráfego de rede utilizando o **Wireshark**, observando o comportamento de protocolos de camada de rede/transporte e analisando o estabelecimento de conexões TCP.

## 🧪 Ambiente

* **Kali Linux** (`10.10.10.20`) — Estação de Análise
* **Debian** (`10.10.10.10`) — Host Alvo
* **VirtualBox** (Rede Interna isolada)
* **Wireshark**

\---

## 🔬 Atividades Realizadas

### 1\. Captura ICMP

Foi realizada uma captura de pacotes ICMP durante um teste de comunicação via `ping` entre Kali e Debian.

* **Filtro utilizado:** `icmp`
* **Resultado:** Capturados pacotes `Echo (ping) request` do Kali (`10.10.10.20`) para o Debian (`10.10.10.10`) e as respectivas respostas `Echo (ping) reply` com 0% de perda.

### 2\. Captura TCP e 3-Way Handshake

Foi iniciada uma conexão via serviço SSH (porta 22) para registrar a abertura de socket TCP.

* **Filtro utilizado:** `tcp` (ou `tcp.port == 22`)
* **A sequência do 3-Way Handshake capturada:**

  1. `\[SYN]` — Kali (`10.10.10.20:59148`) → Debian (`10.10.10.10:22`) | `Seq=0`
  2. `\[SYN, ACK]` — Debian (`10.10.10.10:22`) → Kali (`10.10.10.20:59148`) | `Seq=0 Ack=1`
  3. `\[ACK]` — Kali (`10.10.10.20:59148`) → Debian (`10.10.10.10:22`) | `Seq=1 Ack=1`

\---

## 🕵️ Investigação Detalhada de Tráfego

* **Origem:** `10.10.10.20` (Kali Linux - `08:00:27:74:76:41`)
* **Destino:** `10.10.10.10` (Debian - `08:00:27:ee:8e:5f`)
* **Protocolos Identificados:** ICMP, TCP, SSHv2
* **Portas Envolvidas:** Origem `59148` (Porta alta efêmera) → Destino `22` (SSH)
* **Resultado:** Conexão estabelecida com sucesso e canal criptografado SSH iniciado logo após o handshake TCP.

\---

## 🧠 O que aprendi

* A estrutura e o encapsulamento de um pacote de rede.
* Como aplicar filtros para isolar tráfego de interesse no Wireshark.
* Como validar a conectividade de rede analisando requisições e respostas ICMP.
* A mecânica do **TCP 3-Way Handshake** (`SYN` -> `SYN/ACK` -> `ACK`) para garantia de entrega de dados.
* Como inspecionar cabeçalhos de enlace (MAC) e IP diretamente do frame capturado.

\---

## 🛡️ Relação com Cybersecurity

A análise de tráfego (Network Traffic Analysis) permite monitorar a saúde da rede e identificar comportamentos anômalos. Ela é essencial em atividades de SOC e DFIR para detectar varreduras ativas, tentativas de intrusão, conexões não autorizadas e exfiltração de dados.

\---

## 📸 Evidências do Dia 06

### Conectividade Bidirecional ICMP

!\[Comunicação de Rede Interna](week-02-comunicacaoredeinterna.png)

### Captura de Pacotes ICMP no Wireshark

!\[Captura ICMP no Wireshark](week-02-wireshark.png)

### Análise do TCP 3-Way Handshake (Porta 22)

!\[TCP 3-Way Handshake](week-02-3wayhandshake.png)

\---

# Dia 07 — Reconhecimento e Escaneamento com Nmap

## 🎯 Objetivo

Executar técnicas de reconhecimento de rede utilizando a ferramenta **Nmap** para descoberta de hosts ativos, mapeamento de portas e identificação de serviços no host alvo.

\---

## 🔬 Varreduras Executadas

```
# 1. Varredura padrão (1000 portas mais comuns sem resolução DNS)
nmap -n 10.10.10.10

# 2. Varredura com detecção de versão de serviço
nmap -sV -n 10.10.10.10
```

📊 Resultado da Investigação (Nmap Output)
Host Status: Up (Latência: 0.00063s)

Endereço MAC: 08:00:27:EE:8E:5F (Oracle VirtualBox virtual NIC)

Portas Analisadas: 1000 portas TCP testadas.

Estado das Portas: Todas as 1000 portas em estado closed (reset).

📸 Evidências do Dia 07
Execução de Reconhecimento com Nmap


✅ Checklist de Conclusão
\[x] Entendi o conceito de pacote

\[x] Fiz uma captura no Wireshark

\[x] Identifiquei ICMP

\[x] Identifiquei TCP

\[x] Identifiquei origem e destino

\[x] Identifiquei uma porta

\[x] Encontrei SYN

\[x] Encontrei SYN/ACK

\[x] Encontrei ACK

\[x] Entendi o 3-way handshake

\[x] Fiz uma pequena investigação

\[x] Registrei evidências

\[x] Atualizei o README

\[x] Fiz commit no GitHub



🎯 Esquema do Laboratório (CyberLab)

CYBERLAB

&#x20;       ┌───────────────┐
        │     KALI      │
        │   ANALISTA    │  (10.10.10.20)
        └───────┬───────┘
                │
         captura/análise / nmap
                │
                ▼
        ┌───────────────┐
        │    DEBIAN     │
        │     ALVO      │  (10.10.10.10)
        └───────────────┘

        ICMP → conectividade
        TCP  → comunicação
        SYN  → início
        ACK  → confirmação
        Wireshark / Nmap → investigação

