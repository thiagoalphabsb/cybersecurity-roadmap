# 🛡️ Week 03 — Linux para Cybersecurity

> Terceira semana do projeto **Cybersecurity Roadmap**  
> **Foco:** administração, segurança, investigação e automação em sistemas Linux.

---

## 🎯 Objetivo da Semana

A Week 03 teve como objetivo aprofundar os conhecimentos em **Linux sob a perspectiva de Cybersecurity**, evoluindo do uso básico do sistema para uma visão de administração, controle de privilégios, investigação e automação.

Durante a semana foram trabalhados:

- Usuários e grupos;
- Permissões de arquivos;
- Princípio do menor privilégio;
- Sudo e administração;
- Processos e serviços;
- Logs e investigação;
- Sistema de arquivos;
- Arquivos sensíveis;
- Bash e automação;
- Correlação de evidências;
- Documentação de atividades de segurança.

A proposta foi transformar comandos Linux em **ferramentas de observação, análise e investigação**.

---

# 📅 Dia 01 — Usuários, Grupos e Permissões

## 🎯 Objetivo

Compreender como o Linux controla acesso aos recursos através de usuários, grupos e permissões.

### 🔎 Conceitos estudados

- Usuário;
- Grupo;
- UID e GID;
- Proprietário;
- Permissões `r`, `w` e `x`;
- Permissões numéricas;
- `chmod`;
- `chown`;
- `stat`;
- Princípio do menor privilégio.

### 🧪 Laboratório

Foi criado o usuário de laboratório:

```text
analista
```

E o grupo:

```text
cyberlab
```

O usuário foi associado ao grupo:

```bash
sudo usermod -aG cyberlab analista
```

Também foram criados arquivos com diferentes níveis de permissão para analisar o comportamento do sistema.

Exemplos utilizados:

```bash
chmod 644 publico.txt
chmod 600 privado.txt
chmod 640 restrito.txt
chmod 777 evidencia.txt
```

A permissão `777` foi utilizada como exemplo controlado para demonstrar por que permissões excessivas devem ser evitadas.

### 🛡️ Perspectiva de Cybersecurity

Permissões inadequadas podem permitir acesso, alteração ou execução não autorizada de arquivos.

O princípio aplicado foi:

> **Cada usuário deve possuir somente as permissões necessárias para realizar suas atividades.**

---

# 📅 Dia 02 — Sudo e Privilégio Mínimo

## 🎯 Objetivo

Compreender como o Linux controla operações administrativas e como o `sudo` pode ser utilizado de acordo com o princípio do menor privilégio.

### 🔎 Conceitos estudados

- Usuário comum;
- `root`;
- `sudo`;
- `/etc/sudoers`;
- `/etc/sudoers.d/`;
- Privilégios administrativos;
- Princípio do menor privilégio.

### 🧪 Comandos utilizados

```bash
whoami
```

```bash
id
```

```bash
groups
```

```bash
sudo -l
```

```bash
sudo whoami
```

Foi analisado quais privilégios estavam disponíveis para o usuário e como o sistema impede operações administrativas quando o usuário não possui autorização.

### 🛡️ Perspectiva de Cybersecurity

O controle de privilégios é uma das bases da segurança de sistemas.

Um usuário comprometido com privilégios excessivos pode aumentar significativamente o impacto de um incidente.

Por isso:

> **Privilégio mínimo reduz a superfície de impacto de uma conta comprometida.**

---

# 📅 Dia 03 — Processos e Serviços

## 🎯 Objetivo

Aprender a relacionar processos, serviços, PID e `systemd`, permitindo uma análise mais estruturada do funcionamento do sistema.

### 🔎 Comandos estudados

```bash
ps
```

```bash
ps -ef
```

```bash
pstree -p
```

```bash
top
```

```bash
pgrep -a ssh
```

Para análise de serviços:

```bash
systemctl --type=service --state=running
```

```bash
systemctl status NOME_DO_SERVICO
```

```bash
systemctl is-active NOME_DO_SERVICO
```

```bash
systemctl is-enabled NOME_DO_SERVICO
```

### 🧪 Laboratório — CyberLab Service

Foi criado um serviço controlado para compreender a relação entre:

```text
systemd
   ↓
serviço
   ↓
PID
   ↓
processo
   ↓
comando
```

Serviço utilizado:

```text
cyberlab.service
```

O serviço executava:

```bash
/bin/sleep 3600
```

Após a investigação, o serviço foi interrompido e removido do laboratório.

### 🛡️ Perspectiva de Cybersecurity

A análise de processos e serviços permite identificar:

- processos inesperados;
- serviços desconhecidos;
- consumo anormal de recursos;
- processos relacionados a serviços;
- possíveis indicadores de comprometimento.

---

# 📅 Dia 04 — Logs e Investigação

## 🎯 Objetivo

Utilizar logs como fonte de evidências para investigar eventos ocorridos no sistema Linux.

### 🔎 Conceitos estudados

- `/var/log`;
- `systemd-journald`;
- `journalctl`;
- eventos de sistema;
- timestamps;
- níveis de prioridade;
- logs de autenticação;
- investigação por serviço;
- investigação por período.

### 🧪 Comandos utilizados

```bash
ls -lah /var/log
```

```bash
journalctl
```

```bash
journalctl -b
```

```bash
journalctl --list-boots
```

```bash
journalctl -p warning
```

```bash
journalctl --since "today"
```

```bash
journalctl --since "1 hour ago"
```

Também foram realizadas consultas direcionadas:

```bash
journalctl -b --no-pager | grep -i sudo
```

### 🔍 Evidência encontrada

Durante a investigação foi identificado um evento relacionado ao usuário `analista`:

```text
analista : user NOT in sudoers
```

O evento demonstrou que uma tentativa de utilização de `sudo` foi registrada pelo sistema e que o usuário não possuía autorização administrativa.

### 🧠 Análise

O laboratório demonstrou a importância de diferenciar:

**Evidência:**

> O usuário tentou utilizar `sudo` e o sistema registrou que ele não estava autorizado.

**Interpretação:**

> A existência desse evento, isoladamente, não permite concluir que houve uma tentativa maliciosa.

Essa distinção é importante em processos de investigação e resposta a incidentes.

---

# 📅 Dia 05 — Sistema de Arquivos e Arquivos Sensíveis

## 🎯 Objetivo

Compreender a organização do sistema de arquivos Linux e identificar locais que podem conter informações relevantes para segurança e investigação.

### 🔎 Conceitos estudados

- Estrutura de diretórios Linux;
- Arquivos de configuração;
- Arquivos de usuários;
- Arquivos de grupos;
- Arquivos de autenticação;
- Arquivos de logs;
- Arquivos sensíveis;
- permissões de acesso.

### 📂 Arquivos e diretórios relevantes

Exemplos analisados:

```text
/etc/passwd
/etc/group
/etc/shadow
/etc/sudoers
/etc/sudoers.d/
/var/log/
/home/
```

### 🛡️ Perspectiva de Cybersecurity

Arquivos de configuração e autenticação podem conter informações críticas.

A análise deve considerar:

- quem possui acesso;
- quais permissões estão configuradas;
- se o arquivo contém informações sensíveis;
- se o acesso está de acordo com a necessidade.

---

# 📅 Dia 06 — Bash e Automação

## 🎯 Objetivo

Utilizar comandos Bash para transformar tarefas repetitivas de análise em processos mais rápidos e reproduzíveis.

### 🔎 Conceitos estudados

- Shell;
- comandos encadeados;
- pipes;
- redirecionamento;
- `grep`;
- filtros;
- variáveis;
- scripts Bash;
- automação de tarefas.

### 🧪 Conceitos utilizados

Pipe:

```bash
|
```

Redirecionamento:

```bash
>
```

Adicionar conteúdo:

```bash
>>
```

Busca e filtragem:

```bash
grep
```

### 🛡️ Perspectiva de Cybersecurity

A automação pode ser utilizada para:

- procurar eventos em logs;
- identificar padrões;
- filtrar informações;
- coletar evidências;
- executar verificações repetitivas;
- reduzir tarefas manuais.

O objetivo não é apenas executar comandos mais rapidamente, mas criar procedimentos **reproduzíveis e documentáveis**.

---

# 📅 Dia 07 — Laboratório Integrado

## 🎯 Objetivo

Integrar os conhecimentos adquiridos durante a Week 03 em uma investigação prática.

O laboratório combinou:

```text
Usuário
   ↓
Grupo
   ↓
Permissões
   ↓
Privilégios
   ↓
Processos
   ↓
Serviços
   ↓
Logs
   ↓
Evidências
```

### 🔍 Fluxo de investigação

A investigação foi estruturada seguindo uma sequência lógica:

1. Identificar o usuário;
2. Verificar grupos;
3. Verificar privilégios;
4. Analisar processos;
5. Analisar serviços;
6. Consultar logs;
7. Localizar eventos relevantes;
8. Correlacionar as evidências;
9. Separar fatos de interpretações;
10. Documentar os resultados.

### 🧠 Mentalidade investigativa

O principal aprendizado do laboratório integrado foi evitar conclusões precipitadas.

Em uma investigação de segurança:

> **Primeiro coletamos evidências. Depois analisamos o contexto. Somente então formulamos uma hipótese.**

---

# 🛡️ Principais conhecimentos adquiridos

Ao finalizar a Week 03, foi possível desenvolver conhecimentos práticos em:

### Linux

- Usuários;
- Grupos;
- Permissões;
- Processos;
- Serviços;
- Sistema de arquivos;
- Logs;
- Bash.

### Cybersecurity

- Princípio do menor privilégio;
- Controle de acesso;
- Análise de processos;
- Análise de serviços;
- Investigação baseada em evidências;
- Análise de logs;
- Identificação de eventos;
- Correlação de informações;
- Automação de tarefas.

---

# 🧠 Evolução da Week 03

A evolução da semana pode ser representada da seguinte maneira:

```text
Quem está no sistema?
        ↓
Quais permissões possui?
        ↓
Quais privilégios possui?
        ↓
O que está executando?
        ↓
Quais serviços estão ativos?
        ↓
O que aconteceu?
        ↓
Onde está a evidência?
        ↓
Como documentar?
```

Essa sequência representa uma mudança importante da utilização básica do Linux para uma abordagem orientada à **segurança e investigação**.

---

# 📊 Status da Semana

| Dia | Tema | Status |
|---|---|---|
| 01 | Usuários, grupos e permissões | ✅ Concluído |
| 02 | Sudo e privilégio mínimo | ✅ Concluído |
| 03 | Processos e serviços | ✅ Concluído |
| 04 | Logs e investigação | ✅ Concluído |
| 05 | Sistema de arquivos e arquivos sensíveis | ✅ Concluído |
| 06 | Bash e automação | ✅ Concluído |
| 07 | Laboratório integrado + documentação | ✅ Concluído |

---

# 🚀 Próxima etapa

Com a conclusão da **Week 03**, o CyberLab passa a contar com uma base mais sólida de administração e investigação Linux.

A próxima semana continuará a evolução do roadmap, aproveitando os conhecimentos de:

- Linux;
- redes;
- processos;
- serviços;
- logs;
- análise de evidências;
- automação.

O objetivo será continuar aproximando o laboratório de situações práticas encontradas em ambientes de **Cybersecurity defensiva**.

---

## 📚 Projeto

**Cybersecurity Roadmap**

GitHub:

`https://github.com/thiagoalphabsb/cybersecurity-roadmap`

---

> **Desenvolvido por Thiago S. Silva**
