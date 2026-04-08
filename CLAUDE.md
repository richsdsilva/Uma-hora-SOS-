# 1 HORA — Assistência Técnica
## Contexto do Projeto para Claude Code

---

## O QUE É

App de gestão para assistência técnica de iPhone especializada em alto volume (100-200 aparelhos/dia). Desenvolvido como MVP para a loja **Uma Hora Assistência Técnica** (Shopping Oriental, SP).

Tecnologia atual: **HTML/CSS/JS** hospedado no **GitHub Pages**.
Próximo passo: migrar para **Flutter**.

---

## REPOSITÓRIO

```
https://github.com/richsdsilva/Uma-hora-SOS-
```

Arquivos:
- `index.html` — app completo (todo CSS, HTML e JS em um único arquivo)
- `manifest.json` — configuração PWA
- `sw.js` — service worker para cache offline
- `apple-touch-icon.png` — ícone do app
- `404.html` — redirect para index.html
- `.nojekyll` — desativa Jekyll no GitHub Pages

---

## IDENTIDADE VISUAL

```
--red: #D41F1F       (vermelho principal — header, botão CTA entrega)
--blue: #1A5CC8      (azul — valores, botões principais, seleção)
--green: #16A34A     (verde — aprovado, toggle OK, pronto)
--orange: #D97706    (laranja — alertas, timer de aviso)
--bg: #F2F2F7        (fundo geral)
--white: #fff
--border: #E5E5EA
--text: #0A0A0A
Font: Plus Jakarta Sans (Google Fonts)
```

---

## ESTRUTURA DO APP

5 abas na bottom nav (posição fixa):
1. 📥 **Entrada** — abertura de OS
2. 📋 **Painel** — kanban McDonald's style
3. ✅ **Entrega** — finalização e WhatsApp
4. 📊 **Resultados** — gráficos (só dono)
5. 👤 **Perfil** — ranking e gamificação

---

## REGRAS DE NEGÓCIO

### Fluxo de OS
```
Entrada (atendente) → Fila → Conserto (técnico pega) → Pronto → Entregue
```
- Atendente abre OS: foto, dados cliente, diagnóstico, serviços
- Técnico pega pelo painel: muda status para Conserto
- Técnico finaliza: muda para Pronto
- Atendente entrega: dispara WhatsApp, muda para Entregue

### Controle de acesso
- **Dono**: vê tudo — Entrada, Painel, Entrega, Resultados, Perfil + valores financeiros
- **Atendente**: Entrada, Painel, Entrega, Perfil — SEM valores financeiros
- **Técnico**: Painel, Entrega, Perfil — SEM entrada nem financeiro

### Diagnóstico (grupos colapsáveis, accordion exclusivo)
- **Tela**: Face ID, Tela & Display, Touch Screen
- **Bateria**: slider + input numérico, toggle automático vermelho abaixo de 80%
- **Componentes**: Alto-falante, Câmera Frontal, Câmera Traseira, Botões, Conector
- **Extras**: Higienização (R$50) + Garantias (7d grátis, 1m R$60, 3m R$120, 6m R$200)

### Serviços — grupos exclusivos
- Tela: OLED ou Compatível (não ambas)
- Garantia: só uma por vez
- Higienização: pode combinar com qualquer garantia

### Painel — ordenação
- **Fila**: mais antigo no topo (FIFO)
- **Conserto**: maior timer no topo (mais urgente)
- **Pronto**: maior timer no topo (entrega prioritária)

---

## COMPONENTES PRINCIPAIS

### Toggle iOS
```css
/* Verde = OK, Vermelho = falha */
.ios-toggle.fail .ios-track { background: var(--red); }
/* bolinha vai para esquerda no fail */
.ios-toggle.fail .ios-thumb { margin-left: 0; margin-right: auto; }
```

### Bottom Nav
```css
.bnav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); }
.bnav-icons { height: 38px; overflow: visible; }
.nb .ni { font-size: 24px; } /* ajustar conforme necessário */
```

### Header fixo
```css
.hd { position: sticky; top: 0; z-index: 150; }
```

---

## MODELO COMERCIAL

- **30 dias grátis** para validação
- **R$1.500/mês** após período de teste
- **Garantia estendida**: 30% para o app, 50% dono, 10% técnico, 10% fundo de conserto
- Argumento central: *"O senhor consegue sair daqui e a loja continua funcionando sozinha"*

---

## PRÓXIMOS PASSOS

### Curto prazo (HTML)
- [ ] Banco de dados Firebase (substituir dados fictícios)
- [ ] Voz inteligente com Claude API para preenchimento automático
- [ ] Preços e técnicos editáveis pelo dono
- [ ] LocalStorage para persistir OS durante o dia

### Médio prazo (Flutter)
- [ ] Migrar todo o app para Flutter
- [ ] Notificações push para cliente quando OS fica pronta
- [ ] WhatsApp Business API para disparo automático real
- [ ] Dashboard do dono com métricas em tempo real
- [ ] Publicar na App Store e Play Store

---

## COMO FAZER EDIÇÕES CIRÚRGICAS

Sempre edite apenas o trecho específico. Exemplos:

```bash
# Mudar tamanho dos ícones da barra
# Busca: .nb .ni{font-size:
# Troca só o valor numérico

# Mudar cor de um elemento
# Busca: var(--red) ou #D41F1F
# Troca só onde necessário

# Adicionar função JS
# Busca: // ─── INIT ───
# Adiciona após applyRole();
```

---

## AVISOS IMPORTANTES

- **Não usar `var(--sab)` com fallback alto** — causa barra inferior grande
- **Header deve ter `position:sticky`** — senão some ao abrir teclado
- **Safe area via JS** — `window.innerHeight` para calcular altura real no iOS
- **`overscroll-behavior:none`** no body — evita bounce indesejado
- Todo o app está em **um único arquivo `index.html`** — CSS, HTML e JS juntos
