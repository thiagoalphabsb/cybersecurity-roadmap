# Dia 04 — Enumeração de Serviços e Superfície de Ataque

## 🎯 Objetivo
Investigar a relação entre processos, serviços, portas
e exposição de rede utilizando Debian e Kali Linux.

## 🖥️ Ambiente
- VirtualBox
- Debian — 10.10.10.10/24
- Kali Linux — 10.10.10.20/24
- Rede CyberLab

## 🔎 Ferramentas & Comandos
- systemctl
- ps
- ss
- lsof
- nmap
- nft
- ufw

## 🧪 Investigação

### Serviços no Debian
sshd (PID 2837) — systemctl status ssh confirmou active (running)

### Processos
ps aux | grep ssh → sshd rodando como root, PID 2837

### Portas escutando
ss -tulpn:
- 0.0.0.0:22 (sshd) — LISTEN
- 127.0.0.1:631 (cupsd) — LISTEN
- avahi-daemon em portas UDP diversas

### Nmap
nmap -sV -n --open 10.10.10.10:
22/tcp open ssh OpenSSH 10.0p2 Debian 7+deb13u4

## 🔐 Análise
A porta 631 (CUPS) está em LISTEN internamente, mas com bind em
127.0.0.1, portanto invisível para o Nmap executado do Kali.
A porta 22 (SSH) está em bind 0.0.0.0, sem firewall ativo (ufw
não instalado, nftables sem regras), portanto acessível de
qualquer ponto da rede 10.10.10.0/24.
Superfície de ataque externa real: apenas 1 porta (22/SSH).

## 🧠 O que aprendi
1. Bind determina de onde um serviço pode ser acessado, não apenas se ele "existe".
2. Superfície de ataque se mede pela exposição real, não pela quantidade de processos rodando.
3. ps, ss e lsof mostram ângulos diferentes do mesmo fenômeno (processo, porta, e a correlação entre os dois).
4. Um serviço aberto não é automaticamente uma vulnerabilidade — requer contexto, exposição e avaliação de configuração.
5.IP → TCP → Porta → Serviço
O IP identifica a máquina, o TCP é o protocolo de transporte que garante entrega confiável, a porta identifica qual serviço dentro daquela máquina deve receber os dados.
6.Estados de porta no Nmap:
- **OPEN** → tem processo escutando e aceitando conexões (seu SSH).
- **CLOSED** → a máquina respondeu, mas não há nada escutando ali — recebe RST (seu CUPS, visto de fora).
- **FILTERED** → o pacote foi descartado (silenciosamente ou não) por um firewall/filtro no caminho — o Nmap não consegue nem confirmar se está aberto ou fechado, porque não recebeu resposta nenhuma. Como você viu, sua rede não tem firewall, então esse estado não apareceu nos seus testes — mas é essencial saber reconhecê-lo depois.
7. Bind:
- `127.0.0.1` → só a própria máquina fala consigo mesma.
- `10.10.10.10` → um IP específico de uma interface real (se o cupsd escutasse aqui, só quem acessasse por *essa* interface chegaria nele).
- `0.0.0.0` → todas as interfaces da máquina ao mesmo tempo.

Se um processo estiver rodando, mas estiver vinculado somente a 127.0.0.1, ele necessariamente estará exposto para outras máquinas da rede? Por quê?

Processo → Serviço → Porta → Interface → Rede → Nmap

Processo é o programa rodando na memória o serviço SSH na porta 22 que esta en listen na rede pela interface 0.0.0.0 que foi detectada pela ferramenta Nmap. Se o processo estiver vinculado somente a 127.0.0.1 ele não fica exposto para outras máquinas por estar rodando em uma interface loopback, só conversa com ela mesmo.

## ⚠️ Observações
O laboratório foi realizado em ambiente virtual
controlado utilizando máquinas próprias.