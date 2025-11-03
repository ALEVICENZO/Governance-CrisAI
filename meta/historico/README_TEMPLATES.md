# 📘 README_TEMPLATES.md  
### Diretório: `/governance/meta/templates/`  
**Versão:** 1.0  
**Finalidade:** Armazenar e versionar os modelos corporativos utilizados para criação padronizada de projetos, manifestos, protocolos e blueprints no ecossistema de governança IA-Humano.

---

## 🧭 Propósito
Este diretório contém **templates oficiais e universais** da governança corporativa.  
Eles são utilizados como **ponto de partida padronizado** para a criação de novos projetos dentro da estrutura de governança descrita no `MANIFESTO_GOVERNANCA_v1.2.yaml`.

Os arquivos aqui armazenados **não são instâncias de projeto**, mas sim **modelos reutilizáveis** consumidos automaticamente por pipelines (ex: GitLab CI/CD, agentes IA, ou scripts de bootstrapping).

---

## 🧩 Estrutura e Tipos de Arquivos

| Tipo | Extensão | Função |
|------|-----------|--------|
| **Template de Documento** | `.md` | Estrutura base em formato legível por humanos e IA, com placeholders (ex: `<NOME_DO_PROJETO>`, `<OBJETIVOS>`). |
| **Template de Metadados** | `.yaml` | Arquivo auxiliar com parâmetros técnicos e campos obrigatórios para automação (ex: versionamento, paths, pipelines). |

---

## 📂 Conteúdo Atual

| Arquivo | Função | Nível |
|----------|---------|-------|
| `modelo_protocolo_projeto.md` | Modelo de protocolo de governança aplicado a projetos individuais. | L2 - Projeto |
| `modelo_manifesto_projeto.yaml` | Template YAML do manifesto de projeto, usado para registro e rastreabilidade. | L2 - Projeto |
| `modelo_blueprint.md` | Estrutura de blueprint técnico e arquitetural. | L3 - Engenharia |
| `PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.0.md` | Template textual derivado do protocolo corporativo IA-Humano. | L1 - Corporativo |
| `PROTOCOLO_GOVERNANCA_IA_HUMANO_TEMPLATE_v1.0.yaml` | Template YAML complementar para automação CI/CD. | L1 - Corporativo |

---

## 🧠 Como esses templates são usados

1. **Iniciação de Projeto:**  
   - A pipeline clona os templates relevantes deste diretório.  
   - Cria um novo diretório em `/governance/projects/<NOME_DO_PROJETO>/`.  

2. **Personalização:**  
   - Placeholders (`<NOME_DO_PROJETO>`, `<OBJETIVOS>`, `<DATA_INICIO>`) são substituídos automaticamente.  
   - O `modelo_manifesto_projeto.yaml` é preenchido com os metadados do projeto e registrado no Manifesto.  

3. **Registro:**  
   - O novo protocolo é copiado para `/governance/projects/<projeto>/protocolo/`.  
   - O blueprint é copiado para `/governance/projects/<projeto>/documentos/blueprint/`.  
   - Uma entrada é criada em `/governance/ssot_registry/` com o hash SHA256.  

4. **Auditoria:**  
   - Toda criação e alteração dispara uma entrada em `/governance/auditoria/<projeto>/`.  
   - Os agentes IA_Auditor e IA_Architect validam a integridade dos novos artefatos.  

---

## 🔄 Versionamento e Evolução
Todos os templates seguem versionamento semântico:

- **x.0:** Criação ou redefinição completa.  
- **x.1–x.9:** Ajustes de formatação, novos placeholders, ou atualizações menores.  
- **x+1.0:** Mudanças estruturais significativas (novas seções, regras, ou tipos de arquivo).  

Cada atualização de template deve gerar uma nova entrada no `MANIFESTO_GOVERNANCA_v1.X.yaml`.

---

## ⚙️ Governança Técnica (Uso por Pipelines)

O pipeline CI/CD que consome estes templates deve:

- Validar campos obrigatórios (`required_fields` no YAML).  
- Substituir placeholders de forma segura.  
- Calcular e registrar o `hash_sha256` de cada instância.  
- Registrar a criação do artefato no Manifesto e no SSOT Registry.

---

## 🔐 Política de Acesso

| Tipo de Agente | Permissão | Descrição |
|----------------|------------|------------|
| **IA_Architect** | Leitura | Pode referenciar templates e criar novos derivados. |
| **IA_Developer** | Leitura | Pode consumir templates técnicos para execução. |
| **IA_Auditor** | Leitura/Auditoria | Verifica integridade e hash de templates. |
| **Humano (Orquestrador)** | Leitura/Escrita | Autoriza novas versões e publica templates revisados. |

---

## 🧾 Registro de Versão

```yaml
readme_version: "1.0"
updated_by: "IA_Architect"
approved_by: "Junta Validadora"
last_update: "2025-11-02"
status: "Ativo"
```

---

**Resumo:**  
> Este diretório representa o núcleo da padronização metodológica da governança IA-Humano.  
> Cada template aqui armazenado é um “molde” para replicar a cultura de governança, rastreabilidade e automação corporativa nos futuros projetos.
