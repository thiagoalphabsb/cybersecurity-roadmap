# 🧪 Laboratório: 🐧 Linux Security Fundamentals (Semana 03)

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
ps aux | grep ssh
systemctl status ssh

# Leitura e filtragem de logs de tentativas de autenticação
journalctl -b --no-pager | grep -i sudo

```

---

## 📸 4. Evidências Práticas (Screenshots)

### Evidência 1: Inspeção de Metadados de Arquivo com `stat`

* **O que a imagem demonstra:** Execução do comando `stat evidencia.txt` no diretório `~/cyberlab-permissions`.
* **Achado / Resultado:**
* Confirmação das permissões em formato numérico e simbólico: `Access: (0640/-rw-r-----)`.
* Confirmação do proprietário (`Uid: 1000/debian`) e do grupo atrelado (`Gid: 1002/cyberlab`).
* Registro preciso dos carimbos de data/hora (*Access*, *Modify*, *Change*, *Birth*).



---

### Evidência 2: Alteração e Correção de Permissões Críticas (`chmod 777` → `600`)

* **O que a imagem demonstra:**
* Execução controlada de `chmod 777 privado.txt` tornando o arquivo totalmente exposto (`-rwxrwxrwx`).
* Demonstração do tratamento de erro ao tentar alterar um arquivo inexistente (`priado.txt`).
* Aplicação do hardening com `chmod 600 privado.txt`, redefinindo o acesso exclusivo ao proprietário (`-rw-------`).


* **Achado / Resultado:** Validação da importância do princípio do menor privilégio para evitar a exposição indevida de arquivos sensíveis.

---

### Evidência 3: Verificação de Identidade e Privilégios Sudo

* **O que a imagem demonstra:**
* Saída do comando `whoami` (`debian`) e `id` confirmando a lista de GIDs (incluindo `27(sudo)`).
* Execução de `sudo -l` mostrando a regra de privilégio irrestrito: `(ALL : ALL) ALL`.
* Confirmação de elevação de privilégio bem-sucedida via `sudo whoami`, retornando `root`.


* **Achado / Resultado:** Auditoria completa das permissões administrativas atribuídas à conta de usuário no ambiente.

---

### Evidência 4: Mapeamento e Permissões do Arquivo `/etc/sudoers`

* **O que a imagem demonstra:**
* Listagem do diretório do usuário e verificação direta das permissões do arquivo `/etc/sudoers` e do diretório `/etc/sudoers.d/`.


* **Achado / Resultado:** Confirmação das permissões restritas `-r--r-----` mantidas pelo sistema com propriedade do usuário `root:root`, impedindo edições diretas não autorizadas sem a ferramenta `visudo`.

---

## 🔍 5. Conclusões & Aprendizados

* **Mapeamento de Acessos:** A aplicação correta de permissões POSIX (`600`, `640`) impede que usuários não autorizados ou processos comprometidos leiam ou alterem dados do sistema.
* **Segurança de Arquivos Sensíveis:** O arquivo `/etc/sudoers` deve permanecer estritamente protegido com permissão de leitura exclusiva para o `root`, garantindo a integridade dos privilégios do sistema.
* **Aplicação Profissional (SOC / Support N2):** A correlação `Usuário → Grupo → Permissão → Processo → Evento (Log)` permite identificar comportamentos anômalos, como tentativas negadas de elevação de privilégio (`user NOT in sudoers`), fundamentais para investigação de incidentes.

---

## 🔗 Projetos e Links Relacionados

* 🛣️ [Cybersecurity Roadmap (24 Semanas)](https://www.google.com/search?q=https://github.com/thiagoalphabsb/Cybersecurity-Roadmap)
* 🛡️ [Cybersecurity Portfolio Principal](https://www.google.com/search?q=https://github.com/thiagoalphabsb/Cybersecurity-Portfolio)
* 🧪 [CyberLab Infrastructure](https://www.google.com/search?q=https://github.com/thiagoalphabsb/Cybersecurity-Roadmap/tree/main/labs/cyberlab)


```
