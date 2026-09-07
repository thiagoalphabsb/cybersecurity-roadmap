# 🛡️ Guia de Implementação de MFA — Account Security Hygiene Lab

Este documento detalha a estratégia de avaliação, implementação e mitigação de riscos relacionada
à Autenticação em Duas Etapas (MFA) nas contas do laboratório.

## 📊 Matriz de Avaliação de MFA por Conta

Durante a auditoria de identidade, cada conta foi avaliada com base na criticidade e no tipo de
MFA suportado/implementado:

| ID | Categoria | Criticidade | MFA Inicial | MFA Final | Método Utilizado | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **ACC-001** | E-mail 01 | 🔴 Crítica | Ausente | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-002** | E-mail 02 | 🔴 Crítica | Ausente | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-003** | Rede social 01 | 🟡 Média | Ativo | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-004** | Rede social 02 | 🟡 Média | Ativo | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-005** | Rede social 03 | 🟡 Média | Ativo | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-006** | Google | 🔴 Crítica | Ativo | Ativo | App Autenticador / Passkey | 🟢 Seguro |
| **ACC-007** | Microsoft | 🔴 Crítica | Ativo | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-008** | GitHub | 🔴 Crítica | Ausente | Ativo | App Autenticador | 🟢 Seguro |
| **ACC-009** | Serviço financeiro | 🔴 Crítica | Ativo | Ativo | App Autenticador / Token | 🟢 Seguro |

---

## 🎯 Diretrizes Técnicas de MFA Adotadas

1. **Eliminação de SMS:** Sempre que a plataforma permitia, o MFA baseado em SMS foi substituído por
aplicativos autenticadores (como Bitwarden Authenticator ou Google Authenticator) para mitigar riscos
de *SIM swapping* e interceptação de mensagens.
2. **Uso de Passkeys / Chaves Físicas:** Priorização de padrões modernos de autenticação baseados em
criptografia de chave pública onde suportado (ex.: Google e GitHub).
3. **Gerenciamento de Códigos de Recuperação:** Armazenamento seguro e criptografado dos códigos de
backup de emergência gerados durante a ativação do MFA, garantindo resiliência contra a perda do
dispositivo autenticador.
