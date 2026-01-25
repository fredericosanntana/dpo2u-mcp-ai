# Clawdbot + Claude Code Integration

Este repositorio contem skills, configuracoes e documentacao para otimizar o uso do Clawdbot integrando capacidades do Claude Code.

## Estrutura do Projeto

```
dpo2u-mcp-ai/
├── README.md                                    # Este arquivo
├── ESTUDO-INTEGRACAO-CLAWDBOT-CLAUDE-CODE.md   # Estudo completo de integracao
├── skills/                                      # Skills prontas para Clawdbot
│   ├── code-explorer/                          # Exploracao de codigo
│   ├── task-planner/                           # Planejamento de tarefas
│   ├── shell-executor/                         # Execucao de comandos
│   ├── web-researcher/                         # Pesquisa na web
│   ├── task-manager/                           # Gestao de tarefas
│   ├── github-assistant/                       # Operacoes GitHub
│   ├── code-reviewer/                          # Revisao de codigo
│   ├── brainstorming/                          # Sessoes de brainstorming
│   ├── decision-maker/                         # Tomada de decisao
│   ├── problem-solver/                         # Resolucao de problemas
│   └── project-kickoff/                        # Inicio de projetos
└── config/                                      # Configuracoes de exemplo
```

## Skills Disponiveis

### Skills Tecnicas

| Skill | Descricao | Baseado em |
|-------|-----------|------------|
| `code-explorer` | Explora e analisa codebases | Claude Code Explore agent |
| `task-planner` | Planeja implementacoes complexas | Claude Code Plan agent |
| `shell-executor` | Executa comandos com seguranca | Claude Code Bash tool |
| `web-researcher` | Pesquisa informacoes na web | Claude Code WebSearch/WebFetch |
| `task-manager` | Gerencia lista de tarefas | Claude Code TodoWrite |
| `github-assistant` | Operacoes GitHub via gh CLI | Claude Code GitHub integration |
| `code-reviewer` | Revisa codigo | Claude Code review capabilities |

### Skills Cognitivas

| Skill | Descricao | Metodologias |
|-------|-----------|--------------|
| `brainstorming` | Gera ideias criativas | SCAMPER, Six Hats, Mind Map, HMW |
| `decision-maker` | Auxilia decisoes | RICE, Matriz, Pre-mortem, 10/10/10 |
| `problem-solver` | Resolve problemas | 5 Whys, RCA, PDCA, Fishbone |
| `project-kickoff` | Inicia projetos | Templates, RACI, ADRs |

## Instalacao

### 1. Copiar Skills para Clawdbot

```bash
# Copiar todas as skills
cp -r skills/* ~/clawd/skills/

# Ou copiar skill especifica
cp -r skills/code-explorer ~/clawd/skills/
```

### 2. Verificar Instalacao

```bash
ls ~/clawd/skills/
```

### 3. Reiniciar Clawdbot

Reinicie o Clawdbot para carregar as novas skills.

## Uso

### Invocar Skills

As skills podem ser invocadas automaticamente pelo Clawdbot quando o contexto for apropriado, ou manualmente:

```
Explore este projeto e me de uma visao geral da arquitetura
```

```
Planeje a implementacao de um sistema de autenticacao
```

```
Execute git status e mostre o estado do repositorio
```

### Comandos Recomendados

Para usar com as skills:

```
/think high          # Para tarefas complexas
/verbose on          # Para debug
/status              # Ver contexto atual
```

## Configuracao Recomendada

### Modelo

Use Claude Opus para melhor performance:

```json
{
  "agent": {
    "model": "anthropic/claude-opus-4-5"
  }
}
```

### Think Level

Para tarefas de codigo:
```
/think high
```

## Documentacao

- [Estudo Completo de Integracao](./ESTUDO-INTEGRACAO-CLAWDBOT-CLAUDE-CODE.md)
- [Clawdbot GitHub](https://github.com/clawdbot/clawdbot)
- [Claude Code Docs](https://docs.anthropic.com/claude-code)

## Contribuindo

1. Fork este repositorio
2. Crie uma branch para sua feature
3. Faca suas mudancas
4. Abra um Pull Request

## Licenca

MIT
