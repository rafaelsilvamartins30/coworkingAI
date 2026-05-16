# CONTEXTO.MD

Template de contexto do projeto para agentes de IA.

Use este arquivo para dar contexto mínimo suficiente ao agente sem precisar repetir tudo no prompt.

O objetivo não é criar burocracia. O objetivo é evitar chute técnico, over-engineering e decisões fora da realidade do projeto.

---

## 1. Identificação

- **Nome do projeto:**
- **Descrição curta:**
- **Tipo de projeto:** pessoal / trabalho / estudo / produto / experimento

---

## 2. Objetivo real

Explique em poucas linhas o que o projeto precisa resolver agora.

- **Problema principal:**
- **Usuário ou público-alvo:**
- **Resultado esperado no curto prazo:**

---

## 3. Estágio atual

Marque apenas um.

- [ ] Estudo / teste rápido
- [ ] Protótipo
- [ ] MVP pequeno
- [ ] Produto em crescimento
- [ ] Produção
- [ ] Sistema crítico

### Implicação técnica

- **Quanto rigor é necessário agora?**
- **O que seria over-engineering neste momento?**
- **O que seria simplificação perigosa neste momento?**

---

## 4. Stack atual

| Camada | Tecnologia |
|---|---|
| Linguagem | |
| Framework | |
| Banco de dados | |
| ORM / query builder | |
| Autenticação | |
| Testes | |
| Build / package manager | |
| Deploy / infra | |
| Outras libs relevantes | |

---

## 5. Como rodar e validar

### Execução

```bash
# comando para rodar o projeto
```

### Testes

```bash
# comando para rodar todos os testes
```

### Teste específico

```bash
# comando para rodar teste específico
```

### Build / lint / typecheck

```bash
# comandos de validação adicionais
```

---

## 6. Estrutura do projeto

Explique apenas as pastas/arquivos importantes.

| Caminho | Responsabilidade |
|---|---|
| | |
| | |
| | |

---

## 7. Convenções do projeto

- **Nomes:**
- **Organização de pastas:**
- **Camadas:**
- **DTOs / contratos:**
- **Validação:**
- **Tratamento de erro:**
- **Logs:**
- **Transações:**
- **Testes:**
- **Documentação:**

---

## 8. Restrições e decisões fixas

Liste o que não deve ser alterado sem aprovação.

- 
- 
- 

---

## 9. Decisões pendentes

Liste decisões que ainda precisam ser tomadas pelo usuário.

| Decisão | Opções conhecidas | Observações |
|---|---|---|
| | | |
| | | |

---

## 10. Mudanças futuras prováveis

Liste apenas mudanças realmente prováveis. Não especule demais.

| Mudança | Probabilidade | Prazo aproximado | Impacto técnico |
|---|---|---|---|
| | | | |
| | | | |

---

## 11. Histórico de decisões

Nunca apagar decisões importantes. Adicione novas linhas.

Formato:

```txt
[AAAA-MM-DD] - [Decisão] - [Motivo]
```

Exemplos:

```txt
2026-05-16 - Usar PostgreSQL - Projeto precisa de consultas relacionais simples e integridade referencial.
2026-05-16 - Não usar microserviços - Escopo atual não justifica complexidade operacional.
```

---

## 12. Instruções específicas para agentes

- Não assumir contexto ausente.
- Não alterar arquitetura sem aprovação.
- Não criar abstrações genéricas sem necessidade real.
- Trabalhar em etapas pequenas.
- Sempre validar mudanças relevantes.
- Atualizar documentação quando mudar comportamento, comando ou decisão técnica.
