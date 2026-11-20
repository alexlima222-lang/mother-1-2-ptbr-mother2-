# Checkpoint 23 — ALPHA62: acentos corrigidos e serviços ampliados

**Alfa parcial para teste. A tradução integral ainda não está certificada.** Mother 1 e o conteúdo da ALPHA61 foram preservados.

## Correção encontrada e implementada

A largura de desenho de `í` e `Í` era menor que o acento nas fontes principal e minúscula. Na fonte principal, a largura declarada era 1 pixel, embora houvesse tinta até o segundo pixel; na fonte minúscula, era 3 em vez de 4. Quando o glifo começava na borda de um tile, a rotina nativa podia deixar de copiar o pixel do acento para o tile seguinte.

`font_ptbr.py` agora mede a extensão real do desenho de cada acento e registra uma largura que o abrange. O espaçamento de avanço permanece igual; o roteiro não foi refluído por causa desta correção. Foram corrigidos quatro bytes de métricas na ROM:

| Offset | Anterior | Novo |
|---|---:|---:|
| 0xD62081 | 1 | 2 |
| 0xD6209B | 1 | 2 |
| 0xD624B1 | 3 | 4 |
| 0xD624CB | 3 | 4 |

`verify_font_fix23.py` reverte esses quatro bytes em uma cópia em memória e obtém exatamente o SHA256 da ALPHA61. Portanto, **todos os outros bytes da ROM são idênticos à ALPHA61**, incluindo os 506.767 bytes do roteiro compilado, os créditos, as telas finais e as regiões brasileiras protegidas de Mother 1. A verificação é recuperável sem precisar guardar outra ROM inteira.

## Teste de acentos

A CPU emulada executou `print_character_to_ram` da própria ROM em **832 combinações**: 26 acentos, quatro fontes e oito alinhamentos horizontais. O resultado 4bpp foi comparado pixel a pixel aos glifos esperados; não houve diferenças. Foram conferidos também os valores de avanço retornados.

Quatro controles negativos restauraram as métricas antigas apenas na memória do emulador. Eles reproduziram a perda de um pixel no acento de `í` e `Í` nas fontes principal e minúscula. Ao restaurar a métrica corrigida, o pixel reapareceu. Isso comprova o defeito e a correção, sem depender apenas de uma inspeção visual.

As fixtures usam RAM de trabalho, pilha e registradores declarados, com IRQs desativadas. Elas não percorrem diálogos de uma campanha; testam diretamente a rotina de desenho. O arquivo da ROM permanece inalterado pelos testes.

## Escargo Express

O teste anterior comprovava somente o pedido de coleta. Esta etapa acrescenta transações nativas completas em cenários controlados:

| Caso | Evidência |
|---|---|
| Um item | Biscoito retirado, selecionado no depósito e devolvido; inventário inicial restaurado |
| Três itens | Biscoito, Pãozinho e Hambúrguer retirados e devolvidos na mesma ordem |
| Taxas | $100 → $82 na coleta → $64 na devolução; uma taxa de $18 por viagem, inclusive com três itens |
| Item protegido | Cartão do Banco recusado, sem perda do cartão ou cobrança |
| Cancelamento | Cancelar a confirmação de coleta restituiu o item, sem cobrança |
| Saldo insuficiente | Coleta e devolução recusadas com $17, sem transferência do item |
| Flags | Pedido de coleta e de entrega observados; flags limpas pelas respectivas rotinas |

**Limites:** o cenário inicial recebe dinheiro e itens por fixture de RAM. As entradas de NPC são redirecionadas somente na memória do emulador para os scripts reais do serviço. A rotina `L4023`, de caminhada/remoção do ator, retorna imediatamente nesse ensaio para manter o NPC disponível. Não há edições diretas de dinheiro, inventário ou armazenamento durante as transações bem-sucedidas. Os ramos de saldo insuficiente usam um saldo inicial específico e são isolados por save states.

Esses resultados validam a lógica e a interface de transação; **não validam o trajeto físico até o telefone, o temporizador, a criação do entregador ou suas animações**. As capturas mostram a mãe como NPC de teste, e não um entregador surgido naturalmente.

## Lumine Hall

`writeLumineHallText` da própria ROM foi executada para quatro casos: texto traduzido, nome de cinco letras W, nome com acentos e uma sequência diagnóstica com os 26 acentos. A matriz nativa foi comparada a um modelo independente de composição dos glifos.

Todos os pixels coincidiram; todas as células pertenciam à tabela válida e as sentinelas antes/depois do buffer ficaram intactas. O texto normal ocupou 8.256 bytes de matriz; o nome de largura máxima ocupou 8.384 bytes. A rotina retornou em até três quadros nesses ensaios.

**A imagem diagnóstica é uma reconstrução da matriz gerada, não uma captura da parede em uma campanha.** Permanecem pendentes a cena natural, a PPU da parede, sua rolagem e a integração ao mapa. O teleporte experimental antigo que chegava ao Mundo Perdido continua sem contar como validação da parede.

## Regressão da versão atual

- 27 scripts registrados com sucesso: os 23 anteriores e os quatro novos testes de acentos, matriz de Lumine e transações de um/três itens.
- 489 fragmentos de diálogo renderizados novamente, sem alertas de borda. São trechos lineares em diagnóstico; não certificam cenas completas.
- 252 ajudas de itens, 52 descrições PSI e os testes de nomes do Sr. Saturno passaram. As 252 renderizações completas de nomes de Saturno coincidiram com a referência literal.
- Créditos, elenco e encerramento passaram novamente pelas seis fixtures de desenho/PPU e pelos oito testes de descompressão da BIOS. A abertura natural, café e chá também foram repetidos. Seus limites de cobertura continuam iguais aos do checkpoint 22.
- Suíte instrumentada **120: 2042 verificações, zero falhas**, compilada com as fontes desta etapa. A ROM entregue é a comum ALPHA62, sem instrumentação.
- Reconstrução atômica idêntica com o emulador ativo. Os símbolos comuns foram restaurados após a suíte instrumentada.
- BPS das bases BR e JP reconstruídos e aplicados de volta: os resultados coincidem byte a byte com a ROM entregue; bases erradas foram rejeitadas.

SHA256 da ROM ALPHA62: `0f12c60544d16079aaab1ede2fed3547a3f1d4625565f387229e6c695f8d6e7b`.

## Progresso e gráficos restantes

O roteiro mantém **11.528/11.528 trechos tratados: 100% com tradução/adaptação ou manutenção justificada**. A métrica anterior de edição continua em **99,07% das palavras-fonte em trechos alterados**, ou **98,99%** excluindo alterações só de formatação. Isso não é uma porcentagem global de todos os textos do jogo, nem uma revisão semântica completa.

Foi criado um catálogo de **118 recursos existentes no diretório de dados do projeto upstream**, com tamanho, hash e referências em ASM. Ele não cobre todos os bancos gráficos da ROM japonesa e não marca automaticamente os arquivos como traduzidos.

Foram confirmados pontos para a próxima auditoria: a placa `BURGLIN PARK`, sinais ambientais na imagem de abertura do posto e um arquivo de placa do elenco sem referência direta encontrada. A adaptação precisa respeitar os nomes próprios, a arte, a paleta e a disposição original. Esses gráficos **não foram declarados traduzidos** nesta etapa.

## Pendências

1. Adaptar e validar os gráficos ambientais com texto, ampliando o inventário para os bancos originais da ROM.
2. Percorrer naturalmente o elenco, os créditos e o encerramento com atores e rolagem.
3. Validar a parede de Lumine Hall na própria cena.
4. Validar o ciclo físico do entregador da Escargo, temporizador e demais ramificações dos serviços.
5. Revisão contextual e campanhas completas dos dois jogos; compatibilidade no emulador do Switch.

Não foi incorporado texto de patch SNES nesta etapa. Não há declaração de tradução integral concluída.

## Recuperação

O pacote menor contém ROM comum ALPHA62, BPS das duas bases, capturas e evidências selecionadas. O checkpoint completo contém o código, os textos, os recursos originais, o runtime, entradas compactadas, logs e histórico.

Manter `project/` e `inputs/` lado a lado. Executar `bash project/scripts/setup_runtime.sh`, `python3 project/scripts/extract_inputs.py` e `MOTHER_VERSION=62 python3 project/scripts/rebuild_all.py`. Antes dos testes de emulação, definir `LD_LIBRARY_PATH` para `tools-local/root/usr/lib/x86_64-linux-gnu` e executar `integration03.py`; `run_stage23.py` executa os 27 scripts principais. Os ensaios gráficos e especiais adicionais têm comandos próprios e seus logs no checkpoint.

`verify_font_fix23.py`, `test_accent_tiles.py`, `test_lumine_native.py`, `test_delivery_roundtrip.py`, `test_delivery_three.py` e `inventory_graphics23.py` preservam o trabalho novo desta etapa. Os estados de depuração são específicos do hash da ROM e ficam fora do pacote menor.
