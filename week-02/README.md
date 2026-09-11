# 🛡️ Week 02 — Redes de Computadores & Enumeração de Serviços

Este diretório contém as anotações, análises práticas e documentações de laboratório referente à **Week 02** do programa de capacitação/estudos em **Cybersecurity & Redes**.

---

## 📁 Localização dos Arquivos

Todos os arquivos originais das anotações da semana estão salvos no caminho:
`/cybersecurity-roadmap/docs/`

- `week 02 - day 01 e 02.txt`[cite: 1]
- `week 02 - day 03.txt`[cite: 2]
- `week 02 -day 04.md`[cite: 3]

---

## 📅 Estrutura do Conteúdo

| Dia | Arquivo | Tópico Principal | Resumo do Conteúdo |
| :--- | :--- | :--- | :--- |
| **Dia 01 e 02** | `week 02 - day 01 e 02.txt`[cite: 1] | **Fundamentos de Redes & Camada de Transporte** | Conceitos de LAN/WAN/Internet, Arquitetura Cliente-Servidor, Endereçamento L2/L3 (MAC vs. IP), Sub-roteamento (Subnet Mask, Default Gateway), Serviços de Infraestrutura (DNS, DHCP), TCP vs. UDP, Portas de Rede e o Fluxo de Acesso Web (Handshake 3-way, TLS, HTTP)[cite: 1]. |
| **Dia 03** | `week 02 - day 03.txt`[cite: 2] | **Análise de Interfaces de Rede & Resolução DNS** | Configuração de interfaces físicas em ambiente Linux (Debian), mapeamento de IPs (`enp0s3` e `enp0s8`), roteamento local e levantamento de servidores DNS ativos (`/etc/resolv.conf`)[cite: 2]. |
| **Dia 04** | `week 02 -day 04.md`[cite: 3] | **Enumeração de Serviços & Superfície de Ataque** | Investigação de processos, vinculação de interfaces (Bind), análise de portas escutando (`ss`, `ps`, `lsof`), escaneamento de rede com `nmap` no Kali Linux e avaliação da superfície de ataque exposta[cite: 3]. |

---

## 🔍 Detalhamento dos Módulos

### 🌐 Dias 01 & 02 — Fundamentos de Redes & Protocolos

- **Arquitetura & Redes:** Diferenciação entre redes locais (LAN), redes de longa distância (WAN) e a Internet[cite: 1]. Modelo Cliente-Servidor na prática[cite: 1].
- **Endereçamento L2 vs. L3:**
  - **MAC Address:** Endereço físico gravado na NIC (Camada 2 - Enlace)[cite: 1].
  - **IPv4 & Subrede:** Endereço lógico (Camada 3 - Rede)[cite: 1]. Definição de rede/host via máscara de subrede (ex.: `/24`) e o papel do *Default Gateway*[cite: 1].
- **Serviços Essenciais:**
  - **DNS:** Resolução de nomes para IP (UDP/53)[cite: 1].
  - **DHCP:** Atribuição dinâmica de configurações de rede[cite: 1].
- **Camada de Transporte:**
  - **TCP:** Orientado à conexão, confiável (*3-Way Handshake*: `SYN` → `SYN-ACK` → `ACK`)[cite: 1].
  - **UDP:** Sem conexão, alta performance e baixa latência[cite: 1].
- **Anatomia do Acesso Web (`https://exemplo.com`):**
  1. Consulta ao cache local / Resolução DNS via UDP 53[cite: 1].
  2. Descoberta de MAC do Gateway via ARP[cite: 1].
  3. Estabelecimento de conexão TCP (Handshake de 3 vias na porta 443)[cite: 1].
  4. Handshake TLS/SSL (Criptografia)[cite: 1].
  5. Requisição HTTP (GET) e Renderização da resposta pelo navegador[cite: 1].

---

### 🖥️ Dia 03 — Inspeção de Interfaces & DNS em Ambiente Linux

Mapeamento efetuado nas interfaces ativas do sistema host/VM:

#### Interfaces Físicas Mapeadas

| Informação | Placa 1 (`enp0s3` - NAT / Internet) | Placa 2 (`enp0s8` - Rede Interna / Lab) |
| :--- | :--- | :--- |
| **Endereço IPv4** | `10.0.2.15`[cite: 2] | `10.10.10.10`[cite: 2] |
| **Máscara / Prefixo** | `/24` (`255.255.255.0`)[cite: 2] | `/24` (`255.255.255.0`)[cite: 2] |
| **Gateway Padrão** | `10.0.2.2`[cite: 2] | *Nenhum* (Rede isolada sem roteamento)[cite: 2] |

#### Registros DNS (`/etc/resolv.conf`)

- **Domínio de Busca (`search`):** `saude.gov`[cite: 2]
- **Servidores DNS Primários (Ativos):** `10.1.1.127`, `10.1.2.11`, `10.1.2.12`[cite: 2]
- **Servidores DNS Adicionais:** `10.1.2.13`, `10.1.2.14`, `10.1.1.120`, `10.1.1.12`[cite: 2]
- **Endereço IPv6 DNS:** `fd17:625c:f037:2::3`[cite: 2]

---

### 🎯 Dia 04 — Enumeração de Serviços & Superfície de Ataque

Investigação prática realizada no ambiente **CyberLab** utilizando **Debian** (Alvo - `10.10.10.10`) e **Kali Linux** (Atacante/Auditor - `10.10.10.20`)[cite: 3].

#### Ferramentas Utilizadas
`systemctl`, `ps`, `ss`, `lsof`, `nmap`, `nft`, `ufw`[cite: 3]

#### Achados da Enumeração
1. **SSH (`sshd`):**
   - **PID:** 2837 (Rodando como `root`)[cite: 3].
   - **Bind:** `0.0.0.0:22` (Escutando em todas as interfaces de rede)[cite: 3].
   - **Status Nmap:** `OPEN` (`22/tcp open ssh OpenSSH 10.0p2 Debian 7+deb13u4`)[cite: 3].
2. **CUPS (`cupsd`):**
   - **Bind:** `127.0.0.1:631` (Vinculado apenas ao loopback local)[cite: 3].
   - **Status Nmap:** Invisível / Não detectado externamente pelo Kali Linux[cite: 3].

#### Principais Conclusões & Conceitos Aprendidos
- **Conceito de Bind:** Define a visibilidade do serviço. Serviços vinculados a `127.0.0.1` só aceitam conexões locais e não ficam expostos para a rede externa[cite: 3].
- **Superfície de Ataque Real:** Medida pela exposição efetiva dos serviços na rede (`0.0.0.0` ou IP de interface externa), não apenas pela quantidade de processos ativos[cite: 3].
- **Estados de Porta no Nmap:**
  - **OPEN:** Processo escutando e aceitando conexões[cite: 3].
  - **CLOSED:** Máquina responde com `RST` (sem serviço ativo na porta)[cite: 3].
  - **FILTERED:** Pacotes descartados por regras de firewall (sem resposta)[cite: 3].

---

## ⚠️ Ambiente de testes
Todos os testes e escaneamentos de enumeração foram realizados em um ambiente virtualizado e controlado (**VirtualBox / CyberLab**)[cite: 3].