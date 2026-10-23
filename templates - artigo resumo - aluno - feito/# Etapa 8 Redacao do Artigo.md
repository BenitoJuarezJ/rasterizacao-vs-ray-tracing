# Etapa 8 Redação do artigo

# Título

Z-buffer e BVH sob alta carga geométrica: uma revisão da literatura sobre complexidade assintótica e custo de memória na renderização em tempo real

## Palavras-chave

Z-buffer; Bounding Volume Hierarchy; Ray tracing; Rasterização; Complexidade assintótica; Largura de banda de memória;

## Introdução

A síntese de imagens em tempo real divide-se, em linhas gerais, entre dois paradigmas. A rasterização com Z-buffer percorre as primitivas geométricas da cena e resolve a visibilidade por meio de uma matriz bidimensional de profundidade, com uma comparação de custo constante por pixel e acesso contíguo à memória. O Ray Tracing, por sua vez, percorre os pixels e lança raios contra a cena, apoiando-se em estruturas espaciais hierárquicas, como a Bounding Volume Hierarchy (BVH), para evitar testar cada raio contra todos os polígonos. À medida que a contagem de polígonos das cenas cresce, a indústria gráfica vem deslocando parte de seus pipelines da varredura linear para a travessia de árvores, o que torna relevante entender onde cada estrutura de dados encontra seus limites.

O foco desta revisão é o custo computacional e o custo de memória dessas duas estruturas: de um lado, a matriz bidimensional de profundidade, cujo tempo de varredura cresce de forma linear, $O(N)$, com o número de primitivas e cuja ocupação é proporcional à resolução, $O(W \times H)$; de outro, a travessia de árvores espaciais, cujo custo por raio tende a $O(\log N)$, mas que exige memória adicional para armazenar a hierarquia e esforço para reconstruí-la ou atualizá-la quando a cena é dinâmica.

A literatura analisada indica que o desempenho de ambas as abordagens costuma ser discutido a partir de benchmarks isolados, em hardwares e cenas distintos, e não a partir de uma formulação que permita comparar diretamente os dois paradigmas. Não há, nos trabalhos revisados, uma definição matemática do ponto de virada, isto é, da quantidade de polígonos a partir da qual construir e percorrer a árvore compensa a varredura linear. Essa lacuna é relevante porque a escolha entre os paradigmas depende, na prática, tanto da contagem de primitivas quanto das restrições de memória do hardware.

Diante disso, o objetivo deste trabalho é analisar comparativamente a complexidade assintótica e o custo de memória das estruturas Z-buffer e BVH em pipelines de renderização em tempo real sob alta carga geométrica, a partir de uma revisão bibliográfica de cinco estudos selecionados.

## Metodologia

Trata-se de uma revisão bibliográfica de natureza qualitativa e comparativa, com busca estruturada em bases acadêmicas e análise por eixos temáticos. Antes da busca, o grupo definiu os conceitos centrais (computação gráfica, rasterização e Z-buffer, Ray Tracing e BVH, complexidade e desempenho), seus equivalentes em português e inglês, e os critérios de inclusão e exclusão.

A busca foi realizada em 16/09/2026, sem filtro de ano, em três bases: IEEE Xplore, ACM Digital Library e Scopus. Cada base foi consultada com uma string de busca, combinando operadores booleanos entre os termos em inglês:

IEEE Xplore: ("Ray tracing" OR "BVH") AND ("Rasterization" OR "Z-buffer") AND ("Complexity" OR "Performance"), que retornou 215 resultados;
ACM Digital Library: ("Bounding Volume Hierarchy" OR "BVH") AND ("Z-buffer" OR "Rasterization") AND "Performance", com 134 resultados;
Scopus: ("Real-time rendering") AND ("asymptotic complexity" OR "computational cost") AND ("Ray tracing"), com 82 resultados.

Foram obtidos 431 resultados no total. Após a remoção de 42 duplicatas, 389 registros foram avaliados por título e resumo. Desses, 18 seguiram para leitura completa, e 5 compuseram o conjunto final.

Os critérios de inclusão foram: trabalhos revisados por pares; texto em inglês; publicação em anais de conferências ou periódicos acadêmicos reconhecidos; aderência à engenharia e à matemática de algoritmos de renderização; e disponibilidade do texto integral. Foram excluídos: duplicatas; trabalhos centrados em estética, direção de arte e qualidade visual; trabalhos de conclusão de curso e relatórios técnicos sem revisão por pares; e publicações sem resumo ou sem DOI válido.

Cada artigo incluído foi lido por um integrante do grupo e registrado em um fichamento com problema investigado, objetivo, método, dados, resultados, limitações, contribuição e comentário crítico. Os fichamentos foram então organizados em uma matriz de síntese, que agrupou os estudos por eixos temáticos e registrou convergências, divergências, limitações e lacunas. A análise é qualitativa: os valores numéricos citados (FPS e milissegundos) provêm dos próprios estudos, foram obtidos em hardwares e cenas diferentes e, por isso, não são comparados entre si de forma direta.

## Revisão da literatura

### `[Eixo 1]` Rasterização e Z-buffer: limites de memória e de acesso

A rasterização com Z-buffer tem como vantagem a simplicidade da estrutura: uma matriz de profundidade acessada de forma contígua, com custo constante por pixel. Os estudos revisados mostram que essa vantagem se mantém enquanto a estrutura permanece regular, e que os limites aparecem quando se tenta estender o Z-buffer ou aumentar sua resolução.

Wyman, Hoetzlein e Lefohn (2016) investigam o Irregular Z-Buffer, que substitui o valor único de profundidade por listas encadeadas por pixel para obter visibilidade analítica em sombras, avaliado em uma GeForce GTX 980. Ao armazenar mais do que a profundidade mais próxima, os autores relatam aumento do consumo de memória de vídeo e contenção em operações atômicas quando muitas primitivas caem na mesma região, com casos de alta desordem chegando a 162 ms por quadro. Além disso, as listas podem crescer a ponto de esgotar recursos, de modo que o problema deixa de ser puramente computacional e passa a ser de armazenamento. Segundo os autores, o custo final ainda ficou em ordem de grandeza competitiva com soluções baseadas em ray tracing, como o NVIDIA OptiX. O resultado mostra que a coerência de memória, principal virtude do Z-buffer, se perde quando se introduz uma estrutura de dados irregular dentro dele.

Lambru et al. (2021) comparam quatro técnicas de iluminação global em tempo real em um mesmo framework (C++/OpenGL 4.6), em uma GTX 1070, usando a cena Sponza com 262 mil triângulos. A técnica baseada em mapas de sombra reflexivos (RSM), que depende de matrizes bidimensionais, perde desempenho de forma acentuada quando a resolução da matriz dobra de 512² para 1024², com queda próxima de metade da taxa de quadros. É importante ressaltar que esse crescimento está associado ao tamanho da matriz e não ao número de polígonos, que permaneceu fixo no experimento. O estudo também registra que técnicas de espaço de tela, como o SSDO, sofrem com a sobrecarga do cache da unidade de texturas (TMU) ao acumular dados de regiões distantes. Em síntese, os resultados sustentam que o custo de uma estrutura matricial depende fortemente da resolução e do padrão de acesso, mesmo sem variar a geometria.

Ritschel et al. (2012), em uma revisão do estado da arte em iluminação global interativa, observam que métodos em espaço de tela operam com informação espacial incompleta, pois enxergam apenas o que foi projetado no buffer. Essa limitação conceitual explica por que a rasterização recorre a aproximações quando precisa de dados globais da cena, e antecipa o movimento em direção a estruturas hierárquicas.

Comparando os três estudos, há concordância de que o Z-buffer é eficiente enquanto permanece uma matriz regular, e de que os problemas surgem quando se aumenta a resolução (Lambru et al., 2021), quando se tenta obter informação adicional além da profundidade mais próxima (Wyman; Hoetzlein; Lefohn, 2016) ou quando a informação global é necessária (Ritschel et al., 2012). As evidências, porém, são de natureza distinta: dois estudos são experimentais, em hardwares e cenas diferentes, e o terceiro é uma revisão sem testes próprios.

### `[Eixo 2]`Estruturas hierárquicas espaciais: travessia, memória e atualização

Os estudos sobre estruturas hierárquicas indicam que a travessia logarítmica reduz o trabalho de interseção, mas desloca o gargalo para a memória e para a manutenção da estrutura.

Woop, Brunvand e Slusallek (2006) estimam o desempenho de um projeto de ASIC para ray tracing, a unidade DRPU, modelada em simulação (FPGA e layout de 130 nm) e avaliada em dez malhas renderizadas em 1024 × 768. A estrutura espacial utilizada é uma árvore B-KD, equivalente em propósito à BVH, mas não idêntica a ela. Os autores concluem que o desempenho do ray tracing interativo depende fortemente do uso de cache e que a travessia da estrutura de indexação espacial demanda alta largura de banda de memória. O ray tracing, nesse cenário, é limitado pela memória e não pelo cálculo, e o desempenho depende de o cache L2 abrigar os níveis superiores da árvore. Os autores reconhecem que as projeções se baseiam em simulação, já que o ASIC não foi fabricado, e que cenas dinâmicas prejudicam o desempenho porque a reconstrução da árvore a cada quadro tem custo elevado.

Crassin et al. (2011) propõem o Voxel Cone Tracing, que converte a cena em uma Sparse Voxel Octree e traça cones por essa árvore, usando nós de menor resolução conforme a distância. O método foi avaliado em uma GTX 480 com a cena Sponza (cerca de 280 mil triângulos) e resolução virtual de voxels de 512³, e relata taxas de 11 a 20 quadros por segundo em condições de estresse, com múltiplos cones e objetos dinâmicos. A hierarquia evita buscas exaustivas e faz com que o custo de consulta cresça pouco com a geometria total, mas o consumo de memória para alocar a árvore é elevado e a atualização em ambientes dinâmicos exige modificar a estrutura a cada quadro, o que reduz parte da vantagem da travessia rápida. Vale notar que a octree esparsa é uma estrutura próxima, porém distinta, da BVH.

Lambru et al. (2021) contribuem a este eixo com a medição do Voxel Cone Tracing: a taxa de quadros cai de 145 FPS, com grade de 64³, para 89 FPS, com grade de 512³, o que ilustra que o aumento da resolução do volume também tem custo significativo na estrutura espacial. Ritschel et al. (2012) complementam o quadro ao apontar que abordagens baseadas em ray tracing exigem avaliação extensa da árvore da cena e sofrem com divergência de ramos de execução nas GPUs, além do alto custo de atualização estrutural em cenas totalmente dinâmicas, e ao indicar que estruturas hierárquicas são necessárias para escalar problemas que seriam lineares na varredura tradicional.

Em comum, os estudos mostram que a estrutura hierárquica reduz o custo assintótico da consulta, mas que o desempenho real passa a depender de memória, de cache e da atualização da estrutura. Divergem na origem principal do gargalo: Woop, Brunvand e Slusallek (2006) enfatizam a largura de banda de memória na travessia; Crassin et al. (2011) destacam o consumo de memória e o custo de atualização da estrutura; Ritschel et al. (2012) apontam a divergência de ramos de execução.

### Síntese crítica

Convergências. Os cinco estudos concordam que nenhuma das duas famílias de estruturas é isenta de custo. O Z-buffer oferece acesso regular e previsível, mas seu custo cresce com a resolução e se deteriora quando se tenta estendê-lo com estruturas irregulares. As estruturas hierárquicas reduzem o trabalho de consulta, mas cobram em memória, em cache e em atualização. Com isso, a discussão sobre desempenho nos trabalhos revisados desloca-se do custo aritmético para o acesso à memória.

Divergências. Os estudos atribuem os gargalos a causas diferentes: sobrecarga da TMU (Lambru et al., 2021), contenção atômica e crescimento das listas (Wyman; Hoetzlein; Lefohn, 2016), largura de banda na travessia (Woop; Brunvand; Slusallek, 2006), custo de atualização e consumo de memória da árvore (Crassin et al., 2011) e divergência de ramos de execução (Ritschel et al., 2012). Parte dessas diferenças reflete a escolha de problemas, hardwares e estruturas diferentes, e não necessariamente conclusões incompatíveis.

Limitações da literatura revisada. Primeiro, os estudos cobrem hardwares de épocas distintas (de uma simulação de ASIC em 2006 a uma GTX 1070 em 2021), o que impede comparar números absolutos. Segundo, vários trabalhos tratam de iluminação global e sombras (Lambru et al., 2021; Crassin et al., 2011; Ritschel et al., 2012; Wyman; Hoetzlein; Lefohn, 2016), e não da visibilidade primária com Z-buffer contra BVH, de modo que a transposição dos resultados ao recorte desta revisão é parcial. Terceiro, nenhum estudo utiliza ray tracing em hardware dedicado de produção (RT Cores), e dois dos trabalhos usam estruturas parentes da BVH (árvore B-KD e octree esparsa). Quarto, cada experimento emprega uma única cena ou poucas cenas, em resoluções baixas ou médias.

Lacunas. A literatura analisada não apresenta (i) uma formulação matemática do ponto de virada em que a construção e a travessia de uma árvore passam a compensar a varredura linear; (ii) medições comparáveis do custo de reconstruir ou atualizar a BVH quadro a quadro em cenas dinâmicas, em comparação ao custo constante de reiniciar o Z-buffer; e (iii) avaliações em resoluções mais altas, como 4K, que mostrem como a pressão sobre a matriz de profundidade evolui.

## Considerações finais

Esta revisão procurou responder como a complexidade assintótica e o consumo de memória divergem entre a rasterização com Z-buffer e o Ray Tracing acelerado por BVH quando a quantidade de primitivas cresce. Com base nos cinco estudos analisados, a resposta é que as duas abordagens apresentam perfis de custo diferentes e complementares. O Z-buffer combina estrutura simples e acesso contíguo, com ocupação proporcional à resolução, mas perde eficiência quando a resolução aumenta, quando se exige informação além da profundidade mais próxima ou quando o problema demanda dados globais da cena. As estruturas hierárquicas reduzem o custo de consulta com a escala da geometria, porém transferem o gargalo para a largura de banda de memória, para o consumo de VRAM e para a atualização da estrutura em cenas dinâmicas.

O principal avanço identificado é a convergência dos estudos em torno da memória, e não do cálculo, como fator limitante em ambos os paradigmas. Em contrapartida, o objetivo específico de determinar o ponto de interseção computacional entre as duas técnicas não pôde ser plenamente atendido: a literatura selecionada não define esse ponto, e os dados disponíveis foram obtidos em condições que não permitem calculá-lo por comparação direta. Essa limitação decorre, em parte, do tamanho reduzido do conjunto final (cinco artigos) e do fato de vários deles tratarem de iluminação global e não da visibilidade primária, e a revisão não chega a conclusões sobre a superioridade de uma técnica em termos absolutos.

Como desdobramentos específicos, sugerem-se: (i) um estudo experimental que escale a contagem de triângulos em cenas fixas e meça, em um mesmo hardware, o tempo por quadro da rasterização com Z-buffer e do ray tracing com BVH, incluindo o tempo de construção ou atualização da árvore; (ii) a medição da ocupação de memória e do tráfego de memória em ambos os pipelines, em resoluções de 1080p e 4K; e (iii) a avaliação em hardware com núcleos dedicados de ray tracing, ausente nos estudos revisados, em cenas estáticas e dinâmicas.

## Resumo

A rasterização com Z-buffer e o ray tracing acelerado por Bounding Volume Hierarchy (BVH) são os dois paradigmas principais da renderização em tempo real, e seus custos computacionais e de memória evoluem de formas distintas com o aumento da contagem de polígonos. Este trabalho teve como objetivo analisar comparativamente a complexidade assintótica e o custo de memória dessas duas estruturas sob alta carga geométrica. Realizou-se uma revisão bibliográfica qualitativa, com busca em 16/09/2026 nas bases IEEE Xplore, ACM Digital Library e Scopus, que retornou 431 resultados; após remoção de duplicatas, triagem por título e resumo e leitura completa, cinco estudos foram incluídos e organizados em dois eixos: limites do Z-buffer e estruturas hierárquicas espaciais. Os achados indicam que o Z-buffer oferece acesso regular, mas perde eficiência com o aumento da resolução e com extensões irregulares, enquanto as estruturas hierárquicas reduzem o custo de consulta, mas deslocam o gargalo para a largura de banda, o consumo de memória e a atualização da estrutura em cenas dinâmicas. Conclui-se que, nos estudos revisados, a memória é o principal fator limitante em ambos os paradigmas e que a literatura não define o ponto de virada entre eles, o que indica a necessidade de estudos experimentais comparativos em hardware moderno.

## Referências

CRASSIN, C. et al. Interactive indirect illumination using voxel cone tracing. Computer Graphics Forum, v. 30, n. 7, p. 1921-1930, 2011. DOI: https://doi.org/10.1111/j.1467-8659.2011.02063.x.

LAMBRU, C. et al. Comparative analysis of real-time global illumination techniques in current game engines. IEEE Access, v. 9, p. 125158-125183, 2021. DOI: https://doi.org/10.1109/ACCESS.2021.3109663.

RITSCHEL, T. et al. The state of the art in interactive global illumination. Computer Graphics Forum, v. 31, n. 1, p. 160-188, 2012. DOI: https://doi.org/10.1111/j.1467-8659.2012.02093.x.

WOOP, S.; BRUNVAND, E.; SLUSALLEK, P. Estimating performance of a ray-tracing ASIC design. In: IEEE SYMPOSIUM ON INTERACTIVE RAY TRACING, 2006. Proceedings [...]. IEEE, 2006. p. 7-14. DOI: https://doi.org/10.1109/RT.2006.280209.

WYMAN, C.; HOETZLEIN, R.; LEFOHN, A. Frustum-traced irregular Z-buffers: fast, sub-pixel accurate hard shadows. IEEE Transactions on Visualization and Computer Graphics, v. 22, n. 4, 2016. DOI: https://doi.org/10.1109/TVCG.2016.2572689.

## Checklist

- [x] A introdução termina com o objetivo.
- [x] A metodologia descreve o processo realmente realizado.
- [x] A revisão compara os artigos.
- [x] A conclusão responde ao problema.
- [x] O resumo representa o texto completo.