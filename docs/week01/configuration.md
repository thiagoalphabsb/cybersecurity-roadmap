# 🔐 Bitwarden Configuration

## Objetivo

Utilizar um gerenciador de senhas para reduzir riscos relacionados a:

* reutilização de senhas;
* senhas fracas;
* armazenamento inseguro de credenciais;
* dificuldade de gerenciamento de múltiplas credenciais.

## Configuração realizada

| Controle                         | Status  |
| -------------------------------- | ------  |
| Conta Bitwarden configurada      | ✅      |
| Senha mestre exclusiva           | ✅      |
| MFA do Bitwarden                 | ✅      |
| Gerador de senhas                | ✅      |
| Credenciais armazenadas no cofre | ✅      |
| Revisão das credenciais          | ✅      |

## Boas práticas adotadas

* A senha mestre não é reutilizada em outros serviços.
* Credenciais individuais serão armazenadas no Bitwarden.
* Senhas novas serão geradas utilizando o gerador de senhas.
* Informações sensíveis não serão armazenadas no repositório GitHub.
* Recovery codes não serão publicados no projeto.

# Padrões de Configuração - Bitwarden

## Cofre e Autenticação Mestre
- **Senha Mestre:** Frase-senha (Passphrase) exclusiva de alta entropia.
- **Parametrização do Gerador:**
  - Comprimento mínimo: 20 a 24 caracteres.
  - Conjunto de caracteres: Maiúsculas, minúsculas, números e símbolos (`!@#$%^&*`).

## Estrutura de Organização do Cofre
- **Pastas:** `Pessoal`, `Trabalho`, `Financeiro`, `Serviços de Infraestrutura`.
- **Politica de Preenchimento:** Preenchimento automático ativado apenas mediante confirmação
explícita no domínio correspondente (proteção contra phishing por iFrame).

## Observação

Este documento descreve o processo de configuração sem armazenar senhas, códigos MFA,
tokens ou outras informações confidenciais.
