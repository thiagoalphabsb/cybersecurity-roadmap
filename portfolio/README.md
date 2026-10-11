# 🛡️ Thiago Souza Silva | Cybersecurity & SOC Analyst Portfolio

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/thiago-souza-silva-5607223aa/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/thiagoalphabsb)
[![Location](https://img.shields.io/badge/Location-Brasília%2C%20DF-blue?style=for-the-badge&logo=googlemaps&logoColor=white)](#)

---

## 👨‍💻 Sobre Mim

Profissional em transição de carreira de **Suporte Local N2** para **Análise de Cibersegurança / Operações SOC (Blue Team)**. Graduando em **Segurança da Informação**, utilizo minha sólida experiência prática em suporte, administração de sistemas Windows/Linux e infraestrutura de rede para construir soluções defensivas e conduzir análises de segurança baseadas em evidências.

- 🎓 **Formação:** Graduando em Segurança da Informação
- 📜 **Certificações & Cursos:** Google Cybersecurity Professional Certificate, Cisco Networking Academy, Solyd Pentest 2.0, FIAP Cloud Fundamentals
- 🎯 **Foco Principal:** Monitoramento de Segurança (SOC), Segurança em Active Directory, Análise de Tráfego de Rede e Higiene de Identidades (IAM).

---

## ⚡ Destaques & Evidências Visuais (Highlights)

> *Evidências práticas extraídas dos ambientes de laboratório no CyberLab.*

| Windows Server 2025 & Active Directory | Análise de Tráfego com Wireshark |
| :---: | :---: |
| ![GPO Windows Server](https://github.com/thiagoalphabsb/cybersecurity-portfolio/blob/main/assets/10-day05-GPO-WSB.png) <br><sub>*Criação de GPO `GPO-Workstations-Security-Baseline`, vínculo na OU e configuração de auditoria via PowerShell*</sub> | ![Análise Wireshark SSH](https://github.com/thiagoalphabsb/cybersecurity-portfolio/blob/main/assets/week04-day02-wireshark3way.png) <br><sub>*Captura e inspeção de pacotes SSH (`tcp.port == 22`) entre Kali e Debian no Wireshark*</sub> |

---

## 🚀 Projetos Principais

Uma visão estruturada dos principais projetos desenvolvidos para demonstrar competências práticas em segurança defensiva, infraestrutura, análise de dados e desenvolvimento de software:

---

### 🎯 1. Cybersecurity Roadmap (Projeto Principal — 24 Semanas)
* **Problema:** Estruturar um plano contínuo e metódico para migração de carreira de Suporte Local N2 para Cibersegurança / Blue Team.
* **Solução:** Roadmap prático dividido em 24 semanas cobrindo Redes, Linux, Windows Server, Active Directory, Python, Análise de Tráfego e Investigação de Alertas.
* **Resultado Validado:** Semanas 1 a 6 concluídas com documentação detalhada, relatórios de análise de pacotes e evidências de laboratório.
* 🔗 [Ver Repositório do Roadmap](https://github.com/thiagoalphabsb/Cybersecurity-Roadmap)

---

### 🖥️ 2. Windows Server 2025 — Active Directory & Security Baseline
* **Problema:** Necessidade de simular uma infraestrutura corporativa real para gerenciar identidades centralizadas e aplicar controles defensivos de acesso.
* **Solução:** Provisionamento do Controlador de Domínio (`DC01` / `corp.thiago.lab`) em Windows Server 2025 com serviços AD DS, DNS e Kerberos, estruturação de OUs, modelo IAM (*Least Privilege*) e aplicação de GPOs de auditoria e baseline de segurança.
* **Resultado Validado:**
  - Aplicação e validação de GPO (`GPO-Workstations-Security-Baseline`) vinculada à OU de estações de trabalho.
  - Habilitação de políticas de auditoria local (`auditpol`) para monitoramento de *Logon*, *User Account Management* e eventos críticos (Event IDs 4624, 4625, 4740).
* 🔗 [Abrir Projeto Windows Server 2025](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/projects/windows-server-2025)

---

### 🧪 3. CyberLab — Laboratório Virtual Isolado
* **Problema:** Mapear e testar vetores de ataque e mecanismos defensivos em um ambiente seguro, sem riscos para redes externas ou de produção.
* **Solução:** Construção de uma topologia de rede virtualizada e isolada (Host-Only Virtual Switch) integrando Windows Server 2025, estações clientes Windows e instâncias Kali Linux e Debian para testes de segurança e análise de tráfego.
* **Resultado Validado:**
  - Inspeção e captura de pacotes via Wireshark (`tcp.port == 22`, ARP, DNS, ICMP).
  - Testes de regras de firewall, varreduras com Nmap e simulação de eventos para análise em SIEM/Event Viewer.
* 🔗 [Abrir CyberLab no Roadmap](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/portfolio/cyberlab/README.md)

---

### 🔑 4. Account Security Hygiene
* **Problema:** Vulnerabilidade a ataques de engenharia social, credential stuffing e acessos indevidos por falhas de higiene cibernética.
* **Solução:** Framework prático de higiene de acessos e identidade, cobrindo implementação de MFA/2FA, gerenciadores de senhas, auditoria de sessões ativas e matriz de risco para 9 escopos de contas.
* **Resultado Validado:** Redução demonstrada do nível de risco residual e criação de procedimentos reproduzíveis de auditoria de IAM.
* 🔗 [Ver Repositório de Higiene de Contas](https://github.com/thiagoalphabsb/account-security-hygiene)

---

### 📊 5. Power BI & Análise de Dados Públicos (CNES / SIH-SUS)
* **Problema:** Transformar dados brutos de saúde pública em indicadores executivos e operacionais inteligíveis.
* **Solução:** Pipeline ETL em Power Query, modelagem dimensional em estrela (Star Schema) e métricas avançadas em DAX com base em dados reais do SUS.
* **Resultado Validado:** Dashboards interativos respondendo a perguntas estratégicas sobre capacidade hospitalar e fluxo de internações.
* 🔗 [Ver Repositório Power BI](https://github.com/thiagoalphabsb/Power-BI-Roadmap)

---

### 📱 6. THUNDER-FIT-APP
* **Problema:** Acompanhamento descentralizado e ineficiente de rotinas de treino, controle de cargas e tempo de descanso.
* **Solução:** Aplicação Web/PWA desenvolvida em React 18, TypeScript, Tailwind CSS e Firebase, contando com regras estritas de segurança no Firestore (`request.auth.uid == userId`), armazenamento local/offline e assistente integrado por IA.
* **Resultado Validado:** PWA funcional em execução mobile/desktop, arquitetura modularizada, persistência offline e segurança de dados validadas no backend.
* 🔗 [Ver Apresentação Detalhada no Portfólio](https://github.com/thiagoalphabsb/cybersecurity-portfolio/tree/main/projects) · [Ver Código-Fonte no GitHub](https://github.com/thiagoalphabsb/THUNDER-FIT-APP)

---

## 🛠️ Competências Técnicas

**Sistemas & Redes**  
![Windows Server](https://img.shields.io/badge/Windows_Server_2025-0078D6?style=flat-square&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active_Directory-0078D6?style=flat-square&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux_Debian/Kali-FCC624?style=flat-square&logo=linux&logoColor=black)

**Segurança Defensiva & Análise**  
![Wireshark](https://img.shields.io/badge/Wireshark-167EC6?style=flat-square&logo=wireshark&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-4D4D4D?style=flat-square)
![PowerShell GPO](https://img.shields.io/badge/GPO_&_Sysmon-5391FE?style=flat-square&logo=powershell&logoColor=white)
![IAM & MFA](https://img.shields.io/badge/IAM_&_MFA-4A154B?style=flat-square)

**Scripting & Dados**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-CC292B?style=flat-square&logo=microsoft-sql-server&logoColor=white)
![Power BI DAX](https://img.shields.io/badge/Power_BI_DAX-F2C811?style=flat-square&logo=power-bi&logoColor=black)

---

## 📬 Contato & Conexão

Estou aberto a oportunidades profissionais em **Análise de Cibersegurança / SOC Júnior**, **Suporte Técnico N2/N3** e **Segurança da Informação**.

- **LinkedIn:** [linkedin.com/in/thiago-souza-silva](https://www.linkedin.com/in/thiago-souza-silva-5607223aa/)
- **GitHub:** [github.com/thiagoalphabsb](https://github.com/thiagoalphabsb)
- **Localização:** Brasília, DF - Brasil


