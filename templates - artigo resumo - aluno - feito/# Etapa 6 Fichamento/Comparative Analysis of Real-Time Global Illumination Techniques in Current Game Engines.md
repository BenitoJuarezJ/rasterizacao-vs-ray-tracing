# Comparative Analysis of Real-Time Global Illumination Techniques in Current Game Engines

## Etapa 6 Leitura e fichamento

**Classificação:** Contextualização

### Identificação do artigo

- Referência completa: LAMBRU, C.; MORAR, A.; MOLDOVEANU, F.; ASAVEI, V.; MOLDOVEANU, A. Comparative Analysis of Real-Time Global Illumination Techniques in Current Game Engines. *IEEE Access*, v. 9, p. 125158-125183, 2021.
- DOI ou URL: https://doi.org/10.1109/ACCESS.2021.3109663
- Base de origem: IEEE Xplore
- Texto consultado: https://ieeexplore.ieee.org/abstract/document/9527241
- Leitor responsável: Augusto da Silva Domingues
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
A alta exigência computacional das técnicas de Iluminação Global (GI) em tempo real. O artigo investiga como o desempenho (FPS) de diferentes classes de renderização (baseadas em matrizes e em árvores espaciais) se degrada ao escalar a resolução e o número de amostras na arquitetura da GPU.

### Objetivo do estudo
Avaliar e comparar quantitativamente (por meio da taxa de quadros e carga no hardware) diferentes abordagens algorítmicas de GI em tempo real, implementadas num framework comum em C++ (OpenGL 4.6), testando-as sob os mesmos parâmetros de estresse geométrico.

### Método utilizado
Implementação de quatro abordagens distintas em um mesmo pipeline:
1. Reflective Shadow Map (RSM) - representação matricial/Z-buffer modificada.
2. Light Propagation Volumes (LPV).
3. Voxel Cone Tracing - representação espacial estruturada.
4. Screen Space Directional Occlusion (SSDO).
Foram coletadas métricas de tempo de execução (FPS) utilizando uma cena de teste (Sponza Atrium com 262 mil triângulos) e variando as resoluções das estruturas de dados (ex: matrizes 512² a 1024² e malhas voxel de 64³ a 512³).

### Contexto, amostra ou dados
O hardware utilizado foi uma GPU NVIDIA GTX 1070. O limite de desempenho foi medido calculando apenas a passagem bruta de dados (sombras, oclusão ambiental e difusa indireta) nas resoluções 720p e 1080p, com contagem estática de 262 mil polígonos.

### Principais resultados
O custo computacional aumenta agressivamente de acordo com a estrutura de dados escolhida:
- O algoritmo baseado em Z-buffer modificado (RSM) apresentou forte degradação quadrática $O(N^2)$: ao dobrar a resolução matricial (de 512² para 1024²), o desempenho caiu quase pela metade.
- A estrutura espacial (Voxel Cone Tracing) provou ser extremamente custosa no cache de memória, caindo de 145 FPS (grade 64³) para parcos 89 FPS (grade 512³), demonstrando que estruturas 3D exigem largura de banda massiva.
- Técnicas de espaço de tela (SSDO) apresentaram os piores tempos de resposta devido à sobrecarga no cache da TMU (Texture Mapping Unit) da GPU na tentativa de acumular dados lineares de grandes distâncias.

### Limitações apresentadas
O estudo utiliza um framework próprio de arquitetura multi-pass que adiciona overhead de gerenciamento de alto nível. Além disso, avaliou apenas uma cena geométrica e não incluiu pipelines puramente baseados em Ray Tracing em hardware dedicado (RT Cores), limitando-se ao uso de shaders convencionais.

### Contribuição para o nosso artigo
Validação empírica do custo assintótico. A pesquisa fornece dados numéricos (frames por segundo e tamanhos de grid) que demonstram matematicamente o gargalo do hardware. Comprova a nossa hipótese de que o escalonamento da matriz de varredura ($O(W \times H)$) ou de grids 3D apresenta limitações logísticas severas de barramento de memória (VRAM) quando os polígonos são estressados.

### Comentário crítico
Excelente artigo por isolar as variáveis. Ao testar as diferentes estruturas algorítmicas sob a exata mesma câmera e contagem de polígonos, os autores evidenciaram que a complexidade algorítmica não é apenas uma barreira teórica, mas um limitador físico na GPU (sobrecarga da TMU). Fica claro que abordagens baseadas estritamente em rasterização linear colapsam sob alta contagem de amostras, justificando o uso de estruturas em árvore como o BVH para otimizar as consultas espaciais.

### Citação literal opcional
> "An increased sample set and a higher RSM or volume resolution clearly diminish performance."
Página: 125179

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página.