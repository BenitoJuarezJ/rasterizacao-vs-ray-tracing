# Etapa 7 Matriz de síntese e organização da revisão

## Solicitação

Compare os artigos e organize a revisão por temas ou eixos. Não produza apenas uma sequência de resumos.

## Eixos da revisão

1. Rasterização e Z-buffer: limites de memória, resolução e acesso
2. Estruturas hierárquicas espaciais: travessia, memória e atualização
3. Comparativo entre paradigmas: diversidade de gargalos e lacunas na literatura

## Matriz de síntese

| Eixo | Artigos relacionados | Convergências | Divergências | Limitações | Lacunas |
|---|---|---|---|---|---|
| 1. Rasterização e Z-buffer | Wyman et al. (2016); Lambru et al. (2021); Ritschel et al. (2012) | A representação matricial oferece acesso regular e eficiente enquanto permanece simples, mas perde desempenho quando a resolução cresce, quando precisa de dados fora da tela ou quando armazena listas por texel. | Lambru et al. (2021) apontam falhas de cache na TMU com o aumento de resolução/amostras; Wyman et al. (2016) identificam contenção atômica e divergência no comprimento das listas do IZB; Ritschel et al. (2012) destacam a incompletude espacial do framebuffer. | Lambru et al. (2021) mantêm a contagem de polígonos fixa (262k); Wyman et al. (2016) avaliam sombras duras com estrutura irregular (IZB) e não o Z-buffer convencional sozinho. | Falta medir isoladamente o ponto em que o Z-buffer convencional em 4K (2160p) perde eficiência frente à travessia hierárquica ao escalar os polígonos. |
| 2. Estruturas hierárquicas espaciais | Woop et al. (2006); Crassin et al. (2011); Lambru et al. (2021); Ritschel et al. (2012) | Estruturas hierárquicas (B-KD tree e Sparse Voxel Octree) reduzem o custo de consulta em relação ao total de triângulos, mas o desempenho real depende de cache, memória e coerência de atualização/execução. | Woop et al. (2006) medem baixa banda de DRAM (73–210 MB/s) e alta taxa de acerto no cache L1 (>90%), apontando como limite movimentos incoerentes; Crassin et al. (2011) apontam o alto consumo de VRAM (~1 GB) e custo de atualização dinâmica; Ritschel et al. (2012) destacam a divergência de threads na GPU. | Woop et al. (2006) baseiam os números de ASIC em simulação/extrapolação e usam B-KD tree; Crassin et al. (2011) e Lambru et al. (2021) avaliam octrees/volumes de voxels para iluminação global. | Ausência de medições diretas do custo de reconstrução/atualização de uma BVH padrão quadro a quadro em hardware moderno com RT Cores frente ao Z-buffer. |
| 3. Comparativo Matriz vs. Árvore | Wyman et al. (2016); Lambru et al. (2021); Woop et al. (2006); Crassin et al. (2011); Ritschel et al. (2012) | Não há estrutura vencedora absoluta: o custo deixa de ser puramente aritmético e passa a depender de acesso à memória, cache, sincronização e manutenção da estrutura de dados. | Os estudos não convergem em um único gargalo universal, apontando causas distintas conforme o algoritmo (cache da TMU, contenção atômica, movimentos incoerentes, consumo de VRAM ou divergência de execução). | Hardwares de épocas muito distintas (2006 a 2021) e foco predominante em sombras e iluminação global, impedindo comparação direta dos números absolutos de FPS/ms. | A literatura revisada não apresenta uma formulação matemática nem experimental que defina o ponto de virada (em número de polígonos) entre Z-buffer e BVH. |

## Roteiro da revisão da literatura

### Eixo 1 — Rasterização e Z-buffer: limites de memória, resolução e acesso

- Ideia principal: O Z-buffer convencional é eficiente pelo acesso regular, mas o custo de estruturas matriciais cresce acentuadamente com a resolução e sofre com contenção e perda de coerência quando estendido para armazenar listas encadeadas.
- Evidências que serão usadas: A queda de FPS quase pela metade ao dobrar a matriz do RSM de 512² para 1024² e a sobrecarga da TMU no SSDO em Lambru et al. (2021); a complexidade $O(N)$ com $N = t_f \langle l_{izb} \rangle$, a reconstrução em menos de 2 ms, o custo de 162,9 ms na cena GeeBee Plane (11,7M triângulos) e a escala sublinear de 1080p para 2160p (~2×) em Wyman et al. (2016); e a limitação de informação espacial incompleta em espaço de tela apontada por Ritschel et al. (2012).
- Comparação entre estudos: Lambru et al. (2021) e Wyman et al. (2016) fornecem medições empíricas em GPUs distintas mostrando gargalos de acesso (falhas na TMU vs. contenção atômica e divergência nas listas), enquanto Ritschel et al. (2012) fundamentam conceitualmente a limitação do espaço de tela.
- Ligação com o problema: Demonstra como o custo da abordagem baseada em matriz e suas extensões se comporta diante do aumento da resolução, da quantidade de amostras e da densidade geométrica.

### Eixo 2 — Estruturas hierárquicas espaciais: travessia, memória e atualização

- Ideia principal: Estruturas hierárquicas espaciais reduzem o esforço de consulta geométrica, mas seu desempenho prático depende da coerência dos movimentos na atualização, do consumo de memória de vídeo e da coerência de execução das threads.
- Evidências que serão usadas: Os dados da arquitetura DRPU com árvores B-KD de Woop et al. (2006) (acerto de cache L1 > 90%, banda de DRAM baixa de 73 a 210 MB/s, ciclos de atualização duas ordens de grandeza abaixo da renderização e restrição a movimentos coerentes); os resultados da Sparse Voxel Octree de Crassin et al. (2011) (consumo de ~1 GB de VRAM, 280 ms para construção estática, ~5,5 ms para atualizar objeto dinâmico de 16k triângulos e 11,4 a 30 FPS em Sponza); a queda de 145 para 89 FPS (64³ para 512³) no Voxel Cone Tracing medida por Lambru et al. (2021); e a divergência de threads em GPU destacada por Ritschel et al. (2012).
- Comparação entre estudos: Os estudos convergem quanto ao ganho da hierarquia na fase de consulta, mas divergem no gargalo principal: Woop et al. (2006) mostram baixa banda de memória graças aos caches e apontam a perda de eficiência em movimentos incoerentes, ao passo que Crassin et al. (2011) e Lambru et al. (2021) evidenciam o alto consumo de memória e o custo de resolução/atualização do volume, e Ritschel et al. (2012) enfatizam a divergência de ramos na GPU.
- Ligação com o problema: Esclarece as exigências de memória, cache e atualização que acompanham a redução do custo de busca nas estruturas em árvore.

## Síntese crítica provisória

A literatura analisada demonstra que não há uma estrutura vencedora absoluta entre o paradigma matricial e o hierárquico, nem um único gargalo universal que explique isoladamente o limite de ambos. Enquanto estruturas baseadas em matrizes no pipeline de rasterização oferecem acesso regular, mas sofrem com o crescimento da resolução e falhas de cache na TMU (Lambru et al., 2021), com informação espacial incompleta (Ritschel et al., 2012) ou com contenção atômica e divergência ao introduzir listas encadeadas (Wyman et al., 2016), as estruturas espaciais hierárquicas reduzem o custo de consulta, mas dependem de movimentos coerentes para atualização eficiente (Woop et al., 2006), exigem elevada alocação de memória de vídeo e tempo de atualização (Crassin et al., 2011) e sofrem com divergência de execução na GPU (Ritschel et al., 2012). Assim, os estudos convergem no sentido de que o custo deixa de ser puramente aritmético e passa a depender do acesso à memória, do cache e da manutenção da estrutura, mas permanecem lacunas importantes: apenas Wyman et al. (2016) avaliam resoluções até 2160p (em estrutura irregular, e não no Z-buffer convencional) e nenhum dos trabalhos define matematicamente o ponto de virada entre Z-buffer e BVH.

## Checklist

- [x] Os artigos foram agrupados por ideias.
- [x] Há comparações entre estudos.
- [x] As divergências foram registradas.
- [x] As lacunas são específicas e sustentadas pelas leituras.
