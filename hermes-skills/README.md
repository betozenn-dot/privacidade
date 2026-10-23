# Skills do Hermes Agent para a MarioCar

Pasta com skills prontas para o [Hermes Agent](https://github.com/NousResearch/hermes-agent)
(Nous Research). Cada subpasta é uma skill no formato `SKILL.md` + arquivos de apoio.

## Instalar a skill `mariocar-copy`

```bash
# 1. copie a pasta para o diretório de skills do Hermes
cp -r hermes-skills/mariocar-copy ~/.hermes/skills/

# 2. preencha telefone/WhatsApp e Instagram da loja
nano ~/.hermes/skills/mariocar-copy/references/loja.md

# 3. confira se o Hermes enxergou a skill
hermes skills list        # ou, dentro do chat: /skills
```

## Usar

No CLI, Telegram ou WhatsApp:

```text
/mariocar-copy Fiat Pulse Drive 1.0 Turbo 200 Flex Aut. 2022, 45.000 km, R$ 89.900, único dono
/mariocar-copy instagram Onix LTZ 1.0 Turbo 2021, 60.000 km
```

Ou mande a foto do carro com a ficha e peça "faz a copy".

## WhatsApp (gateway)

```bash
hermes whatsapp            # pareia via QR code (modo bot ou self-chat)
# ~/.hermes/.env
WHATSAPP_ENABLED=true
WHATSAPP_MODE=self-chat    # ou bot, com número dedicado
WHATSAPP_ALLOWED_USERS=5581XXXXXXXXX
hermes gateway install     # roda como serviço
```

## Agendar (cron)

Exemplo: todo dia útil às 9h, gerar a legenda do "carro do dia" e entregar no WhatsApp.

```text
/cron add "weekdays at 9am" "Leia a lista em ~/.hermes/estoque.md, escolha o próximo carro ainda sem legenda e gere a legenda de Instagram com a skill mariocar-copy" --skill mariocar-copy
```

## Personalidade da loja (opcional)

Em `~/.hermes/config.yaml`:

```yaml
agent:
  personalities:
    mariocar: >
      Você é o assistente de marketing da MarioCar, loja de seminovos em Recife.
      Fala português do Brasil, direto e confiante. Nunca inventa dados de veículo.
```

Ativar no chat com `/personality mariocar`.
