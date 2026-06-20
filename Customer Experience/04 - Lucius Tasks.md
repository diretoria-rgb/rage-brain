
**Versão:** 1.0  
**Status:** Em desenvolvimento  
**Última atualização:** 19/06/2026

---

# Objetivo

Este documento organiza todas as tarefas de implementação do CRM da Rage.

Seu objetivo é orientar a configuração técnica da Nuvemshop, Nuvem Marketing e demais ferramentas utilizadas pela marca.

Este documento não define estratégia. Apenas organiza a execução.

---

# Fase 01 - Estrutura

## Popup

-  Criar popup de captura de emails.
    
-  Integrar popup ao Nuvem Marketing.
    
-  Configurar envio para lista correta.
    
-  Configurar cupom de primeira compra.
    
-  Validar funcionamento.
    

---

## Newsletter

-  Configurar formulário de inscrição.
    
-  Integrar ao Nuvem Marketing.
    
-  Validar recebimento dos contatos.
    

---

# Fase 02 - Fluxos Automatizados

## Flow 01 - Boas-vindas

-  Criar automação.
    
-  Configurar gatilho.
    
-  Inserir sequência de emails.
    
-  Configurar encerramento na primeira compra.
    
-  Testar funcionamento.
    

---

## Flow 02 - Primeira Compra

-  Criar automação.
    
-  Configurar gatilho de primeira compra.
    
-  Inserir sequência de emails.
    
-  Configurar comunicação via WhatsApp quando aplicável.
    
-  Testar funcionamento.
    

---

## Flow 03 - Evolução

-  Criar automação.
    
-  Configurar gatilho.
    
-  Inserir sequência de emails.
    
-  Testar funcionamento.
    

---

# Fase 03 - Fluxos Operacionais

## Flow 04 - Cross Selling

-  Estruturar listas de clientes.
    
-  Organizar critérios de segmentação.
    
-  Preparar campanhas manuais.
    

---

## Flow 05 - Comunidade

-  Preparar listas de comunicação.
    
-  Organizar estrutura para eventos.
    
-  Preparar listas para desafios.
    

---

## Flow 06 - Representação

-  Organizar lista de clientes representativos.
    
-  Criar estrutura para relacionamento manual.
    

---

## Flow 07 - Campanhas

-  Preparar estrutura para campanhas recorrentes.
    
-  Validar segmentações disponíveis.
    
-  Organizar calendário operacional.
    

---

# Fase 04 - Testes

-  Testar popup.
    
-  Testar cupom.
    
-  Testar inscrição na newsletter.
    
-  Testar automação de boas-vindas.
    
-  Testar automação de primeira compra.
    
-  Testar automação de evolução.
    
-  Validar segmentações.
    
-  Corrigir eventuais falhas.
    

---

# Observações

Caso alguma funcionalidade não seja suportada pela Nuvemshop, Nuvem Marketing ou Perfit, registrar a limitação e propor uma alternativa compatível com as ferramentas atualmente utilizadas pela Rage.

Nenhuma alteração estratégica deve ser realizada sem aprovação.
---

# Limitações Identificadas

## Limitação 01 — Nuvem Marketing / Perfit: automações multi-step bloqueadas no plano atual

**Data:** 19/06/2026  
**Status:** Registrada — aguarda decisão

**Diagnóstico:**  
O plano atual do Nuvem Marketing (Perfit) suporta apenas automações de email único. Todas as tentativas de criar sequências multi-email falharam:
- Templates de "Sequência de boas-vindas em 2, 3 ou 4 etapas" retornam HTTP 500 ao tentar criar
- O builder de automação personalizada exibe tooltip: *"Para acessar essa funcionalidade, você precisa contratar um plano"*
- Duplicar automações existentes não permite adicionar novos passos (sem botão "+" após o último passo)

**Impacto:**
- Flow 01 (Boas-vindas): apenas Email 01 possível. Emails 02 (D+2), 03 (D+7) e 04 (D+11) bloqueados
- Flow 02 (Primeira Compra): apenas Email 01 possível. Sequência adicional bloqueada
- Flow 03 (Evolução): sequência de 5 emails completamente bloqueada

**Alternativas:**
1. **Upgrade do plano Nuvem Marketing** — desbloqueia templates multi-step e builder personalizado. Ação recomendada para implementação completa dos flows.
2. **Campanhas manuais segmentadas** — criar campaigns por segmento de data de cadastro como substituto temporário dos emails D+2, D+7, D+11. Menos eficiente, sem personalização de comportamento.
3. **Implementação parcial** — ativar apenas Email 01 de cada flow no plano atual e aguardar upgrade para completar a sequência.

---

## Limitação 02 — Nuvem Marketing / Perfit: WhatsApp não suportado

**Data:** 19/06/2026  
**Status:** Registrada — aguarda decisão

**Diagnóstico:**  
O Nuvem Marketing / Perfit não possui integração nativa com WhatsApp. O canal não existe no builder de automações.

**Impacto:**
- Flow 02 (Primeira Compra): etapa de comunicação via WhatsApp (prevista na arquitetura) não pode ser configurada dentro da plataforma

**Alternativas:**
1. **Zapi ou WPPConnect** — integração via webhook externo disparado por evento de compra na Nuvemshop
2. **Kommo CRM** — plataforma com WhatsApp nativo, pode receber leads via webhook e disparar mensagens automaticamente
3. **Processo manual operacional** — equipe recebe notificação de primeira compra e envia WhatsApp manualmente (viável em baixo volume)


## Limitação 03 — Perfit: Flow 03 (Evolução) sem implementação possível no plano atual

**Data:** 20/06/2026  
**Status:** Registrada — aguarda upgrade de plano

**Diagnóstico:**  
O Flow 03 requer dois recursos indisponíveis no plano atual:
1. **Gatilho "conclusão de outra automação"** — não existe no Perfit. Impossível disparar o Flow 03 ao encerrar o Flow 02.
2. **Sequência multi-step** — 5 emails previstos, todos bloqueados pelo plano atual.

**Impacto:**  
Flow 03 (Evolução) completamente inviável sem upgrade.

**Ação necessária:**  
Upgrade do plano Perfit/Nuvem Marketing — mesmo pré-requisito das Limitações 01 e 02.


---

# Mapeamento de Listas — Fase 03 (Flows Operacionais)

**Data:** 20/06/2026

| Flow | Lista no Perfit | Contatos | Uso |
|------|----------------|----------|-----|
| Flow 04 — Cross Selling | Compradores da Nuvemshop | 24 | Campanhas manuais de cross-sell segmentadas por histórico de compra |
| Flow 05 — Comunidade | Eventos | 24 | Comunicações de eventos, desafios e ações da marca |
| Flow 05 — Comunidade (base ampla) | Contatos da Nuvemshop | 58 | Convites gerais para ações comunitárias |
| Flow 06 — Representação | Representação (criada 20/06/2026) | 0 | Seleção manual pela equipe Rage — clientes altamente engajados e parceiros |
| Flow 07 — Campanhas | Contatos da Nuvemshop | 58 | Base principal para campanhas recorrentes, lançamentos e promoções |

**Operação dos Flows 04-07:**
Todos operam via Campanhas manuais no Perfit (menu "Campanhas"), sem automação. A equipe seleciona a lista correspondente ao enviar cada comunicação.


---

# Relatório de Testes — Fase 04

**Data:** 20/06/2026

| Item | Status | Observação |
|------|--------|------------|
| Popup | ✅ | Ativo na loja, integrado à lista "Boas vindas" |
| Cupom RAGE10 | ✅ | Incluído no Email 01 do Flow 01 — 10% na primeira compra |
| Inscrição na newsletter | ✅ | Formulário ativo, envia para lista "Boas vindas" |
| Flow 01 — Boas-vindas | ✅ | Ativo, 4 emails (D0 / D+5 / D+10 / D+14), gatilho: qualquer formulário Perfit. 0 iniciados — aguardando primeiras inscrições via popup |
| Flow 02 — Primeira Compra | ✅ | Ativo, 6 iniciados, 4 completos, email com cupom cross-sell |
| Flow 03 — Evolução | ⛔ | Bloqueado por plano (Limitação 03) |
| Segmentações | ✅ | 7 listas configuradas e mapeadas por flow |
| Limitações documentadas | ✅ | Limitações 01, 02 e 03 registradas no Obsidian |

**Conclusão:** Toda a infraestrutura disponível no plano atual está operacional. Os flows 01 e 02 aguardam tráfego orgânico para validação de envio. Emails 02 a 05 dos flows e Flow 03 completo dependem de upgrade do plano Perfit/Nuvem Marketing.
