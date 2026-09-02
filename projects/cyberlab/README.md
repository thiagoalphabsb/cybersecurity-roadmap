# 🧪 CyberLab v1.0

Laboratório virtual criado para apoiar a jornada de estudos em Cybersecurity.

## 🎯 Objetivo

Construir um ambiente controlado, isolado e reversível para realização de estudos, exercícios e projetos práticos relacionados à Segurança da Informação.

## 🏗️ Ambiente Atual

| Componente   | Configuração                     |
| ------------ | -------------------------------- |
| Hypervisor   | VirtualBox                       |
| VMs          | Debian 13 Trixie e Kali Linux    |
| CPU (Debian) | 2 cores                          |
| RAM (Debian) | 4 GB                             |
| Disco        | 30 GB (Debian) / 79 GB (Kali)    |
| Redes        | Adaptador 1: NAT <br> Adaptador 2: Rede Interna (`CYBERLAB-INTERNAL`) |

## 🌐 Rede

O ambiente conta com duas interfaces ativas em cada máquina:
- **Placa 1 (NAT):** Acesso à Internet para atualização de pacotes e ferramentas.
- **Placa 2 (Rede Interna):** Segmento isolado `CYBERLAB-INTERNAL` (`10.10.10.0/24`) para testes de conectividade e análise de tráfego.

### IPs Estáticos
- **Debian (Server/Admin):** `10.10.10.10/24` (`enp0s8`)
- **Kali Linux (Tester/Security):** `10.10.10.20/24` (`eth1`)

## 🛡️ Princípios de Segurança

* Utilizar somente ambientes próprios ou autorizados
* Não utilizar credenciais reais
* Não utilizar dados sensíveis
* Manter snapshots antes de alterações importantes
* Isolar máquinas vulneráveis de redes externas
* Documentar alterações realizadas
* Manter o laboratório reversível

## 📸 Evidências

As evidências de montagem do laboratório estão armazenadas em:

```text
week-01/evidence/day-02/

🚀 Próximas Expansões
[x] Configurar rede interna

[x] Adicionar segunda máquina Linux (Kali)

[ ] Adicionar Windows

[ ] Criar servidor de serviços

[ ] Criar ambiente de testes Web

[ ] Implementar monitoramento

[ ] Implementar SIEM

[ ] Criar laboratório SOC

[ ] Criar laboratório DFIR

[ ] Criar ambiente Cloud Security

Status: 🟢 Laboratório v1.0 operacional e testado

Projeto: Cybersecurity Roadmap — 24 semanas
