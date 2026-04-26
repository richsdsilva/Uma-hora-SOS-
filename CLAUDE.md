# AI CONTEXT — 1 HORA

## FLUXO
Cliente → OS → Fila → Conserto → Pronto → Entregue

## USUÁRIOS
- Dono: total
- Atendente: entrada + entrega
- Técnico: conserto

## MÓDULOS
- Entrada
- Painel (Fila | Conserto | Pronto)
- Entrega
- Resultados
- Perfil

## REGRAS
- FIFO na fila
- Conserto: maior tempo no topo
- Pronto: último finalizado no topo
- 1 garantia por OS
- Serviços exclusivos por grupo
- Higienização combinável
- Acesso por papel

## AUTOMAÇÕES
- Status inicia timer
- Pronto → envio WhatsApp
- Entrega → registra pagamento

## AI_RULES
- Priorizar velocidade
- Evitar complexidade
- Pensar uso real (loja cheia)
- Componentizar para Flutter

---

## JÁ FEITO (refinamentos UI/UX)

### Design System
- Tokens CSS para radius e shadow (`--radius-card`, `--shadow-card`, etc.)
- Section headers consolidados (`.sec-title`, `.od-section-title`)
- Botões de toggle de seção com classe `.sec-toggle` (discretos, sem destaque)

### Entrada
- Bottom sheet para seleção de modelo com busca e destaque de preços
- Bloco "Aprovação": botões seletores Sim/Não (azul/vermelho), sem campo de prazo
- CTA com animação `.cta.ready` ao selecionar aprovação
- Toasts de ação: azul para abrir OS (`opened`), vermelho para arquivar (`archived`)
- Toast reposicionado para centro-alto da tela (top: 48%), alinhamento interno corrigido
- Número do adesivo obrigatório em todos os fluxos de abertura de OS
- Bloqueio de OS com número duplicado já aberto no sistema

### Voz (entrada por fala)
- Captura contínua com timer de silêncio de 1s (`VOICE_SILENCE_MS`)
- Normalização fonética: "Face aí de" → "Face ID", "USB cê" → "USB-C", etc.
- Pipeline WhatsApp: `_wordsToDigits` → `extractPhoneFromSpeech` → `normalizeWhatsApp`
- Formato final: `+55XXXXXXXXXXX`

### Diagnóstico na Entrada
- Ícones Phosphor corrigidos no `diagSummary` (`.innerHTML` em vez de `.textContent`)
- Modo resumido: exibe apenas itens com falha; "Sem pendências na entrada" se tudo OK
- Modo expandido: falhas primeiro, depois itens OK em grid 2 colunas
- Sem linhas divisórias internas, com respiro visual entre itens

### Tela de OS Salva (Entrega/Painel/Fila/Conserto/Pronto)
- Header do card (`od-hd`): fundo azul claro (`--blue-s`), borda `#BFDBFE`
- Botões Editar e Voltar integrados ao fundo azul, sem contraste excessivo
- Linha de metadados discreta no header: `Atendente: X · Técnico: X`
- Seção "Técnico responsável" removida visualmente (elemento mantido oculto para seletor de técnicos na fila)
- Diagnóstico de entrada unificado: mesmo comportamento em todos os contextos de OS salva
- Sem linhas divisórias na seção "Conferência na saída"

### Painel / Arquivados
- Fluxo correto para arquivar e retomar orçamentos
- Eliminação de duplicatas e conflitos de número no fluxo de arquivados

### Perfil / Resultados
- Ícones removidos antes dos nomes no ranking
- Editor de preços: bug corrigido (`const hd` por iteração, scroll habilitado)

---

## ESTADO TÉCNICO ATUAL
- Arquivo único: `index.html` (~3300 linhas), sem build system
- Ícones: Phosphor Icons Web `@2.1.1` (render via CSS pseudo-elementos)
- Persistência: `localStorage` via `osList` + `persistOS()`
- Papéis: variável `role` ('dono' | 'atendente' | 'tecnico')
- Voz: `webkitSpeechRecognition`, `continuous: true`
- Toasts: `showToast(msg, type, duration)` — tipos: success, opened, archived, error, warning
