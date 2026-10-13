# Além do Óbvio — LP de captação

## Publicar

O arquivo principal é `index.html`. Ele funciona como landing page estática e pode ser publicado em Vercel, Netlify, Cloudflare Pages ou hospedagem própria.

Antes de publicar, atualize no bloco `CONFIG` do fim de `index.html`:

```js
pixelId: 'SEU_PIXEL_ID',
ga4Id: 'SEU_GA4_ID',
gtmId: 'SEU_GTM_ID',
leadEndpoint: 'https://seu-dominio.com/api/leads'
```

Também coloque a foto real da turma em:

```
assets/turma-agosto-2026.jpg
```

A imagem deve ser otimizada em WebP/AVIF ou JPG progressivo e ter ao menos 1800px de largura. Se preferir WebP, ajuste as duas referências a `assets/turma-agosto-2026.jpg` no CSS.

## Rastreio que já está implementado

- UTM: `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term`
- Meta: `campaign_name`, `adset_name`, `ad_name`, `campaign_id`, `adset_id`, `ad_id`, `fbclid`, `_fbp`, `_fbc`
- Localidade aproximada por IP: cidade, UF/região e país
- Referência curta por lead: `AO-XXXX`
- Evento Meta `Lead` com `event_id`, quando o Pixel estiver configurado
- Evento GA4 `generate_lead`, quando o GA4 estiver configurado
- Parâmetro `?headline=a|b|c` para o teste de título

## URLs dos anúncios Meta

Use parâmetros dinâmicos nos anúncios para o comercial receber o contexto completo:

```text
?utm_source=meta&utm_medium=paid_social&utm_campaign={{campaign.name}}&campaign_name={{campaign.name}}&campaign_id={{campaign.id}}&adset_name={{adset.name}}&adset_id={{adset.id}}&ad_name={{ad.name}}&ad_id={{ad.id}}
```

## CRM / planilha e API de Conversões

`leadEndpoint` deve apontar para um endpoint HTTPS que aceite o JSON enviado pela LP. Ele deve:

1. Validar e guardar os dados do lead em CRM/planilha.
2. Registrar data/hora no fuso desejado.
3. Enviar o evento `Lead` para a Meta Conversions API usando **o mesmo** `event_id` recebido no corpo.
4. Responder `2xx` rapidamente.

A CAPI não deve receber token diretamente no navegador: mantenha o token de acesso somente no backend/webhook. Para uma planilha, um Google Apps Script Web App ou Make/Zapier pode receber o JSON e encaminhar ao Google Sheets/CRM; para CAPI, use um serviço/endpoint que guarde o token em segredo.

## Operação comercial

A mensagem do WhatsApp abre no número `+55 11 93620-6406` com o código de referência e todos os campos do lead. Aline e Maxhellen devem manter a mensagem original na conversa para preservar o contexto de campanha.

## Privacidade

A página inclui o consentimento obrigatório para contato por WhatsApp. Antes de mídia paga, publique uma política de privacidade real no link do rodapé e alinhe Pixel, GA4, GTM e geolocalização por IP com a política/CMP e orientação jurídica de LGPD da operação.
