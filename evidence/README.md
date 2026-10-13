# 🖼️ Índice de Evidências — Cybersecurity Roadmap

Esta pasta reúne capturas de tela que demonstram a execução dos laboratórios práticos do roadmap. As evidências complementam a documentação técnica: ajudam a verificar comandos, configurações, testes e resultados observados durante cada atividade.

> **Fluxo recomendado:** atividade → documentação → evidência → resultado observado → aprendizado.

## 🧭 Navegação rápida

| Diretório | Conteúdo | Índice |
|---|---|---|
| [`week01/`](./week01/) | Capturas iniciais do CyberLab, Linux e outras evidências históricas ainda agrupadas neste diretório | [Abrir pasta](./week01/) |
| [`week02/`](./week02/) | Virtualização, comunicação entre máquinas, reconhecimento de rede e análise de tráfego | [README da Semana 02](./week02/README.md) |
| [`week03/`](./week03/) | Linux Security: permissões, comandos, privilégios e evidências de configuração | [README da Semana 03](./week03/README.md) |
| [`week04/`](./week04/) | Redes: endereçamento IP, conectividade, SSH, Nmap, ARP, DNS, Wireshark e nftables | [Abrir pasta](./week04/) |
| [`windows-server-2025/`](./windows-server-2025/) | Instalação do Windows Server 2025, Active Directory, domínio, usuários, estrutura organizacional e GPOs | [README do laboratório](./windows-server-2025/README.md) |

## 📂 Como explorar as evidências

### Semana 01 — Fundamentos e CyberLab

A pasta [`week01/`](./week01/) contém capturas de atividades iniciais de laboratório. Alguns nomes são históricos e nem todos seguem o padrão de nomenclatura atual; confira a documentação relacionada antes de associar uma captura a uma atividade específica.

### Semana 02 — Virtualização e redes

Consulte o [índice de evidências da Semana 02](./week02/README.md). Ele reúne os registros do ambiente virtualizado e dos testes de comunicação e análise de tráfego.

### Semana 03 — Linux Security

Consulte o [índice de evidências da Semana 03](./week03/README.md) para localizar capturas relacionadas a permissões, privilégios e comandos praticados no Linux.

### Semana 04 — Redes e análise de tráfego

As capturas estão em [`week04/`](./week04/). Entre os registros disponíveis estão:

- **Dia 01:** endereços IP das VMs, conectividade, sockets e reconhecimento com Nmap.
- **Dia 02:** SSH, portas e análise do handshake TCP no Wireshark.
- **Dia 03:** tabela de vizinhos/ARP e captura de tráfego ARP.
- **Dia 04:** configuração de resolução de nomes, consultas DNS e captura no Wireshark.
- **Dia 05:** regras nftables, tráfego filtrado, contadores e validação com Nmap.
- **Dia 07:** evidências de reconhecimento e correlação de eventos de rede.

Os nomes dos arquivos identificam as capturas. Para entender o procedimento, os comandos e a interpretação dos resultados, consulte o [README da Semana 04](../week-04/README.md).

### Windows Server 2025 e Active Directory

O [laboratório Windows Server 2025](./windows-server-2025/README.md) possui índice próprio, com capturas da instalação do AD DS, promoção do controlador de domínio, validação do domínio, criação de usuários, estrutura organizacional e políticas de grupo.

## 📝 Relação com a documentação técnica

- [Índice da documentação](../docs/README.md) — registros técnicos e relatórios organizados por semana.
- [README principal do roadmap](../README.md) — objetivo, evolução e estrutura geral do projeto.
- [README da Semana 04](../week-04/README.md) — atividades de redes e links para as evidências correspondentes.

Uma captura de tela comprova apenas o que está visível nela. Sempre que possível, associe-a ao registro técnico que explica o contexto, o procedimento realizado, o resultado observado e suas limitações.

## 🗂️ Padrão para novas evidências

Use nomes descritivos, sem espaços e com extensão correta:

`week-XX-day-YY-descricao.png`

Para projetos independentes:

`nome-do-projeto-etapa-descricao.png`

Boas práticas:

- Salvar o arquivo na pasta correspondente à semana ou ao laboratório.
- Usar nomes que indiquem a atividade demonstrada.
- Preferir PNG para capturas de tela de terminais e interfaces.
- Evitar duplicatas e arquivos sem relação clara com a documentação.
- Atualizar o README da pasta quando novas evidências relevantes forem adicionadas.

## 🔐 Checklist antes de publicar

- [ ] Não há senhas, tokens, chaves ou outros segredos.
- [ ] Dados pessoais desnecessários foram removidos ou ocultados.
- [ ] IPs, domínios e nomes de máquinas são de laboratório ou foram sanitizados quando necessário.
- [ ] A captura corresponde à atividade descrita.
- [ ] O arquivo está no diretório correto e possui nome descritivo.
- [ ] O link foi conferido no GitHub.
- [ ] A documentação explica o que a captura demonstra, sem alegar resultados que ela não comprova.

---

[← Voltar ao Roadmap](../README.md) · [Abrir documentação técnica](../docs/README.md)
