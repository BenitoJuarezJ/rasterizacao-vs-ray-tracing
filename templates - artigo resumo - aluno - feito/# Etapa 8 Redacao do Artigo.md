# Etapa 8 Redação do artigo

# Título

ANÁLISE COMPARATIVA DO CUSTO COMPUTACIONAL E DA COMPLEXIDADE ASSINTÓTICA ENTRE A RASTERIZAÇÃO TRADICIONAL VIA Z-BUFFER E O RAY TRACING ACELERADO POR BOUNDING VOLUME HIERARCHY (BVH) EM CENÁRIOS DE ALTA CONTAGEM DE POLÍGONOS

## Resumo

A rasterização com Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) são os dois paradigmas principais da renderização em tempo real, e seus custos computacionais e de memória evoluem de formas distintas com o aumento da contagem de polígonos. Este trabalho teve como objetivo analisar comparativamente a complexidade assintótica e o custo de memória dessas duas estruturas sob alta carga geométrica. Realizou-se uma revisão bibliográfica qualitativa, com busca em 16/09/2026 nas bases IEEE Xplore, ACM Digital Library e Scopus, que retornou 431 resultados; após remoção de duplicatas, triagem por título e resumo e leitura completa, cinco estudos foram incluídos e organizados em dois eixos: limites do Z-buffer e estruturas hierárquicas espaciais. Os achados indicam que o Z-buffer oferece acesso regular, mas estruturas matriciais perdem eficiência com o aumento da resolução e com extensões irregulares, enquanto as estruturas hierárquicas reduzem o custo de consulta, mas seu desempenho passa a depender de memória, cache, coerência de movimento na atualização e divergência de execução. Conclui-se que os estudos revisados apontam gargalos diferentes conforme a arquitetura analisada — convergindo no fato de que o custo deixa de ser puramente aritmético e passa a depender de acesso à memória, cache e atualização da estrutura — e que a literatura não define o ponto de virada entre os dois paradigmas, indicando a necessidade de estudos experimentais comparativos em um mesmo hardware.

## Palavras-chave

Z-buffer. Bounding Volume Hierarchy. Ray tracing. Rasterização. Complexidade assintótica. Memória.

## Introdução

A síntese de imagens em tempo real divide-se, em linhas gerais, entre dois paradigmas. A rasterização com Z-buffer percorre as primitivas geométricas da cena e resolve a visibilidade por meio de uma matriz bidimensional de profundidade, com uma comparação de custo constante por pixel e acesso contíguo à memória. O Ray Tracing, por sua vez, percorre os pixels e lança raios contra a cena, apoiando-se em estruturas espaciais hierárquicas, como a Bounding Volume Hierarchy (BVH), para evitar testar cada raio contra todos os polígonos. À medida que a contagem de polígonos das cenas cresce, a indústria gráfica vem deslocando parte de seus pipelines da varredura linear para a travessia de árvores, o que torna relevante entender onde cada estrutura de dados encontra seus limites.

O foco desta revisão é o custo computacional e o custo de memória dessas duas estruturas: de um lado, a matriz bidimensional de profundidade, cujo tempo de varredura cresce de forma linear, $O(N)$, com o número de primitivas e cuja ocupação é proporcional à resolução, $O(W \times H)$; de outro, a travessia de árvores espaciais, cujo custo por raio tende a $O(\log N)$, mas que exige memória adicional para armazenar a hierarquia e esforço para reconstruí-la ou atualizá-la quando a cena é dinâmica.

A literatura analisada indica que o desempenho de ambas as abordagens costuma ser discutido a partir de benchmarks isolados, em hardwares e cenas distintos, e não a partir de uma formulação que permita comparar diretamente os dois paradigmas. Não há, nos trabalhos revisados, uma definição matemática do ponto de virada, isto é, da quantidade de polígonos a partir da qual construir e percorrer a árvore compensa a varredura linear. Essa lacuna é relevante porque a escolha entre os paradigmas depende, na prática, tanto da contagem de primitivas quanto das restrições de memória e cache do hardware.

Diante disso, o objetivo deste trabalho é analisar comparativamente a complexidade assintótica e o custo de memória das estruturas Z-buffer e BVH em pipelines de renderização em tempo real sob alta carga geométrica, a partir de uma revisão bibliográfica de cinco estudos selecionados.

## Metodologia

Trata-se de uma revisão bibliográfica de natureza qualitativa e comparativa, com busca estruturada em bases acadêmicas e análise por eixos temáticos. Antes da busca, o grupo definiu os conceitos centrais (computação gráfica, rasterização e Z-buffer, Ray Tracing e BVH, complexidade e desempenho), seus equivalentes em português e inglês, e os critérios de inclusão e exclusão.

A busca foi realizada em 16/09/2026, sem filtro de ano, em três bases: IEEE Xplore, ACM Digital Library e Scopus. Cada base foi consultada com uma string de busca, combinando operadores booleanos entre os termos em inglês:

- **IEEE Xplore:** `("Ray tracing" OR "BVH") AND ("Rasterization" OR "Z-buffer") AND ("Complexity" OR "Performance")`, que retornou 215 resultados;
- **ACM Digital Library:** `("Bounding Volume Hierarchy" OR "BVH") AND ("Z-buffer" OR "Rasterization") AND "Performance"`, com 134 resultados;
- **Scopus:** `("Real-time rendering") AND ("asymptotic complexity" OR "computational cost") AND ("Ray tracing")`, com 82 resultados.

Foram obtidos 431 resultados no total. Após a remoção de 42 duplicatas, 389 registros foram avaliados por título e resumo. Desses, 18 seguiram para leitura completa, e 5 compuseram o conjunto final.

Os critérios de inclusão foram: trabalhos revisados por pares; texto em inglês; publicação em anais de conferências ou periódicos acadêmicos reconhecidos; aderência à engenharia e à matemática de algoritmos de renderização; e disponibilidade do texto integral. Foram excluídos: duplicatas; trabalhos centrados em estética, direção de arte e qualidade visual; trabalhos de conclusão de curso e relatórios técnicos sem revisão por pares; e publicações sem resumo ou sem DOI válido.

Cada artigo incluído foi atribuído a um integrante do grupo, registrado em fichamento (com problema investigado, objetivo, método, dados, resultados, limitações, contribuição e comentário crítico) e auditado a partir dos textos integrais na revisão final, registrando-se que a leitura de Wyman, Hoetzlein e Lefohn (2016) foi realizada na versão de conferência I3D (2015) do mesmo trabalho. Os fichamentos foram então organizados em uma matriz de síntese, que agrupou os estudos por eixos temáticos e registrou convergências, divergências, limitações e lacunas. A análise é qualitativa: os valores numéricos citados (FPS e milissegundos) provêm dos próprios estudos, foram obtidos em hardwares e cenas diferentes e, por isso, não são comparados entre si de forma direta.

## Revisão da literatura

### Rasterização e Z-buffer: limites de memória e de acesso

A rasterização com Z-buffer tem como vantagem a simplicidade da estrutura: uma matriz de profundidade acessada de forma contígua, com custo constante por pixel. Os estudos revisados mostram que essa vantagem se mantém enquanto a estrutura permanece regular, e que os limites aparecem quando se aumenta a resolução da matriz ou quando se introduzem listas encadeadas para consultas analíticas.

Wyman, Hoetzlein e Lefohn (2016) investigam o Irregular Z-Buffer (IZB), que armazena, por texel de uma grade no espaço da luz, uma lista encadeada dos pontos de amostra visíveis pela câmera para calcular sombras duras com precisão subpixel, avaliado em uma GeForce GTX 980. Os autores formalizam a complexidade algorítmica como $O(N)$ para $N$ testes de visibilidade entre triângulos e frustums, em que $N = t_f \langle l_{izb} \rangle$, sendo $t_f$ o número de fragmentos de triângulos gerados no espaço da luz e $\langle l_{izb} \rangle$ o comprimento médio das listas do IZB percorridas por cada fragmento. A estrutura de dados do IZB é reconstruída do zero em menos de 2 ms por quadro (entre 0,6 e 2,1 ms nos testes), mantendo desempenho interativo na maioria das cenas e escalando de forma sublinear com a resolução da tela: passar de 1080p para 2160p (4K) aumenta o custo em cerca de 2× em vez de 4×, graças à remoção antecipada de nós já totalmente ocluídos. Entretanto, o método sofre com contenção em operações atômicas ao atualizar máscaras de visibilidade e com divergência de threads quando listas adjacentes possuem comprimentos muito discrepantes, chegando a 162,9 ms por quadro (a 1080p e 32 amostras por pixel) na cena GeeBee Plane, de 11,7 milhões de triângulos. Na comparação direta com um ray tracer baseado em BVH no estado da arte (OptiX), o sistema realiza entre 0,3× e 2,6× a quantidade de testes de interseção por pixel.

Lambru et al. (2021) comparam quatro classes de técnicas de iluminação global em tempo real baseadas no pipeline de rasterização em um mesmo framework (C++/OpenGL 4.6), em uma GTX 1070, usando a cena Sponza com contagem fixa de 262 mil triângulos. A técnica baseada em mapas de sombra reflexivos (RSM), que utiliza o Z-buffer e matrizes bidimensionais no espaço da luz, perde desempenho de forma acentuada quando a resolução da matriz dobra de 512² para 1024² e quando o conjunto de amostras aumenta, caindo de 226 para 96 FPS em 720p e de 122 para 58 FPS em 1080p. Os autores explicam que uma resolução maior do RSM provoca mais falhas de cache (cache misses) na unidade de mapeamento de texturas (TMU) da GPU. O estudo também registra que técnicas de espaço de tela, como o SSDO, apresentam os menores valores de FPS (chegando a 11,6 FPS em 1080p com 400 amostras) devido à severa sobrecarga no cache da TMU ao acumular iluminação direta de grandes distâncias.

Ritschel et al. (2012), em uma revisão narrativa do estado da arte em iluminação global interativa, observam que métodos em espaço de tela utilizando um *deep framebuffer* têm a vantagem de desacoplar o custo da complexidade geométrica original, mas operam necessariamente com informação espacial incompleta devido ao recorte (*clipping*) e à oclusão de elementos fora da visão da câmera.

Comparando os três estudos, verifica-se que estruturas matriciais no pipeline de rasterização têm seu desempenho governado pela resolução e pelo padrão de acesso ao cache da TMU (Lambru et al., 2021), sofrem com informação incompleta quando restritas ao espaço de tela (Ritschel et al., 2012) e enfrentam contenção atômica e divergência de threads quando convertidas em grades de listas encadeadas (Wyman; Hoetzlein; Lefohn, 2016).

### Estruturas hierárquicas espaciais: travessia, memória e atualização

Os estudos sobre estruturas hierárquicas mostram que organizar a cena em árvores espaciais reduz o esforço de interseção geométrica, mas que o desempenho prático passa a depender do comportamento dos caches, da coerência do movimento na atualização e do consumo de memória.

Woop, Brunvand e Slusallek (2006) descrevem e estimam o desempenho da arquitetura de hardware DRPU (Dynamic Ray Processing Unit), implementada em protótipo FPGA (66 MHz) e projetada para ASIC, avaliada em dez cenas estáticas e dinâmicas a 1024 × 768. Para suportar cenas dinâmicas, os autores utilizam árvores B-KD, definidas no artigo como um tipo de Bounding Volume Hierarchy (BVH) com limites unidimensionais. Graças à execução síncrona SIMD de pacotes de quatro raios coerentes e ao uso de caches dedicados de primeiro nível, o protótipo em FPGA registra taxas de acerto de cache superiores a 90% na maioria das cenas e exige uma largura de banda externa de DRAM baixa, entre 73 e 210 MB/s (Tabela 2), alcançando de 1,7 a 5,9 FPS no FPGA e de 81,2 a 283,2 FPS na estimativa extrapolada para o ASIC DRPU8. Nas cenas dinâmicas, um *Update Processor* dedicado atualiza os limites da árvore B-KD da base para o topo (*bottom-up*) sem alterar sua estrutura, exigindo um número de ciclos cerca de duas ordens de grandeza menor que o de renderização. A limitação declarada pelos autores é que apenas cenas dinâmicas com movimento coerente (como malhas animadas por esqueleto) são tratadas com eficiência: movimentos aleatórios de triângulos geram sobreposição acentuada entre os limites dos nós filhos, forçando a travessia redundante de muitos nós.

Crassin et al. (2011) propõem o Voxel Cone Tracing, que representa a cena em uma octree esparsa de voxels (Sparse Voxel Octree) na GPU e substitui raios individuais por cones que consultam níveis pré-filtrados da árvore. Embora o resumo anuncie taxas de 25 a 70 FPS e desempenho quase independente da cena, a Seção 10 detalha os custos na cena Sponza (280 mil triângulos, octree de 9 níveis com resolução virtual de $512^3$): a construção inicial da octree estática leva cerca de 280 ms, a atualização interativa de um objeto dinâmico (mão com 16 mil triângulos) consome cerca de 5,5 ms por quadro — tempo que depende do tamanho e da quantidade de partes móveis — e a injeção e filtragem da luz leva 16 ms. Com objeto dinâmico e luz móvel, a taxa média é de 30 FPS sem cone especular e 20 FPS com um cone especular em janela de $512^2$, caindo para 11,4 FPS em resolução $1024 \times 768$ com três cones difusos e um especular. Os autores apontam como limitação central o elevado consumo de memória de vídeo, alocando cerca de 1024 MB (1 GB) de VRAM.

Lambru et al. (2021) corroboram o peso da resolução e da atualização em estruturas volumétricas ao medir o Voxel Cone Tracing em 1080p: a taxa de quadros cai de 145 FPS (grade de $64^3$) para 89 FPS (grade de $512^3$) quando o volume é construído apenas uma vez, e cai de 138 FPS ($64^3$) para 52 FPS ($512^3$) quando a voxelização contínua a cada quadro está ativada. Ritschel et al. (2012), por sua vez, apontam que a dificuldade de mapear o ray tracing de Monte Carlo para GPUs reside na incoerência dos raios refletidos: à medida que a iluminação se torna mais complexa, os raios (threads) divergem e o desempenho na GPU cai acentuadamente.

Em conjunto, esses trabalhos mostram que a estrutura hierárquica reduz o custo de consulta sobre a geometria, mas apresenta restrições distintas em cada implementação: necessidade de movimento coerente para evitar sobreposição de nós na atualização de limites (Woop; Brunvand; Slusallek, 2006), elevado consumo de memória (~1 GB) e custo incremental de atualização de objetos dinâmicos (Crassin et al., 2011; Lambru et al., 2021) e perda de eficiência na GPU por divergência de threads em raios incoerentes (Ritschel et al., 2012).

### Síntese crítica

**Convergências.** Os cinco estudos concordam que nenhuma das duas famílias de estruturas é isenta de custo. O Z-buffer e as representações matriciais oferecem acesso regular, mas seu custo cresce com a resolução e sofre quando estendido com listas encadeadas. As estruturas hierárquicas reduzem o trabalho de consulta por raio ou cone, mas seu desempenho real passa a depender de memória, cache, atualização da estrutura e coerência de execução. Assim, há convergência no sentido de que o custo deixa de ser puramente aritmético e passa a depender do gerenciamento de memória, cache e atualização da estrutura de dados.

**Divergências.** Os estudos apontam gargalos específicos diferentes, sem convergir em um único fator isolado: falhas de cache na TMU com o aumento da resolução e amostras (Lambru et al., 2021), contenção atômica e divergência de comprimento de listas no IZB (Wyman; Hoetzlein; Lefohn, 2016), perda de eficiência da árvore B-KD sob movimentos incoerentes apesar da baixa banda de DRAM medida (Woop; Brunvand; Slusallek, 2006), alto consumo de VRAM (~1 GB) e custo de voxelização/atualização dinâmica na octree (Crassin et al., 2011) e divergência de threads na GPU (Ritschel et al., 2012).

**Limitações da literatura revisada.** Primeiro, os estudos cobrem hardwares e arquiteturas de épocas muito distintas (de um protótipo FPGA/ASIC simulado em 2006 a uma GTX 1070 em 2021), o que impede comparar números absolutos entre si. Segundo, vários trabalhos tratam de iluminação global e sombras duras (Lambru et al., 2021; Crassin et al., 2011; Ritschel et al., 2012; Wyman; Hoetzlein; Lefohn, 2016), e não apenas da visibilidade primária com Z-buffer contra BVH. Terceiro, nenhum dos cinco estudos executa medições empíricas em núcleos dedicados modernos de ray tracing comercial (RT Cores), e dois deles analisam estruturas parentes da BVH (árvore B-KD e octree esparsa).

**Lacunas.** A literatura analisada não apresenta: (i) uma formulação matemática ou experimental que determine o ponto de virada exato (em contagem de polígonos) em que construir e percorrer uma BVH passa a compensar a varredura linear do Z-buffer; (ii) medições comparáveis, em um mesmo hardware, do custo de reconstruir ou atualizar uma BVH quadro a quadro frente ao custo de reiniciar o Z-buffer; e (iii) avaliações do Z-buffer convencional em resoluções altas como 2160p (4K) comparadas diretamente à BVH, visto que, entre os estudos revisados, apenas Wyman, Hoetzlein e Lefohn (2016) chegam a 2160p, mas utilizando uma estrutura irregular (IZB).

## Considerações finais

Esta revisão procurou responder como a complexidade assintótica e o consumo de memória divergem entre a rasterização com Z-buffer e o Ray Tracing acelerado por BVH quando a quantidade de primitivas cresce. Com base nos cinco estudos analisados, conclui-se que não há uma estrutura vencedora absoluta: o Z-buffer oferece acesso regular e previsível, mas o custo das estruturas matriciais cresce fortemente com a resolução e sofre com contenção quando estendido para listas por texel; já a BVH e estruturas hierárquicas parentes reduzem o custo assintótico da consulta geométrica, mas seu desempenho prático passa a depender da organização de memória e cache, da coerência do movimento na atualização da árvore e da divergência de execução nas GPUs.

Diferentemente da hipótese de um gargalo único, a revisão identificou que cada estudo aponta um fator limitante distinto (cache da TMU, contenção atômica, movimentos incoerentes, consumo e atualização de memória ou divergência de threads), convergindo na constatação mais ampla de que o desempenho em tempo real não depende apenas do cálculo aritmético de interseção, mas da arquitetura de memória e da manutenção da estrutura. Em contrapartida, o objetivo específico de determinar o ponto de interseção computacional entre as duas técnicas não pôde ser plenamente atendido, pois a literatura selecionada não define esse limiar e os experimentos originais foram conduzidos em hardwares, resoluções e problemas distintos.

Como desdobramentos futuros, recomendam-se: (i) a realização de um experimento controlado em um mesmo hardware moderno (com suporte a RT Cores), escalando progressivamente a contagem de triângulos de cenas idênticas em 1080p e 4K (2160p); (ii) a medição separada do tempo de construção/atualização da BVH e do tempo de travessia em cenas estáticas e com movimentos coerentes e incoerentes; e (iii) a medição direta do consumo de VRAM e da taxa de acerto de cache nos dois pipelines.

## Referências

CRASSIN, C. et al. Interactive indirect illumination using voxel cone tracing. **Computer Graphics Forum**, v. 30, n. 7, p. 1921-1930, 2011. DOI: [https://doi.org/10.1111/j.1467-8659.2011.02063.x](https://doi.org/10.1111/j.1467-8659.2011.02063.x).

LAMBRU, C. et al. Comparative analysis of real-time global illumination techniques in current game engines. **IEEE Access**, v. 9, p. 125158-125183, 2021. DOI: [https://doi.org/10.1109/ACCESS.2021.3109663](https://doi.org/10.1109/ACCESS.2021.3109663).

RITSCHEL, T. et al. The state of the art in interactive global illumination. **Computer Graphics Forum**, v. 31, n. 1, p. 160-188, 2012. DOI: [https://doi.org/10.1111/j.1467-8659.2012.02093.x](https://doi.org/10.1111/j.1467-8659.2012.02093.x).

WOOP, S.; BRUNVAND, E.; SLUSALLEK, P. Estimating performance of a ray-tracing ASIC design. In: IEEE SYMPOSIUM ON INTERACTIVE RAY TRACING, 2006, Salt Lake City. **Proceedings** [...]. Salt Lake City: IEEE, 2006. p. 7-14. DOI: [https://doi.org/10.1109/RT.2006.280209](https://doi.org/10.1109/RT.2006.280209).

WYMAN, C.; HOETZLEIN, R.; LEFOHN, A. Frustum-traced irregular Z-buffers: fast, sub-pixel accurate hard shadows. **IEEE Transactions on Visualization and Computer Graphics**, v. 22, n. 10, p. 2249-2261, 2016. DOI: [https://doi.org/10.1109/TVCG.2016.2572689](https://doi.org/10.1109/TVCG.2016.2572689).

## Checklist

- [x] A introdução termina com o objetivo.
- [x] A metodologia descreve o processo realmente realizado.
- [x] A revisão compara os artigos.
- [x] A conclusão responde ao problema.
- [x] O resumo representa o texto completo.
