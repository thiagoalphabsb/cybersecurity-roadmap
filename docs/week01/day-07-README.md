# 🚀 Dia 07 — Encerramento da Semana 01

## 🎯 Objetivo

Consolidar os conhecimentos estudados durante a primeira semana do **Cybersecurity Roadmap**, revisar os fundamentos de computação, virtualização, Linux, processos e pensamento investigativo e registrar os principais aprendizados para a continuidade da trilha.

---

## 📚 Retrospectiva da Semana

Durante a Week 1, a evolução foi construída do nível mais básico da infraestrutura até a observação investigativa do sistema operacional.

```text
Hardware
   ↓
Sistema Operacional
   ↓
Virtualização
   ↓
Linux / Debian
   ↓
Processos
   ↓
Monitoramento
   ↓
Pensamento Investigativo
   ↓
Cybersecurity
```

A semana teve como foco criar uma base técnica sólida antes de avançar para temas mais específicos de Segurança da Informação.

---

## 🧠 Conhecimentos Consolidados

### 💻 Fundamentos de Computação

- CPU e processamento.
- Memória RAM.
- Armazenamento SSD/HDD.
- Processos.
- Arquivos e sistema operacional.
- Relação entre hardware e software.

### 🖥️ Virtualização e Laboratório

- Conceito de máquina virtual.
- Uso do VirtualBox.
- Organização do ambiente de laboratório.
- Debian como ambiente Linux.
- Kali Linux como ambiente voltado aos estudos de Cybersecurity.

### 🐧 Linux

- Estrutura básica do sistema de arquivos.
- Navegação e utilização do terminal.
- Kernel e sistema operacional.
- Processos e identificação por PID.
- Diretórios importantes do Linux.

### ⚙️ Processos e Monitoramento

Foram praticados comandos como:

```bash
ps aux
ps -ef
top
free -h
cat /proc/<PID>/status
ls -l /proc/<PID>/exe
kill <PID>
```

Também foi realizada uma simulação controlada de consumo elevado de CPU utilizando:

```bash
yes > /dev/null
```

A atividade permitiu observar o comportamento do processo e posteriormente encerrá-lo.

---

## 🔎 Pensamento Investigativo

Um dos principais aprendizados da semana foi compreender que **um comportamento anormal não representa automaticamente um comprometimento**.

O raciocínio desenvolvido foi:

```text
Observar
   ↓
Identificar
   ↓
Coletar evidências
   ↓
Investigar
   ↓
Formular hipóteses
   ↓
Testar
   ↓
Agir
   ↓
Validar
```

Antes de finalizar um processo, é necessário compreender seu contexto, origem, usuário, processo pai, executável e impacto.

---

## 🛡️ Conexão com Cybersecurity

Os fundamentos estudados formam uma base importante para atividades futuras de:

- Análise de incidentes.
- Monitoramento de endpoints.
- Investigação de processos suspeitos.
- Análise de comportamento.
- Resposta a incidentes.
- Threat Hunting.
- Administração e segurança de sistemas Linux.

A principal mudança de mentalidade foi deixar de apenas executar comandos e começar a **interpretar o que está acontecendo no sistema**.

---

## 📝 Principais Aprendizados

1. O hardware fornece os recursos utilizados pelo sistema.
2. O sistema operacional gerencia esses recursos.
3. Processos representam programas em execução.
4. Cada processo possui um PID.
5. O `/proc` fornece informações dinâmicas sobre processos.
6. `ps` e `top` permitem observar processos.
7. `free` e `/proc/meminfo` ajudam na análise da memória.
8. Alto consumo de CPU ou RAM é um indicador, não uma conclusão.
9. Evidências devem ser coletadas antes de ações destrutivas quando o contexto permitir.
10. `SIGTERM` deve ser preferido ao encerramento forçado quando apropriado.
11. `SIGKILL` deve ser tratado como último recurso.
12. A investigação em Cybersecurity depende de contexto, evidências e hipóteses.

---

## 📊 Autoavaliação da Semana 01

| Área | Avaliação |
|---|---:|
| Fundamentos de Computação | 5/5 |
| Hardware | 5/5 |
| Virtualização | 4/5 |
| Linux | 5/5 |
| Sistema de Arquivos | 5/5 |
| Processos | 5/5 |
| PID / PPID | 5/5 |
| CPU / Memória | 5/5 |
| Monitoramento | 5/5 |
| Pensamento Investigativo | 5/5 |
| Relação com Cybersecurity | 5/5 |

### 🎯 Resultado

**Nível de domínio da Week 1: 🟢 Bom / Consolidado**

O principal ponto que permanece em evolução é ganhar velocidade e naturalidade na utilização dos comandos Linux, especialmente por meio da prática contínua no laboratório.

---

## 🧪 Resultado do Laboratório

O ambiente de estudos passou a contar com máquinas virtuais **Debian** e **Kali Linux**, formando a base prática para as próximas etapas do roadmap.

A proposta é continuar utilizando o laboratório para transformar conhecimento teórico em prática reproduzível.

---

## ⚠️ Dificuldades Encontradas

- Consolidar conceitos de baixo nível antes de relacioná-los com Cybersecurity.
- Ganhar familiaridade com comandos Linux.
- Interpretar informações de processos.
- Diferenciar comportamento normal de comportamento potencialmente anômalo.
- Desenvolver o hábito de investigar antes de executar uma ação de mitigação.

Essas dificuldades fazem parte do processo de evolução e serão trabalhadas nas próximas semanas.

---

## 🏁 Conclusão

A **Week 1 — Fundamentos de Computação** foi concluída.

A semana estabeleceu a base necessária para compreender como um sistema funciona antes de estudar como ele pode ser atacado, monitorado ou defendido.

O principal objetivo não foi apenas memorizar comandos, mas desenvolver a capacidade de **observar, interpretar, investigar e tomar decisões com base em evidências**.

> **Fundamentos fortes primeiro. Segurança depois.**

---

## 🚀 Próxima Etapa

### Week 02 — Linux + Networking + Laboratório

A próxima etapa dará continuidade à prática no laboratório, aprofundando Linux, redes e conceitos necessários para avançar na trilha de Cybersecurity.

---

**Status:** 🟢 CONCLUÍDO  
**Semana:** 01 — Fundamentos de Computação  
**Projeto:** cybersecurity-roadmap
