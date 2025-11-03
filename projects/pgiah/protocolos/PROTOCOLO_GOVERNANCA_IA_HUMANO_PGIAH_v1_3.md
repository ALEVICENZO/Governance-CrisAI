document_type: "protocolo"
file_name: "PROTOCOLO_GOVERNANCA_IA_HUMANO_PGIAH_v1_1.md"
project: "PGIAH – Plataforma de Governança IA-Humana"
framework: "CrisAI v1.4"
versao_protocolo: "1.1"
nota_versionamento: "v1.0 (criada por IA_Auditor) foi ANULADA; esta é a primeira versão válida do protocolo de projeto."
herda_de: "PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3"
status: "draft_em_validacao"
responsavel_draft: "IA_Developer (GPT-4)"
supervisao: "IA_Architect (GPT-4)"
validador_semantico: "IA_Governance (Claude 3.5 Sonnet)"
auditor_integridade: "IA_Auditor (Gemini 2.0)"
orquestrador_humano: "Alexandre Vicenzo"
data_criacao: "2025-11-03T22:00:00Z"
derived_from: "/governance/meta/PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md"
checksum: "pending"
PROTOCOLO DE GOVERNANÇA IA–HUMANO — PGIAH (v1.1)

Derivado do PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3 — Framework CrisAI v1.4.

1. Propósito

Estabelecer as regras operacionais, papéis e critérios de auditoria do projeto PGIAH, que implementa o framework CrisAI com foco em responsabilidade, rastreabilidade e propósito.

2. Escopo

Abrange:

Criação/evolução de artefatos (YAML, Markdown, Blueprints, Logs);

Validação semântica, auditoria técnica e registro SSoT;

Operação das Fases 0 e 1 do PGIAH.

Fora de escopo (por ora):

Automação plena via MCP (Fase 2);

Interoperabilidade detalhada com outros projetos (além da referência de homologação ao DockManager v13).

3. Estrutura SSoT (Single Source of Truth)
3.1 Artefato Master

artefato_master_nome: PGIAH_ARQUITETURA_MASTER_v1_0.md

artefato_master_status: PLANEJADO

artefato_master_previsto: 2025-11-10

O Master consolidará arquitetura (MCP, CI/CD, Dashboard) e relacionamentos. Em Fase 0 permanece PLANEJADO e deve ser auditado/publicado até a data prevista.

4. Papéis e Responsabilidades
Papel	Implementação	Responsabilidades
Orquestrador_Humano	Alexandre Vicenzo	Aprovação final, registro no SSoT, direção estratégica e ética.
IA_Architect	GPT-4	Cria blueprints, define arquitetura de componentes/bots e herança documental.
IA_Developer	GPT-4	Implementa artefatos técnicos com base nos blueprints do Architect.
IA_Governance	Claude 3.5 Sonnet	Valida semântica e aderência ao framework/protocolos.
IA_Auditor	Gemini 2.0	Audita integridade (SHA256, diffs, logs) e registra entradas SSoT.
IA_Infra (futuro)	A definir	Executa CI/CD e operação do MCP Server (quando habilitado).

Nota: O papel IA_MetaDeveloper não existe no framework.

5. Homologação e Re-auditoria (Referência: DockManager v13)

A homologação do PGIAH exige re-auditoria do DockManager v13:

IA_Auditor: extrair e verificar SHA256 do SSoT do DockManager v13;

IA_Governance: validar consistência com o Manifesto v1.4 (compatibilidade declarada);

IA_Auditor: emitir Relatório de Integridade de Referência;

Orquestrador_Humano: aprovar compatibilidade e registrar no ssot_registry.

Qualquer menção a “DockManager v14” é vedada neste protocolo.

6. SLAs Específicos — PGIAH (Fase 0)
Processo	SLA (úteis)	Responsável
Blueprint inicial	16h	IA_Architect
Implementação do artefato	16h	IA_Developer
Validação semântica	8h	IA_Governance
Auditoria de integridade	8h	IA_Auditor
Aprovação + registro no SSoT	24h	Orquestrador_Humano
Retrabalho após não conformidade	12h	IA_Developer / IA_Architect

O ciclo completo (blueprint → aprovação final) não deve exceder 48h úteis.

7. Rastreabilidade e Versionamento

Obrigatório em todos os artefatos:

derived_from (origem) e used_by (consumidores);

checksum (SHA256) e timestamp (UTC);

Entrada no ssot_registry com nível de auditoria;

Duplicação de logs em /governance/auditoria.

Encadeamento bidirecional (origem ↔ uso) é mandatório.
A partir da Fase 1, a auditoria terá gatilhos automáticos via MCP.

8. Segurança e Permissões (Least Privilege)
Agente	Permissões	Observações
Orquestrador_Humano	leitura/escrita total	Autoridade final, registros oficiais.
IA_Architect	leitura/escrita (arquitetura)	Define blueprints e herança documental.
IA_Developer	leitura/escrita (artefatos técnicos)	Implementa; não aprova nem audita.
IA_Governance	leitura + comentários	Valida conformidade; não altera conteúdo.
IA_Auditor	leitura + geração de hash/log	Garante integridade; não altera conteúdo.
IA_Infra (futuro)	execução de pipelines	Opera sob aprovação do Orquestrador.

Todas as ações são logadas e auditáveis.

9. Fluxo Operacional (Aderente ao Universal v1.3, com melhoria PGIAH)

IA_Architect cria blueprint do componente/artefato PGIAH;

IA_Developer implementa o artefato com base no blueprint;

IA_Governance valida semântica e aderência ao framework;

IA_Auditor calcula SHA256, registra diffs e minuta SSoT;

IA_Infra (se habilitado) executa CI/CD e monitora;

Orquestrador_Humano aprova e registra no ssot_registry.

Nota sobre o fluxo: mantém-se o padrão universal; a inclusão explícita do IA_Governance entre (2) e (4) é uma extensão justificada para o meta-projeto PGIAH (governança é objeto do próprio projeto).

10. Histórico de Revisão
Data	Versão	Agente	Ação	Observação
2025-11-02	v1.0	IA_Auditor (Gemini 2.0)	Criação indevida	Artefato anulado (violação de papel).
2025-11-03	v1.1	IA_Developer (GPT-4)	Recriação correta	Sob supervisão do IA_Architect (GPT-4).
2025-11-03	v1.1	IA_Governance (Claude 3.5)	Validação	Pendente de parecer formal.
2025-11-03	v1.1	IA_Auditor (Gemini 2.0)	Auditoria	Pendente de hash SHA256.
2025-11-03	v1.1	Orquestrador (A. Vicenzo)	Aprovação	Pendente de registro SSoT.
Referências

Manifesto: MANIFESTO_GOVERNANCA_v1.4.yaml

Protocolo Universal: PROTOCOLO_GOVERNANCA_IA_HUMANO_v1.3.md

Quick Start PGIAH: README_QUICK_START_PGIAH.md

SSoT Registry: /governance/ssot_registry/

Auditoria: /governance/auditoria/