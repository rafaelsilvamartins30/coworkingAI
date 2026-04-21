# AGENTS.md — Diretrizes de Engenharia de Software para IA

> **Versão atual:** V3
> **Histórico de versões:** [V1](#v1--arquitetura-e-clean-code) · [V2](#v2--contexto-e-fluxo-de-trabalho) · [V3](#v3-atual--autonomia-tecnologias-e-testes-por-contexto)
> **Idioma:** Código em inglês · Documentação e comentários em português

---

## ⚠️ Regra Absoluta: CONTEXTO.MD é obrigatório

**Antes de qualquer ação — arquitetura, código, refatoração ou sugestão técnica — verifique se o arquivo `CONTEXTO.MD` está presente e preenchido.**

Se ele não existir ou estiver incompleto:

1. **Pare imediatamente.**
2. Informe o que está faltando.
3. Entregue o template do `CONTEXTO.MD` e peça que seja preenchido.
4. **Não escreva uma linha de código até receber o contexto completo.**

Não existem exceções. Nem para tarefas "simples". O contexto define tudo.

---

## 1. O Contrato de Contexto (CONTEXTO.MD)

O `CONTEXTO.MD` é o documento que orienta **todas** as decisões técnicas. Ele deve conter obrigatoriamente:

| Campo | Descrição |
|---|---|
| **Estágio Atual** | Teste / MVP / Produção / Escalando |
| **Estágio Final Esperado** | Onde o projeto deve chegar |
| **Possíveis Mudanças Futuras** | Features planejadas ou prováveis |
| **Ambiente** | Local / Docker / Cloud / Kubernetes |
| **Objetivos de Negócio** | Curto prazo e médio prazo |
| **Stack atual** | Linguagens, frameworks e libs em uso |

---

## 2. Arquitetura Proporcional ao Contexto

A arquitetura não segue uma regra fixa. Ela segue o `CONTEXTO.MD`.

### Projetos de Teste / Exploração

- Código funcional, direto, sem camadas desnecessárias.
- Testes mínimos ou nenhum (se o objetivo é só validar uma ideia).
- Sem ADR, sem patterns formais.

### MVPs

- Estrutura básica que permita crescer sem reescrever tudo.
- Evite acoplamento forte. Separe responsabilidades mesmo que de forma simples.
- Testes nas regras de negócio principais.

### Produção / Escalável

- Clean Architecture ou equivalente justificado.
- SOLID aplicado com rigor.
- Testes completos (ver Seção 4).
- 12-Factor App onde aplicável.
- Design Patterns apenas quando há um problema real que eles resolvem.

> **A IA nunca deve assumir o nível de rigor sem ler o CONTEXTO.MD. Nunca.**

---

## 3. Regras de Código (Sempre Válidas)

Independente do estágio, estas regras se aplicam sempre:

### 3.1. Nomenclatura

- Código sempre em **inglês**.
- Variáveis e funções: `camelCase`.
- Classes e tipos: `PascalCase`.
- Constantes globais: `UPPER_SNAKE_CASE`.
- Nomes revelam intenção: `findUserById`, não `getUser`. `isEmailValid`, não `check`.

### 3.2. Funções e Responsabilidade

- Cada função faz **uma coisa**.
- Se o nome contém "e" ou "and" (`validateAndSave`), divida.
- Funções com mais de 20 linhas são candidatas a refatoração — avalie.

### 3.3. DRY

- Lógica repetida em 2+ lugares → abstraia.
- Mas não abstraia prematuramente. Espere a segunda repetição real antes de criar a abstração.

### 3.4. Clareza sobre Abstração

- Prefira código explícito a "magia".
- Se uma abstração oculta o fluxo de dados sem ganho claro de produtividade, questione-a.

---

## 4. Testes por Contexto

### Projetos de Teste / Scripts Simples

- Testes são opcionais. Se existirem, cubram o caminho feliz.

### MVPs

- Testes nas regras de negócio centrais.
- Caminho feliz + casos de erro previsíveis.

### Produção / Sistemas Críticos

Testes completos, obrigatórios:

- ✅ Caminho feliz (happy path)
- ✅ Caminhos de erro esperados
- ✅ Entradas inválidas (campos nulos, tipos errados, strings vazias, valores fora do range)
- ✅ Limites e edge cases (ID inexistente, lista vazia, payload gigante)
- ✅ Comportamento sob falha de dependências externas

> A IA deve escrever testes imediatamente após implementar. Se o contexto indicar sistema crítico, proponha TDD.

---

## 5. Tecnologias e Dependências: A IA Sempre Pergunta

A IA **nunca** escolhe ou adiciona tecnologias, frameworks, ORMs ou bibliotecas por conta própria.

### Fluxo obrigatório ao precisar de uma dependência:

1. Identifique a necessidade técnica.
2. Liste as opções que faria sentido considerar, com prós e contras de cada uma.
3. **Pergunte ao desenvolvedor qual deseja usar.**
4. Aguarde a resposta antes de implementar.
5. Após a escolha, registre no `CONTEXTO.MD` (seção Stack).

Isso vale para tudo: desde um simples `lodash` até um ORM pesado como Prisma, Hibernate ou SQLAlchemy.

---

## 6. Autonomia da IA: Quando Agir vs. Perguntar

### A IA deve **sempre perguntar antes** de:

- Criar ou renomear arquivos e pastas
- Alterar estrutura de diretórios
- Modificar configurações de ambiente (`.env`, `docker-compose`, CI/CD)
- Refatorar módulos existentes
- Adicionar ou remover dependências
- Qualquer mudança que afete mais de um arquivo de forma estrutural

### A IA pode agir sem perguntar em:

- Implementações novas dentro de um escopo já aprovado
- Correção de bugs isolados e claramente definidos
- Formatação e nomenclatura dentro das regras deste documento

> Em caso de dúvida: **pergunte sempre.**

---

## 7. Planejamento: To-Do por Feature

Sempre que iniciar um épico ou feature:

1. Gere um checklist em Markdown com os passos necessários.
2. Apresente antes de implementar.
3. Atualize conforme o progresso.

Exemplo:
```markdown
## Feature: Autenticação JWT

- [ ] Criar endpoint POST /api/v1/auth/login
- [ ] Validar credenciais contra o banco
- [ ] Gerar token JWT com expiração
- [ ] Middleware de proteção de rotas
- [ ] Testes: login válido, senha errada, usuário inexistente
```

---

## 8. Registros de Decisão (ADR por Versionamento)

Decisões arquiteturais relevantes são registradas **neste próprio arquivo**, como novas versões.

### O que gera uma nova versão:

- Adição de biblioteca ou framework relevante
- Mudança de banco de dados ou camada de persistência
- Alteração significativa na arquitetura
- Mudança de estágio do projeto (ex: MVP → Produção)

### Como versionar:

Adicione uma seção ao final deste arquivo seguindo o padrão:

```markdown
---

## V2 — [Título da Decisão]
**Data:** DD/MM/AAAA
**Contexto:** Por que essa decisão foi necessária.
**Decisão:** O que foi decidido.
**Consequências:** O que muda, o que melhora, o que piora.
```

O topo do arquivo sempre reflete a **versão atual**. O histórico fica preservado abaixo.

---

## 9. Padrões de Rota e API

Para projetos com APIs HTTP:

- RESTful consistente: `GET /api/v1/users`, `POST /api/v1/users/{id}/roles`
- Versione a API desde o início (`/v1/`), mesmo em MVPs — é fácil de remover, difícil de adicionar depois.
- Erros retornam estrutura consistente:

```json
{
  "error": "USER_NOT_FOUND",
  "message": "Nenhum usuário encontrado com o ID informado.",
  "statusCode": 404
}
```

---

## 10. 12-Factor App (Projetos Online/Cloud)

Quando o ambiente for cloud ou o estágio final indicar isso:

- Configurações via variáveis de ambiente (nunca hardcoded)
- Logs como stream de eventos (stdout, sem arquivos)
- Processos stateless
- Separação clara de build / release / run

---

## Histórico de Versões

---

### V1 — Arquitetura e Clean Code
**Data:** 20/04/2026
**Contexto:** Criação inicial do documento com foco em arquitetura proporcional, clean code e SOLID.
**Decisão:** Estabelecer regras base de nomenclatura, SRP, DRY e padrões de rota.
**Consequências:** Base sólida para qualquer projeto. Sem definição clara de autonomia da IA ou critérios de teste por contexto.

---

### V2 — Contexto e Fluxo de Trabalho
**Data:** 20/04/2026
**Contexto:** Necessidade de formalizar o CONTEXTO.MD como contrato obrigatório e definir fluxo de planejamento por feature.
**Decisão:** CONTEXTO.MD passa a ser bloqueante. Adição de To-Do lists e ADR por versionamento.
**Consequências:** Maior rastreabilidade de decisões. Processo mais estruturado antes de codar.

---

### V3 (atual) — Autonomia, Tecnologias e Testes por Contexto
**Data:** 20/04/2026
**Contexto:** Refinamento com base em como um desenvolvedor experiente realmente trabalha com IA. Eliminação de contradições internas do documento V1/V2 (ex: regras genéricas que não se aplicavam a projetos simples).
**Decisão:** Testes e rigor arquitetural passam a ser proporcionais ao estágio. IA sempre pergunta sobre tecnologias e mudanças estruturais. Estágio Final e Mudanças Futuras tornam-se campos obrigatórios do CONTEXTO.MD.
**Consequências:** Documento mais honesto e aplicável na prática. Elimina over-engineering em projetos simples sem abrir mão de qualidade onde ela importa.
