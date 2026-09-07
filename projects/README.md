# 🛠️ Projetos e Laboratórios Práticos (CyberLab)

Esta pasta concentra os projetos práticos, simulações de ambientes e laboratórios desenvolvidos ao longo da jornada de estudos em **Cybersecurity**. 

O objetivo principal é documentar a aplicação prática de conceitos de segurança da informação, análise de vulnerabilidades, hardening de sistemas e resposta a incidentes.

---

## 📌 Índice de Projetos

| Projeto | Categoria | Principais Ferramentas | Status |
| :--- | :--- | :--- | :--- |
| [Account Security Hygiene](./account-security-hygiene) | Hardening / IAM | Linux, PAM, Bash | 🟢 Concluído |
| [CyberLab] | Laboratório Virtual | VB, Linux, Virtual Machine | 🟡 Em andamento |

---

## 🔍 Detalhamento dos Projetos

### 1. Account Security Hygiene
* **Caminho:** [`/projects/account-security-hygiene`](./account-security-hygiene)
* **Objetivo:** Implementar políticas de boas práticas e fortalecimento de contas/usuários em ambiente Linux.
* **O que foi feito:**
  * Auditoria de permissões de usuários e grupos locais.
  * Configuração de políticas de senhas seguras e expiração.
  * Remoção de contas inativas e restrição de acessos administrativos (sudo).
* **Evidências & Documentação:** Veja a pasta [`/evidence`](../evidence) e os relatórios em [`/docs`](../docs).

### 2. CyberLab
🎯 Objetivo
Construir um ambiente controlado, isolado e reversível para realização de estudos, exercícios e projetos práticos relacionados à Segurança da Informação.
🌐 Rede
O ambiente conta com duas interfaces ativas em cada máquina:
Placa 1 (NAT): Acesso à Internet para atualização de pacotes e ferramentas.
Placa 2 (Rede Interna): Segmento isolado `CYBERLAB-INTERNAL` (`10.10.10.0/24`) para testes de conectividade e análise de tráfego.
IPs Estáticos
Debian (Server/Admin): `10.10.10.10/24` (`enp0s8`)
Kali Linux (Tester/Security): `10.10.10.20/24` (`eth1`)
🛡️ Princípios de Segurança
Utilizar somente ambientes próprios ou autorizados
Não utilizar credenciais reais
Não utilizar dados sensíveis
Manter snapshots antes de alterações importantes
Isolar máquinas vulneráveis de redes externas
Documentar alterações realizadas
Manter o laboratório reversível
📸 Evidências
As evidências de montagem do laboratório estão armazenadas em:
/evidence/day-02/

---

## 🧰 Estrutura Geral de Cada Projeto

Para manter a organização, cada projeto dentro desta pasta segue a estrutura padrão:

```text
nome-do-projeto/
├── README.md          # Documentação específica do projeto
├── scripts/           # Automações e scripts criados (Bash, Python, PowerShell)
└── configs/           # Arquivos de configuração ajustados