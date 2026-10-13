# 🐧 Linux Security Fundamentals (Semana 03)

> **Módulo / Categoria:** Administração de Sistemas & Segurança Defensiva (Linux)
> **Data de Execução:** 15/09/2026
> **Status:** 🟢 Concluído

---

## 🎯 1. Objetivo do Laboratório

Aprofundar os conhecimentos no sistema operacional **Linux sob a perspectiva de Cibersegurança Defensiva**, evoluindo do uso básico do sistema para uma gestão orientada a controle de acessos, análise de processos/serviços, investigação de logs e aplicação do **Princípio do Menor Privilégio**[cite: 20].

- **Controle de Acessos & Permissões:** Gestão de usuários, grupos (`cyberlab`), permissões POSIX (`chmod`, `chown`, `stat`) e auditoria de arquivos sensíveis[cite: 20].
- **Gestão de Privilégios:** Auditoria do comando `sudo`, inspeção do arquivo `/etc/sudoers` e mitigação de permissões excessivas (ex: `777`)[cite: 20].
- **Análise de Processos & Serviços:** Mapeamento da cadeia `Systemd → Serviço → PID → Processo → Socket/Porta`[cite: 20].
- **Investigação por Logs:** Coleta e correlação de eventos de autenticação via `journalctl` e `/var/log`[cite: 20].

---

## 🖥️ 2. Ambiente & Ferramentas

| Recurso / Elemento | Especificação / Detalhe |
| :--- | :--- |
| **Sistema Operacional** | Debian GNU/Linux 13 (`CyberLab-Debian` / Host-Only Network)[cite: 21] |
| **Usuários de Teste** | `debian` (UID 1000), `analista`, `root`[cite: 20, 24] |
| **Grupo de Laboratório** | `cyberlab` (GID 1002)[cite: 20, 21] |
| **Ferramentas Utilizadas** | `chmod`, `chown`, `stat`, `sudo`, `ps`, `systemctl`, `journalctl`, `grep`[cite: 20] |
| **Diretório de Testes** | `~/cyberlab-permissions`[cite: 21, 22] |

---

## 🛠️ 3. Procedimento & Execução

### Passo 1: Gestão de Usuários, Grupos e Permissões POSIX
Criação do grupo `cyberlab`, inclusão do usuário e criação de arquivos de teste para validar a atribuição de permissões octais e o modelo de menor privilégio[cite: 20]:

```bash
# Criar grupo de segurança do laboratório e associar usuário
sudo groupadd cyberlab
sudo usermod -aG cyberlab analista

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

```bash
# Identificar usuário atual, UID/GID e grupos associados
whoami
id

# Listar privilégios sudo permitidos para a conta
sudo -l

# Inspecionar arquivos de configuração do sudoers
ls -l /etc/sudoers
ls -l /etc/sudoers.d/

```

### Passo 3: Análise de Processos, Serviços e Logs de Autenticação

Investigação de processos ativos, sockets de rede e consulta a eventos de segurança no sistema:

```bash
# Monitoramento de processos e serviços ativos
ps -ef | grep ssh
systemctl status ssh

# Leitura e filtragem de logs de tentativas de autenticação
journalctl -b --no-pager | grep -i sudo

```

---

## 📸 4. Relatório de Evidências Práticas

> 📁 **Diretório no GitHub:** [Acessar evidencia/week03](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/evidence/week03)

### 1. Inspeção de Metadados de Arquivo com `stat`
![Metadados de Arquivo com stat](./week-03-statenvidencia.png)

* **O que a imagem demonstra:** Verificação detalhada de metadados do arquivo `evidencia.txt` no diretório `~/cyberlab-permissions` via comando `stat`.
* **Comando Executado:** `stat evidencia.txt`
* **Resultado:** Confirmação da permissão octal `0640` (`-rw-r-----`), vinculação ao usuário `debian` (UID 1000) e grupo `cyberlab` (GID 1002), além dos carimbos de data/hora (*Access*, *Modify*, *Change*, *Birth*).

---

### 2. Ajuste e Correção de Permissões Críticas (`chmod 777` → `600`)
![Alteração de Permissões no Terminal](./week-03-777-600.png)

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

* **Resultado:** O arquivo passou de totalmente vulnerável (`-rwxrwxrwx`) para estritamente protegido (`-rw-------`), garantindo leitura e escrita restritas ao proprietário.

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

* **O que a imagem demonstra:** Mapeamento do diretório de trabalho do laboratório e verificação das permissões do arquivo sensível de administração de privilégios.
* **Comandos Executados:**
```bash
ls -l /etc/sudoers
ls -l /etc/sudoers.d/

```


* **Resultado:** Confirmação de que o arquivo `/etc/sudoers` possui permissão restrita de leitura `-r--r-----` (440) pertencente a `root:root`, impedindo modificações diretas sem o utilitário `visudo`.

---

## 🔍 5. Conclusões & Aprendizados

* **Mapeamento de Acessos:** A aplicação de permissões octais adequadas (`600`, `640`) impede que contas não autorizadas leiam ou modifiquem dados confidenciais no sistema[cite: 20, 22].
* **Proteção de Arquivos Sensíveis:** A integridade de `/etc/sudoers` é mantida através de permissões restritas mantidas pelo sistema (`440` com dono `root`), permitindo edição segura exclusivamente via utilitário `visudo`[cite: 20, 23].
* **Aplicação para SOC / Análise Defensiva:** A correlação entre `Usuário → Grupo → Permissão → Processo → Log` permite identificar anomalias no sistema, como tentativas negadas de uso de `sudo` (`user NOT in sudoers`), fundamentais em investigações de segurança.



---

## 🔗 Projetos e Links Relacionados

* 🐧 [Laboratório Prático de Linux Security (Semana 03)](https://github.com/thiagoalphabsb/cybersecurity-roadmap/blob/main/portfolio/linux-security/README.md)
* 🧪 [CyberLab Infrastructure](https://github.com/thiagoalphabsb/cybersecurity-roadmap/tree/main/portfolio/cyberlab)
* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://github.com/thiagoalphabsb/cybersecurity-roadmap)
