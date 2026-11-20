# Mother 1+2 — Complemento PT-BR de Mother 2

Projeto independente de localização para português brasileiro de **Mother 2**, na coletânea *Mother 1+2* para Game Boy Advance.

## Objetivo e autoria

Este trabalho **complementa uma tradução brasileira anterior de Mother 1**. Não reivindicamos autoria dessa tradução preexistente: nossa contribuição concentra-se em Mother 2, buscando preservar Mother 1 como estava.

**Créditos da tradução anterior: pendentes de identificação e confirmação.** Antes de distribuir patches que possam incorporar esse trabalho, verificaremos sua licença ou obteremos autorização apropriada. O projeto não é oficial e não distribui ROMs comerciais.

## Estado atual — ALPHA62 (checkpoint 23)

**Alfa parcial para testes, não é uma versão final.** O relatório do checkpoint documenta correção das métricas de `í` e `Í`, testes de 832 combinações de acentos, serviços, menus, batalhas e outras rotinas. A ROM ALPHA62 difere da ALPHA61 em apenas quatro bytes de métricas; os dados de Mother 1 foram preservados segundo a verificação automatizada.

Permanecem pendentes a revisão contextual da campanha, alguns gráficos ambientais, integração de cenas naturais, encerramento completo e testes em Nintendo Switch.

## Patches e bases (ainda não publicados)

Os testes locais verificaram dois patches BPS:

| Variante | Base | SHA-1 exigido da base |
| --- | --- | --- |
| BASE_BR | ROM com a tradução brasileira anterior | `2b41a11f925cb99d45bb78b89958604971872250` |
| BASE_JP | ROM japonesa original | `f27336b9c96ca2d06c34e07a61a78538deac32b3` |

Ambos produzem a mesma ROM de teste, cujo SHA-256 é `0f12c60544d16079aaab1ede2fed3547a3f1d4625565f387229e6c695f8d6e7b`. **Os patches não estão incluídos neste pacote público inicial**, até verificarmos os direitos da tradução anterior.

## Documentação

- `docs/RELATORIO_23.md` — relatório técnico do checkpoint 23.
- `docs/release_verification.json` — verificações automatizadas dos BPS e da ROM.
- `docs/README_ORIGINAL_ALPHA62.md` — instruções originais do pacote de teste, preservadas para referência técnica; mencionam arquivos não distribuídos neste repositório.

## Próximas etapas

1. Identificar os autores e a licença da tradução brasileira de Mother 1.
2. Confirmar as bases e as permissões de redistribuição dos patches.
3. Revisar textos, gráficos, cenas e campanha de Mother 2.
4. Publicar um pré-lançamento com os patches autorizados, sem ROMs.

## Créditos

Tradução anterior de Mother 1: **autoria a confirmar**. Complemento de Mother 2: projeto mantido por **alexlima222-lang**, com assistência de ferramentas e do ChatGPT. *Mother* e os recursos originais pertencem aos respectivos titulares de direitos.
