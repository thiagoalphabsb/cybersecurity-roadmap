# 🔐 Account Security Hygiene Lab

Laboratório prático de higiene de segurança de contas digitais, desenvolvido como parte da minha
jornada de estudos e transição para a área de **Cybersecurity** (Blue Team / Governança de Identidades).

---

## 🎯 Objetivo

Avaliar, remediar e hardened a segurança de contas digitais, reduzindo a superfície de exposição a 
vetores de ataque como *Credential Stuffing*, *Password Spraying* e sequestro de sessão, aplicando 
boas práticas relacionadas a:

- Gerenciamento seguro de senhas de alta entropia;
- Autenticação Multifator (MFA);
- Gestão de Acessos e Identidades (IAM);
- Revisão de aplicativos conectados (OAuth);
- Gestão de sessões e dispositivos autorizados;
- Classificação e mitigação de riscos;
- Padronização e documentação de segurança.

---

## 🧪 Metodologia

O laboratório seguiu o fluxo operacional contínuo de resposta e remediação:

`Identificar` ➔ `Analisar` ➔ `Corrigir` ➔ `Validar` ➔ `Documentar`

---

## 🧰 Ferramentas Utilizadas

- **Gerenciador de Credenciais:** Bitwarden (Cofre criptografado com Argon2, senhas geradas 
aleatoriamente com 20+ caracteres);
- **Autenticação de Dois Fatores:** Aplicativo Autenticador (TOTP);
- **Documentação & Controle:** Git, GitHub e Markdown.

---

## 📋 Escopo e Rastreamento de Contas (Simuladas/Higienizadas)

Para validar a postura de segurança do ambiente sem expor dados sensíveis, 9 escopos de contas foram 
mapeados e submetidos ao ciclo de remediação:

| ID Conta | Categoria do Serviço | Status MFA | Estado Inicial | Estado Pós-Remediação |
| :--- | :--- | :---: | :---: | :---: |
| **ACC-001** | E-mail Principal / Provedor | ✅ Ativo | 🔴 Reuso / Senha Fraca | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-002** | Produtividade / Nuvem | ✅ Ativo | 🔴 Reuso / Senha Fraca | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-003** | Repositório / Código | ✅ Ativo | 🔴 Reuso de Senha | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-004** | Serviços Financeiros | ✅ Ativo | 🔴 Reuso de Senha | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-005** | Redes Sociais / Comunicação | ✅ Ativo | 🔴 Reuso / Senha Fraca | 🟢 Cofre Bitwarden (20 chars) |
| **ACC-006** | Conta Provedor (Google) | ✅ Ativo | 🔴 Reuso / Senha Fraca | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-007** | Conta Provedor (Microsoft) | ✅ Ativo | 🔴 Reuso / Senha Fraca | 🟢 Cofre Bitwarden (24 chars) |
| **ACC-008** | Plataforma de E-commerce | ✅ Ativo | 🔴 Reuso de Senha | 🟢 Cofre Bitwarden (20 chars) |
| **ACC-009** | Plataforma de Treinamento/LMS | ✅ Ativo | 🔴 Reuso de Senha | 🟢 Cofre Bitwarden (20 chars) |

---

## 📊 Métricas do Laboratório (Antes × Depois)

| Métrica / Controle | Estado Inicial (Antes) | Estado Final (Depois) | Variação |
| :--- | :---: | :---: | :---: |
| **Contas Auditadas** | 9 | 9 | - |
| **Senhas Reutilizadas** | 7 | 0 | **-100%** |
| **Senhas Fracas / Baixa Entropia** | 6 | 0 | **-100%** |
| **Cobertura no Bitwarden** | 0/9 (0%) | 9/9 (100%) | **+100%** |
| **Adoção de MFA (TOTP)** | 9/9 (100%) | 9/9 (100%) | Mantido |
| **Sessões/Apps Desconhecidos** | 0 | 0 | Mantido Limpo |

---

## 🛡️ Matriz de Classificação de Risco

| Risco Identificado | Nível de Risco | Vetor de Ameaça | Ação de Mitigação Aplicada | Risco Residual |
| :--- | :---: | :--- | :--- | :---: |
| **Senha Reutilizada** | 🔴 Crítico | *Credential Stuffing* a partir de vazamentos de terceiros. | Substituição por senhas únicas de 20-24 caracteres no Bitwarden. | 🟢 Baixo |
| **Senha de Baixa Complexidade** | 🔴 Alto | Ataques de *Brute Force* ou dicionário offline. | Geração automatizada de alta entropia (letras, números, símbolos). | 🟢 Baixo |
| **Ausência de Gestão Central** | 🟡 Médio | Anotações inseguras ou esquecimento de credenciais. | Adoção do Bitwarden com Master Password forte e encriptada. | 🟢 Baixo |
| **Sessões/Apps Antigos** | 🟡 Médio | Hijacking de tokens OAuth ativamente autorizados. | Auditoria e revogação preventiva de sessões/permissões ativas. | 🟢 Baixo |

---

## 📂 Estrutura do Repositório

```text
account-security-hygiene/
│
├── README.md                   # Documentação principal e resumo executivo do laboratório
│
├── checklist/
│   └── security-checklist.md   # Checklist operacional de conformidade contínua
│
├── evidence/
│   └── README.md               # Diretrizes de higienização e anonimização de evidências
│
├── bitwarden/
│   └── configuration.md        # Parâmetros de segurança e regras do cofre de senhas
│
├── mfa/
│   └── mfa-guide.md            # Políticas de autenticação multifator aplicadas
│
├── account-review/
│   └── review-process.md       # Metodologia de auditoria e mapeamento de risco inicial
│
└── lessons-learned/
    └── lessons-learned.md      # Conclusões técnicas e próximos passos do projeto
text```

⚠️ Nota de Segurança e Privacidade
Nenhuma senha, código MFA, token, chave de recuperação, e-mail pessoal ou dado sensível real é
armazenado ou exposto neste repositório. Todas as evidências e referências foram sanitizadas e 
anonimizadas utilizando identificadores fictícios de acordo com os princípios de divulgação e 
documentação segura.

📚 Conclusão e Aprendizados
Este laboratório demonstra na prática que a segurança de uma conta não se resume à criação de uma 
senha forte. Trata-se de um ecossistema integrado de controles defensivos:

Credenciais Exclusivas + MFA Ativo + Mapeamento de Recuperação + Dispositivos Conhecidos + Gestão de 
Sessões + Sanitização de Permissões.
