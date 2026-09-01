# 🛡️ Cybersecurity Roadmap — 24 Weeks

> Jornada prática de estudos em Cybersecurity, com foco em fundamentos, laboratórios, documentação, análise de evidências e construção de portfólio.

---

## 📌 Sobre este projeto

Este repositório documenta minha jornada de estudos em Cybersecurity durante 24 semanas.

O objetivo não é apenas concluir conteúdos teóricos, mas desenvolver a capacidade de:

* compreender fundamentos de computação e segurança;
* montar e utilizar laboratórios seguros;
* executar experimentos práticos;
* analisar evidências;
* investigar problemas;
* documentar métodos e resultados;
* explicar decisões técnicas;
* refazer laboratórios sem depender de tutoriais;
* construir projetos práticos para portfólio.

A metodologia adotada será baseada no ciclo:

**Estudar → Executar → Documentar → Explicar → Refazer**

---

# 🎯 Objetivo da jornada

Ao final das 24 semanas, meu objetivo é conseguir demonstrar conhecimentos práticos em:

* Fundamentos de computação;
* Linux;
* Redes;
* Windows;
* Python aplicado à segurança;
* Segurança Web;
* Pentest autorizado;
* SOC;
* Detecção;
* DFIR;
* Cloud Security;
* GRC;
* Threat Modeling.

Além do conhecimento técnico, o foco será desenvolver capacidade de investigação e documentação técnica.

---

# 🧪 CyberLab

Os laboratórios serão realizados em ambientes próprios, controlados e autorizados.

O ambiente será construído de forma:

* isolada;
* reversível;
* documentada;
* utilizando dados fictícios;
* sem credenciais ou informações reais;
* com snapshots antes de mudanças relevantes.

A infraestrutura será expandida gradualmente conforme novos conteúdos forem estudados.

---

# 📂 Estrutura do repositório

```text
cybersecurity-roadmap/
│
├── README.md
│
├── week-01/
│   ├── README.md
│   ├── notes/
│   ├── evidence/
│   └── docs/
│
├── week-02/
│
├── week-03/
│
├── ...
│
├── projects/
│
└── resources/
```

---

# 📅 Progresso

## Semana 01 — Fundamentos + CyberLab

**Período:** 31/08/2026 – 06/09/2026

### Objetivo da semana

Construir a base de computação necessária para os próximos módulos e preparar o ambiente inicial de laboratório.

### Conteúdos

* CPU;
* RAM;
* armazenamento;
* processos;
* arquivos;
* sistema operacional;
* virtualização;
* máquinas virtuais;
* host e guest;
* hypervisor;
* snapshots;
* fundamentos de segurança;
* hash;
* autenticação e autorização.

### Laboratórios planejados

* Inventário do ambiente;
* Identificação de recursos da VM;
* Observação de processos;
* Exercícios com arquivos;
* Exercício de hash;
* Preparação do CyberLab.

### Evidências

As evidências produzidas durante os laboratórios serão armazenadas na pasta:

week-01/evidence/

### Documentação

Cada laboratório será documentado seguindo o princípio:

**Pergunta → Comando/Filtro → Resultado → Interpretação → Limitação**

---

# 🧠 Diário de aprendizagem

## Dia 01 — 31/08/2026

### Pergunta do dia

Como um computador transforma um programa armazenado em disco em algo que está efetivamente sendo executado?

### O que estudei

* CPU;
* RAM;
* armazenamento;
* processos;
* arquivos;
* sistema operacional.

### O que consegui explicar
### O que consegui executar
### Comandos utilizados

bash
ps
ps aux
ps aux --sort=-%cpu | head
pwd
ls -la
df -h
free -h

### Evidências
### Erro útil
### O que o erro me ensinou
### O que ainda não sei
### Reflexão

---

# 📊 Acompanhamento

A cada semana serão avaliados quatro aspectos:

| Indicador  | Nota |
| ---------- | ---: |
| Expliquei  |  0–5 |
| Executei   |  0–5 |
| Documentei |  0–5 |
| Refiz      |  0–5 |

### Critério pessoal

**0** — Não estudei.

**1** — Apenas vi o conteúdo.

**2** — Entendi superficialmente.

**3** — Consigo executar com bastante consulta.

**4** — Consigo executar e explicar com pequenas consultas.

**5** — Consigo executar, explicar, documentar e reproduzir sem depender do tutorial.

---

# 🐛 Erros úteis

Os erros encontrados durante os laboratórios serão registrados neste projeto.

O objetivo não é esconder erros, mas utilizá-los como parte do processo de aprendizagem.

Para cada erro:

1. O que aconteceu?
2. Qual era a expectativa?
3. Qual foi a causa?
4. Como investiguei?
5. Como resolvi?
6. O que aprendi?
7. Como evitaria o problema novamente?

---

# 🏆 Projetos de portfólio

Ao longo da jornada serão desenvolvidos projetos práticos.

Projetos planejados:

* [ ] Linux Troubleshooting
* [ ] Network Assessment
* [ ] Windows Investigation
* [ ] Python Security Automation
* [ ] Web Security
* [ ] Mini Pentest
* [ ] SOC Investigation
* [ ] DFIR Timeline
* [ ] Threat Modeling
* [ ] Capstone — Operação Café Frio


---

# 🔐 Ética e segurança

Todos os testes práticos serão realizados somente em ambientes próprios, fictícios ou explicitamente autorizados.

Nenhuma informação sensível, credencial real, chave de API ou dado corporativo será armazenado neste repositório.

As evidências publicadas serão sanitizadas antes de qualquer publicação.

---