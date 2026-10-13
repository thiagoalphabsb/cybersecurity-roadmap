# 🧪 Laboratório: Redes de Computadores, Análise de Tráfego & Enumeração (Semana 02)

> **Módulo / Categoria:** Redes, Análise de Tráfego & Enumeração de Serviços  
> **Data de Execução:** 20/08/2026  
> **Status:** 🟢 Concluído  

---

## 🎯 1. Objetivo do Laboratório

Aprofundar os conhecimentos em **Redes de Computadores sob a perspectiva de Cibersegurança Defensiva e Análise de Tráfego**, evoluindo dos conceitos de arquitetura e endereçamento até a captura ativa de pacotes e escaneamento de serviços em ambiente isolado.

- **Arquitetura & Endereçamento:** Mapeamento de Camada 2 (MAC) e Camada 3 (IP), subredes, gateways e análise de arquivos de configuração de rede (`/etc/resolv.conf`).
- **Análise de Tráfego com Wireshark:** Inspeção prática do tráfego ICMP (*Echo Request / Reply*) e captura detalhada do **TCP 3-Way Handshake** (`SYN` → `SYN-ACK` → `ACK`) na porta do SSH.
- **Enumeração & Superfície de Ataque:** Mapeamento de processos escutando interfaces (`ss`, `ps`, `lsof`), conceitos de *IP Bind* (`127.0.0.1` vs `0.0.0.0`) e escaneamento de serviços via **Nmap**.

---

## 🖥️ 2. Ambiente & Ferramentas

| Recurso / Elemento | Especificação / Detalhe |
| :--- | :--- |
| **Ativo Target (Alvo)** | `CyberLab-Debian` (Debian GNU/Linux 13 — `10.10.10.10/24`) |
| **Ativo Tester (Auditoria)** | `CyberLab-Kali` (Kali Linux — `10.10.10.20/24`) |
| **Rede Virtualizada** | Subrede isolada Host-Only (`CYBERLAB-INTERNAL` — `10.10.10.0/24`) |
| **Ferramentas Utilizadas** | Wireshark, Nmap, OpenSSH, `ss`, `ps`, `lsof`, `systemctl`, `ping` |

---

## 🏗️ Topologia da Rede Isolada (CyberLab)

```text
                        CYBERLAB (Rede Interna Isolada)
                                (10.10.10.0/24)
                                       │
            ┌──────────────────────────┴──────────────────────────┐
            │                                                     │
     CyberLab-Kali                                         CyberLab-Debian
      (Kali Linux)                                          (Debian 13)
      10.10.10.20/24                                       10.10.10.10/24
(Wireshark / Scans / Nmap)                              (Serviços / Target)

```

---

## 🛠️ 3. Procedimento & Execução

### Passo 1: Mapeamento de Interfaces & DNS

Inspeção das placas de rede e do arquivo de resolução de nomes no servidor Debian:

```bash
# Inspecionar interfaces de rede e endereçamento
ip a
ip route

# Verificar servidores DNS e sufixo de busca configurados
cat /etc/resolv.conf

```

### Passo 2: Enumeração de Processos e IP Bind

Análise dos sockets ativos e portas escutando no sistema:

```bash
# Listar portas TCP e UDP escutando no sistema
ss -tuln
ps aux | grep sshd

# Verificar serviços vinculados apenas ao loopback local vs todas as interfaces
lsof -i :22
lsof -i :631

```

### Passo 3: Captura de Tráfego com Wireshark (Kali Linux)

Captura de pacotes da rede interna filtrando a comunicação entre o Kali (`10.10.10.20`) e o Debian (`10.10.10.10`):

```bash
# 1. Testar conectividade ICMP
ping -c 4 10.10.10.10

# 2. Iniciar conexão SSH para captura do Handshake TCP
ssh debian@10.10.10.10

```

### Passo 4: Escaneamento Ativo de Serviços com Nmap

Mapeamento de portas abertas e detecção de versões de serviço:

```bash
# Scan de portas TCP mais comuns
nmap -n 10.10.10.10

# Detecção de versão dos serviços expostos
nmap -sV -n 10.10.10.10

```

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

## 🔍 5. Conclusões & Aprendizados

* **Diferenciação de IP Bind:** A análise provou que serviços vinculados a `127.0.0.1` (como o CUPS na porta 631) não ficam expostos à rede externa, enquanto serviços em `0.0.0.0` (como o OpenSSH na porta 22) compõem a superfície de ataque pública do host.
* **Validação do Handshake TCP:** A inspeção no Wireshark confirmou a exatidão das três etapas de sincronização do protocolo TCP antes da troca de dados criptografados da sessão SSH.
* **Mapeamento Defensivo:** O Nmap permitiu verificar exatamente o que um atacante visualizaria na rede local, permitindo validar as regras de firewall e minimizar a exposição desnecessária de serviços.

---

## 🔗 Projetos e Links Relacionados

* 🖥️ [Laboratório Prático de Network Analysis](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/network-analysis)
* 🧪 [CyberLab Infrastructure](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/cyberlab)
* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap)

