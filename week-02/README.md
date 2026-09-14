\# 🛡️ Week 02 — Redes de Computadores, Análise de Tráfego \& Enumeração de Serviços



Este diretório contém a documentação completa, anotações de estudo e análises práticas de laboratório referentes à \*\*Week 02\*\* do programa de estudos em \*\*Cybersecurity \& Redes\*\*.



\---



\## 📁 Localização dos Arquivos de Origem



Os arquivos originais das anotações e práticas estão armazenados em `/cybersecurity-roadmap/docs/`:



\- `week 02 - day 01 e 02.txt`

\- `week 02 - day 03.txt`

\- `week 02 -day 04.md`

\- `week-02-day06-07.md`



\---



\## 📅 Estrutura do Conteúdo Semanal



| Dia | Arquivo | Tópico Principal | Resumo do Conteúdo |

| :--- | :--- | :--- | :--- |

| \*\*Dia 01 e 02\*\* | `week 02 - day 01 e 02.txt` | \*\*Fundamentos de Redes \& Camada de Transporte\*\* | Conceitos LAN/WAN/Internet, Arquitetura Cliente-Servidor, Endereçamento L2/L3 (MAC vs. IP), Máscaras de Rede, Gateway, Serviços DNS/DHCP, TCP vs. UDP e Fluxo de Acesso Web (Handshake 3-way, TLS, HTTP). |

| \*\*Dia 03\*\* | `week 02 - day 03.txt` | \*\*Análise de Interfaces \& DNS em Linux\*\* | Mapeamento de placas de rede físicas (`enp0s3` e `enp0s8`), roteamento e leitura de servidores DNS ativos no Debian (`/etc/resolv.conf`). |

| \*\*Dia 04\*\* | `week 02 -day 04.md` | \*\*Enumeração de Serviços \& Superfície de Ataque\*\* | Investigação de processos (`ps`, `ss`, `lsof`), conceito de IP Bind (`127.0.0.1` vs `0.0.0.0`), escaneamento Nmap no CyberLab e estados de porta. |

| \*\*Dia 06\*\* | `week-02-day06-07.md` | \*\*Análise de Tráfego com Wireshark\*\* | Captura de tráfego ICMP (ping) e inspeção do TCP 3-Way Handshake (`SYN` -> `SYN/ACK` -> `ACK`) na porta SSH (22). |

| \*\*Dia 07\*\* | `week-02-day06-07.md` | \*\*Reconhecimento \& Mapeamento com Nmap\*\* | Varreduras ativas de portas TCP, detecção de versões de serviço (`-sV`) e identificação de hosts ativos na rede local isolada. |



\---



\## 🏗️ Esquema do Laboratório (CyberLab)



```text

&#x20;                      CYBERLAB (Rede Isolada)

&#x20;                      

&#x20;       ┌───────────────┐               ┌───────────────┐

&#x20;       │  KALI LINUX   │               │    DEBIAN     │

&#x20;       │   ANALISTA    ├──────────────►│     ALVO      │

&#x20;       │ (10.10.10.20) │  Scans / Ping │ (10.10.10.10) │

&#x20;       └───────┬───────┘               └───────────────┘

&#x20;               │

&#x20;   Captura de Tráfego (Wireshark) / Escaneamento (Nmap)

```



🔍 Detalhamento dos Módulos



🌐 Dias 01 \& 02 — Fundamentos de Redes \& Protocolos

Arquitetura \& Redes: Diferenciação entre LAN (Rede Local), WAN (Rede Aberta/Longa Distância) e a Internet. Funcionamento do modelo Cliente-Servidor.



Endereçamento L2 vs. L3:



MAC Address (L2): Endereço físico gravado na placa de rede (NIC).



IP Address (L3): Endereço lógico roteável. Identificação de sub-rede via máscara (ex.: /24 ou 255.255.255.0) e saída de tráfego via Default Gateway.



Serviços Essenciais:



DNS (Porta 53 UDP/TCP): Resolução de nomes legíveis em endereços IP.



DHCP: Atribuição dinâmica de IP, máscara, gateway e DNS para novos hosts.



Camada de Transporte:



TCP: Orientado à conexão, confiável e ordenado (3-Way Handshake).



UDP: Sem conexão, leve e veloz (usado para streaming, jogos e DNS).



Anatomia de um Acesso Web (https://exemplo.com):



Resolução DNS via UDP 53.



Resolução do MAC do Gateway via protocolo ARP.



Estabelecimento de conexão TCP (Handshake de 3 vias na porta 443).



Negociação de chaves e criptografia via TLS/SSL.



Requisição HTTP (GET) e processamento da resposta pelo navegador.



🖥️ Dia 03 — Inspeção de Interfaces \& DNS no DebianLevantamento executado nas interfaces ativas do sistema Debian:Interfaces Físicas MapeadasInformaçãoPlaca 1 (enp0s3 - NAT / Internet)Placa 2 (enp0s8 - Rede Interna / Lab)Endereço IPv410.0.2.1510.10.10.10Máscara / Prefixo/24 (255.255.255.0)/24 (255.255.255.0)Gateway Padrão10.0.2.2Nenhum (Rede interna isolada)



Registros DNS (/etc/resolv.conf)

Domínio de Busca (search): saude.gov



Servidores DNS Primários (Ativos): 10.1.1.127, 10.1.2.11, 10.1.2.12



Servidores DNS Adicionais: 10.1.2.13, 10.1.2.14, 10.1.1.120, 10.1.1.12



Endereço IPv6 DNS: fd17:625c:f037:2::3

🎯 Dia 04 — Enumeração de Serviços \& Superfície de Ataque

Investigação de processos e serviços expostos no alvo Debian (10.10.10.10) a partir do Kali Linux (10.10.10.20).



Ferramentas Utilizadas

systemctl, ps, ss, lsof, nmap, nft, ufw



Achados da Enumeração

SSH (sshd):



PID: 2837 (executado como root).



Bind: 0.0.0.0:22 (Escutando em todas as interfaces).



Status Nmap: OPEN (22/tcp open ssh OpenSSH 10.0p2 Debian 7+deb13u4).



CUPS (cupsd):



Bind: 127.0.0.1:631 (Vinculado apenas ao loopback local).



Status Nmap: Invisível para conexões externas via rede.



Conceitos Relevantes

IP Bind: Vinculações em 127.0.0.1 garantem que o serviço só se comunique localmente. Para exposição na rede, utiliza-se o IP da interface ou 0.0.0.0 (todas as interfaces).



Superfície de Ataque: Calculada pelos serviços acessíveis externamente, e não apenas pelo número absoluto de processos rodando na máquina.



🦈 Dia 06 — Análise de Tráfego com Wireshark

Captura e análise profunda de pacotes no Kali Linux (10.10.10.20) interceptando conexões com o Debian (10.10.10.10).



Análises Executadas

Tráfego ICMP (Ping):



Filtro: icmp



Confirmou a conectividade bidirecional na Camada 3 (Rede) com envio de Echo Request e retorno de Echo Reply.



TCP 3-Way Handshake (SSH - Porta 22):



Filtro: tcp.port == 22



Fluxo registrado:



\[SYN] — Kali (10.10.10.20:59148) ➔ Debian (10.10.10.10:22) | Seq=0



\[SYN, ACK] — Debian (10.10.10.10:22) ➔ Kali (10.10.10.20:59148) | Seq=0 Ack=1



\[ACK] — Kali (10.10.10.20:59148) ➔ Debian (10.10.10.10:22) | Seq=1 Ack=1



🔎 Dia 07 — Reconhecimento e Escaneamento com Nmap

Mapeamento ativo da máquina alvo no CyberLab.



Comandos Executados



\# 1. Varredura padrão das 1000 portas mais comuns sem resolução DNS

nmap -n 10.10.10.10



\# 2. Detecção de versões dos serviços expostos

nmap -sV -n 10.10.10.10



Resultados

Host Status: Up (Latência: 0.00063s)



Endereço MAC: 08:00:27:EE:8E:5F (Oracle VirtualBox NIC)



Portas Abertas Identificadas: 22/tcp (OpenSSH)



Estados de Porta Nmap:



OPEN: Aceita conexões ativas.



CLOSED: Responde com pacote RST (sem serviço na porta).



FILTERED: Pacote bloqueado/descartado por regras de Firewall sem resposta.



✅ Checklist de Conclusão da Semana

\[x] Compreensão da estrutura e encapsulamento de pacotes



\[x] Captura de tráfego com Wireshark



\[x] Identificação de tráfego ICMP e TCP



\[x] Mapeamento de portas e conceitos de IP Bind



\[x] Análise detalhada do TCP 3-Way Handshake



\[x] Mapeamento de ativos e enumeração de serviços com Nmap



\[x] Documentação e atualização do arquivo README.md



⚠️ Observação Legal e de Ambiente

Todos os estudos, escaneamentos e capturas de pacotes foram executados exclusivamente em ambiente virtualizado e controlado (CyberLab / VirtualBox).

