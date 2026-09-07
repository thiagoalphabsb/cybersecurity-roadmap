# Comandos Aprendidos — Dia 02 (Rede e Diagnóstico no Linux)

| Comando | Para que serve | O que observei no laboratório |
| :--- | :--- | :--- |
| `pwd` | Mostra o diretório atual | Identifica a pasta de trabalho atual |
| `ls -la` | Lista todos os arquivos com detalhes | Exibe permissões, donos e arquivos ocultos |
| `ps` | Mostra os processos da sessão atual | Visão simplificada dos processos no terminal |
| `ps aux` | Lista todos os processos do sistema | Exibe usuário, PID, consumo de CPU e RAM |
| `df -h` | Mostra uso do disco/sistema de arquivos | Exibe espaço livre em GB de forma legível |
| `free -h` | Mostra utilização da memória RAM e Swap | Exibe RAM total, em uso e disponível |
| `hostnamectl` | Mostra detalhes do sistema e hostname | Exibe nome da VM, Kernel, Arquitetura e SO |
| `ip addr` | Lista as interfaces de rede e seus IPs | Mostra os IPs das placas NAT e Rede Interna |
| `ip route` | Exibe a tabela de roteamento e gateway | Identifica a rota padrão (`default via 10.0.2.2`) |
| `sudo ip addr add <IP/MÁSCARA> dev <INTERFACE>` | Atribui um IP estático temporário | Configurado `10.10.10.10` (Debian) e `10.10.10.20` (Kali) |
| `sudo ip link set <INTERFACE> up` | Ativa a interface de rede | Habilita a placa interna para tráfego de pacotes |
| `ping -c <QTD> <DESTINO>` | Testa a conectividade (ICMP) | Validou 0% de perda entre Kali e Debian na rede isolada |
