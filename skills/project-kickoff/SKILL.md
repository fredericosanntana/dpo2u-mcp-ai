---
name: project-kickoff
description: Estrutura o inicio de novos projetos com planejamento e documentacao
---

# Project Kickoff

Voce e um gerente de projetos que ajuda a estruturar o inicio de novos projetos de forma organizada e completa.

## Quando Usar

- Iniciar um novo projeto
- Criar documentacao inicial
- Definir escopo e objetivos
- Planejar arquitetura
- Organizar time e responsabilidades

## Template de Kickoff

```markdown
# Project Kickoff: [Nome do Projeto]

## 1. Visao Geral

### Problema
[Qual problema estamos resolvendo?]

### Solucao
[Como vamos resolver?]

### Objetivos (SMART)
- **S**pecifico: [O que exatamente]
- **M**ensuravel: [Como medir sucesso]
- **A**lcancavel: [E realista?]
- **R**elevante: [Por que importa]
- **T**emporal: [Ate quando]

### Nao-Escopo
[O que NAO faz parte deste projeto]

---

## 2. Stakeholders

| Papel | Nome | Responsabilidade |
|-------|------|------------------|
| Product Owner | @nome | Decisoes de produto |
| Tech Lead | @nome | Decisoes tecnicas |
| Designer | @nome | UX/UI |
| Dev | @nome | Implementacao |

### RACI Matrix

| Atividade | Responsavel | Aprovador | Consultado | Informado |
|-----------|-------------|-----------|------------|-----------|
| Arquitetura | Tech Lead | PO | Devs | Todos |
| Design | Designer | PO | Tech Lead | Devs |
| Codigo | Devs | Tech Lead | - | PO |

---

## 3. Requisitos

### Funcionais
- [ ] RF01: [Requisito 1]
- [ ] RF02: [Requisito 2]
- [ ] RF03: [Requisito 3]

### Nao-Funcionais
- [ ] RNF01: Performance - [especificacao]
- [ ] RNF02: Seguranca - [especificacao]
- [ ] RNF03: Escalabilidade - [especificacao]

### User Stories

**US01:** Como [persona], quero [acao] para [beneficio]

**Criterios de Aceite:**
- [ ] Dado [contexto], quando [acao], entao [resultado]
- [ ] Dado [contexto], quando [acao], entao [resultado]

---

## 4. Arquitetura

### Tech Stack

| Camada | Tecnologia | Justificativa |
|--------|------------|---------------|
| Frontend | React | Time experiente |
| Backend | Node.js | Produtividade |
| Database | PostgreSQL | Confiabilidade |
| Infra | AWS | Escala |

### Diagrama de Arquitetura

\`\`\`
[Cliente] --> [CDN] --> [Load Balancer]
                              |
                    +---------+---------+
                    |                   |
               [API Server]        [API Server]
                    |                   |
                    +---------+---------+
                              |
                         [Database]
\`\`\`

### ADRs (Architecture Decision Records)

**ADR-001: Usar PostgreSQL em vez de MongoDB**
- Status: Aceito
- Contexto: Precisamos de ACID compliance
- Decisao: PostgreSQL
- Consequencias: Mais estrutura, menos flexibilidade

---

## 5. Cronograma

### Milestones

| Marco | Data | Entregavel |
|-------|------|------------|
| M1 - Setup | Semana 1 | Ambiente configurado |
| M2 - MVP | Semana 4 | Features core funcionando |
| M3 - Beta | Semana 6 | Testes com usuarios |
| M4 - Launch | Semana 8 | Producao |

### Fases

**Fase 1: Discovery & Setup (Semana 1)**
- [ ] Definir requisitos detalhados
- [ ] Setup de ambiente
- [ ] CI/CD configurado
- [ ] Repositorio criado

**Fase 2: Core Development (Semanas 2-4)**
- [ ] Feature 1
- [ ] Feature 2
- [ ] Feature 3
- [ ] Testes unitarios

**Fase 3: Polish & Beta (Semanas 5-6)**
- [ ] Bug fixes
- [ ] Performance tuning
- [ ] Beta testing
- [ ] Feedback loop

**Fase 4: Launch (Semanas 7-8)**
- [ ] Documentacao final
- [ ] Deploy producao
- [ ] Monitoramento
- [ ] Retrospectiva

---

## 6. Riscos

| Risco | Probabilidade | Impacto | Mitigacao |
|-------|---------------|---------|-----------|
| Atraso | Media | Alto | Buffer de 20% |
| Escopo creep | Alta | Medio | Change request process |
| Tech debt | Media | Alto | Code review rigoroso |
| Turnover | Baixa | Alto | Documentacao |

---

## 7. Comunicacao

### Rituais

| Ritual | Frequencia | Duracao | Participantes |
|--------|------------|---------|---------------|
| Daily | Diaria | 15min | Devs |
| Sprint Planning | Bi-semanal | 1h | Time |
| Demo | Bi-semanal | 30min | Stakeholders |
| Retro | Bi-semanal | 1h | Time |

### Canais

- **Slack:** #projeto-x (discussoes rapidas)
- **Jira:** Tracking de tarefas
- **Confluence:** Documentacao
- **GitHub:** Codigo e PRs

---

## 8. Definition of Done

Uma feature so esta "pronta" quando:

- [ ] Codigo revisado (PR aprovado)
- [ ] Testes passando (unit + integration)
- [ ] Documentacao atualizada
- [ ] Deploy em staging
- [ ] QA aprovado
- [ ] Product Owner aceita

---

## 9. Metricas de Sucesso

### KPIs do Projeto
| Metrica | Baseline | Meta | Atual |
|---------|----------|------|-------|
| Velocity | - | 30 pts/sprint | - |
| Bug rate | - | < 5% | - |
| Coverage | - | > 80% | - |

### KPIs do Produto
| Metrica | Baseline | Meta | Atual |
|---------|----------|------|-------|
| Usuarios ativos | 0 | 1000 | - |
| NPS | - | > 50 | - |
| Retention | - | > 60% | - |

---

## 10. Proximos Passos

### Imediato (Esta semana)
1. [ ] Aprovar este documento
2. [ ] Setup de repositorio
3. [ ] Configurar CI/CD
4. [ ] Primeira sprint planning

### Curto prazo (Proximo mes)
1. [ ] MVP funcional
2. [ ] Primeiros usuarios de teste
3. [ ] Feedback inicial

---

## Aprovacoes

| Stakeholder | Aprovado | Data |
|-------------|----------|------|
| Product Owner | [ ] | - |
| Tech Lead | [ ] | - |
| Sponsor | [ ] | - |
```

## Checklist de Kickoff

### Antes da Reuniao
- [ ] Documento de kickoff preparado
- [ ] Stakeholders identificados
- [ ] Agenda enviada
- [ ] Sala/call reservada

### Durante a Reuniao
- [ ] Apresentar visao e objetivos
- [ ] Alinhar expectativas
- [ ] Definir papeis
- [ ] Discutir riscos
- [ ] Definir proximos passos

### Apos a Reuniao
- [ ] Enviar ata
- [ ] Criar repositorio/board
- [ ] Agendar rituais
- [ ] Primeira tarefa atribuida

## Dicas

1. **Envolva stakeholders cedo** - Alinhamento evita retrabalho
2. **Documente decisoes** - ADRs salvam discussoes futuras
3. **Defina "pronto"** - Evita debates sobre completude
4. **Planeje para falhar** - Riscos mitigados sao gerenciaveis
5. **Comece pequeno** - MVP primeiro, escala depois
6. **Celebre marcos** - Motivacao importa
