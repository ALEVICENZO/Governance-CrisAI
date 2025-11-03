---
framework_name: "CrisAI"
framework_acronym: "CRIS"
framework_meaning: "Cognitive Responsible Innovation System"
framework_tagline: "Inovação Cognitiva com Responsabilidade e Propósito"
framework_version: "1.4"
framework_named_for: "Cris Vicenzo"
last_reviewed: "2025-11-02"
---

# 🧭 Governança Corporativa IA-Humano — Vicenzo Corp (CrisAI)

## Propósito
Este documento estabelece o ponto de origem da Governança Corporativa IA-Humano para a organização `vicenzo_corp`.
Define como humanos e agentes de IA colaboram sob princípios de rastreabilidade, integridade e conformidade, em um ciclo contínuo de melhoria e aprendizado.

## 🎯 Ponto de Entrada do Framework

**Para sistemas, pipelines e IAs:**
- **Arquivo de entrada:** `MANIFESTO_GOVERNANCA_v1.4.yaml` (em `/governance/meta/`)
- **Função:** Roteador que aponta para contextualização de cada projeto

**Para humanos (primeira leitura):**
- **Arquivo de entrada:** `README_GOVERNANCE_ROOT.md` (este documento)
- **Função:** Visão estrutural e explicação do framework

**Ordem de leitura recomendada:**
1. `README_GOVERNANCE_ROOT.md` → Entenda a estrutura
2. `MANIFESTO_GOVERNANCA_v1.4.yaml` → Veja projetos e contextualização
3. `CONTEXT_MAP_GOVERNANCA_v1.4.yaml` → Entenda relacionamentos entre artefatos

---

## Estrutura Hierárquica

```
/governance/                           # Raiz da governança
├── README_GOVERNANCE_ROOT.md          # Este documento (ponto de entrada humano)
│
├── meta/                              # Protocolos e artefatos corporativos universais
│   ├── historico/
│   ├── MANIFESTO_GOVERNANCA_v1.4.yaml                        # 🎯 Roteador (aponta projetos)
│   ├── CONTEXT_MAP_GOVERNANCA_v1.4.yaml                      # Mapa de relacionamentos
│   ├── README_GOVERNANCA_CORPORATIVA_v1.4.md                 # Documentação completa
│   ├── README_HISTORICO_v1.4.md                              # Narrativa evolutiva
│   ├── PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.yaml
│   ├── PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md                # Protocolo universal
│   ├── PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.yaml
│   └── PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md  # Guia metodológico
│
├── templates/                         # Modelos genéricos para criação de novos projetos
│   ├── historico/
│   ├── README_TEMPLATES_v1.4.md
│   ├── PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.yaml
│   ├── PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.md
│   ├── modelo_readme_quick_start_projeto.md                  # Template contextualização
│   ├── modelo_protocolo_projeto.md
│   ├── modelo_manifesto_projeto.yaml
│   ├── modelo_blueprint.yaml
│   └── modelo_blueprint.md
│
├── projects/                          # Portfólio de projetos
│   │
│   ├── pgiah/                        # Projeto PGIAH (Plataforma de Governança IA-Humana)
│   │   ├── README_QUICK_START_PGIAH.md              # Contextualização do projeto
│   │   ├── protocolos/
│   │   │   └── PROTOCOLO_GOVERNANCA_IA_HUMANO_PGIAH_v1.0.md
│   │   ├── documentos/
│   │   │   └── PGIAH_CONCEITO_TECH.md
│   │   ├── blueprints/
│   │   │   ├── Blueprint_Pipeline_CI_CD_v1_0.md
│   │   │   ├── Blueprint_MCP_Server_Minimal_v1_0.md
│   │   │   └── Blueprint_UI_Dashboard_Basic_v1_0.md
│   │   └── auditoria/
│   │
│   └── dockmanager/                  # Projeto DockManager v13 (Homologado)
│       ├── README_QUICK_START_DOCKMANAGER.md        # Contextualização do projeto
│       ├── conceito/
│       │   └── DOCK_MANAGER_v13_CONCEITO_TECH.md
│       ├── documentos/
│       │   ├── README_DOCKMANAGER_v13.md
│       │   ├── MEMORANDO_HOMOLOGACAO_V13.md
│       │   ├── DOCK_MANAGER_v13_TECH.md
│       │   └── DOCK_MANAGER_v13_EXT_FISCAL.md
│       ├── protocolos/
│       │   └── PROTOCOLO_GOVERNANCA_IA_HUMANO_DOCKMANAGER_v1_3.md
│       ├── blueprints/
│       │   └── Blueprint_Fase1_Motor_Workflows_v1_0.md
│       └── auditoria/
│
├── ssot_registry/                     # Registros de auditoria (SHA256, timestamps)
│   ├── historico/
│   └── SSOT_ENTRY_*.yaml             # Registros individuais de artefatos
│
├── auditoria/                         # Logs de auditoria, diffs, relatórios de conformidade
│
└── historico/                         # Versões anteriores de documentos (arquivamento)
```

O manifesto define `/governance/` como raiz e ponto de origem do registro da governança corporativa.

---

## 🎯 Fluxo de Contextualização (Framework CrisAI)

O framework CrisAI implementa **contextualização em cascata** para que IAs trabalhem de forma focada e eficiente:

### **Como funciona:**

1. **Orquestrador indica projeto:**
   - Alexandre diz: "Trabalhe no projeto PGIAH"

2. **IA lê Manifesto:**
   - Arquivo: `/governance/meta/MANIFESTO_GOVERNANCA_v1.4.yaml`
   - Busca seção: `contextualizacao_projetos`
   - Identifica projeto: `PGIAH`

3. **Manifesto aponta para contextualização:**
   ```yaml
   pgiah:
     quickstart: "/governance/projects/pgiah/README_QUICK_START_PGIAH.md"
     protocolo: "/governance/projects/pgiah/protocolos/PROTOCOLO_GOVERNANCA_IA_HUMANO_PGIAH_v1.0.md"
   ```

4. **IA lê README_QUICK_START:**
   - Aprende: o que é o projeto, equipe, fluxo, documentos, status

5. **IA lê PROTOCOLO do projeto:**
   - Aprende: regras operacionais específicas

6. **IA está 100% contextualizada:**
   - Pronta para trabalhar especificamente no PGIAH

### **Benefícios:**
- ✅ IA não precisa ler documentos de outros projetos
- ✅ Contextualização focada e eficiente
- ✅ Economia de tokens (40-85%)
- ✅ Escalável para N projetos

---

## Papéis Fundamentais

- **Orquestrador_Humano (Alexandre Vicenzo):** Responsável por aprovar e consolidar decisões de alto nível, indicar projetos para IAs.
- **IA_Architect (GPT-4):** Interpreta contexto global, gera artefatos e propaga diretrizes para outros agentes.
- **IA_Developer:** Implementa artefatos derivados e blueprints com base em subsets técnicos.
- **IA_Governance (Claude 3.5 Sonnet):** Monitora conformidade, valida semântica e mantém consistência documental.
- **IA_Auditor (Gemini 2.0):** Valida integridade (hashes, estrutura YAML, diffs, logs) e emite alertas de divergência.

---

## Fluxo de Automação

1. **Pipeline/IA lê:** `MANIFESTO_GOVERNANCA_v1.4.yaml` como ponto inicial
2. **IA_Architect:** Interpreta contexto e gera artefatos
3. **IA_Governance:** Valida conformidade semântica e aderência aos protocolos
4. **IA_Auditor:** Valida integridade via `ssot_registry` (hashes SHA256)
5. **Junta Validadora:** Confirma integridade humana (multidisciplinar)
6. **Orquestrador:** Aprova e registra no SSoT Registry
7. **Atualizações:** Versionadas com hash e timestamp

---

## Rastreabilidade e Auditoria

Todos os arquivos são registrados no `ssot_registry` com:
- **Hash SHA256:** Garante integridade do conteúdo
- **Timestamp UTC:** Rastreabilidade temporal
- **Cadeia de validação:** IA_Architect → IA_Governance → IA_Auditor → Orquestrador

A rastreabilidade é bidirecional:
- Cada arquivo aponta para sua origem (`derived_from`)
- Cada arquivo aponta para quem o usa (`used_by`)

Logs de auditoria são duplicados na pasta `auditoria` para redundância.

---

## Política de Atualização

Durante a fase de estabilização (pré-produção), todas as atualizações permanecem dentro da mesma versão (v1.4).
Somente após homologação será emitida a versão final **v1.4-final**.

**Toda modificação deve:**
1. Ser validada pela Junta Validadora
2. Ser registrada com nova entrada no changelog do manifesto
3. Ser auditada com hash SHA256 atualizado no `ssot_registry`

O manifesto é o artefato de referência obrigatória para novas iniciativas corporativas.

---

## Documentos Relacionados

**Corporativos (em `/governance/meta/`):**
- **MANIFESTO_GOVERNANCA_v1.4.yaml** — Registro central, changelog, portfólio e roteador (🎯 entry point)
- **CONTEXT_MAP_GOVERNANCA_v1.4.yaml** — Mapa estrutural e de relacionamentos completo
- **README_GOVERNANCA_CORPORATIVA_v1.4.md** — Documentação detalhada do framework
- **README_HISTORICO_v1.4.md** — Narrativa evolutiva do framework (v1.0 → v1.4)
- **PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md** — Regras, papéis, fluxos e SLAs universais
- **PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md** — Guia normativo para criação de protocolos

**Templates (em `/governance/templates/`):**
- **modelo_readme_quick_start_projeto.md** — Template para contextualização de novos projetos

**Projetos (em `/governance/projects/`):**
- **PGIAH** — Plataforma de Governança IA-Humana (em desenvolvimento - Fase 0)
- **DockManager v13** — Plataforma Logística Low-Code (homologado ✅)

---

## 📌 Nota sobre Versionamento

- **Framework CrisAI:** v1.4 (unificado em 2025-11-02)
- **Última revisão deste documento:** 2025-11-03
- **Status:** Ativo e em evolução

---

**Este documento é mantido por:**
- **IA_Governance** (Claude 3.5 Sonnet) — Validação semântica e conformidade
- **IA_Auditor** (Gemini 2.0) — Integridade estrutural e formatação
- **Orquestrador_Humano** (Alexandre Vicenzo) — Aprovação final e direção estratégica

---

**Framework CrisAI v1.4**  
*Cognitive Responsible Innovation System + AI*  
*"Inovação Cognitiva com Responsabilidade e Propósito"*  
Em homenagem a Cris Vicenzo.
