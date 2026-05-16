# Prompt — Tarefa média

Use quando a mudança envolver fluxo, regra de negócio pequena, teste ou mais de um arquivo.

```md
Tarefa:
[descreva exatamente o que deve ser feito]

Contexto:
Leia `AGENTS.md` e `CONTEXTO.MD` se existirem.
Use principalmente:
- [arquivo/pasta 1]
- [arquivo/pasta 2]

Comportamento atual:
[descreva o estado atual]

Comportamento esperado:
[descreva o estado desejado]

Restrições:
- Antes de editar, faça um plano curto.
- Liste arquivos que pretende alterar.
- Faça a menor alteração funcional possível.
- Não refatore fora do escopo.
- Não altere contratos públicos, migrations, configs ou arquitetura sem pedir.
- Se precisar mexer em arquivos fora do escopo, pare e explique.

Validação:
- Crie ou ajuste testes necessários.
- Rode [comando/teste específico].

Saída final:
1. o que mudou;
2. arquivos alterados;
3. testes/validações executados;
4. riscos restantes.
```
