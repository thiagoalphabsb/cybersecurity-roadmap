# 🛡️ Week 01 — Fundamentos de Computação, Linux e CyberLab

> Primeira semana do projeto **Cybersecurity Roadmap**  
> **Foco:** Fundamentos de hardware, virtualização, redes isoladas no VirtualBox, inspeção de processos no Linux e mentalidade investigativa.

---

## 🎯 Objetivo da Semana

Construir uma base técnica sólida para Cybersecurity, unindo teoria e prática:
1. **Fundamentos:** Entender a interação entre hardware, sistema operacional, memória e processos.
2. **Infraestrutura:** Criar a rede isolada do **CyberLab** no VirtualBox com Debian e Kali Linux.
3. **Análise de Processos & Investigação:** Praticar a observação, monitoramento e respostas a eventos no terminal Linux com foco em segurança.

---

## 📅 Progresso Diário

| Dia | Tema Principal | Foco Prático | Status |
|---|---|---|:---:|
| **Day 01** | Fundamentos de Computação & Hardware | CPU, RAM, armazenamento, OS e gerencia de VMs | 🟢 Concluído |
| **Day 02** | Virtualização, Redes Internas & Snapshots | Atribuição de IPs estáticos, interface de rede isolada e conectividade ICMP | 🟢 Concluído |
| **Day 03** | Linux Debian & Inspeção do Sistema | Comandos de inspeção (`ls`, `df`, `free`, `hostnamectl`) e inventário | 🟢 Concluído |
| **Day 04** | Sistemas Operacionais, Processos & `/proc` | Estrutura de PIDs/PPIDs e análise do diretório `/proc` | 🟢 Concluído |
| **Day 05** | Processos Linux & Investigação de Incidentes | Simulações de alto consumo, sinais (`SIGTERM`/`SIGKILL`) e investigação | 🟢 Concluído |
| **Day 06** | Revisão, Hardening & Documentação | Organização do portfólio no GitHub e consolidação das evidências | 🟢 Concluído |
| **Day 07** | Encerramento & Avaliação | Fechamento do relatório da semana e planejamento da Week 02 | 🟢 Concluído |

> **Status da Semana:** 🟢 **WEEK 01 CONCLUÍDA**

---

## 🧭 Evolução do Aprendizado

```text
  [ Hardware & OS ]
         ↓
  [ Virtualização ]
         ↓
 [ Redes Isoladas (Lab) ]
         ↓
  [ Linux / Terminal ]
         ↓
[ Análise de Processos ]
         ↓
 [ Coleta & Inspeção ]
         ↓
 [ Investigação / SOC ]
```

📚 Principais Competências Desenvolvidas

💻 Fundamentos & Hardware
Arquitetura: Interação entre CPU, memória RAM, disco e Kernel.

Sistemas Operacionais: Ciclo de vida de um processo, estados de execução, PIDs e PPIDs.

🖥️ Virtualização & Infraestrutura de Laboratório
VirtualBox: Criação, isolamento e gerenciamento de máquinas virtuais Debian 13 e Kali Linux.

Snapshots: Criação de pontos de restauração de segurança (BASE-LINUX-INSTALADO).

Arquitetura de Rede: Configuração dual-adapter (Placa 1 em NAT para acesso à internet / Placa 2 em Rede Interna CYBERLAB-INTERNAL para comunicação isolada).

🐧 Linux & Administração
Estrutura do Sistema: Navegação no sistema de arquivos e abstração do diretório /proc.

Análise do Sistema: Diagnóstico de recursos com free, df, hostnamectl e uname.

🔎 Investigação & Monitoramento
Análise de Processos: Inspeção avançada usando ps aux, ps -ef e top.

Encerramento de Processos: Controle e envio de sinais do Kernel (kill -15 SIGTERM e kill -9 SIGKILL).

Formulação de Hipóteses: Diagnóstico de anomalias (diferenciando consumo legítimo de comportamento suspeito).

## 🛠️ Comandos & Práticas do Laboratório

### 1. Comandos do Sistema e Redes

| Comando | Descrição / Finalidade | Aplicação no Laboratório |
| :--- | :--- | :--- |
| `hostnamectl` | Detalhes da VM e Kernel | Identificação da versão e arquitetura do Debian |
| `free -h` / `df -h` | Leitura de RAM e Disco | Análise de capacidade e recursos disponíveis |
| `ip addr` / `ip route` | Exibe placas e rotas de rede | Identificação dos adaptadores NAT e Rede Interna |
| `sudo ip addr add <IP/MÁSCARA> dev <IF>` | Atribui IP estático temporário | Atribuídos 10.10.10.10 (Debian) e 10.10.10.20 (Kali) |
| `sudo ip link set <IF> up` | Ativa a interface de rede | Habilita a placa interna para tráfego isolado |
| `ping -c 4 <DESTINO>` | Teste de conectividade ICMP | Validação de comunicação entre Kali e Debian (0% perda) |

2. Inspeção de Processos & Simulação
Simulação controlada de processo em segundo plano:
sleep 120 &
ps aux | grep sleep

Simulação de alto consumo de CPU:
yes > /dev/null &
top -b -n 1 | head -n 20
cat /proc/<PID>/status
ls -l /proc/<PID>/exe
kill -9 <PID>

🛡️ Mentalidade de Cybersecurity & Investigação
A principal habilidade cultivada nesta semana foi a análise orientada a evidências. Um processo consumindo elevado uso de CPU ou memória não é automaticamente malicioso.

Fluxo de Investigação Praticado:
[ Observar anomalia ]
        ↓
[ Identificar PID / Usuário ]
        ↓
[ Inspecionar /proc e binário ]
        ↓
[ Formular hipótese ]
        ↓
[ Validar impacto no sistema ]
        ↓
[ Tomar ação (Controle / Interrupção) ]

📸 Evidências do Laboratório
1. Visão Geral do VirtualBox
Painel de gerenciamento do VirtualBox exibindo as VMs configuradas para o CyberLab.

2. Status do Debian & Snapshot
Ponto de restauração BASE-LINUX-INSTALADO garantindo a integridade do ambiente.

3. Configuração de Rede Interna
Configuração do adaptador NAT e da rede interna isolada CYBERLAB-INTERNAL.

4. Teste de Conectividade entre VMs
Validação de comunicação ICMP do Debian (10.10.10.10) para o Kali Linux (10.10.10.20) com 0% de perda de pacotes.

## 📊 Avaliação de Desempenho — Week 01

| Área de Conhecimento | Avaliação | Status |
| :--- | :---: | :--- |
| Fundamentos de Hardware & OS | 5/5 | 🟢 Excelente |
| Virtualização & Snapshots | 5/5 | 🟢 Excelente |
| Redes Internas & Conectividade | 5/5 | 🟢 Concluído |
| Comandos Linux & Terminal | 5/5 | 🟢 Excelente |
| Análise de Processos & /proc | 5/5 | 🟢 Excelente |
| Raciocínio de Investigação | 5/5 | 🟢 Excelente |

Resultado Geral: 🟢 Base Consolidada

🧠 Retrospectiva & Lições Aprendidas
"Fundamentos fortes primeiro. Base de segurança solida depois."

🚀 Próximos Passos (Week 02)
Na Week 02, o roadmap continuará explorando:

Aprofundamento em arquitetura de redes (Modelos OSI e TCP/IP, sub-redes, portas e serviços).

Ferramentas de análise de pacotes e inspeção de rede (tcpdump, wireshark e nmap).

Práticas continuadas de administração e defesa no CyberLab.
EOF
