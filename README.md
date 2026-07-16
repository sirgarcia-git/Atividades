Abaixo 2 links de imagens de exemplo:
aqui tif direto:
CB4A-MUX-L4-SR/2026_06/CBERS_4A_MUX_RAW_2026_06_19.13_17_01_ETC2/213_113_0/4_BC_UTM_WGS84/CBERS_4A_MUX_20260619_213_113_L4_BAND5_GRID_SURFACE.tif
e aqui é um arquivo .zip. dentro dele na pasta GRANULE/nome_dir/IMG_DATA você encontrará alguns arquivos .jp2:
S2_L1C_BUNDLE/v001/18/L/XR/2026/07/S2A_MSIL1C_20260705T151931_N0512_R125_T18LXR_20260705T232908/S2A_MSIL1C_20260705T151931_N0512_R125_T18LXR_20260705T232908.zip

Você pode preparar uma função em python, que recebe o caminho de uma imagem (pode ser um .tif ou um .jp2), 
um tipo de compressão (LZW, DEFLATE, ZSTD, pode ser arquivo descomprimido também), os parâmetros dessa compressão (quando existirem)
e um tamanho de bloco (128, 256, 512) me gere a mesma imagem em um arquivo .tif de saída, que por opção pode ou não estar no formato cloud optimized geotiff.

Você pode fazer por partes, comece com o mais simples, primeiro uma função que recebe o caminho da imagem e um tipo de compressão e gera a imagem saida,
depois você complementa passando os parâmetros de compressão, depois o tipo de blocagem, depois a geração de COG.

Obs: você pode escolher entre fazer a função no python chamando a gdal em python, ou fazer a função em python chamando a gdal por linha de comando.

Por exemplo. Quando você gera com (ou sem) alguma compressão, tem que verificar se o arquivo de saída está na compressão desejada, por exemplo,
quando está sem compressão ao invés de deixar o arquivo descomprimido, ele está mantendo a compressao atual.

Na gdal se não me engano usa um comando RAW quando não tem. Só fazer esse pequeno ajuste. Você pode olhar essas características rodando um gdalinfo no arquivo.
A parte do JP2, chamando a gdal pelo python deve dar problema mesmo.

Vocẽ pode agora repetir o exercício feito, mas criando um comando da gdal pra linha de comando, pra isso você vai usar a biblioteca `os`
