# Etapa 10 Preparação da apresentação

## Solicitação

Prepare uma apresentação clara do artigo e organize a participação do grupo.

## Dados da apresentação

- Título do artigo: Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos
- Evento ou disciplina: Computabilidade e Complexidade de Algoritmos
- Data: 27/10/2026
- Tempo disponível: 15 minutos
- Integrantes: Grupo 8: Benito Juarez Jesus Viana Aguiar, Renan Veras de Andrade, Augusto Domingues da Silva e Thiago de Luca Fernandes

## Estrutura

| Parte | Conteúdo principal | Responsável | Tempo |
|---|---|---|---:|
| Abertura | Z-buffer: varredura das primitivas, custo O(N). BVH: árvore espacial, custo por raio ~O(log N). Lacuna: o ponto de virada entre os dois não está definido. | Thiago de Luca Fernandes | 2 min 15 s |
| Objetivos | Pergunta: como a complexidade e a memória divergem entre Z-buffer e BVH quando as primitivas crescem? Objetivo geral: comparar as duas estruturas a partir de 5 estudos. Objetivo específico não atendido plenamente: o ponto de interseção entre as técnicas. | Thiago de Luca Fernandes | 1 min 30 s |
| Metodologia | Busca em 16/09/2026 (IEEE Xplore, ACM DL, Scopus): 431 resultados, 389 triados, 18 lidos e 5 incluídos (2006 a 2021). Análise qualitativa por eixos; os números dos estudos não são comparados entre si. | Benito Juarez Jesus Viana Aguiar | 2 min |
| Resultados da revisão | Eixo 1 — Z-buffer (Lambru, Wyman, Ritschel): o custo da matriz depende da resolução e do acesso (Benito, 1 min 45 s). Eixo 2 — Estruturas hierárquicas e achado central (Woop, Crassin, Lambru, Ritschel): consulta mais barata, mas memória, atualização e divergência pesam; os estudos apontam gargalos diferentes (Renan, 3 min 30 s). | Benito Juarez Jesus Viana Aguiar e Renan Veras de Andrade | 5 min 15 s |
| Conclusão | Não há estrutura vencedora absoluta: o Z-buffer tem acesso regular, mas custo que cresce com a resolução; a BVH reduz o custo de consulta, mas depende de memória, cache e atualização. O ponto de virada não está definido. Próximo passo: experimento em um mesmo hardware, de 1080p a 4K. | Augusto Domingues da Silva | 4 min |

## Mensagem principal

Não há estrutura vencedora absoluta: o Z-buffer é simples e regular, mas o custo de estruturas matriciais cresce com a resolução, enquanto a BVH e estruturas parentes reduzem o custo assintótico da consulta, mas o desempenho real passa a depender de memória, cache e atualização da estrutura. Os cinco estudos revisados apontam gargalos diferentes, e a literatura não define o ponto de virada entre os dois paradigmas. Por isso, falta um estudo experimental comparativo, em um mesmo hardware, que escale a geometria.

## Perguntas esperadas

1. Pergunta: Qual é o ponto de virada em que a BVH passa a compensar mais do que o Z-buffer?  
   Resposta: Os cinco estudos não definem esse ponto. Os números vêm de hardwares, cenas e problemas diferentes (de uma simulação de ASIC em 2006 a uma GTX 1070 em 2021), o que impede calculá-lo por comparação direta. Essa é uma lacuna identificada pela revisão. O desdobramento sugerido é um experimento que escale a contagem de triângulos em um mesmo hardware, incluindo o tempo de construção ou atualização da árvore.
2. Pergunta: Cinco artigos não são poucos para tirar conclusões? Os estudos tratam mesmo de Z-buffer contra BVH?  
   Resposta: O conjunto saiu de uma busca estruturada: 431 resultados, 389 após remover duplicatas, 18 lidos na íntegra e 5 incluídos pelos critérios de inclusão e exclusão. O artigo reconhece o tamanho reduzido do conjunto como limitação. Reconhece também que vários estudos tratam de iluminação global e sombras e não da visibilidade primária, e que dois usam estruturas parentes da BVH (árvore B-KD e octree esparsa). Por isso a revisão não conclui pela superioridade absoluta de uma técnica.
3. Pergunta: Então a memória é o principal fator limitante nos dois paradigmas?  
   Resposta: Não de forma única. Os estudos apontam gargalos diferentes: contenção atômica em Wyman et al., divergência de threads em Ritschel et al., consumo de memória e custo de atualização em Crassin et al., e, em Woop et al., uma banda de DRAM medida baixa, com a restrição de que só movimentos coerentes são tratados com eficiência. Há convergência apenas no sentido de que o custo deixa de ser só aritmético e passa a depender de acesso à memória, cache e atualização da estrutura.

## Checklist

- [x] A apresentação respeita o tempo.
- [x] Os slides possuem pouco texto e boa legibilidade.
- [x] As fontes das imagens e dados foram informadas.
- [x] Todos conhecem o problema, o método e as conclusões.
- [x] O grupo realizou pelo menos um ensaio completo.
- [x] Os integrantes estão preparados para responder perguntas.