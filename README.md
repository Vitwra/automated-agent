# Automated Agent 🤖

Um sistema de agentes inteligentes baseado em IA que automatiza a organização de tarefas e gerenciamento de projetos. O projeto integra agentes com modelos de linguagem avançados para criar uma experiência de gerenciamento de tarefas conversacional e intuitiva.

---

## 📋 Visão Geral do Projeto

**Automated Agent** é uma plataforma que combina a inteligência artificial (Google Gemini) com serviços de gerenciamento de tarefas (Trello) para criar um sistema automático de organização de trabalho. O agente conversacional pode:

- 🗓️ Gerenciar tarefas diárias automaticamente
- 📝 Criar, listar e filtrar tarefas
- 🔄 Atualizar status de tarefas em tempo real
- ⏰ Fornecer contexto temporal para organização
- 💬 Interagir de forma natural e intuitiva

---

## 🏗️ Arquitetura do Projeto

```
automated-agent/
├── agents/
│   ├── agent04/
│   │   ├── agenttaskmanager/
│   │   │   ├── __init__.py
│   │   │   └── agent.py          # Lógica principal do agente
│   │   └── requirements.txt
│   ├── .adk/                      # Configuração Google ADK
│   ├── .lab/                      # Ambiente de laboratório
│   └── requirements.txt
├── .git/                          # Controle de versão
├── .gitignore
└── README.md                      # Este arquivo
```

---

## 🛠️ Tecnologias Utilizadas

### Backend & IA
- **[Google AI Development Kit (ADK)](https://ai.google.dev/adk)** - Framework para desenvolvimento de agentes com IA
- **[Gemini 2.5 Flash](https://ai.google.dev/models/gemini-2-5-flash)** - Modelo de linguagem grande (LLM) para processamento natural de linguagem
- **Python 3.x** - Linguagem de programação principal

### Integrações
- **[Trello API](https://developer.atlassian.com/cloud/trello/rest/api-reference/)** - Plataforma de gerenciamento de tarefas com suporte a API
- **[py-trello](https://github.com/sarushan/Trello-API-python-wrapper)** - Wrapper Python para a Trello API

### Utilitários
- **python-dotenv** - Gerenciamento de variáveis de ambiente (credenciais)
- **datetime** - Processamento de datas e horas

---

## 🚀 Funcionalidades Principais

### 1. **Adicionar Tarefas** (`adicionar_tarefa`)
Cria novas tarefas no Trello com nome, descrição e data de vencimento.

```python
adicionar_tarefa(
    nome_da_task="Implementar autenticação",
    descricao_da_task="Adicionar sistema de login com OAuth",
    due_date="2026-05-31"
)
```

### 2. **Listar Tarefas** (`listar_tarefas`)
Retorna todas as tarefas ou filtra por status:
- "todas" - Todas as tarefas
- "a fazer" - Tarefas pendentes
- "em andamento" - Tarefas em progresso
- "concluido" - Tarefas concluídas

```python
tarefas = listar_tarefas(status="em andamento")
# Retorna: [{"nome": "...", "descricao": "...", "status": "...", ...}]
```

### 3. **Atualizar Status** (`mudar_status_tarefa`)
Move tarefas entre diferentes listas no Trello.

```python
mudar_status_tarefa(
    nome_da_task="Implementar autenticação",
    novo_status="em andamento"
)
```

### 4. **Contexto Temporal** (`get_temporal_context`)
Fornece data e hora atual formatadas para organização de tarefas.

```python
contexto = get_temporal_context()
# Retorna: "2026/05/23 18:40:53"
```

### 5. **Agente Conversacional**
Um agente de IA que:
- Inicia conversas perguntando as tarefas do dia
- Cria cards automaticamente
- Continua perguntando até que não haja mais tarefas
- Gerencia todo o ciclo de vida das tarefas

---

## 📦 Dependências

```
google-adk
py-trello
datetime
python-dotenv
```

Para instalar as dependências:

```bash
pip install -r agents/requirements.txt
```

---

## 🔐 Configuração & Variáveis de Ambiente

O projeto utiliza credenciais do Trello armazenadas em arquivo `.env`:

```env
TRELLO_API_KEY=seu_api_key
TRELLO_API_SECRET=seu_api_secret
TRELLO_TOKEN=seu_token
```

### Como Obter as Credenciais:
1. Acesse [https://trello.com/app-key](https://trello.com/app-key)
2. Gere o API Key
3. Crie um Token com permissões apropriadas
4. Crie um board no Trello chamado "AutomatedAgent" com listas: "A FAZER", "EM ANDAMENTO", "CONCLUÍDO"

---

## 💡 Como o Agente Funciona

O agente é baseado em **Agentic AI** - um padrão onde um LLM atua como um raciocínio central que pode:

1. **Entender intents do usuário** em linguagem natural
2. **Selecionar ferramentas apropriadas** baseado no contexto
3. **Executar ações** através das APIs do Trello
4. **Aprender com o contexto** para melhorar respostas

**Instrução do Agente:**
> Você é um agente de organização de tarefas. Sua função é receber uma tarefa e criar um card no Trello com o nome e descrição da tarefa. Você deve me perguntar as atividades que tenho no dia e criar um card para cada uma delas.

---

## 📊 Estrutura de Dados

Cada tarefa no sistema possui:

```json
{
  "nome": "Nome da tarefa",
  "descricao": "Descrição detalhada",
  "vencimento": "Data de vencimento",
  "status": "A FAZER | EM ANDAMENTO | CONCLUÍDO",
  "id": "id_do_card_no_trello"
}
```

---

## 🔄 Fluxo de Uso Típico

```
1. Usuário inicia conversa com o agente
   ↓
2. Agente pergunta: "Quais são suas tarefas para hoje?" (com data/hora)
   ↓
3. Usuário responde com atividades
   ↓
4. Agente usa adicionar_tarefa() para criar cards
   ↓
5. Agente pergunta: "Tem mais alguma tarefa?"
   ↓
6. Loop até usuário responder "não"
   ↓
7. Usuário gerencia tarefas através do agente
   ↓
8. Agente atualiza status no Trello via mudar_status_tarefa()
```

---

## 🎯 Casos de Uso

- ✅ **Produtividade Pessoal**: Organizar tarefas diárias com conversação natural
- ✅ **Gerenciamento de Projetos**: Coordenar múltiplas atividades em tempo real
- ✅ **Automação de Workflows**: Criar workflows automáticos baseados em IA
- ✅ **Assistente de Tarefas**: Ter um assistente conversacional sempre disponível

---

## 🔧 Desenvolvimento

### Executar o Agente
```python
from agents.agent04.agenttaskmanager import root_agent

# O agente está pronto para ser utilizado via integração com Google ADK
```

### Estender Funcionalidades
Para adicionar novas ferramentas ao agente:

1. Crie uma nova função Python
2. Adicione à lista `tools` do agente
3. Atualize a instrução do agente

```python
root_agent = Agent(
    model='gemini-2.5-flash',
    tools=[ferramenta_nova1, ferramenta_nova2, ...],
)
```

---

## 📝 Notas Técnicas

- **Modelo de IA**: Gemini 2.5 Flash (escolhido pela velocidade e eficiência)
- **Idioma**: Português-BR (suporta conversas em português)
- **Integração**: Trello como backend de persistência
- **Escalabilidade**: Pode ser estendido com novas integrações (Jira, Google Tasks, etc.)

---