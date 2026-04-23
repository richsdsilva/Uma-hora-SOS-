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
