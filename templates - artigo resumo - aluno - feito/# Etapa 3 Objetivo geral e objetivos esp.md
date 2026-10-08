# Etapa 3 Objetivo geral e objetivos específicos

## Problema de pesquisa
Como a complexidade assintótica e o consumo de memória divergem entre a rasterização (com Z-buffer) e o Ray Tracing (com aceleração BVH) ao escalar exponencialmente o número de primitivas e polígonos em sistemas gráficos de tempo real?

## Objetivo geral
Analisar comparativamente a complexidade assintótica (Big-O) e o custo de memória (footprint) gerado pelas estruturas Z-buffer e Bounding Volume Hierarchy (BVH) em pipelines de computação gráfica de renderização estressada.

## Objetivos específicos
1. Conceituar a arquitetura e a mecânica das listas de oclusão por profundidade (Z-buffer) e as estruturas de árvore espacial (BVH).
2. Mensurar o comportamento do tempo de execução da rasterização sob a métrica Big-O ao escalar primitivas geométricas em tela.
3. Estruturar a diferença formal de preenchimento e exigência do cache de memória da GPU entre as matrizes bidimensionais e a travessia de grafos/árvores.
4. Determinar o ponto de intersecção computacional em que o uso do Ray Tracing sobrepassa a eficiência da varredura baseada em rasterização.

## Quadro de alinhamento
| Elemento | Texto |
|---|---|
| Problema | Como a complexidade assintótica e o consumo de memória divergem entre Z-buffer e BVH ao escalar polígonos exponencialmente? |
| Objetivo geral | Analisar comparativamente a complexidade assintótica (Big-O) e o custo de memória das estruturas Z-buffer e BVH. |
| Resultado esperado | Um artigo de revisão documentando os limites assintóticos de ambas as técnicas, comprovando de forma lógica e matemática o gargalo técnico gerado pelo uso de cada estrutura de dados sob estresse em tempo real. |

## Produto da etapa
Um objetivo geral e quatro objetivos específicos.

## Checklist
- [x] Os objetivos começam com verbos no infinitivo.
- [x] O objetivo geral responde ao problema.
- [x] Os objetivos específicos detalham o objetivo geral.
- [x] Os objetivos são compatíveis com uma revisão bibliográfica.