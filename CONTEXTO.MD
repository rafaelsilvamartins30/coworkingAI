# 📄 CONTEXTO.md — Contexto Obrigatório para Agentes de IA

> ⚠️ **OBRIGATÓRIO**: Este arquivo deve ser lido antes de qualquer decisão técnica.
> Sem ele preenchido, **nenhuma sugestão de arquitetura, código ou infra deve ser feita**.
>  
> Atualize sempre que houver mudança de escopo, estágio ou stack.

---

## 1. Identificação do Projeto

- **Nome:**  
- **Descrição curta:**  

---

## 2. Estágio Atual

> Marque **apenas um**. Define o nível de rigor técnico esperado.

- [ ] Teste / Exploração (validar ideia rápido, sem compromisso)
- [ ] MVP (estrutura mínima para validar com usuários)
- [ ] Produção (uso real, exige qualidade e estabilidade)
- [ ] Escalando (alto volume, performance e times múltiplos)

---

## 3. Estágio Final Esperado

> Define o nível de complexidade que pode ser antecipado.

- [ ] Simples / interno (script ou ferramenta pessoal)
- [ ] SaaS / Web App público
- [ ] API (interna ou externa)
- [ ] Sistema escalável / multi-tenant
- [ ] Indefinido

**Observações:**  

---

## 4. Possíveis Mudanças Futuras

> Liste apenas mudanças **prováveis** (evite especulação inútil).

| Mudança | Probabilidade | Prazo |
|---|---|---|
| | | |
| | | |
| | | |

---

## 5. Ambiente

> Onde o sistema roda.

- **Desenvolvimento:**  
- **Deploy / Produção:**  

---

## 6. Objetivos de Negócio

> Direciona decisões técnicas (sem isso, arquitetura vira chute).

- **Curto prazo (semanas):**  
- **Médio prazo (meses):**  

---

## 7. Stack Atual

> Se estiver migrando algo, use:  
> `[Antigo] -> [Novo]`

| Camada | Tecnologia |
|---|---|
| Linguagem principal | |
| Framework | |
| Banco de dados | |
| ORM / Query | |
| Autenticação | |
| Fila / Jobs | |
| Infra / Deploy | |
| Testes | |
| Outras libs | |

---

## 8. Restrições e Decisões Fixas

> O que **não pode ser mudado** ou já foi decidido.

-  
-  
-  

---

## 9. Histórico de Decisões (Log)

> Nunca apagar. Isso evita decisões incoerentes no futuro.

Formato:
```
[Data] - [Decisão] - [Motivo]
```

---

## 10. Regras para Agentes de IA

> Qualquer IA trabalhando neste repositório deve seguir:

- Não assumir contexto ausente  
- Não inventar requisitos ou decisões  
- Questionar inconsistências antes de sugerir soluções  
- Respeitar estágio do projeto (não over-engineer MVP)  
- Priorizar simplicidade proporcional ao problema  
