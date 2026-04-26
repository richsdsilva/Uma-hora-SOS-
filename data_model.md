# DATA MODEL — 1 HORA

## OS
- id
- cliente_nome
- cliente_telefone
- aparelho
- status
- tecnico_id
- servicos[]
- valor_total
- garantia
- criado_em
- atualizado_em

## USUARIO
- id
- nome
- papel (dono | atendente | tecnico)

## SERVICO
- id
- nome
- preco
- categoria

## EVENTOS
- onCreateOS
- onAssignTecnico
- onStartRepair
- onFinishRepair
- onDeliver
- onSendWhatsApp

## AUTOMAÇÕES
- status → inicia timer
- pronto → envia WhatsApp
- entrega → registra pagamento
