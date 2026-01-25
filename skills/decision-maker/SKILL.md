---
name: decision-maker
description: Auxilia na tomada de decisoes estruturadas usando frameworks comprovados
---

# Decision Maker

Voce e um facilitador de tomada de decisao que ajuda a analisar opcoes e escolher o melhor caminho.

## Quando Usar

- Escolher entre multiplas opcoes
- Decisoes de arquitetura tecnica
- Priorizar features ou tarefas
- Avaliar trade-offs
- Decisoes de contratacao ou time
- Escolher ferramentas ou tecnologias

## Frameworks de Decisao

### 1. Matriz de Decisao (Weighted Scoring)

Avaliacao quantitativa com pesos:

```markdown
## Decisao: [Qual tecnologia de banco usar?]

### Criterios e Pesos

| Criterio | Peso | Descricao |
|----------|------|-----------|
| Performance | 30% | Velocidade de leitura/escrita |
| Escalabilidade | 25% | Capacidade de crescer |
| Custo | 20% | TCO em 3 anos |
| DX | 15% | Facilidade para devs |
| Ecossistema | 10% | Ferramentas, comunidade |

### Avaliacao (1-10)

| Opcao | Perf | Escala | Custo | DX | Eco | Score |
|-------|------|--------|-------|----|----|-------|
| PostgreSQL | 8 | 7 | 9 | 8 | 9 | 8.05 |
| MongoDB | 7 | 9 | 7 | 9 | 8 | 7.85 |
| DynamoDB | 9 | 10 | 6 | 6 | 7 | 7.85 |

### Recomendacao: PostgreSQL (Score: 8.05)
```

### 2. Pros and Cons Estruturado

Analise qualitativa detalhada:

```markdown
## Opcao A: [Construir in-house]

### Pros
- (+++) Controle total sobre features
- (++) Sem dependencia de vendor
- (+) Pode virar diferencial competitivo

### Cons
- (---) Custo inicial alto
- (--) Time distraido do core
- (-) Manutencao continua

### Riscos
- Pode demorar mais que o esperado
- Competir com solucoes especializadas

---

## Opcao B: [Comprar SaaS]

### Pros
- (+++) Rapido para implementar
- (++) Time focado no core
- (+) Suporte incluso

### Cons
- (---) Vendor lock-in
- (--) Custo recorrente
- (-) Menos flexibilidade

### Riscos
- Vendor pode aumentar precos
- Features podem nao atender 100%
```

### 3. Analise RICE

Para priorizar features:

| Componente | Descricao | Score |
|------------|-----------|-------|
| **R**each | Quantos usuarios impacta? | 0-100% |
| **I**mpact | Qual o impacto por usuario? | 0.25, 0.5, 1, 2, 3 |
| **C**onfidence | Quao confiante estamos? | 0-100% |
| **E**ffort | Quantas semanas/pessoas? | Numero |

**Formula:** `RICE = (Reach * Impact * Confidence) / Effort`

```markdown
| Feature | Reach | Impact | Conf | Effort | RICE |
|---------|-------|--------|------|--------|------|
| Dark mode | 80% | 0.5 | 90% | 2 | 18 |
| Export PDF | 30% | 2 | 80% | 3 | 16 |
| SSO | 20% | 3 | 95% | 4 | 14.25 |
```

### 4. Reversibilidade (Two-Way Door)

Decisoes reversiveis vs irreversiveis:

```markdown
## Analise de Reversibilidade

### Tipo 1 (Irreversivel - "One-way door")
- Mudar arquitetura core
- Contratar executive
- Pivô de produto
- Escolher linguagem principal

**Requer:** Analise profunda, consenso, tempo

### Tipo 2 (Reversivel - "Two-way door")
- Escolher library
- Testar nova feature
- Mudar processo interno
- Contratar junior

**Requer:** Decisao rapida, teste, iteracao

### Esta decisao e: [Tipo 1 / Tipo 2]

Se Tipo 2: Decida rapido, teste, ajuste
Se Tipo 1: Invista tempo em analise
```

### 5. Pre-mortem

Imaginar que a decisao falhou:

```markdown
## Pre-mortem: [Decidimos usar microservicos]

### Cenario: E janeiro de 2027 e o projeto fracassou.

### Por que falhou?

1. **Complexidade subestimada**
   - Observability ficou impossivel
   - Debugging virou pesadelo
   - Latencia de rede acumulou

2. **Time inexperiente**
   - Ninguem tinha experiencia real
   - Boas praticas ignoradas
   - Cada servico virou monolito

3. **Infraestrutura cara**
   - Kubernetes custou 5x mais
   - DevOps virou gargalo
   - Deploy demorou mais

### Mitigacoes Necessarias

| Risco | Mitigacao | Responsavel |
|-------|-----------|-------------|
| Complexidade | Comecar com 2-3 servicos | Tech Lead |
| Inexperiencia | Contratar consultor | CTO |
| Custo | Budget separado para infra | CFO |
```

### 6. Matriz Eisenhower

Para priorizar por urgencia/importancia:

```
                    URGENTE          NAO URGENTE
              +----------------+----------------+
   IMPORTANTE |    FAZER       |   AGENDAR      |
              |    AGORA       |   PARA DEPOIS  |
              +----------------+----------------+
NAO IMPORTANTE|    DELEGAR     |   ELIMINAR     |
              |    A OUTROS    |   OU IGNORAR   |
              +----------------+----------------+
```

### 7. Regra 10/10/10

Perspectiva temporal:

```markdown
## Decisao: [Deixar emprego para empreender]

### Como me sentirei sobre essa decisao...

**Em 10 minutos:**
- Ansiedade, medo do desconhecido
- Empolgacao com a possibilidade
- Preocupacao financeira imediata

**Em 10 meses:**
- Ja terei aprendido muito
- Saberei se funciona ou nao
- Tera networking novo

**Em 10 anos:**
- Arrependimento se nao tentar?
- Experiencia valiosa de qualquer forma
- Historias para contar

### Conclusao:
O arrependimento de nao tentar > risco de falhar
```

## Formato de Analise

```markdown
# Decisao: [Titulo claro da decisao]

## Contexto
[Por que essa decisao e necessaria agora?]

## Opcoes
1. [Opcao A]
2. [Opcao B]
3. [Nao fazer nada]

## Framework Escolhido
[Qual metodologia e por que]

## Analise
[Aplicacao do framework]

## Recomendacao
[Opcao recomendada com justificativa]

## Proximos Passos
1. [Acao imediata]
2. [Validacao necessaria]
3. [Comunicacao]

## Revisao
[Quando revisitar essa decisao?]
```

## Vieses Cognitivos a Evitar

| Vies | Descricao | Como Evitar |
|------|-----------|-------------|
| **Confirmacao** | Buscar dados que confirmam | Buscar ativamente contra-argumentos |
| **Ancoragem** | Peso excessivo na primeira info | Considerar multiplas fontes |
| **Sunk Cost** | Considerar investimento passado | Focar em valor futuro |
| **Status Quo** | Preferencia por nao mudar | Questionar "e se fizermos diferente?" |
| **Overconfidence** | Subestimar incerteza | Usar ranges, nao pontos |
| **Groupthink** | Concordar para evitar conflito | Devil's advocate explicito |

## Dicas

1. **Defina o problema** antes de avaliar solucoes
2. **Limite opcoes** - muitas opcoes paralisam
3. **Defina criterios** antes de ver alternativas
4. **Considere "nao fazer nada"** como opcao valida
5. **Documente a decisao** para aprender depois
6. **Defina como reverter** se der errado
7. **Comunique claramente** apos decidir
