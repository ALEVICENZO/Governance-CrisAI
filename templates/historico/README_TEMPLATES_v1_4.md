# 📘 README_TEMPLATES_v1.4.md  
### Diretório: `/governance/templates/`  
**Versão:** 1.4  
**Data:** 2025-11-02  
**Finalidade:** Documentação completa dos templates corporativos para criação padronizada de projetos

---

## 🎯 Propósito

Este diretório contém **templates oficiais e universais** da governança corporativa v1.4.  
Eles são **GENÉRICOS e PORTÁVEIS**, aplicáveis a qualquer domínio de negócio ou stack tecnológico.

**Diferença fundamental:**
- ✅ **Templates** (aqui) = GENÉRICOS, com placeholders
- 📁 **Projetos** (`/governance/projects/`) = ESPECÍFICOS, com valores reais

---

## 📂 Templates Disponíveis

| Arquivo | Propósito | Status | Baseado Em |
|---------|-----------|--------|------------|
| `modelo_blueprint.md` | Template para blueprints técnicos | ✅ **Completo** | DockManager Blueprint Fase 1 |
| `modelo_protocolo_projeto.md` | Template para protocolo de projeto | ✅ **Completo** | Protocolo DockManager v1.3 |
| `modelo_manifesto_projeto.yaml` | Template para manifesto de projeto | ✅ **Completo** | Estrutura expandida |
| `PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.md` | Template bilíngue (PT/EN) | ✅ **Completo** | Protocolo corporativo v1.3 |
| `PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.yaml` | Metadados estruturados | ✅ **Completo** | YAML corporativo |

---

## 📋 1. modelo_blueprint.md

### **Propósito**
Template genérico para criação de blueprints técnicos executáveis por IAs.

### **Estrutura**
```markdown
1. Contexto e Escopo
2. Arquitetura Funcional (Visão Lógica)
3. Modelagem Técnica (Entidades, APIs)
4-N. #BLOCK:<NOME> (Blocos técnicos implementáveis)
N+1. Integração com Sistemas Externos
N+2. Auditoria e Rastreabilidade
N+3. Observabilidade
N+4. Segurança
N+5. Testes e QA
N+6. Fluxo de Execução IA-Humano
N+7. Roadmap de Implementação
N+8. Referências
```

### **Características**
- ✅ Usa `<PLACEHOLDERS>` para valores específicos
- ✅ Inclui exemplos genéricos
- ✅ Referencia DockManager como caso de uso
- ✅ Blocos marcados `#BLOCK:*` para IAs implementarem
- ✅ Seções de observabilidade e segurança

### **Como Usar**
1. Copiar para `/governance/projects/<projeto>/blueprints/`
2. Renomear: `Blueprint_<PROJETO>_Fase<X>_<Modulo>_v1.0.md`
3. Substituir `<PLACEHOLDERS>`:
   - `<NOME_DO_PROJETO>` → nome real do projeto
   - `<FASE_OU_MODULO>` → ex: "Fase 1: Motor de Workflows"
   - `<STACK_TECNOLOGICO>` → ex: "Node.js + NestJS"
   - `<COMPONENTE_X>` → nomes dos componentes específicos
4. Preencher seções técnicas baseado no CONCEITO_TECH.md
5. Validar com IA_Architect e Junta Validadora

### **Exemplo Real**
Consulte: `/governance/projects/dockmanager/Blueprint_Fase1_Motor_Workflows_v1_0.md`

---

## 📋 2. modelo_protocolo_projeto.md

### **Propósito**
Template genérico para protocolos específicos de projeto que **herdam** do protocolo corporativo.

### **Estrutura**
```markdown
1. Objetivo (herda do corporativo)
2. Papéis e Responsabilidades
   2.1 Universais (herdados)
   2.2 Adicionais (projeto-específico)
3. Componentização Específica
4. Context Pack e Controle de Tokens
5. Fluxo de Entrega Multiagente
6. SLAs (padrão + customizados)
7. Padrões de Código e Design System
8. Hierarquia SSoT
9. Junta Validadora
10. Infraestrutura e Observabilidade
11. Critérios de Aceite
12. Revisões e Evolução
13. Conclusão
14. Referências
```

### **Características**
- ✅ **NÃO repete** o que está no protocolo corporativo
- ✅ Adiciona APENAS especificidades do projeto
- ✅ Define papéis IA adicionais (IA_Fiscal, IA_Payments, etc.)
- ✅ Lista os 5 papéis universais obrigatórios (incluindo IA_Governance)
- ✅ Customiza SLAs se necessário
- ✅ Define stack tecnológico específico
- ✅ Documenta hierarquia SSoT do projeto

### **Como Usar**
1. Copiar para `/governance/projects/<projeto>/protocolos/`
2. Renomear: `PROTOCOLO_GOVERNANCA_IA_HUMANO_<PROJETO>_v1.0.md`
3. Substituir `<PLACEHOLDERS>`
4. Preencher seção 2.2 (Papéis Adicionais) se necessário
5. Definir stack tecnológico (Seção 7.2)
6. Documentar hierarquia SSoT (Seção 8)
7. Definir Junta Validadora (Seção 9)
8. Validar com Orquestrador e Junta

### **Exemplo Real**
Consulte: `/governance/projects/dockmanager/PROTOCOLO_GOVERNANCA_IA_HUMANO_DOCKMANAGER_v1_3.md`

---

## 📋 3. modelo_manifesto_projeto.yaml

### **Propósito**
Template YAML para criação de manifestos de projetos individuais (OPCIONAL - apenas para projetos complexos).

### **Estrutura**
```yaml
manifesto_version: '0.1'
project:
  name, code, version, status, domain, complexity
purpose: <descrição>
scope: <objetivos, features, out_of_scope>
documents:
  master, derived, blueprints, protocol, governance
ai_agents:
  universal, specialized
stack:
  backend, frontend, messaging, infrastructure
validation_team:
  business, technical, compliance, user, auditor
phases:
  - phase 1, 2, 3...
metrics:
  business, technical
audit:
  registry_path, ssot_integrity, compliance
lessons_learned: [...]
risks: [...]
changelog: {...}
references: {...}
```

### **Características**
- ✅ **OPCIONAL** - use apenas para projetos grandes/complexos
- ✅ Projetos simples podem usar apenas README + Protocolo
- ✅ Estrutura completa de metadados
- ✅ Rastreabilidade de fases e métricas
- ✅ Registro de lições aprendidas e riscos

### **Como Usar**
1. Avaliar se o projeto precisa de manifesto próprio
2. Copiar para `/governance/projects/<projeto>/`
3. Renomear: `MANIFESTO_<PROJETO>_v0.1.yaml`
4. Preencher TODOS os campos obrigatórios
5. Atualizar conforme o projeto evolui
6. Registrar no `MANIFESTO_GOVERNANCA_v1.4.yaml` corporativo

### **Quando Usar**
- ✅ Projetos com múltiplas fases complexas
- ✅ Projetos com múltiplos agentes IA especializados
- ✅ Projetos que precisam de rastreabilidade detalhada de métricas
- ❌ Projetos simples (< 3 meses, 1-2 agentes IA)

---

## 📋 4. PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.md

### **Propósito**
Template **bilíngue (PT/EN)** completo e consolidado para protocolos de projeto.

### **Características ESPECIAIS**
- ✅ **Bilíngue:** Português e Inglês lado a lado
- ✅ **Completo:** Todas as 14 seções (v1.3.2 estava truncado)
- ✅ **Metadados YAML:** Header completo para pipelines
- ✅ **4 Blocos de Governança:** SSoT, Regras, Automação, Agentes
- ✅ **Compatível:** v1.0, v1.3, v1.3.1, v1.3.2, v1.4

### **Estrutura (14 Seções)**
```markdown
1. Propósito e Escopo (PT/EN)
2. Blocos de Governança (4 blocos)
3. Agentes do Projeto (universal + opcionais)
   - Universais: IA_Architect, IA_Developer, IA_Auditor, IA_Governance
   - Opcionais: IA_Fiscal, IA_Infra, etc.
4. Componentização
5. Hierarquia SSoT
6. SLAs e Fluxos
7. Stack Tecnológico
8. Segurança e Compliance
9. Observabilidade
10. Critérios de Aceite
11. Política de Rollback
12. Changelog do Projeto
13. Referências
14. Conclusão
```

### **Diferença do modelo_protocolo_projeto.md**
| Aspecto | modelo_protocolo_projeto.md | TEMPLATE_v1.4.md |
|---------|----------------------------|------------------|
| Idioma | Português | Bilíngue (PT/EN) |
| Formato | Prosa | Estruturado (blocos) |
| Metadados | Simples | YAML completo |
| Uso | Projetos nacionais | Projetos internacionais ou pipelines |

### **Como Usar**
- Use **modelo_protocolo_projeto.md** para projetos brasileiros simples
- Use **TEMPLATE_v1.4.md** para projetos internacionais ou que precisam de integração CI/CD forte

---

## 📋 5. PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.4.yaml

### **Propósito**
Metadados estruturados que acompanham o template .md, para consumo por pipelines e IAs.

### **Estrutura**
```yaml
# Metadados
version, title, organization, framework_version

# Bloco 1: SSoT
ssot: paths, templates

# Bloco 2: Governança
governance_rules: SLAs, required_fields

# Bloco 3: Automação
automation: hooks, audit config

# Bloco 4: Agentes
agents: universal, optional, human

# Estruturas
ssot_structure, componentization, compliance, rollback

# Versionamento
version_info, changes, compatibility
```

### **Como Usar**
1. **NÃO editar manualmente** (gerado automaticamente)
2. Consumido por pipelines CI/CD
3. Lido por IAs para validação estrutural
4. Sincronizado com o .md correspondente

---

## 🔄 Como Criar um Novo Projeto

### **Passo a Passo Completo**

```bash
# 1. Criar estrutura de diretórios
mkdir -p /governance/projects/<projeto>/{conceito,documentos,blueprints,protocolos,auditoria}

# 2. Copiar templates
cp /governance/templates/modelo_protocolo_projeto.md \
   /governance/projects/<projeto>/protocolos/PROTOCOLO_GOVERNANCA_IA_HUMANO_<PROJETO>_v1.0.md

cp /governance/templates/modelo_blueprint.md \
   /governance/projects/<projeto>/blueprints/Blueprint_<PROJETO>_Fase1_<Modulo>_v1.0.md

# 3. (Opcional) Copiar manifesto para projetos complexos
cp /governance/templates/modelo_manifesto_projeto.yaml \
   /governance/projects/<projeto>/MANIFESTO_<PROJETO>_v0.1.yaml

# 4. Substituir placeholders
# <NOME_DO_PROJETO> → nome real
# <CODIGO_INTERNO> → código do projeto
# <STACK_TECNOLOGICO> → tecnologias específicas

# 5. Criar CONCEITO_TECH.md (SSoT Master)
# Este é criado por humanos, não é template

# 6. Validar com Junta Validadora

# 7. Registrar no MANIFESTO_GOVERNANCA_v1.4.yaml
```

---

## 🎓 Lições Aprendidas (DockManager)

### **O Que Funcionou**
- ✅ Templates genéricos permitem reutilização em qualquer domínio
- ✅ Placeholders `<>` tornam óbvio o que precisa ser preenchido
- ✅ Exemplos práticos (DockManager) ajudam a entender estrutura
- ✅ Separação clara entre genérico (template) e específico (projeto)
- ✅ Inclusão de IA_Governance como papel obrigatório garante conformidade

### **Armadilhas a Evitar**
- ❌ **NÃO** fazer hardcode de detalhes técnicos nos templates
- ❌ **NÃO** criar templates "vazios demais" (sem estrutura)
- ❌ **NÃO** criar templates "cheios demais" (muito específicos)
- ❌ **NÃO** esquecer de referenciar o projeto piloto (DockManager)

---

## 📊 Comparação: Templates vs. Projeto Real

| Aspecto | Template | DockManager (Real) |
|---------|----------|-------------------|
| **Stack** | `<linguagem>` | Node.js + NestJS |
| **Papéis IA** | IA_<Role> | IA_Fiscal, IA_Infra |
| **Componentes** | `<COMPONENTE_X>` | Motor de Workflows, Módulo Fiscal |
| **SLAs** | Padrão (16h, 48h) | Customizados (12h fiscal) |
| **Economia Tokens** | `<X%>` | 40% (Tech), 85% (Fiscal) |

---

## 🔍 Validação de Templates

### **Checklist antes de usar:**
- [ ] Todos os `<PLACEHOLDERS>` identificados?
- [ ] Estrutura de seções completa?
- [ ] Referências ao protocolo corporativo corretas?
- [ ] Exemplos genéricos (não específicos de DockManager)?
- [ ] Instruções de preenchimento claras?
- [ ] Referência ao DockManager como exemplo prático?

---

## 📚 Referências

### **Documentos Corporativos**
- `PROTOCOLO_METODOLOGICO_CORPORATIVO_IA_HUMANO_v1.0.md`
- `PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md`
- `MANIFESTO_GOVERNANCA_v1.4.yaml` ← **[Manifesto Corporativo](../MANIFESTO_GOVERNANCA_v1.4.yaml)**
- `CONTEXT_MAP_GOVERNANCA_v1.4.yaml`
- `README_HISTORICO_v1.4.md`

### **Projeto Piloto (Exemplo Real)**
- `/governance/projects/dockmanager/`
- `DOCK_MANAGER_v13_CONCEITO_TECH.md`
- `Blueprint_Fase1_Motor_Workflows_v1_0.md`
- `PROTOCOLO_GOVERNANCA_IA_HUMANO_DOCKMANAGER_v1_3.md`

---

## 🔢 Versionamento Semântico de Templates

### **Esquema de Versionamento**

Os templates seguem versionamento semântico alinhado com o framework:

```
v1.4.0 → Versão base alinhada com framework v1.4
v1.4.1 → Correções não-destrutivas (patches)
v1.5.0 → Novas funcionalidades não-destrutivas
v2.0.0 → Mudanças estruturais (breaking changes)
```

### **Quando Incrementar Versão**

| Tipo de Mudança | Versão | Exemplo |
|-----------------|--------|---------|
| **Correção de bug/typo** | Patch (1.4.0 → 1.4.1) | Corrigir SLA inconsistente |
| **Nova seção opcional** | Minor (1.4.0 → 1.5.0) | Adicionar seção "Testes E2E" |
| **Mudança obrigatória** | Major (1.4.0 → 2.0.0) | Alterar estrutura de YAML |

### **Correções Aplicadas (v1.4.0+corrections)**

Em 2025-11-02, foram aplicadas **correções não-destrutivas** nos templates v1.4:

1. ✅ **Adicionado `framework_version: "1.4"`** em todos os headers YAML
2. ✅ **Harmonizado SLA de auditoria** (removido "12h" inconsistente)
3. ✅ **Adicionadas referências cruzadas opcionais** (`manifest_reference`)
4. ✅ **Parametrização de paths** com macros `{{project_path}}`
5. ✅ **Centralização de macros** no `CONTEXT_MAP_GOVERNANCA_v1.4.yaml`

**Impacto:** Não-destrutivo, totalmente retrocompatível  
**Documentação:** Registrado no `MANIFESTO_GOVERNANCA_v1.4.yaml` (seção `corrections`)

---

## 🎯 Próximos Passos

Após dominar esses templates, você poderá:
1. Criar novos projetos em < 1 hora
2. Garantir conformidade automática com o framework v1.4
3. Reutilizar estruturas validadas pelo DockManager
4. Escalar a governança IA-Humano para múltiplos projetos

---

**Última atualização:** 2025-11-02  
**Versão:** 1.4  
**Status:** Completo e validado  
**Próxima revisão:** 2026-05-02
