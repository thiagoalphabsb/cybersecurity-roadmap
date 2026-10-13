# 📸 Evidências Técnicas — Redes, Análise de Tráfego & Enumeração (Semana 02)

> Repositório de evidências visuais e relatórios de execução prática da **Semana 02** do CyberLab, cobrindo testes de conectividade de rede interna, captura de pacotes ICMP, inspeção do **TCP 3-Way Handshake** no Wireshark e escaneamento ativo de serviços com Nmap.

---

## 🎯 Sumário do Laboratório

1. [Teste de Comunicação em Rede Interna (Debian ↔ Kali)](#1-teste-de-comunicação-em-rede-interna-debian--kali)
2. [Captura e Análise de Tráfego ICMP no Wireshark](#2-captura-e-análise-de-tráfego-icmp-no-wireshark)
3. [Análise do TCP 3-Way Handshake & Sessão SSH](#3-análise-do-tcp-3-way-handshake--sessão-ssh)
4. [Reconhecimento & Escaneamento de Serviços com Nmap](#4-reconhecimento--escaneamento-de-serviços-com-nmap)

---

## 📸 Relatório de Evidências Práticas

### 1. Teste de Comunicação em Rede Interna (Debian ↔ Kali)
![week-02-comunicacaoredeinterna.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-comunicacaoredeinterna.png)

* **O que a imagem demonstra:** Teste bidirecional de conectividade em Camada 3 (Network Layer) utilizando o utilitário `ping` entre os dois ativos da rede isolada do CyberLab.
* **Comandos Executados:**
  - No host `Debian` (`10.10.10.10`): `ping -c 4 10.10.10.20`
  - No host `Kali` (`10.10.10.20`): `ping -c 4 10.10.10.10`
* **Resultado:** 0% de perda de pacotes (*0% packet loss*) e latência média inferior a `1ms`, confirmando a correta configuração do switch virtual isolado (*Host-Only Network*).

---

### 2. Captura e Análise de Tráfego ICMP no Wireshark
![week-02-wireshark.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-wireshark.png)

* **O que a imagem demonstra:** Intercepção em tempo real dos pacotes ICMP no Wireshark na interface `eth1` da máquina Kali (`10.10.10.20`).
* **Filtro Aplicado:** `icmp`
* **Análise do Fluxo Confirmada:**
  - Sequência perfeita de pares **Echo (ping) request** (origem `10.10.10.20` para `10.10.10.10`) e **Echo (ping) reply** (resposta de `10.10.10.10` para `10.10.10.20`).
  - Inspeção de cabeçalhos mostrando tamanho do quadro (`98 bytes on wire`) e payload contendo a sequência de bytes padrão do ICMP.

---

### 3. Análise do TCP 3-Way Handshake & Sessão SSH
![week-02-3wayhandshake.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-3wayhandshake.png)

* **O que a imagem demonstra:** Captura profunda da negociação da sessão TCP e estabelecimento de túnel criptografado SSHv2 entre o Kali (`10.10.10.20`) e o Debian (`10.10.10.10`).
* **Análise dos Pacotes (TCP 3-Way Handshake):**
  1. **Frame 1 (`SYN`):** `10.10.10.20:59148` ➔ `10.10.10.10:22` | `Seq=0`
  2. **Frame 2 (`SYN, ACK`):** `10.10.10.10:22` ➔ `10.10.10.20:59148` | `Seq=0 Ack=1`
  3. **Frame 3 (`ACK`):** `10.10.10.20:59148` ➔ `10.10.10.10:22` | `Seq=1 Ack=1`
* **Desdobramento:** Sequência imediata de troca de chaves SSHv2 (*Key Exchange Init*, *PQ/T Hybrid Key Exchange*) e ativação de mensagens encriptadas (*New Keys / Encrypted packet*).

---

### 4. Reconhecimento & Escaneamento de Serviços com Nmap
![week-02-nmap-reconhecimento.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-nmap-reconhecimento.png)

* **O que a imagem demonstra:** Execução de varreduras ativas de portas no host alvo `10.10.10.10` a partir da estação de auditoria Kali.
* **Comandos Executados & Análise:**
  - `nmap -n 10.10.10.10`: Varredura rápida das portas TCP mais comuns (confirmando host ativo com MAC `08:00:27:EE:8E:5F`).
  - `nmap -sV -n 10.10.10.10`: Varredura de detecção de serviços e versões.
* **Resultado para Análise Defensiva:** Identificação das respostas de reset TCP (*Not shown: 1000 closed tcp ports (reset)*), indicando que portas sem serviço ativo rejeitam conexões explicitamente via pacote `RST`.

---

## 🛡️ Tabela de Ferramentas & Aplicação em Investigação / SOC

| Ferramenta / Protocolo | Função Executada | Aplicação Técnica em SOC / Blue Team |
| :---: | :--- | :--- |
| **Ping / ICMP** | Verificação de conectividade L3 | Diagnóstico básico de alcance de rede e detecção de bloqueios por firewall |
| **Wireshark** | Captura e inspeção de quadros/pacotes | Análise detalhada de tráfego, verificação de Handshakes TCP e depuração de protocolos |
| **TCP 3-Way Handshake** | Estabelecimento de sessão orientada à conexão | Identificação de varreduras *SYN Scan* e tentativas de abuso de recursos (*SYN Flood*) |
| **Nmap (`-sV`)** | Mapeamento ativo de portas e versões | Mapeamento de superfície de ataque e identificação de serviços desatualizados/vulneráveis |

---

## 🔗 Projetos Relacionados

* 🖥️ [Laboratório Prático de Network Analysis](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/network-analysis)
* 🧪 [CyberLab Infrastructure](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/portfolio/cyberlab)
* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)
