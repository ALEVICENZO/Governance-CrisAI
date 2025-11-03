---
title: "DockManager v13 – Plataforma Low-Code de Gestão Logística"
document_type: derived
subset_type: technical_only
derived_from: DOCK_MANAGER_v13_CONCEITO_TECH.md
context_scope: "Sections 2-11"
usage_restriction: ia_developer_only
version: v13_release_candidate
governance_protocol: "v1.4"
date: "Novembro/2025"
author: "Alexandre Vicenzo"
tags: ["Low-Code", "Workflow Engine", "No-Code Integration", "Logistics", "ERP", "Governança IA-Humana"]
---

# DOCK_MANAGER_v13_TECH

> Versão técnica e blueprint de engenharia com foco nos Pilares, Stack, Workflows e Integrações
> Otimizada para consumo por agentes IA de desenvolvimento


# DOCK_MANAGER_v13_TECH

> Versão técnica focada em arquitetura, implementação e componentes

## 2. ARQUITETURA DA SOLUÇÃO E PLATAFORMA

2.1 Componentes de Negócio (O "Quê")
Estes são os elementos de UI e lógica de negócio que o usuário final utiliza, e que são orquestrados pelo Motor de Workflows.
Sistema Kanban Visual (Operacional, Setorial e Admin): As interfaces visuais onde os "Cards" (NF-e ou NFS-e) são gerenciados.
Dashboard Operacional (Visão Aeroporto): O painel informativo (read-only) focado no fluxo físico.
Bot de Mensageria (Telegram/WhatsApp): A interface de Ação Rápida (Nível 1) e Check-in.
IA Preditiva: O módulo de inteligência que analisa tempos e sugere alocações (ver Seção 6).

> **Nota:** IA Preditiva aplica-se apenas ao fluxo físico, não ao administrativo/fiscal.

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


---

> **Fim do documento técnico**
> Seções 12-14 disponíveis apenas no documento MASTER (CONCEITO_TECH.md)
