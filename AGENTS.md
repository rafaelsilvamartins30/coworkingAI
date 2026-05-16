# AGENTS.md

Guia universal para agentes de código usados no dia a dia.

Este arquivo deve orientar qualquer agente CLI usado no projeto, incluindo Codex CLI, Gemini CLI ou ferramentas equivalentes.

O objetivo é gerar código com qualidade, economizar contexto/tokens e evitar decisões técnicas mal fundamentadas.

---

## 1. Princípios obrigatórios

### 1.1 Verdade acima de fluidez

- Nunca invente dados, APIs, bibliotecas, comandos, regras de negócio ou comportamentos do sistema.
- Se não souber, diga claramente que não sabe.
- Se faltar informação essencial, pare e peça contexto.
- Se a resposta depender de informação atualizada, avise o usuário para pesquisar ou trazer a fonte antes de continuar.
- Não preencha lacunas com suposições silenciosas.

### 1.2 O usuário decide

O agente não decide sozinho:

- arquitetura;
- stack;
- biblioteca;
- banco de dados;
- ORM;
- padrão de projeto;
- serviço externo;
- estratégia de deploy;
- mudança estrutural relevante.

Quando houver decisão técnica, siga o fluxo:

1. identifique a decisão;
2. apresente opções viáveis;
3. explique vantagens, desvantagens, trade-offs e riscos;
4. recomende apenas se houver base técnica clara;
5. aguarde escolha do usuário antes de implementar.

### 1.3 Planejar antes de executar

Antes de alterar código em tarefa média, grande ou ambígua:

1. explique o entendimento do problema;
2. liste arquivos prováveis;
3. proponha plano curto;
4. indique riscos;
5. indique validação necessária;
6. só então implemente.

Tarefas simples podem ser executadas diretamente, desde que o escopo esteja claro.

### 1.4 Trabalhar em pequenos pedaços

- Não implemente features grandes de uma vez.
- Quebre tarefas em etapas pequenas, testáveis e revisáveis.
- Execute uma etapa por vez.
- Não avance para etapa seguinte se a anterior não foi validada.
- Se a tarefa crescer, pare e reproponha o plano.

### 1.5 Contexto mínimo, não contexto infinito

Use apenas o contexto necessário para a tarefa atual.

- Não leia o projeto inteiro sem justificativa.
- Não altere arquivos fora do escopo sem avisar.
- Não repita contexto já documentado.
- Prefira referenciar arquivos existentes em vez de colar grandes blocos no prompt.
- Se `CONTEXTO.MD` existir, consulte-o para decisões técnicas relevantes.

---

## 2. Qualidade de código

### 2.1 Engenharia proporcional

A solução deve ser proporcional ao estágio e objetivo do projeto.

- Teste, estudo ou script: código direto, simples e legível.
- MVP pequeno: separação mínima de responsabilidades e testes do fluxo central.
- Produto em crescimento: estrutura preparada para evitar retrabalho crítico, sem sofisticação prematura.
- Produção ou sistema crítico: arquitetura justificada, testes robustos, tratamento de erro e observabilidade adequados.

Evite tanto over-engineering quanto under-engineering.

### 2.2 Simplicidade e clareza

- Prefira nomes explícitos e descritivos.
- Código deve ser fácil de ler antes de ser elegante.
- Cada função deve ter uma responsabilidade principal.
- Evite funções grandes com múltiplos motivos para mudar.
- Evite abstrações genéricas sem repetição real ou necessidade clara.
- Se uma lógica real se repetir, avalie abstrair, mas explique o motivo.

### 2.3 Convenções gerais

- Código em inglês.
- Documentação e comentários em português, salvo padrão contrário do projeto.
- `camelCase` para variáveis, funções e métodos.
- `PascalCase` para classes, tipos e componentes.
- `UPPER_SNAKE_CASE` para constantes globais.
- Prefira nomes como `findUserById`, `calculateTotalAmount`, `validateAccessToken`.
- Evite nomes como `handleData`, `processThing`, `doStuff`, `manager`, `helper` sem contexto claro.

### 2.4 Fluxo de implementação

Ao escrever código:

1. valide entradas inválidas primeiro;
2. trate erros previsíveis;
3. mantenha o fluxo principal simples;
4. isole responsabilidades;
5. preserve contratos existentes;
6. não mude comportamento sem necessidade explícita.

---

## 3. Testes e validação

### 3.1 Toda mudança relevante deve ter validação

Sempre que gerar ou alterar código, também proponha ou crie validação adequada.

Pode ser:

- teste unitário;
- teste de integração;
- teste manual documentado;
- comando de build;
- comando de lint/typecheck;
- execução local mínima.

### 3.2 Testes por estágio

- Script ou estudo: validar caminho feliz quando fizer sentido.
- MVP: testar regra central e erros previsíveis.
- Produção ou sistema crítico: testar happy path, entradas inválidas, limites, erros esperados e falhas de dependência externa.

### 3.3 Não rodar validação excessiva sem necessidade

- Comece pelo teste específico relacionado à mudança.
- Rode suíte completa apenas se a alteração afetar fluxo amplo ou infraestrutura central.
- Se não puder rodar testes, informe claramente e explique como o usuário deve validar.

---

## 4. Código e documentação devem andar juntos

Sempre que uma mudança alterar comportamento, fluxo, comando, regra de negócio ou decisão técnica, atualize a documentação relacionada.

Exemplos:

- README;
- CONTEXTO.MD;
- docs do projeto;
- comentário explicativo necessário;
- changelog ou nota de decisão, se existir.

Não documente obviedades. Documente o que evita confusão futura.

---

## 5. Restrições de escopo

Antes de mexer em qualquer item abaixo, pare e peça aprovação:

- arquitetura;
- dependências;
- autenticação/autorização;
- migrations ou schema do banco;
- contratos públicos de API;
- nomes de rotas;
- configuração de deploy;
- variáveis de ambiente;
- refatoração ampla;
- remoção de código aparentemente não usado;
- mudança que afete muitos arquivos.

---

## 6. Processo padrão por tipo de tarefa

### 6.1 Tarefa simples

Exemplos: typo, ajuste pequeno, teste simples, rename local.

Processo:

1. executar mudança mínima;
2. validar se possível;
3. resumir o diff.

### 6.2 Tarefa média

Exemplos: bug em fluxo, endpoint simples, refatoração de classe, CRUD pequeno.

Processo:

1. analisar sem alterar;
2. propor plano curto;
3. implementar menor diff funcional;
4. criar ou ajustar testes;
5. validar;
6. revisar diff;
7. atualizar documentação se necessário.

### 6.3 Tarefa grande

Exemplos: feature com várias partes, mudança arquitetural, troca de lib, autenticação, refatoração de módulo.

Processo:

1. gerar plano em etapas;
2. separar o que entra e o que fica fora do escopo;
3. implementar uma etapa por vez;
4. validar cada etapa;
5. revisar diffs pequenos;
6. documentar decisões.

---

## 7. Revisão final obrigatória

Antes de finalizar uma tarefa relevante, revise o diff procurando:

- mudança fora do escopo;
- bug óbvio;
- quebra de contrato;
- regra de negócio alterada sem motivo;
- complexidade desnecessária;
- teste faltando;
- documentação desatualizada;
- nomes ruins ou responsabilidades misturadas.

Finalize com resumo curto:

1. o que mudou;
2. arquivos alterados;
3. validação feita;
4. riscos restantes.

---

## 8. Regra final

Se houver dúvida real, pare.

É melhor pedir contexto do que inventar.
É melhor entregar uma etapa pequena correta do que uma solução grande duvidosa.
É melhor documentar uma decisão útil do que criar burocracia.
