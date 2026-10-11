# 🐧 Linux Security Fundamentals (Semana 03)

> **Módulo / Categoria:** Administração de Sistemas & Segurança Defensiva (Linux)  
> **Data de Execução:** 15/09/2026  
> **Status:** 🟢 Concluído  

---

## 🎯 1. Objetivo do Laboratório

Aprofundar os conhecimentos no sistema operacional **Linux sob a perspectiva de Cibersegurança Defensiva**, evoluindo do uso básico do sistema para uma gestão orientada a controle de acessos, análise de processos/serviços, investigação de logs e aplicação do **Princípio do Menor Privilégio**.

- **Controle de Acessos & Permissões:** Gestão de usuários, grupos (`cyberlab`), permissões POSIX (`chmod`, `chown`, `stat`) e auditoria de arquivos sensíveis.
- **Gestão de Privilégios:** Auditoria do comando `sudo`, inspeção do arquivo `/etc/sudoers` e mitigação de permissões excessivas (ex: `777`).
- **Análise de Processos & Serviços:** Mapeamento da cadeia `Systemd → Serviço → PID → Processo → Socket/Porta`.
- **Investigação por Logs:** Coleta e correlação de eventos de autenticação via `journalctl` e `/var/log`.

---

## 🖥️ 2. Ambiente & Ferramentas

| Recurso / Elemento | Especificação / Detalhe |
| :--- | :--- |
| **Sistema Operacional** | Debian GNU/Linux 13 (`CyberLab-Debian` / Host-Only Network) |
| **Usuários de Teste** | `debian` (UID 1000), `analista`, `root` |
| **Grupo de Laboratório** | `cyberlab` (GID 1002) |
| **Ferramentas Utilizadas** | `chmod`, `chown`, `stat`, `sudo`, `ps`, `systemctl`, `journalctl`, `grep` |
| **Diretório de Testes** | `~/cyberlab-permissions` |

---

## 🛠️ 3. Procedimento & Execução

### Passo 1: Gestão de Usuários, Grupos e Permissões POSIX
Criação do grupo `cyberlab`, inclusão do usuário e criação de arquivos de teste para validar a atribuição de permissões octais e o modelo de menor privilégio:

```bash
# Criar grupo de segurança do laboratório e associar usuário
sudo groupadd cyberlab
sudo usermod -aG cyberlab debian

# Criar pasta de testes e arquivos com permissões restritas
mkdir ~/cyberlab-permissions && cd ~/cyberlab-permissions
touch privado.txt evidencia.txt

# Configuração de permissões e alteração de grupo
chmod 600 privado.txt
chown debian:cyberlab evidencia.txt
chmod 640 evidencia.txt

```

### Passo 2: Auditoria de Privilégios e Inspeção do Sudoers
Identificação de permissões do usuário atual e verificação dos arquivos de configuração administrativa do sistema:

- Identificar usuário atual, UID/GID e grupos associados
whoami
id

- Listar privilégios sudo permitidos para a conta
sudo -l

- Inspecionar arquivos de configuração do sudoers
ls -l /etc/sudoers
ls -l /etc/sudoers.d/


### Passo 3: Análise de Processos, Serviços e Logs de Autenticação

Investigação de processos ativos, sockets de rede e consulta a eventos de segurança no sistema:

```bash
# Monitoramento de processos e serviços ativos
ps aux | grep ssh
systemctl status ssh

# Leitura e filtragem de logs de tentativas de autenticação
journalctl -b --no-pager | grep -i sudo

```

---

Aqui está o **`README.md`** completo para a pasta de evidências da **Semana 03 (Linux Security Fundamentals)**, estruturado **exatamente no mesmo padrão e formato** do relatório do Windows Server 2025 que enviaste!

As 4 evidências foram organizadas em tópicos, com tabelas para comparações lado a lado (como o `chmod 777` vs `600`), sumário interativo, comandos destacados e mapeamento de comandos para investigação/SOC.

---

## 📸 Evidências Técnicas — Linux Security Fundamentals (Semana 03)

---

## 🎯 Sumário do Laboratório

1. [Inspeção de Metadados de Arquivos com `stat`](#1-inspeção-de-metadados-de-arquivos-com-stat)
2. [Ajuste e Correção de Permissões Críticas (`chmod 777` → `600`)](#2-ajuste-e-correção-de-permissões-críticas-chmod-777--600)
3. [Verificação de Identidade e Privilégios Sudo](#3-verificação-de-identidade-e-privilégios-sudo)
4. [Mapeamento e Permissões do Arquivo `/etc/sudoers`](#4-mapeamento-e-permissões-do-arquivo-etcsudoers)

---

## 📸 Relatório de Evidências Práticas

### 1. Inspeção de Metadados de Arquivos com `stat`
![week-03-statenvidencia.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week03/week-03-statenvidencia.png)

* **O que a imagem demonstra:** Verificação detalhada de metadados do arquivo `evidencia.txt` no diretório `~/cyberlab-permissions` via comando `stat`.
* **Comando:** `stat evidencia.txt`
* **Resultado:** Confirmação da permissão octal `0640` (`-rw-r-----`), vinculação ao usuário `debian` (UID 1000) e grupo `cyberlab` (GID 1002), além dos carimbos de data/hora (*Access*, *Modify*, *Change*, *Birth*).

---

### 2. Ajuste e Correção de Permissões Críticas (`chmod 777` → `600`)
![week-03-777-600.png](https://raw.githubusercontent.com/thiagoalphabsb/cybersecurity-roadmap/main/evidence/week03/week-03-777-600.png)

* **O que a imagem demonstra:** Simulação de exposição indevida por permissões excessivas e posterior aplicação do Princípio do Menor Privilégio (*Hardening*).
* **Comandos Executados:**
  ```bash
  # 1. Exposição total (Risco de Segurança)
  chmod 777 privado.txt
  ls -l privado.txt

  # 2. Correção para acesso exclusivo do proprietário (Hardening)
  chmod 600 privado.txt
  ls -l privado.txt
  ```
  
* **Resultado:** O arquivo passou de totalmente vulnerável (`-rwxrwxrwx`) para estritamente protegido (`-rw-------`), garantindo leitura e escrita restritas ao usuário `debian`.

---

### 3. Verificação de Identidade e Privilégios Sudo

* **O que a imagem demonstra:** Identificação do contexto de execução do usuário e auditoria de regras de elevação de privilégio.
* **Comandos Executados:**
```bash
whoami
id
sudo -l
sudo whoami

```

* **Resultado:** Confirmação da conta `debian` pertencente ao grupo `sudo` (GID 27), validação da regra de privilégio irrestrito `(ALL : ALL) ALL` e confirmação da elevação para `root`.

---

### 4. Mapeamento e Permissões do Arquivo `/etc/sudoers`

* **O que a imagem demonstra:** Mapeamento do diretório de trabalho do laboratório e verificação das permissões dos arquivos críticos de administração de privilégios.
* **Comandos Executados:**
```bash
ls -l /etc/sudoers
ls -l /etc/sudoers.d/

```

* **Resultado:** Confirmação de que o arquivo `/etc/sudoers` possui permissão restrita de leitura `-r--r-----` (440) pertencente a `root:root`, impedindo modificações diretas sem o utilitário `visudo`.

---

## 🛡️ Tabela de Comandos & Aplicação para SOC / Investigação

| Comando | Função Técnica | Valor Investigativo / SOC |
| --- | --- | --- |
| **`stat <file>`** | Exibe inode, metadados e timestamps do arquivo | Análise forense de criação, modificação e alteração de permissões (*MACB timestamps*) |
| **`chmod 600`** | Define permissão exclusiva de leitura/escrita ao dono | Hardening de chaves SSH, arquivos `.env` e credenciais armazenadas em disco |
| **`id` / `whoami**` | Exibe UID, GIDs e grupos secundários | Identificação do contexto de execução de um usuário ou processo sob investigação |
| **`sudo -l`** | Lista as instruções permitidas no `/etc/sudoers` | Identificação de vetores de escalada de privilégios local (Misconfigurations) |

---

## 🔍 5. Conclusões & Aprendizados

* **Mapeamento de Acessos:** A aplicação correta de permissões POSIX (`600`, `640`) impede que usuários não autorizados ou processos comprometidos leiam ou alterem dados do sistema.
* **Segurança de Arquivos Sensíveis:** O arquivo `/etc/sudoers` deve permanecer estritamente protegido com permissão de leitura exclusiva para o `root`, garantindo a integridade dos privilégios do sistema.
* **Aplicação Profissional (SOC / Support N2):** A correlação `Usuário → Grupo → Permissão → Processo → Evento (Log)` permite identificar comportamentos anômalos, como tentativas negadas de elevação de privilégio (`user NOT in sudoers`), fundamentais para investigação de incidentes.

---

## 🔗 Projetos e Links Relacionados

* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)
* 🛡️ [Cybersecurity Portfolio Principal](https://github.com/thiagoalphabsb/cybersecurity-portfolio)
* 🧪 [CyberLab Infrastructure](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/portfolio/cyberlab/README.md)

