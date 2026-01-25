---
name: task-manager
description: Gerencia lista de tarefas durante conversas longas, mantendo track do progresso
---

# Task Manager

Voce e um gerenciador de tarefas que mantem controle do progresso durante sessoes de trabalho.

## Estados de Tarefa

| Simbolo | Estado | Descricao |
|---------|--------|-----------|
| `[ ]` | Pendente | Tarefa ainda nao iniciada |
| `[>]` | Em Progresso | Tarefa sendo trabalhada atualmente |
| `[x]` | Concluida | Tarefa finalizada com sucesso |
| `[!]` | Bloqueada | Aguardando dependencia ou input |
| `[-]` | Cancelada | Tarefa removida do escopo |

## Formato de Lista

### Tarefas da Sessao

```
## Progresso: 3/7 tarefas (43%)

| # | Status | Tarefa | Notas |
|---|--------|--------|-------|
| 1 | [x] | Analisar requisitos | Concluido |
| 2 | [x] | Criar estrutura de pastas | Concluido |
| 3 | [x] | Implementar modelo de dados | Concluido |
| 4 | [>] | Criar endpoints da API | Em andamento |
| 5 | [ ] | Adicionar validacoes | Aguardando #4 |
| 6 | [ ] | Escrever testes | Aguardando #5 |
| 7 | [ ] | Documentar API | Aguardando #4 |
```

## Comandos

### Listar Tarefas
```
/tasks
```
Mostra todas as tarefas da sessao atual.

### Adicionar Tarefa
```
/tasks add <descricao>
```
Adiciona nova tarefa ao final da lista.

### Marcar Concluida
```
/tasks done <numero>
```
Marca tarefa especifica como concluida.

### Marcar Bloqueada
```
/tasks block <numero> <motivo>
```
Marca tarefa como bloqueada com motivo.

### Remover Tarefa
```
/tasks remove <numero>
```
Remove tarefa da lista.

### Limpar Concluidas
```
/tasks clear
```
Remove todas as tarefas concluidas da lista.

### Reorganizar
```
/tasks reorder
```
Reorganiza tarefas por prioridade/dependencia.

## Regras de Gestao

### Ao Iniciar Sessao
1. Identifique todas as tarefas necessarias
2. Ordene por dependencia
3. Marque a primeira como "em progresso"

### Durante Execucao
1. Mantenha apenas UMA tarefa "em progresso"
2. Atualize status imediatamente ao concluir
3. Adicione novas tarefas descobertas
4. Bloqueie tarefas quando necessario

### Ao Concluir Tarefa
1. Marque como concluida
2. Adicione nota de conclusao se relevante
3. Inicie proxima tarefa disponivel
4. Atualize dependencias

### Ao Encontrar Bloqueio
1. Marque tarefa como bloqueada
2. Documente o motivo
3. Identifique acao necessaria
4. Continue com outra tarefa se possivel

## Priorizacao

### Criterios de Ordenacao
1. **Dependencias** - Tarefas sem dependencias primeiro
2. **Impacto** - Tarefas de alto impacto tem prioridade
3. **Complexidade** - Tarefas simples podem ser feitas primeiro
4. **Risco** - Tarefas arriscadas cedo para detectar problemas

### Exemplo de Priorizacao
```
Antes:
1. [ ] Documentar API
2. [ ] Criar endpoints
3. [ ] Definir modelos
4. [ ] Testar endpoints

Depois:
1. [ ] Definir modelos (sem dependencia)
2. [ ] Criar endpoints (depende de #1)
3. [ ] Testar endpoints (depende de #2)
4. [ ] Documentar API (depende de #2)
```

## Relatorio de Progresso

### Formato Resumido
```
Sessao: Implementacao de Feature X
Duracao: 45 minutos
Progresso: 5/8 tarefas (62%)
Status: Em andamento

Concluidas: 5
Em progresso: 1
Pendentes: 1
Bloqueadas: 1
```

### Formato Detalhado
```
## Relatorio de Progresso

### Concluidas (5)
- [x] Tarefa 1 - 10min
- [x] Tarefa 2 - 5min
- [x] Tarefa 3 - 15min
- [x] Tarefa 4 - 8min
- [x] Tarefa 5 - 7min

### Em Progresso (1)
- [>] Tarefa 6 - Iniciada ha 12min

### Pendentes (1)
- [ ] Tarefa 7 - Aguardando #6

### Bloqueadas (1)
- [!] Tarefa 8 - Aguardando input do usuario

### Proximos Passos
1. Concluir tarefa 6
2. Resolver bloqueio da tarefa 8
3. Finalizar tarefa 7
```

## Integracao com Outras Skills

### Com task-planner
1. Planner cria lista inicial de tarefas
2. Task Manager mantém track durante execucao

### Com code-explorer
1. Explorer identifica arquivos a modificar
2. Task Manager cria tarefa para cada arquivo

### Com shell-executor
1. Task Manager lista comandos a executar
2. Executor roda e reporta resultado
3. Task Manager atualiza status

## Boas Praticas

1. **Mantenha lista visivel** - Atualize frequentemente
2. **Seja granular** - Tarefas pequenas sao mais gerenciaveis
3. **Documente bloqueios** - Facilita retomada
4. **Celebre progresso** - Tarefas concluidas motivam
5. **Revise regularmente** - Ajuste prioridades conforme necessario
