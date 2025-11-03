---
version: "1.3.1"
title_pt: "PROTOCOLO DE GOVERNANÇA IA-HUMANO (TEMPLATE CONSOLIDADO)"
title_en: "AI–HUMAN GOVERNANCE PROTOCOL (CONSOLIDATED TEMPLATE)"
language_support: ["pt-BR", "en-US"]
derived_from:
  - "PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.0.md"
  - "PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.3.md"
organization: "Vicenzo_Corp"
maintainer: "Orquestrador_Humano"
status: "Aprovado"
last_review: "2025-11-02"
ssot_registry_hint: "/governance/ssot_registry/"
---

# PT — Propósito
Este protocolo consolida diretrizes **corporativas (v1.3)** e rotinas **operacionais (v1.0)**, criando um único artefato autossuficiente para colaboração IA↔Humano.
# EN — Purpose
This protocol merges **corporate guidelines (v1.3)** with **operational routines (v1.0)**, creating a single self‑contained artifact for AI↔Human collaboration.

## PT — Escopo e Aplicação
Válido para todos os projetos do framework GAA. Deve ser instanciado por projeto e versionado no SSoT.
## EN — Scope and Applicability
Valid for all GAA framework projects. Must be instantiated per project and versioned in the SSoT.

## PT — Princípios
1) Autonomia supervisionada  2) Auditabilidade contínua (SHA256)  3) Separação de papéis  4) Refinamento iterativo  5) Neutralidade de domínio.
## EN — Principles
1) Supervised autonomy  2) Continuous auditability (SHA256)  3) Role separation  4) Iterative refinement  5) Domain neutrality.

## PT — Papéis (Classes)
Orquestrador_Humano, IA_Architect, IA_Developer, IA_Auditor, IA_QA, IA_Fiscal (expandir conforme projeto).
## EN — Roles (Classes)
Orchestrator_Human, IA_Architect, IA_Developer, IA_Auditor, IA_QA, IA_Compliance (extend per project).

## PT — Estrutura Operacional (Consolidada)
1. Context Pack (≤500 palavras) → 2. Geração de artefato → 3. Validação (Junta) → 4. Auditoria (diff+hash) → 5. Registro SSoT.
## EN — Operational Structure (Consolidated)
1. Context Pack (≤500 words) → 2. Artifact generation → 3. Validation (Board) → 4. Audit (diff+hash) → 5. SSoT registry.

## PT — SLAs e Políticas
Revisão humana: 48h úteis • Contexto ativo por IA: ≤500 palavras • Máx. 2 ciclos de revisão • Rollback automatizado por hash.
## EN — SLAs and Policies
Human review: 48 business hours • Active context per agent: ≤500 words • Max 2 review cycles • Hash‑based automated rollback.

## PT — Regras de Versionamento e SSoT
Registrar cada artefato com SHA256 e `derived_from`; enviar entrada ao `/governance/ssot_registry/` a cada commit.
## EN — Versioning and SSoT Rules
Record each artifact with SHA256 and `derived_from`; submit an entry to `/governance/ssot_registry/` on every commit.

## PT — Fluxo de Execução (incorporado da v1.0)
Fases: Planejar → Gerar → Validar → Auditar → Homologar → Registrar. Checkpoints: critérios de aceite, diffs, hash, parecer da Junta.
## EN — Execution Flow (incorporated from v1.0)
Phases: Plan → Generate → Validate → Audit → Approve → Register. Checkpoints: acceptance criteria, diffs, hash, Board report.

## PT — Auditoria e Rastreabilidade (incorporado da v1.0)
Trilhas: `audit_trail.json`, `RELATORIO_VALIDACAO.md`; cálculo SHA256 por arquivo; política de retenção definida no Manifesto.
## EN — Audit and Traceability (incorporated from v1.0)
Trails: `audit_trail.json`, `RELATORIO_VALIDACAO.md`; per‑file SHA256; retention policy defined in the Manifesto.

## PT — Instanciação de Projeto (exemplo)
Criar `/governance/projects/{{project_name}}/protocolos/PROTOCOLO_GOVERNANCA_IA_HUMANO_{{project_name}}_v1.0.md` com papéis, SLAs e escopo.
## EN — Project Instantiation (example)
Create `/governance/projects/{{project_name}}/protocolos/PROTOCOLO_GOVERNANCA_IA_HUMANO_{{project_name}}_v1.0.md` with roles, SLAs, scope.

## PT — Apêndice: Tabela de Responsabilidades
- Orquestrador: contexto e aceite final • Architect: desenho e decisões de arquitetura • Developer: implementação • Auditor: hash/diff • Junta: conformidade.
## EN — Appendix: Responsibility Table
- Orchestrator: context and final acceptance • Architect: design and architectural decisions • Developer: implementation • Auditor: hash/diff • Board: compliance.

## PT — Fechamento
Este template substitui v1.0 e v1.3, mantendo compatibilidade retroativa.
## EN — Closing
This template replaces v1.0 and v1.3, preserving backward compatibility.
