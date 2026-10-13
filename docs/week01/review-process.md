# 🔎 Security Account Assessment

## Objetivo

Avaliar a postura de segurança das contas digitais selecionadas,
identificando riscos relacionados a credenciais, autenticação,
recuperação de conta, dispositivos, sessões e aplicativos conectados.

## Contas avaliadas

| ID      | Categoria          | Criticidade |
| ------- | ------------------ | ----------- |
| ACC-001 | E-mail 01          | Crítica     |
| ACC-002 | E-mail 02          | Crítica     |
| ACC-003 | Rede social 01     | Média       |
| ACC-004 | Rede social 02     | Média       |
| ACC-005 | Rede social 03     | Média       |
| ACC-006 | Google             | Crítica     |
| ACC-007 | Microsoft          | Crítica     |
| ACC-008 | GitHub             | Crítica     |
| ACC-009 | Serviço financeiro | Crítica     |

---

## Controles avaliados

Cada conta será analisada considerando:

### 1. Senha

* A senha é única?
* A senha é forte?
* A senha está armazenada no Bitwarden?
* Existe reutilização da senha em outro serviço?

### 2. MFA

* MFA está habilitado?
* Qual método de autenticação é utilizado?
* O método está funcionando corretamente?

### 3. Recuperação

* E-mail de recuperação está atualizado?
* Telefone de recuperação está atualizado?
* Métodos de recuperação antigos foram removidos?
* Recovery codes estão armazenados de forma segura?

### 4. Sessões e dispositivos

* Existem dispositivos desconhecidos?
* Existem sessões antigas?
* Dispositivos não utilizados foram removidos?
* Existe alguma atividade suspeita?

### 5. Aplicativos e permissões

* Existem aplicativos conectados?
* Existem aplicativos desconhecidos?
* Existem permissões desnecessárias?
* Aplicativos antigos foram revogados?

---

## Matriz de avaliação

| ID      | Senha | MFA | Recuperação | Dispositivos/Sessões | Aplicativos | Risco |
| ------- | ----- | --- | ----------- | -------------------- | ----------- | ----- |
| ACC-001 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-002 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-003 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-004 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-005 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-006 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-007 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-008 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |
| ACC-009 | ⬜    | ⬜  | ⬜          | ⬜                   | ⬜          | ⬜    |

## Classificação de risco

🔴 **Crítico** — risco elevado e ação imediata necessária.

🟠 **Alto** — risco relevante que deve ser corrigido prioritariamente.

🟡 **Médio** — risco que deve ser tratado durante a revisão.

🟢 **Baixo** — controle adequado ou risco residual reduzido.

## Metodologia

A avaliação será realizada antes das correções e repetida após a implementação dos controles.

Dessa forma será possível comparar:

**Estado inicial → Correções → Estado final**

Nenhuma senha, código MFA, token, recovery code ou informação pessoal será registrada neste documento.

# 📊 Resultado da Avaliação Inicial

Foram avaliadas 9 contas digitais utilizando uma metodologia baseada em seis áreas principais:

* Segurança das credenciais
* Autenticação multifator
* Recuperação de conta
* Dispositivos e sessões
* Aplicativos conectados
* Permissões

## Indicadores iniciais

| Indicador                  |   Resultado |
| -------------------------- | ----------: |
| Contas avaliadas           |           9 |
| MFA ativo                  |  9/9 — 100% |
| Recuperação atualizada     |  9/9 — 100% |
| Senhas reutilizadas        | 7/9 — 77,8% |
| Senhas fracas              | 6/9 — 66,7% |
| Credenciais no Bitwarden   |    0/9 — 0% |
| Dispositivos desconhecidos |         0/9 |
| Sessões desconhecidas      |         0/9 |
| Aplicativos desconhecidos  |         0/9 |
| Permissões desnecessárias  |         0/9 |

## Diagnóstico

A avaliação inicial demonstrou que os principais controles relacionados à autenticação, recuperação
de contas, dispositivos, sessões e aplicativos conectados estavam adequados.

O principal ponto de melhoria identificado foi a **higiene das credenciais**, especialmente a
reutilização de senhas e a utilização de senhas consideradas fracas.

## Plano de remediação

As correções serão realizadas priorizando contas críticas com senhas fracas e reutilizadas.

O objetivo é:

* eliminar a reutilização de senhas;
* substituir senhas fracas por credenciais fortes e exclusivas;
* centralizar o gerenciamento das credenciais no Bitwarden;
* manter MFA ativo;
* validar novamente os controles após as alterações.

A avaliação será repetida após a remediação para permitir uma comparação objetiva entre o estado inicial e o estado final.

> Nenhuma senha, código MFA, token, recovery code ou informação pessoal foi registrada no projeto.
