---
framework_name: "CrisAI"
framework_acronym: "CRIS"
framework_meaning: "Cognitive Responsible Innovation System"
framework_tagline: "Inovação Cognitiva com Responsabilidade e Propósito"
framework_version: "1.4" 
framework_named_for: "Cris Vicenzo"
document_type: "readme"
project: "<NOME_PROJETO>"
framework_name: "CrisAI"
framework_acronym: "CRIS"
framework_meaning: "Cognitive Responsible Innovation System"
framework_tagline: "Inovação Cognitiva com Responsabilidade e Propósito"
framework_version: "1.4"
framework_named_for: "Cris Vicenzo"
purpose: "Recontextualização rápida do projeto <NOME_PROJETO>"
prerequisite: "MANIFESTO_GOVERNANCA_v1.4.yaml"
read_next: "PROTOCOLO_<NOME_PROJETO>_v1.0.md"
created_at: "<DATA>"
status: "active"
---

# 💡 Pré-requisito
Antes de ler este documento, você **DEVE** ter lido:
- 📜 `MANIFESTO_GOVERNANCA_v1.4.yaml`

O Manifesto explica o framework CrisAI completo. Este documento explica apenas o projeto **<NOME_PROJETO>**.

---

# 📘 O que é <NOME_PROJETO>?
<DESCRICAO_PROJETO>

> Exemplo: "Este projeto implementa a plataforma X para gerenciar Y, com objetivo de Z."

---

# 👥 Equipe e Papéis
| Papel | Agente | Responsabilidades |
|-------|--------|-------------------|
| <PAPEL_1> | <AGENTE_1> | <RESPONSABILIDADE_1> |
| <PAPEL_2> | <AGENTE_2> | <RESPONSABILIDADE_2> |
| <PAPEL_3> | <AGENTE_3> | <RESPONSABILIDADE_3> |

Substitua a tabela acima por todos os papéis específicos do projeto, mantendo as colunas conforme o template.

---

# ⚙️ Fluxo Operacional
1. <FLUXO_OPERACIONAL_ITEM_1>
2. <FLUXO_OPERACIONAL_ITEM_2>
3. <FLUXO_OPERACIONAL_ITEM_3>

> Formato: lista numerada descrevendo passo-a-passo da operação do projeto (ex: geração → validação → auditoria → aprovação).

---

# 📁 Documentos Essenciais
- `PROTOCOLO_<NOME_PROJETO>_v1.0.md`
- Blueprints do projeto (pasta `/governance/projects/<NOME_PROJETO>/blueprints/`)
- Outros documentos relevantes: políticas, contratos, diagramas

---

# 🧩 Recontextualização Rápida
Para se contextualizar neste projeto:
1. Leia `MANIFESTO_GOVERNANCA_v1.4.yaml` (framework)
2. Leia este arquivo (Quick Start do projeto)
3. Leia `PROTOCOLO_<NOME_PROJETO>_v1.0.md` (detalhes operacionais)

> Importante: siga esta ordem — o Manifesto define os princípios; o Protocolo define as regras operacionais.

---

# 🧭 Status Atual
| Item | Valor |
|------|-------|
| Fase | <FASE> |
| Objetivo Atual | <OBJETIVO_ATUAL> |
| Próximos Passos | <PROXIMOS_PASSOS> |
| Agentes Ativos | <IA_ARCHITECT_IMPLEMENTATION>, <IA_GOVERNANCE_IMPLEMENTATION>, <IA_AUDITOR_IMPLEMENTATION> |
| Orquestrador | <ORQUESTRADOR_NOME> |

---

# 📝 Instruções de Uso deste Template
Este é um **TEMPLATE**. Para criar o README de um novo projeto:

1. Copie este arquivo como `README_QUICK_START_<NOME_PROJETO>.md` no caminho `/governance/projects/<NOME_PROJETO>/`.
2. Substitua TODOS os placeholders no formato `<TEXTO>`:
   - `<NOME_PROJETO>`, `<DESCRICAO_PROJETO>`, `<PAPEL_*>`, `<AGENTE_*>`, `<RESPONSABILIDADE_*>`,
     `<FLUXO_OPERACIONAL_*>`, `<DATA>`, `<FASE>`, `<OBJETIVO_ATUAL>`, `<PROXIMOS_PASSOS>`,
     `<IA_ARCHITECT_IMPLEMENTATION>`, `<IA_GOVERNANCE_IMPLEMENTATION>`, `<IA_AUDITOR_IMPLEMENTATION>`, `<ORQUESTRADOR_NOME>`.
3. Remova esta seção de instruções antes de publicar.
4. Submeta para validação:
   - `Claude` (IA_Governance) — valida semântica e conformidade
   - `Gemini` (IA_Auditor) — audita integridade YAML e links
5. Após validação, registre no SSoT Registry e inclua a entrada em `MANIFESTO_GOVERNANCA_v1.4.yaml` (se necessário).

---

# 📌 Checklist de Qualidade (para o autor)
- [ ] Header YAML preenchido e correto
- [ ] 9 seções presentes
- [ ] Todos os placeholders em formato `<TEXTO>`
- [ ] Instruções de uso mantidas até a publicação
- [ ] Formatação Markdown clara e legível
- [ ] Tamanho estimado: 3-4 páginas após preenchimento
- [ ] Exemplo ou comentário explicativo onde necessário

---
