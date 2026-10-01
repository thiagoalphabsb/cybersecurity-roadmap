# 🌐 Network Analysis — Análise de Redes e Tráfego

## Objetivo

Investigar o comportamento de uma rede e correlacionar informações de rede, transporte e aplicação com serviços e processos executados nos hosts.

## Técnicas e ferramentas

- IPv4
- ICMP
- TCP
- UDP
- DNS
- ARP
- MAC
- Nmap
- Wireshark
- ip
- ss
- ping
- systemctl
- nftables

## Linha de investigação

1. Qual é o host?
2. Qual é o endereço IP?
3. Qual é o MAC?
4. Qual protocolo está sendo utilizado?
5. Qual porta está envolvida?
6. Qual serviço responde?
7. Qual processo está associado?
8. Existe alguma regra de firewall interferindo?
9. O tráfego observado confirma a hipótese?

## Exemplos práticos

### Enumeração

O Nmap foi utilizado para identificar portas abertas e serviços disponíveis.

### Sockets e processos

Ferramentas Linux foram utilizadas para relacionar portas em escuta aos processos e serviços responsáveis por elas.

### Wireshark

A análise de pacotes permitiu observar resolução DNS, comunicação TCP, estabelecimento de conexão e tráfego entre hosts.

### ARP

A análise de ARP permitiu relacionar endereços IP e MAC dentro da rede local.

### Firewall

Foram realizados testes com nftables, incluindo regras de aceitação e descarte, observando o efeito das regras sobre o tráfego.

## Modelo de análise

**Evento → evidência → hipótese → validação → correlação → conclusão**

## Evidências

[Evidence](../../evidence/)

## Competências demonstradas

- Network troubleshooting
- Network security
- TCP/IP
- Packet analysis
- DNS
- ARP
- Port enumeration
- Firewall
- Linux networking
- Investigação baseada em evidências

## Relação com Cibersegurança

A análise de redes é uma competência fundamental para identificar exposição de serviços, compreender tráfego e apoiar investigações de incidentes.