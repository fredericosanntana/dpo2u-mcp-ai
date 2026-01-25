# Estudo de Integração: Claude Code + Clawdbot

## Objetivo

Otimizar o uso do Clawdbot integrando as capacidades de agentes, skills e comandos do Claude Code para criar um assistente de IA mais poderoso e versátil.

---

## 1. Análise Comparativa dos Sistemas

### 1.1 Arquitetura Clawdbot

| Componente | Descrição |
|------------|-----------|
| **Gateway** | Control plane WebSocket na porta 18789 |
| **Workspace** | `~/clawd` - memoria, logs, skills customizadas |
| **Config** | `~/.clawdbot/clawdbot.json` - configuracao principal |
| **Sessions** | `~/.clawdbot/agents/main/sessions/` - historico |
| **Skills** | Configuradas em `clawdbot.json` ou `~/clawd/skills/` |
| **Agentes** | Runtime Pi com RPC mode e tool streaming |
| **Canais** | WhatsApp, Telegram, Discord, Slack, Signal, etc. |
| **Comandos** | `/status`, `/new`, `/think`, `/verbose`, `/usage`, `/models` |
| **Memoria** | `MEMORY.md` (longo prazo) + `memory/YYYY-MM-DD.md` (diario) |
| **Semantic Search** | Embeddings para busca de contexto historico |

#### Arquivos do Workspace (`~/clawd`)

| Arquivo | Funcao |
|---------|--------|
| `MEMORY.md` | Fatos de longo prazo sobre o usuario |
| `AGENTS.md` | Instrucoes operacionais do agente |
| `SOUL.md` | Persona e personalidade |
| `TOOLS.md` | Notas sobre ferramentas |
| `BOOTSTRAP.md` | Ritual de primeira execucao |
| `USER.md` | Perfil do usuario |
| `memory/` | Logs diarios de conversas |

#### Configuracao de Skills (`~/.clawdbot/clawdbot.json`)

```json
{
  "skills": {
    "entries": {
      "web-search": { "enabled": true },
      "github": {
        "enabled": true,
        "env": { "GITHUB_TOKEN": "token" }
      }
    }
  }
}
```

#### Semantic Search (Memoria de Longo Prazo)

```json
{
  "agents": {
    "defaults": {
      "memorySearch": {
        "provider": "openai",
        "model": "text-embedding-3-small",
        "remote": {
          "apiKey": "your_openai_key"
        }
      }
    }
  }
}
```

### 1.2 Arquitetura Claude Code

| Componente | Descrição |
|------------|-----------|
| **Tools** | Read, Write, Edit, Glob, Grep, Bash, WebFetch, WebSearch, TodoWrite |
| **Subagents** | Explore, Plan, General-purpose, Custom agents |
| **Skills** | Arquivos SKILL.md em `.claude/skills/<skill>/` |
| **MCP** | Model Context Protocol para integrações externas |
| **Hooks** | Sistema de eventos lifecycle (PreToolUse, PostToolUse, etc.) |
| **Comandos** | `/plan`, `/compact`, `/context`, `/mcp`, `/memory`, etc. |

---

## 2. Mapeamento de Capacidades

### 2.1 Subagents Claude Code → Skills Clawdbot

| Claude Code Agent | Função | Skill Clawdbot Equivalente |
|-------------------|--------|----------------------------|
| **Explore** | Busca e análise de código | `code-explorer` |
| **Plan** | Planejamento de implementação | `task-planner` |
| **General-purpose** | Tarefas complexas multi-step | `multi-task` |
| **Bash** | Execução de comandos shell | `shell-executor` |

### 2.2 Tools Claude Code → Comandos/Skills Clawdbot

| Claude Code Tool | Função | Implementação Clawdbot |
|------------------|--------|------------------------|
| **Read** | Ler arquivos | Skill `file-reader` |
| **Write** | Criar/sobrescrever arquivos | Skill `file-writer` |
| **Edit** | Edição cirúrgica de arquivos | Skill `file-editor` |
| **Glob** | Busca por padrões de arquivo | Skill `file-finder` |
| **Grep** | Busca em conteúdo | Skill `content-searcher` |
| **Bash** | Execução de comandos | Skill `shell` |
| **WebFetch** | Busca de conteúdo web | Skill `web-fetcher` |
| **WebSearch** | Pesquisa na web | Skill `web-searcher` |
| **TodoWrite** | Gestão de tarefas | Skill `task-manager` |

### 2.3 Comandos Claude Code → Comandos Clawdbot

| Claude Code | Clawdbot Atual | Recomendação |
|-------------|----------------|--------------|
| `/plan` | - | Implementar `/plan` |
| `/compact` | - | Implementar `/compact` |
| `/context` | `/status` | Expandir `/status` |
| `/memory` | - | Implementar `/memory` |
| `/mcp` | - | Implementar `/mcp` |
| `/tasks` | - | Implementar `/tasks` |
| `/rewind` | `/reset` | Manter `/reset` |

---

## 3. Skills Recomendadas para Criação

### 3.1 Skill: code-explorer

```markdown
---
name: code-explorer
description: Explora e analisa estrutura de código, encontra arquivos e busca padrões
---

# Code Explorer

Você é um agente especializado em explorar e analisar codebases.

## Capacidades

1. **Busca de Arquivos**: Encontre arquivos por nome ou padrão glob
2. **Análise de Estrutura**: Mapeie a estrutura de diretórios
3. **Busca de Código**: Encontre definições, referências e padrões
4. **Documentação**: Gere resumos da estrutura do projeto

## Uso

Para explorar um projeto, especifique:
- Diretório raiz
- Padrões de interesse (ex: `**/*.ts`, `src/**/*.py`)
- O que você está procurando

## Exemplos

\`\`\`bash
# Listar estrutura
find . -type f -name "*.ts" | head -20

# Buscar definições
grep -r "class.*extends" --include="*.ts"

# Analisar imports
grep -r "^import" --include="*.ts" | sort | uniq -c | sort -rn
\`\`\`
```

### 3.2 Skill: task-planner

```markdown
---
name: task-planner
description: Planeja implementações complexas dividindo em etapas acionáveis
---

# Task Planner

Você é um arquiteto de software especializado em planejamento de tarefas.

## Metodologia

1. **Análise**: Entenda o escopo completo da tarefa
2. **Decomposição**: Divida em subtarefas menores
3. **Ordenação**: Defina dependências e prioridades
4. **Estimativa**: Avalie complexidade de cada etapa
5. **Documentação**: Crie checklist acionável

## Formato de Output

Para cada tarefa, forneça:
- [ ] **Tarefa**: Descrição clara
  - Arquivos envolvidos: `lista de arquivos`
  - Dependências: `tarefas anteriores`
  - Complexidade: Baixa/Média/Alta

## Regras

- Nunca pule a fase de análise
- Sempre identifique riscos potenciais
- Sugira testes para cada mudança
- Considere backward compatibility
```

### 3.3 Skill: shell-executor

```markdown
---
name: shell-executor
description: Executa comandos shell com segurança e validação
---

# Shell Executor

Você é um especialista em operações de linha de comando.

## Regras de Segurança

1. **NUNCA** execute comandos destrutivos sem confirmação
2. **SEMPRE** valide paths antes de operações de arquivo
3. **EVITE** comandos com `rm -rf`, `dd`, ou similares
4. **PREFIRA** comandos read-only quando possível

## Comandos Seguros

\`\`\`bash
# Git operations
git status
git log --oneline -10
git diff

# File operations (read-only)
ls -la
cat arquivo.txt
head -20 arquivo.txt

# Process info
ps aux | grep processo
df -h
free -m
\`\`\`

## Comandos que Requerem Confirmação

- Qualquer operação de escrita/delete
- Commits e pushes
- Instalação de pacotes
- Mudanças de configuração
```

### 3.4 Skill: web-researcher

```markdown
---
name: web-researcher
description: Pesquisa informações na web e analisa conteúdo de URLs
---

# Web Researcher

Você é um pesquisador especializado em buscar e sintetizar informações da web.

## Capacidades

1. **Busca**: Pesquise tópicos específicos
2. **Fetch**: Obtenha conteúdo de URLs
3. **Análise**: Extraia informações relevantes
4. **Síntese**: Resuma descobertas

## Formato de Resposta

### Pesquisa: [Tópico]

**Fontes Consultadas:**
- [Título](URL) - Resumo breve

**Descobertas Principais:**
1. Ponto relevante 1
2. Ponto relevante 2

**Conclusão:**
Síntese das informações encontradas
```

### 3.5 Skill: task-manager

```markdown
---
name: task-manager
description: Gerencia lista de tarefas durante conversas longas
---

# Task Manager

Você é um gerenciador de tarefas que mantém track do progresso.

## Estados de Tarefa

- `[ ]` **Pendente**: Não iniciada
- `[→]` **Em Progresso**: Sendo trabalhada
- `[✓]` **Concluída**: Finalizada
- `[✗]` **Bloqueada**: Aguardando dependência

## Formato

### Tarefas Atuais

| # | Status | Tarefa | Notas |
|---|--------|--------|-------|
| 1 | [✓] | Descrição | Completada em X |
| 2 | [→] | Descrição | Em andamento |
| 3 | [ ] | Descrição | Aguardando #2 |

## Comandos

- `/tasks` - Listar todas as tarefas
- `/tasks add <descrição>` - Adicionar tarefa
- `/tasks done <número>` - Marcar como concluída
- `/tasks clear` - Limpar tarefas concluídas
```

---

## 4. Implementação de Novos Comandos

### 4.1 Comando `/plan`

**Propósito**: Entrar em modo de planejamento antes de executar

**Implementação**:
```
/plan <descrição da tarefa>

Quando ativado:
1. Analisa a tarefa solicitada
2. Não executa nenhuma ação imediatamente
3. Apresenta plano detalhado com etapas
4. Aguarda confirmação para prosseguir
```

### 4.2 Comando `/tasks`

**Propósito**: Gerenciar lista de tarefas da sessão

**Implementação**:
```
/tasks - Lista tarefas atuais
/tasks add <descrição> - Adiciona nova tarefa
/tasks done <id> - Marca tarefa como concluída
/tasks clear - Remove tarefas concluídas
```

### 4.3 Comando `/context`

**Propósito**: Visualizar uso de contexto da conversa

**Implementação**:
```
/context

Output:
Tokens usados: 12,450 / 200,000
Contexto: ████████░░░░░░░░░░░░ 6.2%
Mensagens: 24
Arquivos carregados: 3
```

### 4.4 Comando `/memory`

**Propósito**: Gerenciar memória persistente do projeto

**Implementação**:
```
/memory - Mostra memória atual
/memory add <informação> - Adiciona à memória
/memory clear - Limpa memória
```

---

## 5. Integração com MCP (Model Context Protocol)

### 5.1 Conceito

O MCP permite conectar o Clawdbot a ferramentas externas de forma padronizada.

### 5.2 Servidores MCP Recomendados

| Servidor | Função | Uso |
|----------|--------|-----|
| **GitHub MCP** | Operações Git/GitHub | Issues, PRs, repos |
| **Filesystem MCP** | Acesso a arquivos | Read/Write seguro |
| **PostgreSQL MCP** | Acesso a banco | Queries, schemas |
| **Slack MCP** | Integração Slack | Mensagens, canais |
| **Notion MCP** | Documentação | Páginas, databases |

### 5.3 Configuração no Clawdbot

Criar arquivo `.mcp.json` no diretório do Clawdbot:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/allowed/path"]
    }
  }
}
```

---

## 6. Sistema de Hooks

### 6.1 Eventos Disponíveis

Adaptar do Claude Code para Clawdbot:

| Evento | Quando | Uso |
|--------|--------|-----|
| `MessageReceived` | Mensagem recebida | Validação, contexto |
| `BeforeResponse` | Antes de responder | Formatação, filtros |
| `AfterResponse` | Após responder | Logging, analytics |
| `ToolExecution` | Ferramenta executada | Auditoria, limites |
| `SessionStart` | Sessão iniciada | Carregar contexto |
| `SessionEnd` | Sessão finalizada | Salvar estado |

### 6.2 Exemplo de Hook

```json
{
  "hooks": {
    "BeforeResponse": [
      {
        "type": "command",
        "command": "echo 'Validating response...'",
        "timeout": 5
      }
    ],
    "ToolExecution": [
      {
        "matcher": "shell.*",
        "hooks": [
          {
            "type": "command",
            "command": "scripts/validate-shell-command.sh"
          }
        ]
      }
    ]
  }
}
```

---

## 7. Estrutura de Skills Clawdbot

### 7.1 Formato SKILL.md

```markdown
---
name: skill-name
description: Descrição curta do que a skill faz
---

# Nome da Skill

Instruções detalhadas para o agente.

## Quando Usar

Descreva situações de uso.

## Como Usar

Exemplos e comandos.

## Exemplos

\`\`\`bash
# Exemplo de comando
comando exemplo
\`\`\`
```

### 7.2 Localização

```
~/clawd/skills/
├── code-explorer/
│   └── SKILL.md
├── task-planner/
│   └── SKILL.md
├── shell-executor/
│   └── SKILL.md
├── web-researcher/
│   └── SKILL.md
└── task-manager/
    └── SKILL.md
```

---

## 8. Roadmap de Implementação

### Fase 1: Skills Básicas (Semana 1-2)
- [ ] Criar skill `code-explorer`
- [ ] Criar skill `shell-executor`
- [ ] Criar skill `file-editor`
- [ ] Testar integração básica

### Fase 2: Skills Avançadas (Semana 3-4)
- [ ] Criar skill `task-planner`
- [ ] Criar skill `task-manager`
- [ ] Criar skill `web-researcher`
- [ ] Implementar comando `/tasks`

### Fase 3: Comandos (Semana 5-6)
- [ ] Implementar `/plan`
- [ ] Implementar `/context`
- [ ] Implementar `/memory`
- [ ] Expandir `/status`

### Fase 4: Integrações (Semana 7-8)
- [ ] Configurar MCP servers
- [ ] Implementar sistema de hooks
- [ ] Testar integrações externas
- [ ] Documentar configurações

### Fase 5: Otimização (Semana 9-10)
- [ ] Performance tuning
- [ ] Ajuste de prompts
- [ ] Testes de usuário
- [ ] Documentação final

---

## 9. Configuração Recomendada

### 9.1 Modelo

```json
{
  "agent": {
    "model": "anthropic/claude-opus-4-5"
  }
}
```

### 9.2 Think Level

Para tarefas complexas, usar:
```
/think high
```

### 9.3 Verbosidade

Para debug:
```
/verbose on
```

---

## 10. Métricas de Sucesso

| Métrica | Antes | Meta |
|---------|-------|------|
| Tempo de resposta para tarefas de código | N/A | < 30s |
| Taxa de sucesso em operações de arquivo | N/A | > 95% |
| Satisfação do usuário | N/A | > 4.5/5 |
| Tarefas concluídas sem intervenção | N/A | > 80% |

---

## 11. Referências

- [Clawdbot GitHub](https://github.com/clawdbot/clawdbot)
- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [Agent Skills Standard](https://agentskills.org)

---

## 12. Próximos Passos

1. **Validar** este estudo com a equipe
2. **Priorizar** skills mais importantes
3. **Criar** ambiente de desenvolvimento
4. **Implementar** primeira skill (code-explorer)
5. **Testar** integração com Clawdbot
6. **Iterar** baseado em feedback

---

*Documento criado em: Janeiro 2026*
*Versão: 1.0*
