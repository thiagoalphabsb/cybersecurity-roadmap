# Dia 05 - Observando Processos no Linux e Investigação de Incidentes

## 🎯 Objetivo

Analisar o comportamento de processos no Linux sob a ótica de **Cybersecurity e Resposta a Incidentes**, aprendendo a mapear o consumo de CPU e Memória, formular hipóteses investigativas, coletar evidências e tomar decisões de mitigação seguras.

\---

## 🔍 Mapeamento e Estrutura dos Processos

```text
PID (Process ID)
 ↓
/proc/PID (Diretório virtual com informações do processo)
 ↓
Informações detalhadas do processo
(estado, usuário, memória, processo pai, executável, etc.)
```

O diretório `/proc/<PID>` fornece informações dinâmicas sobre processos em execução e permite investigar características importantes de cada processo.

\---

## 🧪 Laboratório Prático

### 1\. Listagem de processos

```bash
ps aux
ps -ef
```

Identificar usuário, PID, consumo de CPU, consumo de memória, comando e processo pai (PPID).

### 2\. Monitoramento em tempo real

```bash
top
```

Observar processos com maior consumo de CPU e memória e a utilização geral dos recursos.

### 3\. Investigação de um processo específico

```bash
ps -p <PID> -f
cat /proc/<PID>/status
ls -l /proc/<PID>/exe
```

Esses comandos permitem verificar informações como usuário, PID, PPID, estado, UID, memória e executável associado.

\---

## 🧠 Leitura do Uso de Memória

```bash
free -h
cat /proc/meminfo
```

`free` apresenta um resumo da memória RAM, enquanto `/proc/meminfo` fornece informações detalhadas gerenciadas pelo kernel.

\---

## 🧪 Simulação de Processo Controlado

```bash
sleep 120
```

Em outro terminal:

```bash
ps aux | grep sleep
```

Após identificar o PID:

```bash
kill <PID>
```

Objetivo: observar na prática a relação entre **processo → PID → monitoramento → encerramento**.

\---

## ⚠️ Simulação Controlada de Alto Consumo de CPU

```bash
yes > /dev/null
```

Monitorar:

```bash
top
```

Localizar:

```bash
ps aux | grep yes
```

Encerrar após a observação:

```bash
kill <PID>
```

> ⚠️ Esta é uma simulação controlada de alto consumo de CPU. Ela não representa, por si só, um ataque ou comprometimento do sistema. O processo deve ser encerrado após a observação.

\---

## 🧠 Pensamento Crítico \& Cybersecurity: Formulação de Hipóteses

Ao observar anomalias na utilização de CPU ou Memória, formular hipóteses antes de qualquer ação destrutiva:

❓ Processo legítimo?

❓ Atualização de sistema em segundo plano?

❓ Aplicação com problema ou travada?

❓ Loop infinito em execução?

❓ Atividade inesperada fora do horário comercial?

❓ Possível comprometimento ou artefato malicioso (ex.: mineração de criptomoedas, malware)?

### Coleta de Evidências

A primeira atitude diante de um comportamento anormal é **investigar e registrar**, e não apagar as pistas imediatamente.

\---

## ❓ Caso de Estudo: "Processo Consumindo 90% da CPU"

### Pergunta

Se um processo desconhecido estiver consumindo 90% da CPU, você deve simplesmente executar o `kill`?

### Resposta

**Não necessariamente.**

O encerramento imediato sem investigação prévia pode causar perda de dados, interrupção de serviços críticos e perda de informações importantes para a investigação.

A ação deve considerar o contexto, a criticidade do processo e o impacto sobre o sistema.

\---

# 🛠️ Fluxo Prático de Investigação e Mitigação

## 1\. Investigação Inicial — Identificar a Origem

```bash
ps -p <PID> -f
cat /proc/<PID>/status
ls -l /proc/<PID>/exe
```

Identificar quem executou o processo, seu PPID, estado e executável associado.

## 2\. Avaliação de Risco — Analisar o Impacto

Verificar se o processo é legítimo ou pertence a uma aplicação conhecida, como `systemd`, banco de dados, backup, indexadores ou aplicações do ambiente.

## 3\. Mitigação — Redução de Prioridade

Se o processo for **legítimo**, mas estiver sobrecarregando a CPU e não puder ser desligado:

```bash
renice -n 19 -p <PID>
```

> A utilização de `renice` deve ocorrer somente após compreender o processo e avaliar o impacto da alteração.

## 4\. Finalização Segura — Interromper Graciosamente

```bash
kill <PID>
kill -15 <PID>
```

O sinal padrão de `kill` é o **SIGTERM**, que solicita um encerramento controlado.

## 5\. Finalização Forçada — Último Recurso

```bash
kill -9 <PID>
```

O **SIGKILL** determina o encerramento imediato pelo kernel e deve ser tratado como último recurso.

> ⚠️ O `kill -9` não permite que o processo execute sua rotina normal de encerramento.

\---

# 🔎 Raciocínio Investigativo

**Alto consumo de CPU ou memória é um indicador, não uma conclusão.**

Um processo consumindo muitos recursos pode ser legítimo, resultado de atualização, uma aplicação com falha, um loop, atividade inesperada ou, dependendo das evidências, parte de um possível comprometimento.

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

Esse raciocínio reduz ações precipitadas e ajuda a preservar evidências durante uma investigação.

\---

# 🧠 O que Aprendi

* Processos possuem identificadores únicos chamados **PID**.
* O diretório `/proc` permite investigar informações dinâmicas dos processos.
* `ps` fornece uma visão dos processos em execução.
* `top` permite monitoramento em tempo real.
* `free` e `/proc/meminfo` ajudam na análise de memória.
* Alto consumo de CPU ou memória não significa automaticamente comprometimento.
* A investigação deve começar pela coleta e análise de evidências.
* `SIGTERM` permite uma tentativa de encerramento controlado.
* `SIGKILL` deve ser utilizado como último recurso.
* Decisões em Cybersecurity devem considerar contexto, impacto e evidências.

\---

# 📝 Dificuldades Encontradas

* Diferenciar um processo legítimo de um comportamento potencialmente anômalo.
* Entender a relação entre PID, PPID e `/proc/<PID>`.
* Interpretar as informações apresentadas pelo `top`.
* Relacionar consumo de recursos com possíveis cenários de incidentes.
* Entender quando uma ação de mitigação pode ser mais adequada do que a finalização imediata.

\---

# 📊 Autoavaliação do Dia 05

|Tema|Nota|
|-|-:|
|Processos|5/5|
|PID|5/5|
|`/proc`|5/5|
|Memória|5/5|
|CPU|5/5|
|`ps`|5/5|
|`top`|5/5|
|Investigação|5/5|
|Relação com Cybersecurity|5/5|

\---

# 🎯 Conclusão

O Dia 05 consolidou os fundamentos de **processos, CPU, memória e monitoramento no Linux**, conectando esses conceitos ao pensamento investigativo em Cybersecurity.

O principal aprendizado foi entender que um comportamento anormal deve ser **observado, investigado e contextualizado antes de uma ação de mitigação**.

\---

## 🚀 Próximo Passo

**Dia 06 — Revisão e consolidação dos fundamentos da Semana 01**

O próximo estudo deverá consolidar os conhecimentos adquiridos nos primeiros dias antes do encerramento da Semana 01.

\---

**Status:** 🟢 Concluído  
**Semana:** 01 — Fundamentos de Computação

