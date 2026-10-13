# 🧪 Laboratório: Virtualização & Provisionamento do CyberLab (Semana 02)

> **Módulo / Categoria:** Infraestrutura, Virtualização & Segurança Defensiva  
> **Data de Execução:** 01/09/2026  
> **Status:** 🟢 Concluído  

---

## 🎯 1. Objetivo da Semana

A **Semana 02** teve como foco a construção e o provisionamento inicial do **CyberLab**, o ambiente de simulação virtualizado e isolado que serve de base para os exercícios práticos do roadmap.

- **Engenharia de Virtualização:** Configuração do Oracle VirtualBox, alocação de vCPUs, memória RAM e discos virtuais dinâmicos (VDI).
- **Isolamento de Rede:** Criação e validação da rede interna isolada (*CYBERLAB-INTERNAL*) na faixa `10.10.10.0/24`, impedindo qualquer impacto na rede física ou na internet.
- **Gerenciamento de Estado (Snapshots):** Criação de pontos de restauração virgens (*Clean Baselines*) em cada VM para permitir *rollback* rápido após simulações de testes ou alterações de configuração.
- **Provisionamento Linux:** Instalação e configuração inicial das máquinas **CyberLab-Debian** (servidor de aplicação/serviços) e **CyberLab-Kali** (estação de auditoria e análise de segurança).

---

## 🏗️ 2. Arquitetura & Topologia da Rede Interna

O ambiente é totalmente contido no host físico (Windows 11) e utiliza interfaces em ponte/NAT apenas para atualizações pontuais, mantendo uma interface secundária conectada ao switch virtual da rede interna do laboratório.

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
 (Servidor / SysAdmin / Target)                (Auditoria / SOC / Tester)

```

---

## 🖥️ 3. Matriz de Ativos do Laboratório (Semana 02)

| VM / Hostname | Sistema Operacional | Função / Papel no Lab | IP Interno | Recursos (RAM / Disco) | Snapshot Baseline |
| --- | --- | --- | --- | --- | --- |
| **CyberLab-Debian** | Debian GNU/Linux 13 | Servidor Target / Serviços | `10.10.10.10/24` | 3.8 GB / 30 GB VDI | `BASE-LINUX-INSTALADO` |
| **CyberLab-Kali** | Kali Linux Rolling | Estação de Auditoria & SOC | `10.10.10.20/24` | 2.0 GB / 79 GB VDI | `CYBERLAB-CLEAN-01` |

> *Nota: O ecossistema do laboratório foi expandido nas semanas posteriores (Semanas 05 e 06) com a inclusão da VM `DC01` (Windows Server 2025 Datacenter / Active Directory).*

---

## 🛠️ 4. Procedimento & Passo a Passo de Execução

### Passo 1: Configuração do VirtualBox & Rede Interna

Criação do switch virtual isolado para permitir a comunicação entre as VMs sem roteamento para a interface física:

1. Acesso a **VirtualBox ➔ Gerenciador de Redes de Host / Redes Internas**.
2. Definição do nome da rede interna: `CYBERLAB-INTERNAL`.
3. Configuração do adaptador secundário de cada VM para **Rede Interna** (*Internal Network*).

### Passo 2: Instalação e Hardening do Debian (`CyberLab-Debian`)

* Instalação limpa do Debian 13 (x86-64).
* Configuração do hostname `debian` e atribuição do IP estático `10.10.10.10/24` na interface `enp0s8`.
* Instalação e verificação do serviço OpenSSH para testes de conectividade e análise de tráfego.

### Passo 3: Configuração da Estação de Auditoria (`CyberLab-Kali`)

* Importação do appliance Kali Linux.
* Configuração do IP estático `10.10.10.20/24` na interface `eth1` atrelada à `CYBERLAB-INTERNAL`.
* Validação das ferramentas nativas de análise (`Nmap`, `Wireshark`, `OpenSSH`).

### Passo 4: Validação de Conectividade & Gestão de Snapshots

* Teste de comunicação bidirecional via `ping` entre `10.10.10.10` e `10.10.10.20`.
* Criação de imagens de estado de todas as máquinas virtuais após a instalação e teste inicial de conectividade:
```bash
# Validação da criação dos snapshots no VirtualBox para ambiente limpo
VBoxManage snapshot "CyberLab-Linux" take "BASE-LINUX-INSTALADO"
VBoxManage snapshot "kali-linux-2026.2" take "CYBERLAB-CLEAN-01"

```

---

## 📸 5. Relatório de Evidências Práticas (Virtualização & Rede)

### 1. Painel do Oracle VirtualBox & Ativos Provisionados
![week-02-vms-virtualbox.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/vms-virtualbox.png)

* **O que a imagem demonstra:** Visão geral do Oracle VirtualBox Gerenciador com o ativo Debian em execução e os appliances configurados para a topologia do laboratório.
* **Resultado:** Validação do provisionamento dos hipervisores e suporte de execução para o CyberLab.

---

### 2. Ponto de Restauração Baseline (Snapshot Debian)
![week-02-day-02-snapshot-debian.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/day-02-snapshot-debian.png)

* **O que a imagem demonstra:** Registro e criação do Snapshot BASE-LINUX-INSTALADO na VM Debian.
* **Resultado:** Ponto de restauração limpo (Clean Baseline) estabelecido em 01/09/2026, garantindo a capacidade de rollback rápido do sistema após testes ou falhas.

---

### 3. Teste de Comunicação em Rede Interna (Debian ↔ Kali)
![week-02-comunicacaoredeinterna.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-comunicacaoredeinterna.png)

* **O que a imagem demonstra:** Teste bidirecional de conectividade em Camada 3 (Network Layer) utilizando o utilitário `ping` entre os dois ativos da rede isolada do CyberLab.
* **Comandos Executados:**
  - No host `Debian` (`10.10.10.10`): `ping -c 4 10.10.10.20`
  - No host `Kali` (`10.10.10.20`): `ping -c 4 10.10.10.10`
* **Resultado:** 0% de perda de pacotes (*0% packet loss*) e latência média inferior a `1ms`, confirmando a correta configuração do switch virtual isolado (*Host-Only Network*).

---

### 4. Análise do TCP 3-Way Handshake & Sessão SSH
![week-02-3wayhandshake.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-3wayhandshake.png)

* **O que a imagem demonstra:** Captura profunda da negociação da sessão TCP e estabelecimento de túnel criptografado SSHv2 entre o Kali (`10.10.10.20`) e o Debian (`10.10.10.10`).
* **Análise dos Pacotes (TCP 3-Way Handshake):**
  1. **Frame 1 (`SYN`):** `10.10.10.20:59148` ➔ `10.10.10.10:22` | `Seq=0`
  2. **Frame 2 (`SYN, ACK`):** `10.10.10.10:22` ➔ `10.10.10.20:59148` | `Seq=0 Ack=1`
  3. **Frame 3 (`ACK`):** `10.10.10.20:59148` ➔ `10.10.10.10:22` | `Seq=1 Ack=1`
* **Desdobramento:** Sequência imediata de troca de chaves SSHv2 (*Key Exchange Init*, *PQ/T Hybrid Key Exchange*) e ativação de mensagens encriptadas (*New Keys / Encrypted packet*).

---

### 5. Reconhecimento & Escaneamento de Serviços com Nmap
![week-02-nmap-reconhecimento.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week02/week-02-nmap-reconhecimento.png)

* **O que a imagem demonstra:** Execução de varreduras ativas de portas no host alvo `10.10.10.10` a partir da estação de auditoria Kali.
* **Comandos Executados & Análise:**
  - `nmap -n 10.10.10.10`: Varredura rápida das portas TCP mais comuns (confirmando host ativo com MAC `08:00:27:EE:8E:5F`).
  - `nmap -sV -n 10.10.10.10`: Varredura de detecção de serviços e versões.
* **Resultado para Análise Defensiva:** Identificação das respostas de reset TCP (*Not shown: 1000 closed tcp ports (reset)*), indicando que portas sem serviço ativo rejeitam conexões explicitamente via pacote `RST`.
---

## 🔍 6. Conclusões & Aprendizados

* **Segurança por Isolamento:** A utilização de uma rede interna isolada (*CYBERLAB-INTERNAL*) garante total liberdade para execução de escaneamentos com Nmap, testes de serviços e auditorias sem risco de vazamento de tráfego para a rede física.
* **Garantia de Reprodutibilidade:** O uso rigoroso de snapshots baseline permite reverter alterações ou arquivos corrompidos em segundos, mantendo a consistência do laboratório ao longo de todo o roadmap.
* **Validação de Comunicação L3:** A confirmação do tráfego bidirecional entre o Debian e o Kali validou o ambiente para o início das práticas de redes e segurança de sistemas.

---

## 🔗 Projetos e Links Relacionados

* 🖥️ [Laboratório Prático de Network Analysis](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/network-analysis)
* 🧪 [CyberLab Infrastructure](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/cyberlab)
* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/cybersecurity-roadmap)

