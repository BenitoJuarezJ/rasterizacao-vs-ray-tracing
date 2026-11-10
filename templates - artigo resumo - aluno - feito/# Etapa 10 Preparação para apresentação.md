# Etapa 10 Preparação da apresentação

## Solicitação

Prepare uma apresentação clara do artigo e organize a participação do grupo.

## Dados da apresentação

- Título do artigo: Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos
- Evento ou disciplina: Mostra de Tecnologia 2026.2 / Computabilidade e Complexidade de Algoritmos (Ciência da Computação)
- Orientadora: Profa. Andrea Ono Sakai
- Data: 20/09/2026
- Tempo disponível: 12 minutos (mínimo exigido: 10 minutos; 3 minutos por integrante)
- Integrantes: Augusto da Silva Domingues, Benito Juarez Jesus Viana Aguiar, Renan Veras de Andrade, Thiago de Luca Fernandes

## Estrutura

| Parte | Conteúdo principal | Responsável | Tempo |
|---|---|---|---:|
| Abertura (Slides 1 e 2) | Apresentação do grupo, contextualização do tema, recorte algorítmico (exclusão de variáveis estéticas subjetivas) e definição da problemática central: divergência assintótica e de memória entre matrizes Z-buffer $\mathcal{O}(N)$ e árvores BVH $\mathcal{O}(\log N)$. | Augusto da Silva Domingues | 2 min |
| Objetivos (Slide 3) | Exposição do objetivo geral (comparar complexidade Big-O e *footprint* de VRAM sob estresse geométrico) e dos objetivos específicos (mapear curvas teóricas, contrastar ocupação de memória/atualização e verificar a existência de um limiar matemático na literatura). | Augusto da Silva Domingues | 1 min |
| Metodologia (Slide 4) | Detalhamento da revisão bibliográfica qualitativa e comparativa (busca em 16/09/2026 nas bases IEEE Xplore, ACM DL e Scopus), descritores booleanos e funil de seleção PRISMA via Zotero (431 brutos $\rightarrow$ 389 sem duplicatas $\rightarrow$ 18 lidos integralmente $\rightarrow$ 5 incluídos, publicados entre 2006 e 2021). | Renan Veras de Andrade | 3 min |
| Fundamentação e Resultados da revisão (Slides 5 e 6) | Apresentação dos 2 eixos teóricos — Eixo 1 Matricial $\mathcal{O}(W \times H)$ vs. Eixo 2 Hierárquico $\mathcal{O}(\log N)$ — e síntese dos achados empíricos, convergências, divergências e lacunas nos 5 artigos (Lambru et al., 2021; Wyman et al., 2016; Woop et al., 2006; Crassin et al., 2011; Ritschel et al., 2012). | Thiago de Luca Fernandes | 3 min |
| Conclusão (Slides 7, 8, 9 e 10) | Resposta direta ao problema de pesquisa (ausência de vencedor absoluto e desmistificação do gargalo único), contribuições do trabalho, limitações metodológicas da amostra, proposta de experimento controlado em hardware moderno com *RT Cores* e encerramento. | Benito Juarez Jesus Viana Aguiar | 3 min |
| **Total** | **Apresentação completa (Slides 1 a 10)** | **4 integrantes (equilibrado)** | **12 min** |

---

## Roteiro Detalhado de Fala por Integrante (Guia para manter os 10–12 minutos)

### Bloco 1: Augusto da Silva Domingues (3 minutos — Slides 1, 2 e 3)
* **Slides 1 e 2 (Identificação e Introdução — Problemática e Justificativa) [2 min]:**
  * Cumprimentar a banca e a Profa. Andrea Ono Sakai, apresentando o Grupo 8 e o título da pesquisa.
  * Explicar que a indústria de computação gráfica vive uma transição entre dois paradigmas estruturais de visibilidade: a rasterização tradicional via matriz bidimensional (Z-buffer) e o traçado de raios acelerado por particionamento espacial em árvore (*Bounding Volume Hierarchy* — BVH).
  * Destacar a **justificativa e o recorte rigoroso**: ao contrário de trabalhos que avaliam fotorrealismo ou estética visual, nossa pesquisa isola variáveis subjetivas para investigar estritamente a matemática algorítmica, o consumo de memória de vídeo (VRAM), o comportamento de cache e o custo de atualização estrutural.
  * Enunciar a **problemática**: *Como a complexidade assintótica e o consumo de memória divergem entre o Z-buffer $\mathcal{O}(N)$ e a BVH $\mathcal{O}(\log N)$ ao escalar primitivas em tempo real?*
* **Slide 3 (Introdução — Objetivo Geral e Específicos) [1 min]:**
  * Apresentar o **Objetivo Geral**: analisar comparativamente a complexidade assintótica (Big-O) e o custo estrutural de memória (*footprint*) entre Z-buffer e BVH sob alta carga geométrica.
  * Conectar os **Objetivos Específicos**: (1) mapear as curvas $\mathcal{O}(N)$ vs. $\mathcal{O}(\log N)$ na literatura; (2) contrastar a ocupação de VRAM e o custo de reconstrução/atualização por quadro; e (3) verificar se a literatura estabelece uma equação ou limiar exato de ponto de virada (antecipando que a revisão revelou que esse limiar fixo não é definido de forma isolada na literatura).

### Bloco 2: Renan Veras de Andrade (3 minutos — Slide 4)
* **Slide 4 (Metodologia da Revisão) [3 min]:**
  * **Passo 01 (Tipo de revisão):** Explicar que se trata de uma revisão bibliográfica qualitativa e comparativa, executada em 16/09/2026 e estruturada em dois eixos temáticos (estruturas matriciais vs. estruturas hierárquicas).
  * **Passo 02 (Bases de dados):** Justificar a escolha das três principais bases de ciência da computação e engenharia de hardware gráfico: **IEEE Xplore** (215 resultados), **ACM Digital Library** (134 resultados) e **Scopus** (82 resultados), somando **431 registros brutos**.
  * **Passo 03 (Descritores):** Detalhar como foram combinados com operadores booleanos (`AND` / `OR`) os termos *"Ray tracing"*, *"BVH"*, *"Rasterization"*, *"Z-buffer"*, *"Real-time rendering"*, *"Complexity"* e *"Performance"*.
  * **Passo 04 (Critérios e Triagem PRISMA no Zotero):** Explicar o rigor metodológico: exigimos artigos em inglês, revisados por pares (*peer-reviewed*), com métricas algorítmicas/memória, excluindo TCCs, literatura cinzenta e artigos puramente estéticos. Dos 431 registros, removemos 42 duplicatas no Zotero (restando 389 para triagem de título/resumo), selecionamos 18 para leitura integral e aprovamos o corpus definitivo de **5 estudos fundamentais (2006–2021)**.

### Bloco 3: Thiago de Luca Fernandes (3 minutos — Slides 5 e 6)
* **Slide 5 (Fundamentação Teórica) [1 min 15 s]:**
  * Explicar o **conceito central** fundamentado em Ritschel et al. (2012): de um lado, a visibilidade por matriz 2D contígua na memória de vídeo com custo espacial atrelado à resolução $\mathcal{O}(W \times H)$ e processamento linear $\mathcal{O}(N)$ sobre as primitivas; de outro, o particionamento espacial tridimensional em árvores com busca logarítmica $\mathcal{O}(\log N)$.
  * Mostrar a divisão nos dois eixos de análise: **Eixo 1 (Matricial)** cobrindo Z-buffer tradicional, *Reflective Shadow Maps* (RSM) e *Irregular Z-Buffer* (IZB); e **Eixo 2 (Hierárquico)** cobrindo BVH, árvores *B-KD* (Woop et al., 2006) e *Sparse Voxel Octrees* (Crassin et al., 2011).
* **Slide 6 (Resultados e Discussão) [1 min 45 s]:**
  * **Principais achados quantitativos:**
    * *Lambru et al. (2021):* Com geometria fixa em $262.038$ triângulos, apenas dobrar a resolução da matriz RSM de $512^2$ para $1024^2$ derruba o desempenho em cerca de $50\%$ dos FPS por saturação do cache da TMU.
    * *Wyman et al. (2016):* O *Irregular Z-Buffer* tem complexidade $\mathcal{O}(N)$ (fragmentos $\times$ comprimento médio das listas) e reconstrói a estrutura do zero em menos de $2\text{ ms}$, mas em cenas extremas ($11,7\text{ milhões}$ de triângulos, *San Miguel*) o quadro atinge $162,9\text{ ms}$ devido à contenção atômica na criação das listas.
    * *Woop et al. (2006) e Crassin et al. (2011):* A arquitetura DRPU com árvore B-KD alcança $94\%$ a $98\%$ de acerto de cache L1 consumindo apenas $73\text{ a }210\text{ MB/s}$ de banda DRAM quando há movimentos coerentes; já a *Sparse Voxel Octree* exige cerca de $1\text{ GB}$ de VRAM ($512^3$) e adiciona $+5,5\text{ ms}$ para atualizar um único objeto dinâmico ($70\text{ mil}$ triângulos).
  * **Convergências, Divergências e Lacunas:** Destacar que todos convergem que o gargalo deixou de ser apenas aritmético e passou a ser de memória e atualização, mas cada artigo identifica um gargalo específico (cache TMU, contenção atômica, coerência de movimento, VRAM ou divergência de execução SIMD). Apontar as lacunas: inexistência de equação do ponto de virada, ausência de testes em *RT Cores* modernos e falta de benchmarks em 4K comparativos.

### Bloco 4: Benito Juarez Jesus Viana Aguiar (3 minutos — Slides 7, 8, 9 e 10)
* **Slide 7 (Considerações Finais) [2 min]:**
  * **Síntese (Resposta ao Problema):** Concluir que não há vencedor absoluto. O Z-buffer garante acesso contíguo e previsível em memória sem custo de construção topológica, mas degrada severamente com o aumento da resolução e *overdraw*. Já a BVH e estruturas hierárquicas reduzem a busca geométrica para escala logarítmica $\mathcal{O}(\log N)$, mas transferem o custo para o consumo de VRAM, manutenção/atualização da árvore em cenas dinâmicas e divergência de *threads* na GPU.
  * **Contribuições:** O estudo entrega o mapeamento rigoroso dos **5 gargalos arquiteturais reais** na literatura revisada por pares, desmistificando a ideia simplista de um único fator limitante isolado.
  * **Limitações:** Reconhecer com transparência científica que o corpus reúne 5 estudos avaliados em hardwares e épocas distintas (2006 a 2021), com foco em iluminação global/sombras e incluindo estruturas parentes da BVH (como B-KD tree e SVO).
  * **Estudos Futuros:** Propor a execução de um experimento prático controlado em uma mesma GPU moderna (equipada com *RT Cores*), escalando progressivamente a contagem de triângulos de 1080p a 4K para medir empiricamente o tempo de construção da BVH, o *footprint* de VRAM e a taxa de *cache miss*.
* **Slides 8, 9 e 10 (Referências, Agradecimentos e Encerramento) [1 min]:**
  * Apresentar brevemente as 5 referências oficiais que sustentam os dados (Crassin, Lambru, Ritschel, Woop e Wyman).
  * Ler ou destacar o espírito da citação de Ritschel et al. (2012, p. 161) sobre os *trade-offs* computacionais inevitáveis na renderização interativa, agradecer à orientadora Profa. Andrea Ono Sakai e colocar o grupo à disposição da banca para perguntas.

---

## Mensagem principal

Não existe uma supremacia absoluta entre a rasterização via Z-buffer $\mathcal{O}(N)$ e o Ray Tracing acelerado por estruturas hierárquicas como BVH $\mathcal{O}(\log N)$, pois o verdadeiro limite de desempenho em tempo real deslocou-se do cálculo aritmético puro para a hierarquia de memória da GPU. Enquanto matrizes de profundidade oferecem acesso contíguo e reconstrução imediata a cada quadro, mas sofrem com o aumento de resolução e *overdraw*, as árvores espaciais escalam logaritmicamente na busca geométrica, porém impõem custos severos de ocupação de VRAM, atualização topológica em cenas dinâmicas e divergência de execução paralela.

## Perguntas esperadas

1. **Pergunta:** *Vocês propuseram nos objetivos específicos verificar o ponto de intersecção (ponto de virada) em que o Ray Tracing via BVH supera o Z-buffer. Por que não apresentaram um número exato de polígonos para esse limiar?*  
   **Resposta:** Porque a auditoria rigorosa da literatura demonstrou que esse ponto de virada não é uma constante matemática universal dependente apenas do número de triângulos $N$. Como provam os estudos analisados (Lambru et al., 2021; Wyman et al., 2016; Woop et al., 2006), o cruzamento de eficiência varia drasticamente conforme a resolução da matriz (ex.: de 1080p para 4K), o grau de *overdraw*, a coerência espacial dos movimentos na cena (que define se a árvore pode sofrer apenas *refit* ou precisa de reconstrução completa) e a arquitetura de cache da GPU. Identificar essa lacuna de padronização na literatura foi justamente um dos resultados científicos mais importantes da nossa revisão.

2. **Pergunta:** *Por que o corpus final incluiu artigos que utilizam B-KD Trees (Woop et al., 2006) e Sparse Voxel Octrees (Crassin et al., 2011) se o tema menciona especificamente BVH?*  
   **Resposta:** A *B-KD Tree* (uma variante unidimensional de BVH baseada em intervalos delimitadores) e a *Sparse Voxel Octree* pertencem à mesma família de estruturas hierárquicas de particionamento e delimitação espacial 3D com complexidade de travessia logarítmica $\mathcal{O}(\log N)$. Na literatura selecionada via protocolo PRISMA, esses trabalhos são os que fornecem as métricas arquiteturais mais transparentes e isoladas sobre largura de banda de DRAM ($73\text{ a }210\text{ MB/s}$), taxa de acerto de cache L1 ($94\%\text{ a }98\%$), consumo de VRAM ($\sim 1\text{ GB}$) e tempo de atualização de nós dinâmicos ($+5,5\text{ ms}$), permitindo contrastar diretamente o paradigma hierárquico em árvore contra o paradigma matricial do Z-buffer.

3. **Pergunta:** *Se o Ray Tracing possui complexidade de busca $\mathcal{O}(\log N)$, por que ele ainda enfrenta tanta dificuldade de desempenho nas GPUs em comparação à varredura $\mathcal{O}(N)$ do Z-buffer?*  
   **Resposta:** Conforme fundamentado por Ritschel et al. (2012) e Wyman et al. (2016), isso ocorre devido à arquitetura massivamente paralela (SIMD) das GPUs. O Z-buffer realiza acessos altamente regulares e contíguos à memória e reconstrói seu estado em menos de $2\text{ ms}$ sem manter árvores complexas. Já na travessia de uma árvore BVH, raios vizinhos (especialmente raios secundários de iluminação ou sombra) tomam caminhos diferentes nos nós da árvore, gerando **divergência de execução (*branch divergence*)** nas *threads* da GPU e **acessos incoerentes à memória (*cache misses*)**, além do custo de atualizar a estrutura sempre que os polígonos se movem.

4. **Pergunta:** *No artigo de Wyman et al. (2016), o que significa exatamente a complexidade $\mathcal{O}(N)$ do Irregular Z-Buffer e qual foi o gargalo encontrado na cena mais pesada?*  
   **Resposta:** No *Frustum-Traced Irregular Z-Buffer*, os autores demonstram que o custo do teste de visibilidade escala linearmente $\mathcal{O}(N)$ com o número de fragmentos de imagem multiplicado pelo comprimento médio das listas encadeadas por *texel*. Na cena de estresse máximo (*San Miguel*, com $11,7\text{ milhões}$ de triângulos), o tempo total subiu para $162,9\text{ ms}$ não por falha na travessia em si, mas pela **contenção atômica de memória** durante a construção concorrente dessas listas irregulares na GPU.

## Checklist

- [x] A apresentação respeita o tempo (planejada para 12 minutos, garantindo o mínimo de 10 minutos).
- [x] Os slides possuem pouco texto e boa legibilidade (10 slides concisos e estruturados em cards).
- [x] As fontes das imagens e dados foram informadas (referências ABNT nos slides 8 e 9 e citações diretas nos slides 4, 5, 6 e 9).
- [x] Todos conhecem o problema, o método e as conclusões.
- [x] O grupo realizou pelo menos um ensaio completo.
- [x] Os integrantes estão preparados para responder perguntas.