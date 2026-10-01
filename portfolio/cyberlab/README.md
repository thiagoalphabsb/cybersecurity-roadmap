# 🧪 CyberLab — Laboratório de Cibersegurança

## Objetivo

Construir um ambiente controlado para praticar fundamentos de Cibersegurança, Linux, redes, enumeração e investigação técnica.

## Ambiente

- Debian
- Kali Linux
- VirtualBox
- Rede interna do laboratório
- SSH
- Nmap
- Ferramentas nativas de Linux

## Atividades realizadas

### Preparação do ambiente

Configuração das máquinas virtuais, interfaces de rede e comunicação entre os hosts.

Topologia utilizada durante os laboratórios:

- Kali Linux → 10.10.10.20/24
- Debian → 10.10.10.10/24

### Enumeração

O Nmap foi utilizado para identificar portas TCP acessíveis no host Debian. Durante a evolução do laboratório, a porta **22/tcp** foi identificada como aberta e associada ao serviço SSH.

### Correlação técnica

A investigação foi além da identificação da porta, relacionando:

**IP → porta → socket → serviço → processo**

## Competências demonstradas

- Virtualização
- Linux
- TCP/IP
- IPv4
- SSH
- Nmap
- Enumeração
- Análise de serviços
- Investigação técnica
- Documentação de evidências

## Evidências

[Evidence](../../evidence/)

## Resultado

O CyberLab tornou-se a base prática para os exercícios posteriores de redes, serviços, firewall, análise de tráfego e segurança.

## Próximos passos

- Windows e Active Directory
- Vulnerability Management
- SOC
- SIEM
- Incident Response
- DFIR
- Cloud Security