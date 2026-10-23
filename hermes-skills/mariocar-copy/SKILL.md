---
name: mariocar-copy
description: Gera copy de anúncio para veículos seminovos da MarioCar.
version: 1.0.0
author: Mario Oliveira (MarioCar) + Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [copywriting, carros, seminovos, marketing, whatsapp, instagram]
    category: marketing
---

# MarioCar Copy

Transforma a ficha de um carro (modelo, ano, km, preço, opcionais) em copy pronta
para publicar: anúncio longo (OLX, Webmotors, Marketplace), versão curta
(Stories, WhatsApp) e legenda para Instagram (Reels, feed).

Use esta skill para:
- Criar o anúncio de um carro que acabou de entrar no estoque.
- Reescrever um anúncio fraco com mais apelo de venda.
- Gerar legenda e hashtags para um Reel ou post do carro.
- Responder rápido quando alguém mandar só a foto + "faz a copy".

## Quando usar

Sempre que a mensagem contiver dados de um veículo à venda e pedir "copy",
"anúncio", "legenda", "texto pra postar" ou similar. Também quando chegar uma
foto de carro acompanhada de ficha técnica.

## Pré-requisitos

- Nenhuma ferramenta externa. Só leitura dos arquivos desta skill.
- Para fotos: um modelo com visão ativo (ou `auxiliary.vision` configurado).
- Dados da loja em `references/loja.md`. Edite esse arquivo uma vez com o
  telefone/WhatsApp real.

## Como rodar

Como comando:

```text
/mariocar-copy Fiat Pulse Drive 1.0 Turbo 200 Flex Aut. 2022, 45.000 km, R$ 89.900
/mariocar-copy curta Onix LTZ 1.0 Turbo 2021 60 mil km
/mariocar-copy instagram HB20 Vision 2023 (foto em anexo)
```

Em linguagem natural: "Cria uma copy pro Pulse 2022 com 45 mil km" também aciona.

## Referência rápida

| Pedido                          | Template                          |
|---------------------------------|-----------------------------------|
| "copy", "anúncio" (padrão)      | `templates/anuncio-longo.md` + `templates/anuncio-curto.md` |
| "curta", "stories", "whatsapp"  | `templates/anuncio-curto.md`      |
| "instagram", "reel", "legenda"  | `templates/legenda-instagram.md`  |
| Exemplo de resultado final      | `exemplos/pulse-2022.md`          |
| Tom de voz e regras             | `references/estilo.md`            |
| Dados da loja (endereço, zap)   | `references/loja.md`              |

## Procedimento

1. Extraia da mensagem: marca, modelo, versão, motor, câmbio, combustível, ano,
   km, cor, preço, opcionais, procedência (único dono, revisões, IPVA, laudo).
   Se houver foto, use-a só para confirmar cor, rodas e estado aparente.
2. Leia `references/estilo.md` e `references/loja.md` com `skill_view`.
3. Escolha o template pela tabela acima. Sem indicação, entregue longo + curto.
4. Preencha o template. O que não foi informado fica entre colchetes, por
   exemplo `[valor]`, `[único dono]`. Nunca invente preço, km, potência,
   opcional ou "sem sinistro".
5. Ajuste o gancho ao ponto forte real do carro: baixa km, único dono, câmbio
   automático, turbo, preço abaixo da tabela. Um gancho por anúncio.
6. Revise o tamanho: legenda Instagram até 2.200 caracteres; mensagem WhatsApp
   até 4.096 (o gateway corta acima disso).
7. Responda só com a copy pronta para colar, mais uma linha dizendo quais
   campos entre colchetes faltam preencher.

## Armadilhas

- Dados técnicos de versão (cv, tamanho da central, airbags) variam por ano.
  Só cite o que vier na ficha ou o que for universalmente conhecido do modelo.
- No WhatsApp, `# Título` vira negrito e markdown de tabela não renderiza.
  Use `*negrito*` e listas simples.
- Não coloque dados pessoais de cliente ou vendedor além do contato da loja
  (LGPD). Nunca invente CPF, placa ou chassi.
- Evite "oportunidade única" e "imperdível" em toda frase. Um CTA forte basta.
- Não prometa financiamento aprovado nem taxa. Use "consulte condições".

## Verificação

- Todo dado numérico na copy veio da mensagem ou está entre colchetes.
- Há título com modelo + ano + km, lista de destaques, bloco de procedência,
  preço e CTA com WhatsApp da loja.
- Tom bate com `references/estilo.md` (direto, confiante, sem exagero).
- Se pediram Instagram: há hashtags locais (Recife) e no máximo 15 no total.
