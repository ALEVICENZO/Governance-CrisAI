---
title: "DockManager v13 – Plataforma Low-Code de Gestão Logística"
document_type: master
version: v13_release_candidate
hierarchy:
  master: true
  derived_documents:
    - DOCK_MANAGER_v13_TECH.md
    - DOCK_MANAGER_v13_EXT_FISCAL.md
governance_protocol:
  version: "v1.4"
  ia_architect: full_context
  ia_developer: derived_technical
  ia_fiscal: derived_fiscal
  human_audit: master_only
hash_reference: "f0164494589352ae"
date: "Novembro/2025"
author: "Alexandre Vicenzo"
tags: ["Low-Code", "Workflow Engine", "No-Code Integration", "Logistics", "ERP", "Governança IA-Humana"]
---

# DOCK_MANAGER_v13_CONCEITO+TECH

> Versão integral com seções 1–15 e Extensão Fiscal
> Documento base para desenvolvimento seguindo Protocolo de Governança v1.4



DockManager v13 - Plataforma Low-Code de Gestão Logística
(Versão Integrada: Plataforma v13 + Fluxo Detalhado v12)

## 1. RESUMO EXECUTIVO


### Visão Geral

O DockManager evolui de um produto para uma plataforma low-code de automação e gestão visual. Ele combina um motor de workflows flexível (Pilar 1) e um estúdio de integração no-code (Pilar 2) com um assistente de IA (Pilar 3).
A plataforma é entregue com um "Template Padrão (v12)" robusto, pronto para otimizar o recebimento de mercadorias (fluxo físico) e a aprovação de documentos fiscais (fluxo administrativo/NFS-e).

### Problema

Caos nas docas de recebimento com filas desorganizadas.
Tempo de espera excessivo dos motoristas (média 2-4 horas).
Divergências físicas e fiscais contaminando inventário e custos.
Comunicação fragmentada entre equipes (Doca, Compras, Fiscal, Financeiro).
Documentos fiscais (Serviços, etc.) misturados com o fluxo de doca.
Rigidez de soluções "hardcoded" que não se adaptam à realidade de cada empresa, exigindo customizações caras.

### Solução

Uma plataforma de implementação No-Code/Low-Code que entrega, como "Template Padrão", um fluxo de negócio de ZERO TOLERÂNCIA, baseado em três pilares:
Motor de Workflows (Low-Code): Permite que cada empresa desenhe seu próprio fluxo de aprovação (físico ou admin) arrastando e soltando "Nodes".
MCP Integration Studio (No-Code): Um "Discovery Guiado" que permite ao implementador criar conectores com qualquer sistema (ERP, WMS, Bancos de Dados) via API, SQL ou leitura de arquivos.
DockBot (Assistente de IA Contextual): Um chat de IA integrado (In-App e Telegram/WhatsApp) que explica o sistema e guia os usuários na customização dos workflows.
Funcionalidades de Negócio (Template Padrão v12):
Classificação de Fluxo (Físico vs. Administrativo) na captura.
Gate Virtual para NF-e (Mercadorias) e NFS-e (Serviços).
Kanbans Visuais (Operacional, Setoriais e Administrativos).
Dashboard Operacional (Visão Aeroporto) para controle de pátio.
Fila de Transações Persistente e Auditoria Retroativa.

### Benefícios Esperados (Estratégicos)

Redução drástica no tempo de espera e aumento no throughput das docas.
Proteção integral do Kardex e CMV.
Gestão unificada de documentos fiscais (NF-e e NFS-e).
Plataforma 100% adaptável à realidade de qualquer empresa, sem necessidade de codificação para customizações de processo ou integração.

## 2. ARQUITETURA DA SOLUÇÃO E PLATAFORMA

2.1 Componentes de Negócio (O "Quê")
Estes são os elementos de UI e lógica de negócio que o usuário final utiliza, e que são orquestrados pelo Motor de Workflows.
Sistema Kanban Visual (Operacional, Setorial e Admin): As interfaces visuais onde os "Cards" (NF-e ou NFS-e) são gerenciados.
Dashboard Operacional (Visão Aeroporto): O painel informativo (read-only) focado no fluxo físico.
Bot de Mensageria (Telegram/WhatsApp): A interface de Ação Rápida (Nível 1) e Check-in.
IA Preditiva: O módulo de inteligência que analisa tempos e sugere alocações (ver Seção 6).


> **Nota importante:** A IA Preditiva aplica-se EXCLUSIVAMENTE ao fluxo físico (mercadorias/docas), 
> não sendo utilizada em fluxos administrativos ou fiscais (NFS-e, documentos tributários).

2.2 Componentes Técnicos (Serviços de Background)
Monitor Inteligente: Serviço de WebSocket + Polling para atualizações em tempo real.
Fila de Transações Persistente: Garante 100% de entrega de dados ao ERP/WMS, mesmo se estiverem offline (ver Seção 13).
Auditoria Retroativa: Jobs noturnos que reconciliam dados entre DockManager, ERP e SEFAZ (ver Seção 9).
2.3 Pilares da Plataforma Low-Code (O "Como")
Esta é a arquitetura de implementação que permite a flexibilidade total.
2.3.1 Pilar 1: O Motor de Workflows (O "N8N" do DockManager)
Este é o núcleo da flexibilidade. Substitui a "Matriz de Roteamento" estática.
Como Funciona:
O Administrador/Implementador terá uma tela de "arrastar e soltar".
A lógica descrita nas "FASES" (Seção 3) se torna uma biblioteca de "Nodes" (Nós) pré-construídos.
O fluxo da v12 (Físico vs. Admin) virá como o "Template de Workflow Padrão". O cliente pode usá-lo ou cloná-lo para modificar.
2.3.2 Pilar 2: O MCP Integration Studio (O "Discovery" No-Code)
O Motor de Workflows (Pilar 1) decide o quê fazer. O MCP Integration Studio decide como fazer a integração.
Como Funciona:
Criação do Conector: O implementador (no Painel Admin) clica em "Novo Conector" (ex: "Conector ERP").
Discovery Guiado: O sistema pergunta: "Como vamos ler os Pedidos de Compra?"
[ ] API (REST/SOAP)
[ ] Banco de Dados (SQL)
[ ] Arquivo (FTP/Pasta/Sharepoint)
Mapeamento Visual (No-Code): O implementador fornece o endpoint (API) ou a query (SQL) e mapeia visualmente os campos (ex: order_id -> PO_ID).
Ativação: O conector é salvo (ex: "Conector ERP - TOTVS") e fica disponível para ser usado nos Nodes do Motor de Workflows.
Impacto: Resolve o problema de múltiplos MCPs. O cliente pode ter vários conectores (ERP, WMS, DB de Contratos) gerenciados centralmente.
2.3.3 Pilar 3: O DockBot (Assistente de IA Contextual)
A IA que explica o sistema e reduz a curva de aprendizado da plataforma low-code.
Como Funciona:
Base de Conhecimento: A IA é treinada com este próprio documento de conceito, manuais de usuário e FAQs.
Chat In-App: Um ícone de "Chat" ficará disponível em todas as telas.
IA Contextual: Responde dúvidas de uso ("Como faço check-in?") e de configuração ("Como eu pulo o Gate Virtual no workflow?").
Integração com Mensageria: O mesmo DockBot responderá no Telegram/WhatsApp quando o usuário digitar /ajuda.

## 3. FLUXO OPERACIONAL (TEMPLATE PADRÃO v12)

Abaixo, descrevemos o Template de Workflow Padrão (baseado na v12), que é 100% customizável no Motor de Workflows (Pilar 1).
FASE 1: Classificação e Gate Virtual
MCP consulta Fontes (Node On: Documento Recebido):
Consulta SEFAZ (NF-e) periodicamente.
Consulta Prefeituras (NFS-e) periodicamente (se Conector NFS-e estiver ativo, ver 5.5.3).
Download automático dos XMLs autorizados.
IA faz a Classificação de Fluxo (Node Classificar Documento):
O sistema analisa o documento (NF-e vs NFS-e) e o CFOP.
Resultado A: Fluxo Físico (Mercadoria)
Documento é uma NF-e com CFOP de circulação de mercadoria.
Segue para o "Gate Virtual de Doca" (Passo 4).
Resultado B: Fluxo Administrativo (Não-Físico)
Documento é uma NFS-e (Serviço) ou NF-e de Serviço/Simbólica (ex: CFOP 5.3xx, Bonificação, Industrialização).
Segue para o "Gate Virtual Administrativo" (Passo 5).
Gate Virtual de Doca (Fluxo Físico):
Node Fazer Match PO (Produto) (usando um Conector do Pilar 2) é executado.
Match perfeito → Status: " ✅ Liberado para embarque" → Node Criar Card (Kanban Operacional) na Visão Futuro. (SEGUE PARA FASE 2).
Divergência detectada → Status: " ⚠️ Resolver antes do embarque" → Node Criar Card (Kanban Setorial) (Compras/Fiscal).
Sem pedido → Status: " ❌ Bloqueado - Criar pedido" → Node Criar Card (Kanban Setorial) (Compras).
Resultado: 80% dos problemas físicos resolvidos antes do caminhão sair.
Gate Virtual Administrativo (Fluxo Não-Físico):
Node Fazer Match PO (Serviço) (usando outro Conector) é executado.
Match perfeito → Status: " ✅ Aprovado" → Node Criar Card (Kanban Administrativo) (Financeiro).
Divergência detectada → Status: " ⚠️ Divergência de Contrato" → Node Criar Card (Kanban Administrativo) (Gerente/Compras).
Sem pedido → Status: " ❌ Bloqueado - Criar PO Serviço" → Node Criar Card (Kanban Administrativo) (Gerente/Compras).
Resultado: Documentos não-físicos entram no fluxo de aprovação digital sem tocar na operação logística.
FASE 2: Planejamento (Kanban Operacional - Visão Futura)

### Aplica-se apenas ao Fluxo Físico

Node Disparar IA Preditiva é executado para os cards "Liberados para embarque".
IA aloca o melhor slot e notifica o time de Compras/Operações.
Sinalização Visual: Cards de Cross-Docking (se habilitado) recebem um ícone especial (ex: 🔁) para planejamento prioritário.
Time de Compras utiliza visão futura para evitar overbooking de doca.
Equipe operacional se prepara e aloca recursos.
FASE 3: Check-in Obrigatório (Todos os Cenários)

### Aplica-se apenas ao Fluxo Físico

Motorista chega na portaria.
Node On: Check-in (Motorista) é disparado (via Bot).
A. Check-in Normal (via Mensageria):
Motorista abre Telegram/WhatsApp e envia número da NF-e (física).
Bot valida e confirma dados.
B. Check-in via Preposto (Fallback):
Definição: O "Preposto" é um papel fallback (ex: porteiro) que realiza o check-in manual no sistema.
Resultado: Garante 100% de cobertura operacional.
C. Check-in Múltiplas NF-es:
Sistema cria card mestre com sub-cards.
D. Entrega "Cega" (sem pedido prévio):
Bot não rejeita, cria card tipo "AGUARDANDO_PO".
Dispara ALERTA URGENTE para Canal COMPRAS.
IA aloca no melhor slot disponível.
Card criado no Kanban Operacional.
Motorista recebe confirmação com doca/horário/posição.
FASE 4: Gestão Visual (Kanbans e Dashboard)
Operador de Doca (Gestão) vê o Kanban Operacional e gerencia o fluxo físico.
Gestor (Compras/Fiscal/QC) vê os Kanbans Setoriais e gerencia pendências físicas.
Gerente/Financeiro (Gestão) vê os Kanbans Administrativos e gerencia pendências de serviços/NFS-e.
Operador de Pátio/Conferente (Informação) vê o Dashboard Operacional (Visão Aeroporto) (apenas fluxo físico) e acompanha o status de chegadas.
Sistema detecta mudanças (ações de Drag & Drop disparam Nodes de workflow) e notifica os envolvidos.
FASE 5: Monitoramento e Alertas
Monitor detecta alterações no Kanban (Físico):
Card com check-in removido → CRÍTICO (15min para resolver)

### Doca/horário alterado → Notifica motorista


### Slot emergência ativado → Notifica supervisores

FASE 6: Execução, Conferência e Baixa (Passagem de Bastão)

### Aplica-se apenas ao Fluxo Físico

Sistema avisa motorista quando chegar sua vez (Status no Dashboard: "Chamado")
Descarga inicia → Card muda status (azul) (Status no Dashboard: "Descarregando")
CONFERÊNCIA FÍSICA E QUALIDADE:
A. Conferência de Quantidade: Valida quantidade física vs NF-e. (Opcional: Node Capturar (Balança IoT)).
B. Controle de Qualidade (QC): Avaria, Temperatura, Validade. (Opcional: Node Capturar (Termômetro IoT)).
C. Cenário Normal (tudo OK):
Conferente dá baixa no Canal DOCA.
IA identifica o tipo de fluxo:
Fluxo Padrão (Armazenagem): Node Executar Baixa (ERP) é disparado. Se Conector WMS (5.5.5) estiver habilitado, Node Sinalizar WMS (Putaway) é disparado.
Fluxo Cross-Docking (Sinalizado 🔁): Node Executar Baixa (ERP) é disparado. Se Conector WMS (5.5.5) estiver habilitado, Node Sinalizar WMS (Cross-Docking) é disparado.
Card concluído → Histórico (Status no Dashboard: "Liberado")
D. Cenário Divergência (quantidade ou qualidade):
BLOQUEIO TOTAL: Sistema impede baixa.
Alerta imediato → Aciona o fluxo de decisão (Nível 1 ou 2) no canal (Compras ou Qualidade).
FASE 7: Gestão de Devolução (Integral, Parcial ou Reagendada)

### Aplica-se apenas ao Fluxo Físico

Trigger: Decisão de devolução (Compras ou Qualidade)
FLUXO A - Devolução Integral:
Canal FISCAL gera NF-e devolução total.
Motorista libera saída com toda carga.
FLUXO B - Devolução Parcial (ex: 90 OK, 10 avariadas):
Entrada (parte boa): Sistema libera 90un para ERP.
Devolução (parte ruim): 10un movidas para Quarentena. Canal FISCAL gera NF-e de devolução parcial.
FLUXO C - Devolução Reagendada:
Cenário: Decisão de devolução tomada, mas o motorista não pode levar a carga imediatamente.
Fluxo: O card é marcado como "AGUARDANDO RETORNO" e movido para a "Visão Futuro" do Kanban.
Liberação física (Fluxo A e B):
Nota de Compliance Fiscal (Atrito Gerenciado): A espera do motorista pela emissão da NF-e de Devolução não é uma falha, mas um requisito legal obrigatório.

## 4. SISTEMA KANBAN E DASHBOARDS (Componentes de UI)

4.1 Kanban Operacional (Visão Doca)
Propósito: Gestão ativa e interativa (drag & drop) do fluxo físico.
Colunas: Representam docas físicas
Cards: Entregas com check-in confirmado (inclui ícones 🔁 para Cross-Dock).
Usuário: Operador de Doca, Supervisor.
4.2 Kanban de Planejamento (Visão Futuro)
Propósito: Planeamento de capacidade e alocação de recursos do fluxo físico.
Cards fantasma: Previsões da IA (semi-transparentes, com ícones 🔁).
Cards de Saída: Devoluções reagendadas (Fluxo C)
Usuário: Time de Compras, Supervisor Operacional.
4.3 Kanbans Setoriais (Visão de Gestão Holística)
Propósito: Painéis de gestão de exceções para os times de back-office (Compras, Fiscal, QC) visualizarem e gerenciarem apenas as pendências de suas áreas (ex: divergências de PO físico, controle de qualidade).
Exemplo (Kanban Fiscal - Físico):
Colunas: Pendente Análise NCM, Liberado, Quarentena Fiscal.
Sincronia: Ações na Mensageria (Nível 1) movem o card automaticamente no Kanban (e vice-versa).
Usuário: Gestor (Compras, Fiscal, QC).
4.4 Kanbans Administrativos (Visão de Fluxo Digital)
Propósito: Painéis de gestão de documentos não-físicos (NFS-e, NF-e de serviço, etc.) que não passam pela doca.
Fluxo: Um card (NFS-e) é o objeto mestre. Ele é roteado da FASE 1 direto para este Kanban para aprovação e encaminhamento ao financeiro.
Exemplo (Kanban Administrativoistrativo/Serviços):
Colunas: [Aguardando Aprovação Gerente], [Aguardando PO (Serviço)], [Enviado para Pagamento], [Concluído].
Usuário: Gestor (Financeiro, Admin, Compras de Serviço).
4.5 Dashboard Operacional (Visão Aeroporto)
Propósito: Visualização informativa (read-only) do status de todas as chegadas físicas, projetada para alta visibilidade (ex: TVs no pátio ou doca).
Colunas: FORNECEDOR, PLACA, NF-e, PREVISÃO, DOCA (alocada), STATUS (ex: No Pátio, Atrasado, Chamado, Descarregando, Liberado).
Usuário: Operador de Pátio, Conferente, Motoristas (em espera).
4.6 Slots de Emergência
Visualmente diferenciados (vermelho) no Kanban Operacional.
Não alocáveis automaticamente pela IA.
Ativação manual por supervisores.
4.7 Gestão de Quarentena
Área física segregada para produtos em análise (Fluxo Físico).
Tipos de quarentena:
QC: Produtos reprovados por qualidade
FISCAL: Divergência tributária pendente
QUANTIDADE: Aguardando decisão de ajuste
DEVOLUÇÃO: Preparando retorno ao fornecedor
Status híbrido no Kanban: "90un OK | 10un Quarentena"

## 5. PAINEL ADMINISTRATIVO (NÚCLEO DE GOVERNANÇA)

Esta seção descreve as interfaces que o "Implementador" e o "Admin Avançado" usam para configurar a plataforma.
5.1 Política de Proteção, Alçadas e Grupos
Define as regras de negócio que os Nodes de Lógica do Motor de Workflows irão consumir.

### Grupos Flexíveis

Admin cria grupos customizados (ex: Compras Jr, Compras Sr, Fiscal, Qualidade, Controller, Admin/Financeiro)

### Política de Proteção ERP (por Grupo)

Modo de operação (Proteção Total / Configurável / Flexível)
Tolerâncias por campo (atribuídas por grupo):
Quantidade: % aceitável e ação
Valor unitário: % e ação
Fluxo de Aprovação em Cascata:
Regra: Divergência de 2% no valor.
Ação: Node Verificar Divergência roteia para o grupo "Compras Jr" (Nível 1).
Escalonamento: Se >2% mas <5%, roteia para "Compras Sr" (Nível 2).

### Permissões Disponíveis (por Grupo)

visualizar_kanban_operacional, visualizar_kanban_fiscal, visualizar_kanban_admin
mover_cards, ativar_emergencia
configurar_sistema, dar_baixa
aprovar_divergencia_n1_mensageria
aprovar_divergencia_n2_kanban
aprovar_provisao_contabil (Permissão Nível Controller)
aprovar_nfs_e (Permissão Nível Admin/Financeiro)
acessar_motor_workflows (Permissão de Implementador)
gerenciar_conectores_mcp (Permissão de Implementador)
5.2 Motor de Workflows (Interface de Gestão)
Esta seção substitui a antiga "Matriz de Roteamento" estática. Aqui, o admin/implementador gerencia os workflows visuais (Pilar 1).
Interface: Tela visual "arrastar e soltar".
Templates: "Template Padrão (DockManager v12)" vem pré-instalado.
5.2.1 Template Padrão: Matriz de Roteamento (Visualização do Workflow)
A tabela abaixo (da v12) não é "hardcoded", mas sim uma representação visual de como o "Template Padrão" está configurado no Motor de Workflows.
5.2.2 Roteamento por Tipo de Documento/Operação (Lógica do Workflow Padrão)
Documento = NFS-e (Serviço) → Ignora match PO → Roteia para "Kanban ADMINISTRATIVO".
NF-e (CFOP 5.910 - Bonificação) → Ignora match PO → Roteia para "Kanban FISCAL" para aprovação.
NF-e (CFOP 5.901 - Industrialização) → Ignora match PO → Roteia para "Kanban PRODUÇÃO" (Setorial).
NF-e (PO Tipo 'CROSS-DOCK') → Aplica flag 🔁 (Se habilitado na Seção 5.5.1) → Roteia para Baixa (Fluxo Físico).
5.2.3 Biblioteca de Nodes (Exemplos)
5.3 SLA e Escalonamento Compulsório
No "Template Padrão", este fluxo é implementado no Motor de Workflows:
Node: Enviar Alerta (Nível 2) -> Node: Esperar (60min) (Timeout do SLA de 5.2.1)
(Se não houver resposta) -> Node: Enviar Alerta (Supervisor) (T+30min)
(Se não houver resposta) -> Node: Mover Card (Quarentena Fiscal) (T+60min - Decisão Compulsória)
5.4 Governança de Logs
Política de Retenção de Logs:
O admin define o tempo de retenção dos logs de auditoria (Padrão: 5 anos, para compliance fiscal).
O Log de Auditoria agora registra as execuções de workflow e as alterações no Motor de Workflows.
5.5 MCP Integration Studio (Interface de Gestão)
Esta seção substitui os antigos formulários estáticos. Aqui, o implementador gerencia os conectores (Pilar 2).
Interface: Um "Discovery Guiado" No-Code (Pilar 2.3.2).
Fontes Suportadas: API (REST/SOAP), Banco de Dados (SQL), Arquivos (FTP/Sharepoint).
Mapeador Visual: Interface de "arrastar e soltar" para mapear campos.
5.5.1 Tabela de Conectores (Toggles - Interface "Admin Simplificado")
Esta tabela (da v12) é a interface do "Admin Simplificado" (Seção 5.6). Ela não cria conectores, mas habilita/desabilita os workflows que os utilizam.
5.5.2 Conector SEFAZ (NF-e) (por Tenant)
Certificado Digital A1: Upload criptografado (em cofre digital)
Agente MCP (On-Premise): Instruções para instalação (necessário para Certificado A3)
Alertas de Renovação: (60/30/10 dias)
5.5.3 Conector NFS-e (Prefeituras) (por Tenant)
Provedor (ex: PlugNotas, NFe.io): [Campo de Provedor]
API Key: [Campo de Chave]
Cidades Monitoradas: [Lista de Cidades]
Nota: A habilitação deste conector é feita na Tabela 5.5.1.
5.5.4 Conector ERP (por Tenant)
Tipo de ERP: (SAP, TOTVS, Protheus, Outro)
Endpoint (API/WebService): [Campo de URL]
API Key (Token): [Campo de Chave]
Regras de Negócio (vinculadas ao ERP):
Gestão de Provisão Contábil (Conta Transitória):
( ) Automático: (Ver Tabela 5.5.1) O DockManager cria lançamentos provisórios no ERP.
( ) Requer Aprovação Manual: (Default) O DockManager sugere o lançamento, mas requer aprovação do grupo Controller.
5.5.5 Conector WMS (por Tenant)
Tipo de WMS: (Senior, TOTVS, Outro, Mesmo do ERP)
Endpoint (API/WebService): [Campo de URL]
API Key (Token): [Campo de Chave]
Nota: A habilitação deste conector é feita na Tabela 5.5.1.
5.5.6 Conectores IoT/Automação (por Tenant)
Endpoint (API) Balança: [Campo de URL da API da Balança]
Endpoint (API) Termômetro: [Campo de URL da API do Termômetro]
Nota: A habilitação destes conectores é feita na Tabela 5.5.1.
5.5.7 Conectores de Mensageria (por Tenant)
Canal Padrão: Telegram
Token do Bot: [Campo de Chave]
Canal Opcional: WhatsApp (via Broker)
Provedor (Broker): (Twilio, Gupshup, Outro)
Endpoint da API do Broker: [Campo de URL]
Token de Autenticação: [Campo de Chave]
5.5.8 Conectores de IA (Roadmap FASE 6)
Provedor de IA (Opcional): (Google AI, OpenAI, Outro)
Endpoint API: [Campo de URL]
API Key: [Campo de Chave]
5.6 Níveis de Interface (UX)
Propósito: Simplificar a adoção e reduzir a complexidade para diferentes perfis de usuário no Painel Administrativo.
Admin Simplificado: Acesso aos Kanbans e à Tabela de Toggles (5.5.1).
Admin Avançado/Implementador: Acesso total, incluindo Motor de Workflows (5.2) e MCP Integration Studio (5.5).

## 6. TABELA DE TEMPO MÉDIO (APRENDIZADO IA)

É o modelo de dados usado pelo Node Disparar IA Preditiva.

## 7. EXPERIÊNCIA DO USUÁRIO

7.1 Motorista (via Mensageria)
Faz check-in (fluxo físico), recebe posição na fila e alertas.
7.2 Analista (Compras, Fiscal, QC) (via Mensageria)
Recebe alertas acionáveis para Decisões Nível 1 (físicas).
Recebe deep links para Decisões Nível 2 no Kanban Setorial.
7.3 Gestor (Supervisor) (via Kanban Setorial e BI)
Vê a "visão holística" das pendências da sua equipe (Kanbans Físicos).
Mede SLAs, identifica gargalos e toma Decisões Nível 2.
Acessa o Módulo de BI para KPIs estratégicos (Seção 10).
7.4 Operador (via Kanban Operacional e Dashboard)
Gestão: Vê o Kanban Operacional para gerenciar o fluxo físico.
Informação: Vê o Dashboard Operacional (Visão Aeroporto) para status rápido.
7.5 Usuário Administrativo/Financeiro (via Mensageria e Kanban Administrativo)
Recebe alertas de NFS-e pendentes de aprovação (Nível 1).
Usa deep links para aprovar divergências de contrato/valor no Kanban Administrativoistrativo (Nível 2).
7.6 (NOVO) Implementador (Painel Admin)
Usa o MCP Integration Studio (Pilar 2) para criar Conectores (API, DB).
Usa o Motor de Workflows (Pilar 1) para desenhar/ajustar os fluxos de negócio.
7.7 (NOVO) Todos os Usuários (DockBot)
Interagem com o DockBot (Pilar 3) via chat In-App ou Mensageria para tirar dúvidas contextuais sobre como usar ou configurar o sistema.

## 8. ARQUITETURA DE DECISÕES (FLUXO HÍBRIDO)

O padrão Nível 1 / Nível 2 da v12 é mantido como um design pattern implementado no "Template Padrão" do Motor de Workflows.

### Decisões em Camadas (Gestão de Alçadas)

Nível 1: Ação Rápida (Interface: Telegram/WhatsApp)
O que é: Decisões de baixo risco, binárias ou dentro da tolerância (para fluxos físicos ou admin).
Fluxo: O bot de mensageria envia botões inline.
Exemplo (Físico):
⚠️ Divergência Detectada (NF: 100un | PO: 99un) Tolerância de 1% OK.
$$Ajustar PO para 100$$$$Reprovar Lote$$
Exemplo (Admin):
🔔 Nova NFS-e (Serviço TI) - R$ 1.500,00 PO de Serviço encontrado.
$$Aprovar Pagamento$$$$Enviar para Análise$$
Nível 2: Ação Complexa (Interface: Kanban Setorial/Admin)
O que é: Decisões com impacto fiscal (NCM), financeiro (Valor) ou fora da tolerância.
Fluxo: O bot de mensageria NÃO envia botões de ação. Ele envia um deep link tagueado.
Exemplo (Admin):
⚠️ Divergência de NFS-e (Serviço TI) NF: R$ 1.800,00 | PO: R$ 1.500,00 Ação Nível 2 Requerida.
$$Ver Detalhes no Kanban Administrativo 🔗$$
Ação do Link: O usuário clica e é levado ao Kanban (Setorial ou Admin), diretamente no card da nota, com todos os dados para análise.

### Registro e Auditoria (Integridade de Log)

Log completo: Quem decidiu, quando, o quê (para ambos os fluxos).
Rastreabilidade Mensageria: Log armazena o message_id da decisão (Nível 1) ou do alerta (Nível 2).
Feedback Loop da IA: Log registra sugestao_ia, acao_humana e origem_correcao.
Registro de Causa Raiz: Após a decisão, o bot oferece opções de log (ex:
$$Erro Fornecedor$$
,
$$Erro Cadastro$$
) para alimentar o BI.
Auditoria de Governança: Todas as alterações no Painel Administrativo (Seção 5), incluindo alterações no Motor de Workflows, são registradas no log.
Assinatura de Log: Cada entrada de log recebe um Hash SHA256 com timestamp, garantindo imutabilidade para auditoria.

## 9. TRATAMENTO DE EXCEÇÕES (Serviços da Plataforma)

9.1 Auditoria Retroativa (ERP e SEFAZ)

## 1. Reconciliação com ERP

Gatilho: Job noturno do MCP Server.
Ação: Reconsulta o ERP buscando por NF-es/NFS-e dos últimos 7 dias que foram alteradas manualmente no ERP.
Resultado: Se detecta uma nota com status divergente, gera um alerta no Kanban (Fiscal ou Admin) para reconciliação. 2. Reconciliação com SEFAZ (Gate Virtual)
Gatilho: Job noturno do MCP Server.
Ação: Reconsulta o status na SEFAZ de todas as NF-es que estão na "Visão Futuro" (cards fantasma).
Resultado: Se uma NF-e for Cancelada ou Denegada na SEFAZ, o "card fantasma" é automaticamente removido e o "Canal COMPRAS" é notificado.
9.2 Divergências (Pré-Entrega e Físicas)
Detectadas na FASE 1 ou FASE 6, acionam o fluxo de decisão (Seção 8).
9.3 Entregas "Cegas" (Sem PO)
Card "AGUARDANDO_PO" é criado e o Canal COMPRAS é acionado com urgência.
9.4 Fallbacks (Plano de Contingência)
SEFAZ/Prefeitura indisponível: Cache local de notas processadas.
Certificado expirado: Alerta antecipado 60/30/10 dias.
ERP/WMS Indisponível: Garantido pela Fila de Transações Persistente (Seção 13).
Falha de Mensageria (Fluxo Formal):
Padrão: Bot Telegram/WhatsApp.
Falha 1: Sistema aciona fallback para SMS.
Falha 2: Alertas escalam para o Painel de Supervisão (requer ação manual).
WebSocket falha: Polling garante integridade.

## 10. MÉTRICAS E KPIs (Módulo de BI)


### Visualização e Acesso aos KPIs

Os KPIs são disponibilizados em camadas distintas, com base no perfil de acesso:
Camada Tática (Tempo Real): Visível diretamente nos Kanbans Setoriais e Kanbans Administrativos. Gestores veem KPIs táticos (ex: COUNT de notas pendentes) em tempo real.
Camada Estratégica (BI): Disponibilizada através do Módulo de Análise de Causa Raiz (BI).

### KPIs Operacionais (Fluxo Físico)

Tempo médio de espera (Check-in → Início Descarga)

### Tempo médio de permanência (Check-in → Saída)

Taxa de ocupação das docas (meta: >80%)
Taxa de utilização de conferentes (meta: >85%)
% Resolvido pré-embarque (pelo Gate Virtual) (meta: >80%)
Tempo médio em quarentena (meta: <24h)

### Tempo médio de Cross-Docking (inbound→outbound)

% de Check-in via Preposto (Fallback)

### KPIs Administrativos (Fluxo Não-Físico)

Tempo médio de aprovação de NFS-e (Captura → Aprovação Final)
% de NFS-e com divergência de PO/Contrato
Volume de NFS-e processado vs. NF-e

### KPIs de Qualidade e Compliance (Geral)


### Taxa de reprovação QC (% de lotes físicos)

Principais motivos de reprovação (Avaria, Temperatura, Validade)
Taxa de devolução (Parcial vs. Integral)
% de divergências Físico vs. NF-e (detectadas na FASE 6)
% de divergências NF-e vs. PO (detectadas na FASE 1)
Acuracidade do Inventário (baseada em divergências evitadas)

### KPIs Financeiros e de Governança (Geral)


### Multas fiscais evitadas (compliance)

Valor em "Conta Transitória" (notas em validação fiscal/financeira)

### Tempo médio de liberação (Kanban Fiscal e Admin)

Tempo médio de resolução por equipe (Compras vs. Fiscal vs. Admin)

### Análise de Causa Raiz (BI e Analytics)

Dashboard de reincidência de divergências (por fornecedor, produto, NCM, ou Serviço).
Ranking de principais motivos de reprovação (QC).
Relatório de performance da IA (sugestões vs. correções humanas).
Relatório de Reconciliação (Auditoria): Logs e KPIs da Auditoria Retroativa.

## 11. ROADMAP DE IMPLEMENTAÇÃO (Revisado para Plataforma)


### FASE 1 - Plataforma Core (Mês 1-3)

Construção dos 3 Pilares (v1.0):
Pilar 1: Motor de Workflows (com Nodes essenciais).
Pilar 2: MCP Integration Studio (com Conectores de API REST e DB SQL).
Pilar 3: DockBot (com base de conhecimento inicial).
Construção dos Componentes de UI: Kanbans, Dashboard.

### FASE 2 - Template Padrão (Mês 4-5)

Usar a FASE 1 para implementar o "Template de Workflow Padrão (v12)":
Fluxo Físico (NF-e) + Fluxo Administrativo (NFS-e).
Fluxo Híbrido (Nível 1 / Nível 2).
Serviços de Background (Fila Persistente, Auditoria Retroativa).
FASE 3 - Expansão da Biblioteca de Conectores (Mês 6-9)
Adicionar Conectores Nativos no MCP Studio (Pilar 2) para:
WMS (Senior, TOTVS, etc.)
Prefeituras (NFS-e via PlugNotas, NFe.io)

### Sistemas de Arquivos (FTP, Sharepoint)

FASE 4 - Expansão da Biblioteca de Nodes (Mês 10-12)
Adicionar Nodes Avançados no Motor de Workflows (Pilar 1) para:
Conectores IoT (Balanças, Termômetros Portáteis).
Logística Reversa (Devoluções de cliente).
Integração YMS (Yard Management).

### FASE 5 - Ecosistema Conectado (Ano 2)

Construção de novas interfaces que consomem os workflows:
Portal do Fornecedor.
App Mobile Motorista.
Evolução do DockBot (Pilar 3) para IA generativa e sugestões proativas.
(Roadmap v12 (Fases 5 e 6) movido para o backlog de expansão da plataforma)

## 12. PRINCÍPIO FUNDAMENTAL: PROTEÇÃO CONFIGURÁVEL DO ERP

(Esta filosofia de negócio é implementada via Alçadas (5.1) e lógica no Motor de Workflows).
FLEXIBILIDADE COM PROPÓSITO O DockManager permite que cada empresa configure seu nível ideal de proteção, desde tolerância zero até flexibilidade controlada.
Filosofia Central:
Proteção Total (Recomendada): Zero tolerância para máxima integridade
Proteção Configurável: Tolerâncias definidas por campo e alçada de grupo
Modo Flexível: Aceita divergências com rastreabilidade
Modos de Operação:
Modo 1: Proteção Total (Best Practice)
✅ 100% correto → Entrada liberada
❌ Qualquer divergência → Bloqueado até resolver
Modo 2: Proteção Configurável
Tolerâncias por campo (quantidade, valor, etc.)
Ações customizadas (auto-ajuste da IA ou validação humana)

### Aprovação em cascata por alçada

Modo 3: Flexibilidade Controlada

### Aceita divergências com aprovação


### Registro completo para audit trail

Resultado Garantido (em qualquer modo):
✓ Rastreabilidade total - Toda decisão registrada
✓ Visibilidade completa - Divergências sempre sinalizadas
✓ Compliance mantido - Documentação para auditoria
✓ Melhoria contínua - IA aprende padrões

## 13. CONSIDERAÇÕES TÉCNICAS


### Stack Tecnológica

Frontend Kanban: React/Vue.js + Tailwind
Backend: Node.js + Express
Database: PostgreSQL
Real-time: Socket.io
Cache: Redis
Mensageria: Telegram API (Padrão) / APIs de Brokers WhatsApp (Opcional)
MCP Server: Node.js
Hospedagem: Cloud própria (sem vendor lock-in)
Fila de Transações Persistente (Resiliência ERP/WMS)
Para garantir 100% de consistência, o MCP Server atua como uma fila persistente.
Todas as transações de escrita (ex: baixa no ERP, comando ao WMS, aprovação de NFS-e) são primeiro registradas em um log transacional no banco do DockManager.
Um worker separado é responsible por tentar enviar ao sistema de destino.
Se o sistema falhar (offline/timeout), o status fica "Pendente" e o worker tentará novamente (com exponential backoff), garantindo a entrega do evento sem perda de dados.

### Segurança


### Autenticação JWT


### Criptografia de dados sensíveis

Audit trail imutável: Logs com hash SHA256 + Timestamp (Retenção de 5 anos)

### Backup automático


### Compliance LGPD

Isolamento de Tenant: Tokens de API, Webhooks e Certificados segregados por cliente.

### Autenticação Simplificada

Motoristas (Fluxo Físico): Apenas número da NF-e (simplicidade > adoção)
Justificativa: Facilidade de adoção é crítica
Foco: Remover barreiras de entrada para motoristas

### Gestão Fiscal e Contábil

Conta Transitória: Notas bloqueadas registradas como "Em Validação"
Proteção do CMV: Nada afeta custos até decisão final
Provisão automática: Controlada pelo Admin (ver Seção 5.5.4).
Audit trail fiscal: Todo movimento rastreado para compliance

### Escalabilidade


### Arquitetura multi-tenant


### Suporta múltiplos clientes


### Configuração por cliente

"Cloud própria": Sem vendor lock-in (deploy em qualquer IaaS ou on-premise)

## 14. DIFERENCIAIS COMPETITIVOS (Merge v12 + v13)

🔧 MOTOR DE WORKFLOWS LOW-CODE
Substitui matrizes de roteamento rígidas. Flexibilidade total para desenhar o processo de qualquer empresa.
🔌 MCP INTEGRATION STUDIO (NO-CODE)
Substitui formulários de API estáticos. Permite ao implementador conectar-se a qualquer API, DB ou Arquivo com mapeamento visual.
🤖 DOCKBOT (ASSISTENTE DE IA CONTEXTUAL)
Reduz a curva de aprendizado da plataforma low-code, respondendo dúvidas de uso e configuração em linguagem natural.
🎯 TEMPLATE PADRÃO "BEST-PRACTICE" (v12)
O cliente não começa do zero. Ele recebe uma solução robusta (Fluxo Duplo, Nível 1/2) pronta para usar ou adaptar.
🏭 GESTÃO DE KANBANS UNIFICADA (FLUXO DUPLO)
Classificação de Fluxo (Físico vs. Administrativo) na entrada.
Visão holística (Operacional, Setorial, Admin) que separa o fluxo físico do digital.
📦 GESTÃO LOGÍSTICA COMPLETA (v12)
(Devolução Parcial/Reagendada, Quarentena, Cross-Docking) disponíveis como Nodes pré-construídos.

### Resiliência e Governança

(Fila Persistente, Auditoria Retroativa, Logs com Hash SHA256, Retenção de 5 anos).
🔐 ISOLAMENTO MULTI-TENANT ROBUSTO
Certificados (A1/A3) e Tokens de API segregados.

## 15. CONCLUSÃO (Revisada para Plataforma)

O DockManager v13 evolui de um produto para uma plataforma de automação logística Low-Code. Ele resolve o problema central de rigidez ao unificar uma arquitetura de implementação flexível (os Três Pilares) com um template de negócio robusto (o fluxo detalhado da v12).
A plataforma blinda o ERP combinando a agilidade da Mensageria (Nível 1) com a visão holística dos Kanbans (Nível 2), agora segmentados por fluxo (Operacional, Setorial e Administrativo), tudo orquestrado por um Motor de Workflows visual que o próprio cliente pode adaptar.
A solução oferece:
Plataforma Flexível: O cliente desenha seu processo.
Integração No-Code: O implementador conecta qualquer sistema (API, DB, Arquivo).
Suporte Inteligente: O DockBot (IA) ensina o usuário a usar e configurar.
Template "Best-Practice" (v12): Um fluxo de classe mundial (NF-e, NFS-e, Gate Virtual, Kanbans, etc.) pronto para uso no Dia 1.
Resiliência e Governança Total: Fila Persistente, Auditoria Imutável e Proteção Configurável do ERP.
O DockManager v13 (Integrado) é o conceito final que une uma visão de negócio de ponta com uma arquitetura de implementação moderna, garantindo adaptabilidade e longevidade à solução.
Próximos passos:
Detalhamento técnico (Blueprint) da FASE 1 (Construção dos 3 Pilares).
Início do desenvolvimento da plataforma.
Implementação do "Template Padrão v12" sobre a plataforma.
Documento de Conceito v13.0 (Integrado) - Novembro 2025 Versão Final: Plataforma Low-Code (v13) + Fluxo de Negócio Detalhado (v12).
Seção de complemento a versão 13:
Integração de  "Motor Fiscal" ou uma "API de Saneamento Fiscal".
É uma observação extremamente importante, porque a complexidade tributária no Brasil (especialmente a Substituição Tributária, ou "ST") é tão grande que nenhum sistema (nem mesmo um ERP) deve tentar calculá-la "na mão".
O cálculo da ST, do MVA (Margem de Valor Agregado) e até mesmo do CEST (Código Especificador da Substituição Tributária) correto depende de:
O NCM do produto.
O Estado de Origem.
O Estado de Destino.
Os "Protocolos" e "Convênios" (acordos) de ST entre esses estados.
O regime tributário da sua empresa (Simples, Lucro Presumido, Real).
Exatamente como você disse, existem serviços de API especializados nisso (como IBPT, TaxMasters, Saneamento Fiscal, etc.) onde você envia o NCM e a rota, e eles devolvem a tributação correta.

### A Nossa Proposta (Como a v13 resolve isso)

Você acabou de descrever o caso de uso perfeito para a nossa arquitetura de plataforma v13, especificamente a combinação dos Pilares 1 e 2.
Nós não precisamos construir esse motor fiscal. Nós só precisamos "plugar" o motor fiscal que o cliente já usa.
Veja como isso funcionaria no DOCK_MANAGER_13_Plataforma_LowCode.md:

## 1. No Pilar 2: O MCP Integration Studio (O "Como")

O implementador (ou nosso time de implantação) usaria o "Discovery Guiado" para criar um novo "Conector":
Nome do Conector: Conector - Motor Fiscal (IBPT)
Tipo: API (REST)
Ação (Endpoint): api.ibpt.com.br/v1/tax
Autenticação: [API Key do Cliente]
Mapeamento Visual (No-Code): O implementador mapearia os campos.
Input (Saída do DockManager): Enviar NCM_da_NF e Estado_Origem.
Output (Entrada no DockManager): Receber CEST_Correto e ST_Calculada.
Uma vez salvo, este conector fica disponível para uso no workflow.

## 2. No Pilar 1: O Motor de Workflows (O "O Quê")

Agora, o implementador pode usar esse novo "poder". Ele editaria o "Template Padrão v12" (o fluxo da FASE 1 - Gate Virtual):
On: Documento Recebido (SEFAZ) (Gatilho)
...
Node: Fazer Match PO (Produto) (Node de Lógica)
(NOVO NODE ADICIONADO) Node: Validar Tributação (Motor Fiscal)
Este node chama o Conector - Motor Fiscal (IBPT) que criamos no Pilar 2.
Ele compara o CEST_da_NF com o CEST_Correto retornado pela API.
Node: Verificar Divergência (Lógica)
Este node agora tem uma nova regra: "A tributação (CEST/ST) está correta?"
Se Sim: Fluxo normal (Kanban Operacional).
Se Não: O workflow dispara o Node: Criar Card (Kanban Fiscal) e anexa a mensagem: "DIVERGÊNCIA TRIBUTÁRIA: O CEST correto é [CEST_Correto]."

### Proposta de Ajuste (Se você aprovar)

O documento v13 já permite isso conceitualmente. No entanto, para tornar isso explícito (como fizemos com o WMS e IoT), eu proponho:
Não alterar o documento agora.
Mas, se você aprovar o conceito, na próxima vez que editarmos o v13, podemos adicionar:
Um Node de exemplo na Seção 5.2.3 (Biblioteca de Nodes) chamado: Node: Validar Tributação (Motor Fiscal).
Um exemplo de Conector no Roadmap (FASE 3) ao lado de WMS e Prefeituras, chamado: Conectores Fiscais (IBPT, TaxMasters).
Isso deixa claro que nossa plataforma é 100% capaz de lidar com essa complexidade, delegando o cálculo a quem é especialista, exatamente como você intuiu.


| Tipo de Problema | Canal Primário (Node Enviar Alerta) | Kanban Destino (Node Criar Card) | SLA (Node Esperar) | Validação Humana? (Lógica do Node) |
|---|---|---|---|---|
| Divergência Qtd (<1%) | COMPRAS | Setorial COMPRAS | 45 min | Não (IA auto-ajusta) |
| Divergência Qtd (>1%) | COMPRAS | Setorial COMPRAS | 30 min | Sim |
| Divergência NCM/CFOP | FISCAL | Setorial FISCAL | 60 min | Sim |
| Avaria (QC) | QUALIDADE | Setorial QUALIDADE | 30 min | Sim |
| Temperatura (QC) | QUALIDADE | Setorial QUALIDADE | 15 min | Sim |
| NFS-e (Serviço) | ADMIN/FINANCEIRO | Kanban ADMIN | 120 min | Sim |
| NF-e (Bonificação) | FISCAL | Setorial FISCAL | 60 min | Sim |




| Tipo | Nome do Node | Descrição |
|---|---|---|
| Trigger | On: Documento Recebido (SEFAZ/Prefeitura) | Inicia o workflow na captura do MCP. |
| Trigger | On: Check-in (Motorista) | Inicia o workflow via Bot. |
| Lógica | Classificar Documento (CFOP) | Retorna "FÍSICO" ou "ADMINISTRATIVO". |
| Lógica | Fazer Match PO (Produto/Serviço) | Usa um Conector MCP (Pilar 2) para validar a nota. |
| Lógica | Verificar Divergência (Valor/Qtd) | Compara o XML com o "Match PO" e Alçadas (5.1). |
| Lógica | Esperar (Delay) | Pausa o workflow por X minutos (para SLA). |
| Ação | Criar Card (Kanban Operacional/Setorial/Admin) | Cria o card no Kanban especificado. |
| Ação | Enviar Alerta (Canal) | Posta uma mensagem (Nível 1 ou 2) em um canal. |
| Ação | Disparar IA Preditiva | Envia a NF-e para o módulo de IA (Seção 6). |
| Ação | Executar Baixa (ERP) | Usa um Conector MCP para dar a baixa final no ERP. |
| Ação | Sinalizar WMS (Putaway) | Usa um Conector MCP para chamar o WMS. |




| Conector | Módulo Habilitado? | Descrição | Default |
|---|---|---|---|
| Integração NFS-e | [ ] Habilitado | Habilita a consulta a Prefeituras para Notas Fiscais de Serviço. | Desligado |
| Provisão Contábil | [ ] Automático | Habilita a criação automática de lançamentos provisórios no ERP. | Manual |
| Integração WMS | [ ] Habilitado | Habilita a sinalização de Putaway e Cross-Docking para um WMS externo. | Desligado |
| Balança (IoT) | [ ] Habilitado | Permite a captura automática de peso na conferência (Fase 6). | Desligado |
| Termômetro (IoT) | [ ] Habilitado | Permite a captura automática de temperatura no QC (Fase 6). | Desligado |
| WhatsApp (Broker) | [ ] Habilitado | Habilita o WhatsApp como canal de mensageria (requer broker pago). | Desligado |
| IA Externa | [ ] Habilitado | Permite que a IA Preditiva consulte modelos externos (Roadmap). | Desligado |




| Fornecedor | Região | Categoria | Tempo Médio Descarga | Desvio Padrão | Pontualidade (Hist.) | Última Atualização |
|---|---|---|---|---|---|---|
| ABC Foods | Norte | Refrigerados | 1h 15min | ±10min | 85% (No prazo) | Atualizado hoje |
| XYZ Dist. | Sul | Secos (Paletizado) | 45 min | ±5min | 98% (No prazo) | Atualizado hoje |
| Importa Ltda | SP | Secos (Batido) | 2h 30min | ±30min | 60% (Atrasado) | Há 3 dias |



---

## Apêndice: Mapeamento De-Para (DOCX v13 → Markdown)

| Seção DOCX | Seção Markdown | Arquivo |
|------------|----------------|---------|
| 1. Resumo Executivo | ## 1. RESUMO EXECUTIVO | CONCEITO+TECH |
| 2. Arquitetura da Solução | ## 2. ARQUITETURA DA SOLUÇÃO | CONCEITO+TECH, TECH |
| 3. Fluxo Operacional v12 | ## 3. FLUXO OPERACIONAL | CONCEITO+TECH, TECH |
| 4. Sistema Kanban | ## 4. SISTEMA KANBAN | CONCEITO+TECH, TECH |
| 5. Integrações | ## 5. INTEGRAÇÕES | TECH |
| 6. IA Preditiva | ## 6. IA PREDITIVA | TECH |
| 7. Governança | ## 7. GOVERNANÇA | TECH |
| 8. Roadmap | ## 8. ROADMAP | CONCEITO+TECH |
| 9. Requisitos | ## 9. REQUISITOS | TECH |
| 10. Segurança | ## 10. SEGURANÇA | TECH |
| 11. Métricas | ## 11. MÉTRICAS | CONCEITO+TECH |
| 12. Casos de Uso | ## 12. CASOS DE USO | CONCEITO+TECH |
| 13. Próximos Passos | ## 13. PRÓXIMOS PASSOS | CONCEITO+TECH |
| Apêndice Fiscal | Arquivo separado | EXT_FISCAL |
