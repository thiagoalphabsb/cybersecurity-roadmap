# 📋 Security Account Checklist — Account Security Hygiene Lab

Este checklist documenta as práticas de segurança aplicadas e validadas em todas as contas
do escopo do laboratório (ACC-001 a ACC-009).

## 🔑 Credenciais e Gestão de Cofre
- [x] Todas as contas possuem senhas exclusivas (sem reutilização).
- [x] Senhas fracas foram substituídas por senhas de alta entropia (20–24 caracteres).
- [x] Implementação de palavra-chave secreta personalizada em camadas no Bitwarden.
- [x] 100% das credenciais centralizadas e criptografadas no Bitwarden.
- [x] Preenchimento automático e gerador de senhas adotados como padrão.

## 🛡️ Autenticação em Duas Etapas (MFA)
- [x] MFA habilitado em todas as contas de criticidade crítica (e-mails, GitHub, serviços financeiros).
- [x] MFA habilitado em todas as redes sociais (criticidade média).
- [x] Priorização de aplicativos autenticadores em detrimento de métodos vulneráveis como SMS.
- [x] Códigos de recuperação gerados, salvos com segurança e testados.

## 🔎 Revisão de Acessos, Sessões e Permissões
- [x] Aplicativos de terceiros conectados revisados e conexões órfãs revogadas.
- [x] Sessões ativas e dispositivos desconhecidos encerrados.
- [x] E-mails e telefones de recuperação de contas validados e atualizados.

## 🔄 Validação e Ciclo de Vida
- [x] Teste prático de ciclo de vida (logout/login) executado com sucesso após cada alteração.
- [x] Matriz de risco revisada com redução de status de 🔴 Alto Risco para 🟢 Baixo Risco em todo
o escopo.
