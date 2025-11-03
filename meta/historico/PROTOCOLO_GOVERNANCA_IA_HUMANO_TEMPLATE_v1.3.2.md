---
# ===============================================================
# METADADOS DE GOVERNANÇA (PARA O PIPELINE)
# ===============================================================
version: "1.3.2"
title_pt: "PROTOCOLO DE GOVERNANÇA IA-HUMANO (TEMPLATE CONSOLIDADO)"
title_en: "AI–HUMAN GOVERNANCE PROTOCOL (CONSOLIDATED TEMPLATE)"
language_support: ["pt-BR", "en-US"]

# COMPATIBILIDADE E RASTREABILIDADE
compatibility:
  derived_from_yaml: "PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.3.2.yaml"
  derived_from_md:
    - "PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.0.md"
    - "PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.3.1.md"
  backward_compatible_with: ["v1.0", "v1.3", "v1.3.1"]

# IDENTIDADE CORPORATIVA
organization: "Vicenzo_Corp"
maintainer: "Orquestrador_Humano"
status: "Template Aprovado"

# ===============================================================
# DADOS DE INSTANCIAÇÃO (A SER PREENCHIDO PELO ORQUESTRADOR)
# ===============================================================
project_name: "<NOME_DO_PROJETO>"
project_code: "<CODIGO_INTERNO>"
created_by: "Human_Orchestrator"
approved_by: "Junta Validadora (Sistemas, Negócio, Compliance)"
created_at: "<AAAA-MM-DD>"
status: "Em Configuração"
registry_path: "/governance/projects/<NOME_DO_PROJETO>/protocolo/"
context_scope: "project_specific"
---

# 🧭 1. PROPÓSITO E ESCOPO (PURPOSE & SCOPE)

**PT:** Este protocolo define as regras de governança IA-Humano específicas do projeto **`<NOME_DO_PROJETO>`**. Ele herda e implementa os princípios do `PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md`.
**EN:** This protocol defines the specific AI-Human governance rules for the **`<PROJECT_NAME>`** project. It inherits and implements the principles from `PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md`.

- **Objetivo Estratégico:** `<ex: Reduzir o tempo de validação de documentos fiscais em 30%>`
- **Escopo Inicial:** `<resumo dos principais módulos ou entregáveis>`

---

# 🏛️ 2. BLOCOS DE GOVERNANÇA (GOVERNANCE BLOCKS)

Este protocolo é governado pelos 4 blocos definidos no `v1.3.2.yaml`:

## 2.1. Bloco 1: SSoT e Hierarquia (SSoT & Hierarchy)
**PT:** Define onde os artefatos mestres estão e onde este projeto será instanciado, conforme o `ssot.instantiation_path_template`.
**EN:** Defines where master artifacts are and where this project will be instantiated, as per the `ssot.instantiation_path_template`.

## 2.2. Bloco 2: Regras de Governança (Governance Rules & SLAs)
**PT:** Este projeto adere aos seguintes SLAs e regras contratuais:
- **Revisão Humana:** 48 horas
- **Auditoria de IA:** 12 horas
- **Limite de Contexto:** 500 palavras por agente
- **Campos Obrigatórios:** Todos os `required_fields_on_instantiation` (como `project_name`) devem ser preenchidos.
**EN:** This project adheres to the following SLAs and contractual rules:
- **Human Review:** 48 hours
- **AI Audit:** 12 hours
- **Context Limit:** 500 words per agent
- **Required Fields:** All `required_fields_on_instantiation` (like `project_name`) must be completed.

## 2.3. Bloco 3: Automação e Pipeline (Automation & Pipeline)
**PT:** O pipeline de CI/CD executará os seguintes *hooks* para este projeto: `validate_structure`, `register_manifest`, `create_audit_log`, `generate_hash_sha256`.
**EN:** The CI/CD pipeline will execute the following hooks for this project: `validate_structure`, `register_manifest`, `create_audit_log`, `generate_hash_sha256`.

## 2.4. Bloco 4: Agentes e Atores (Agents & Actors)
**PT:** Define os papéis de IA e Humanos que atuarão neste projeto.
**EN:** Defines the AI and Human roles that will act on this project.

---

# 🧠 3. AGENTES DO PROJETO (PROJECT AGENTS)

## 3.1. Agentes IA (Padrão)
- **IA_Architect:** Desenha *blueprints* técnicos.
- **IA_Developer:** Implementa *blueprints* e código.
- **IA_Auditor:** Valida integridade (hashes, diffs) e conformidade com este protocolo.

## 3.2. Agentes IA (Opcionais/Específicos do Projeto)
```yaml
# PT: Adicione IAs especializadas necessárias para <NOME_DO_PROJETO>
# EN: Add specialized AIs needed for <PROJECT_NAME>
agents_ia_extended:
  - id: IA_Fiscal
    role: "Especialista em Tributação e Compliance"
    scope: "Validar regras de negócio fiscais e conformidade de NFS-e"
  - id: IA_Logistics
    role: "Especialista em Processos Logísticos"
    scope: "Otimizar fluxos de doca e agendamento"