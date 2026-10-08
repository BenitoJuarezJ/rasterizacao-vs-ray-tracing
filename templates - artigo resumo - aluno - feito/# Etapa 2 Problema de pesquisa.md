# Etapa 2 Problema de pesquisa

## Tema aprovado
Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos.

## Pergunta de pesquisa
Como a complexidade assintótica e o consumo de memória divergem entre a rasterização (com Z-buffer) e o Ray Tracing (com aceleração BVH) ao escalar exponencialmente o número de primitivas e polígonos em sistemas gráficos de tempo real?

## Verificação
- O que se deseja descobrir ou compreender? A ausência de clareza matemática exata no custo-benefício computacional durante o ponto de virada (quando a quantidade de polígonos torna a travessia de árvores mais eficiente que a varredura linear).
- Qual é o objeto da pergunta? Complexidade assintótica (Notação Big-O) e custo de memória (footprint).
- Qual é o contexto ou recorte? Renderização gráfica em tempo real sob alta carga geométrica.
- A pergunta pode ser respondida por artigos científicos? Sim. As bases de dados acadêmicas da computação possuem literatura rica comparando algoritmos, consumo de VRAM e tempos de clock de CPU/GPU.
- Por que essa pergunta é relevante? Porque a indústria gráfica está em transição do Z-buffer para o Ray Tracing, sendo imperativo entender os gargalos matemáticos que limitam ambas as estruturas.

## Produto da etapa
Pergunta de pesquisa aprovada.

## Checklist
- [x] Está escrita em forma de pergunta.
- [x] É clara e objetiva.
- [x] Está alinhada ao tema.
- [x] Pode ser respondida por revisão bibliográfica.
- [x] Não exige experimento que não será realizado.

## Contribuições
| Integrante | Atividade realizada |
|---|---|
| Thiago de Luca Fernandes | Formulação direta da pergunta de pesquisa, alinhando a necessidade de verificar restrições matemáticas e de memória. |