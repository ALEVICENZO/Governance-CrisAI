# 📚 SSoT Registry - Framework v1.4
Este diretório centraliza os registros de Fonte Única da Verdade (Single Source of Truth) de todos os projetos e protocolos da organização.

## 🎯 Propósito
Manter rastreabilidade completa de todos os artefatos corporativos e de projetos através de:
- Referência ao documento master (ex: CONCEITO_TECH.md)
- Lista de documentos derivados
- Hash SHA256 de controle de integridade
- Última data de validação
- Cadeia de validação (IA + Humano)

## 📊 Estrutura de Entrada SSoT
Cada entrada SSoT contém:
```yaml
ssot_entry:
  artifact: "<nome_do_arquivo>"
  version: "<versao>"
  sha256: "<hash_sha256>"
  registered_at: "<timestamp_utc>"
  registry_path: "<path_no_repositorio>"
  maintainer: "<responsavel>"
  organization: "Vicenzo_Corp"
  validated_by: [lista de validadores]
  notes: "Descrição e contexto"
  framework_version: "1.4"
  document_type: "<tipo>"
  audit_level: "<critical|high|medium>"
```

## 📋 Registros Atuais (Framework v1.4)

### Documentos Corporativos (Meta)
- **CONTEXT_MAP_GOVERNANCA_v1.4.yaml** - Mapa estrutural universal
- **MANIFESTO_GOVERNANCA_v1.4.yaml** - Registro central e changelog
- **PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md/.yaml** - Protocolo universal
- **PROTOCOLO_METODOLOGICO_v1.0.md/.yaml** - Guia metodológico
- **README_GOVERNANCE_ROOT.md** - Ponto de entrada
- **README_GOVERNANCA_CORPORATIVA_v1.4.md** - Documentação completa

### Registro de Governança
- **governance_root_record.yaml** - Registro do ponto de entrada universal

## ✅ Validação e Auditoria
Todos os registros são:
1. **Calculados** - Hash SHA256 automático
2. **Validados** - IA_Auditor + IA_Governance
3. **Aprovados** - Orquestrador_Humano / Junta_Validadora
4. **Rastreáveis** - Timestamp UTC e cadeia de validação
5. **Imutáveis** - Logs mantidos por 5 anos

## 🔄 Atualização de Registros
Quando um documento é atualizado:
1. Novo hash SHA256 é calculado
2. Registro SSoT é atualizado
3. Hash anterior é arquivado no histórico
4. IA_Auditor valida integridade
5. IA_Governance verifica conformidade

## 📁 Convenção de Nomenclatura
```
SSOT_ENTRY_<DOCUMENTO>_v<VERSAO>.yaml
```

Exemplos:
- `SSOT_ENTRY_CONTEXT_MAP_v1.4.yaml`
- `SSOT_ENTRY_MANIFESTO_v1.4.yaml`
- `SSOT_ENTRY_PROTOCOLO_GOVERNANCA_v1.3.yaml`

## 🔐 Níveis de Auditoria
- **critical** - Documentos corporativos core, mudanças requerem aprovação máxima
- **high** - Documentos importantes, mudanças requerem validação técnica
- **medium** - Documentos operacionais, validação simplificada

## 📅 Última Atualização
- **Data**: 2025-11-03T00:41:30Z
- **Framework**: v1.4
- **Validado por**: IA_Auditor + IA_Governance + Orquestrador_Humano
- **Correções aplicadas**: Encoding UTF-8 + Versionamento unificado
