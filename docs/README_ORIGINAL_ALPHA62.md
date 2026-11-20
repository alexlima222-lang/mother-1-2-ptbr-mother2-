# Mother 1+2 PT-BR — checkpoint 23 / ALPHA62

**Alfa parcial para teste; ainda não é a candidata final.**

Corrigidas as métricas de í/Í nas fontes principal e minúscula. Testados 832 casos de acentos, quatro matrizes de Lumine Hall, coleta/devolução de um e três itens da Escargo e recusas/cancelamento. A ROM difere da ALPHA61 somente em quatro bytes de métricas; Mother 1 e todo o conteúdo traduzido anterior foram preservados.

## Testar

Extrair o ZIP e abrir `build/MOTHER12_PTBR_ALPHA62.gba` no emulador de GBA. Use seu próprio save; o pacote menor não inclui estados de depuração. Switch ainda não validado.

Os BPS BASE_BR e BASE_JP geram a mesma ROM de 16.777.216 bytes. Aplique apenas à base correspondente sem cabeçalho, nunca sobre uma alfa anterior.

- BR SHA1: `2b41a11f925cb99d45bb78b89958604971872250`.
- JP SHA1: `f27336b9c96ca2d06c34e07a61a78538deac32b3`.
- ALPHA62 SHA256: `0f12c60544d16079aaab1ede2fed3547a3f1d4625565f387229e6c695f8d6e7b`.

## Reconstruir

1. Manter project/ e inputs/ lado a lado.
2. `bash project/scripts/setup_runtime.sh`
3. `python3 project/scripts/extract_inputs.py`
4. `MOTHER_VERSION=62 python3 project/scripts/rebuild_all.py`
5. Definir `LD_LIBRARY_PATH="$PWD/tools-local/root/usr/lib/x86_64-linux-gnu"`.
6. `python3 project/scripts/integration03.py`
7. `python3 project/scripts/run_stage23.py`

A suíte instrumentada atual é a 120. Após compilá-la, reconstruir a versão comum 62 para restaurar os símbolos usados pelas fixtures.

O roteiro mantém 100% dos trechos tratados, com a métrica anterior de edição em 99,07%. Permanecem gráficos ambientais, encerramento natural, parede de Lumine na cena, trajeto/temporizador do entregador, revisão contextual, campanhas e Switch. Os testes de matriz e transação não certificam essas rotas.

Ver `reports/RELATORIO_23.md`, `reports/status.json` e `reports/RETOMADA.md` para evidências e limites.
