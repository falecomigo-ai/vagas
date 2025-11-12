# 🧠 Desafio Técnico – Desenvolvedor Backend (AI Stack)

## 📍 Cenário Real

Você foi contratado como **Desenvolvedor Backend** em uma empresa SaaS que oferece **assistentes de vendas inteligentes** para equipes comerciais via WhatsApp, e-mail e CRM.  
O produto utiliza **modelos de linguagem (LLMs)** para automatizar mensagens, responder clientes e gerar insights de performance.

O time quer que você lidere a criação do **módulo central de “IA conversacional com memória e ferramentas”**, que permitirá que os agentes de IA da plataforma sejam configuráveis e conectem-se a dados reais de cada cliente.

---

## 🧩 Parte 1 — Análise de Requisitos e Arquitetura

### 🧾 Requisitos Funcionais

1. O sistema deve receber mensagens de um usuário e gerar respostas usando uma API de LLM (OpenAI, Claude, Gemini, etc.);
2. O sistema deve manter **memória da conversa** por usuário;
3. O sistema deve permitir a execução de **ações externas (“ferramentas”)**, como:
   - Buscar dados de vendas em um banco local;
   - Fazer chamadas a APIs externas (por exemplo, dados de mercado);
4. O sistema deve expor essas funcionalidades via uma **API REST ou WebSocket**;
5. O sistema deve registrar métricas de uso (tokens, tempo de inferência, custo estimado);
6. Deve ser **containerizável (Docker)**.

### 🧱 Requisitos Não Funcionais

- Código limpo e modular;
- Logs e rastreabilidade de execução;
- Escalável horizontalmente (sem depender de estado em memória local);
- Configuração via `.env`;
- Documentação clara (`README.md` e `ARCHITECTURE.md`).

---

### 🧠 Sua primeira tarefa

Crie um arquivo chamado `ARCHITECTURE.md` com:

- Descrição da arquitetura proposta (pode incluir diagramas);
- Componentes principais (API Gateway, Core LLM Service, Memory Layer, Tool Executor, etc.);
- Justificativas técnicas (por que escolher determinado framework, cache, mensageria, etc.);
- Estratégia de observabilidade e logs;
- Plano de escalabilidade (ex: workers, filas, cache distribuído);
- Modelo de dados resumido (entidades principais e suas relações).

---

## ⚙️ Parte 2 — Implementação do Módulo de IA

Implemente um **MVP funcional** da arquitetura descrita.

### ✅ Funcionalidades mínimas

#### 1. Endpoint `/chat`

- **Entrada:**
  ```json
  {
    "user_id": "123",
    "message": "Quais foram as vendas do mês passado?"
  }
  ```
- **Processo:**

  - Use uma API de LLM (OpenAI, Claude, Gemini ou outra);
  - Mantenha **memória da conversa** por usuário (Redis, Postgres ou arquivo local);
  - Gere e retorne a resposta com metadados.

- **Saída:**
  ```json
  {
    "response": "As vendas do mês passado foram 42 contratos fechados.",
    "model": "gpt-4o",
    "tokens_used": 823,
    "context_size": 6,
    "memory": [...]
  }
  ```

#### 2. Agente com ferramentas

Implemente uma camada de “Agent” que decide, com base na pergunta:

- Se deve responder direto com o LLM;
- Ou acionar uma ferramenta externa (ex: buscar dados locais).

Você pode usar **CrewAI, LangChain, LlamaIndex, Semantic Kernel** ou criar algo do zero.

#### 3. Observabilidade

- Registre logs estruturados contendo:
  - `user_id`
  - `prompt`
  - `tokens_used`
  - `time_ms`
  - `tool_called`

Armazene localmente (arquivo, DB ou log estruturado no console).

---

## 🧮 Parte 3 — Bônus de Arquitetura Real

Esses itens são opcionais, mas contam pontos extras:

1. **Fila de Processamento (RabbitMQ, Kafka ou BullMQ)**

   - As requisições de IA vão para uma fila → worker processa.

2. **Cache Inteligente (Redis)**

   - Se a mesma pergunta for feita novamente, retorne o resultado anterior.

3. **Módulo de Métricas**

   - Tokens por usuário, custo estimado, tempo médio de resposta.

4. **Configuração Multi-LLM**

   - Suporte a múltiplos provedores (OpenAI, Claude, Gemini) via variável de ambiente.

5. **Deploy com Docker Compose**
   - Incluindo `api`, `redis` e `worker`.

---

## 🧾 Entregáveis

| Item                                 | Obrigatório | Descrição                                    |
| ------------------------------------ | ----------- | -------------------------------------------- |
| `ARCHITECTURE.md`                    | ✅          | Documento técnico com visão e justificativas |
| Código fonte                         | ✅          | API funcional e organizada                   |
| `README.md`                          | ✅          | Instruções de setup, execução e endpoints    |
| Dockerfile / docker-compose          | ✅          | Configuração de ambiente                     |
| Logs e métricas básicas              | ✅          | Demonstração de observabilidade              |
| Demonstração (vídeo ou GIF opcional) | 💡          | Mostrando chat e ferramentas em ação         |

---

## 🧩 Avaliação

| Critério                                | Peso |
| --------------------------------------- | ---- |
| Clareza e coerência da arquitetura      | 25%  |
| Código limpo, modular e funcional       | 25%  |
| Domínio de LLMs e frameworks de agentes | 25%  |
| Observabilidade e escalabilidade        | 15%  |
| Documentação técnica                    | 10%  |

---

## 💬 Dica Final

Mais importante do que “fazer funcionar” é **mostrar que você pensa como um arquiteto de produto de IA**.  
Queremos ver raciocínio, clareza e capacidade de projetar algo escalável e sustentável — não apenas chamadas de API.

---

### 📦 Entrega

1. Publique o repositório em modo público no GitHub;
2. Inclua instruções claras de como rodar (`npm install`, `docker-compose up`, etc.);
3. Envie o link do repositório e, se quiser, um pequeno vídeo de demonstração do fluxo em ação.
