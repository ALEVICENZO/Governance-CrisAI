---
title: "PROTOCOLO DE GOVERNANÇA IA-HUMANO — TEMPLATE DE PROJETO"
version: "v1.0"
derived_from: "/governance/meta/PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md"
governance_level: "L2 - Instância de Projeto"
project_name: "<NOME_DO_PROJETO>"
project_code: "<CÓDIGO_INTERNO>"
created_by: "Human_Orchestrator"
approved_by: "Junta Validadora (Sistemas, Negócio, Compliance, Fiscal)"
created_at: "<AAAA-MM-DD>"
status: "Em Configuração"
registry_path: "/governance/projects/<NOME_DO_PROJETO>/protocolo/"
context_scope: "project_specific"
---

# 🧭 1. PROPÓSITO
Este protocolo define as regras de governança IA-Humano específicas do projeto **<NOME_DO_PROJETO>**,  
herdando os princípios do Protocolo Metodológico Corporativo.

Ele estabelece:
- Os papéis humanos e de IA aplicáveis a este projeto;
- As fases, checkpoints e SLAs de colaboração;
- A política de auditoria e baseline;
- O modelo de comunicação entre agentes e pipeline.

---

# ⚙️ 2. CONTEXTO E ESCOPO
- **Tipo de Projeto:** <ex: Produto Digital / Automação / ERP / Data Platform>
- **Objetivo Estratégico:** <ex: Reduzir lead time de processos logísticos em 40%>
- **Escopo Inicial:** <resumo dos principais módulos ou entregáveis>
- **Deriva de:** PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md

---

# 🧠 3. PAPÉIS E AGENTES

## 3.1. Agentes IA
```yaml
agents_ia:
  - id: IA_Architect
    role: "Arquiteta de Soluções"
    scope: "Modelagem de arquitetura, integrações e padrões de design"
  - id: IA_Developer
    role: "Desenvolvedora Técnica"
    scope: "Implementação e documentação de código"
  - id: IA_QA
    role: "Analista de Qualidade"
    scope: "Testes automatizados, revisão de requisitos e validação técnica"
  - id: IA_Auditor
    role: "Auditor de Integridade"
    scope: "Validação de versões, hashes e baselines"
  # Exemplo de IA específica:
  - id: IA_Logistics
    role: "Especialista em Processos Logísticos"
    scope: "Planejamento e otimização de fluxos físicos"
```

## 3.2. Agentes Humanos
```yaml
agents_human:
  - id: Human_Orchestrator
    role: "Orquestrador de Projeto"
    responsibilities:
      - Coordenação de entregas IA ↔ Humano
      - Aprovação de baseline e documentação final
  - id: Human_Reviewer
    role: "Revisor Técnico"
    responsibilities:
      - Revisão de código, arquitetura e artefatos técnicos
  - id: Human_Stakeholder
    role: "Representante de Negócio"
    responsibilities:
      - Validação de requisitos funcionais e metas de valor
```

---

# 📆 4. FASES DO PROJETO

| Fase | Nome | Objetivo | Entregável | Auditor |
|------|------|-----------|-------------|----------|
| 0 | Setup & Governança | Instanciar protocolo, definir agentes e personas | Protocolo do Projeto | IA_Auditor |
| 1 | Conceito | Desenhar e validar blueprint inicial | Documento de Conceito | Human_Orchestrator |
| 2 | Desenvolvimento | Implementar MVP | Código, Docs, Logs | IA_QA |
| 3 | Validação | Validar requisitos técnicos e de negócio | Checklist de Aceite | Junta Validadora |
| 4 | Baseline & Auditoria | Fixar versão e publicar no Manifesto | Hash + Registro no ssot_registry | IA_Auditor |

---

# ⏱️ 5. SLAs E CHECKPOINTS
```yaml
sla:
  revision_humana: "48h"
  auditoria_ia: "12h"
  commit_automatizado: "Em tempo real"
checkpoints:
  - "Revisão de Conceito"
  - "Validação Técnica"
  - "Validação de Negócio"
  - "Baseline e Auditoria"
```

---

# 🔐 6. AUDITORIA E RASTREABILIDADE

Todos os artefatos devem conter:
- **Hash SHA256 de baseline**
- **Registro automático no ssot_registry**
- **Log de auditoria** com diffs entre versões

> Logs e diffs são validados pelo agente `IA_Auditor` e publicados em  
> `/governance/auditoria/<projeto>/v<versao>/diff_report.md`

---

# 🧩 7. RELAÇÃO COM O MANIFESTO

Ao ser homologado, este protocolo será registrado no **Manifesto Corporativo**:
```yaml
projetos_ativos:
  - nome: "<NOME_DO_PROJETO>"
    protocolo: "/governance/projects/<NOME_DO_PROJETO>/protocolo/PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.0.md"
    derived_from: "/governance/meta/PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md"
    status: "Ativo"
```

---

# 🧾 8. POLÍTICA DE ATUALIZAÇÃO

- As revisões deste protocolo devem seguir controle de versão semântico (`v1.x`).
- Cada atualização deve passar pela **Junta Validadora**.
- Alterações estruturais exigem aprovação da **Governança Corporativa** (nível meta).

---

# ✅ 9. HOMOLOGAÇÃO
- **Data de Homologação:** <AAAA-MM-DD>  
- **Versão Homologada:** v1.0  
- **Junta Responsável:** Sistemas, Negócio, Compliance, Fiscal  
- **Assinatura de Integridade:** <hash>

---

> **FIM DO TEMPLATE**
> Este documento é uma instância derivada do protocolo corporativo.
> Utilize este arquivo como base para iniciar qualquer novo projeto.
