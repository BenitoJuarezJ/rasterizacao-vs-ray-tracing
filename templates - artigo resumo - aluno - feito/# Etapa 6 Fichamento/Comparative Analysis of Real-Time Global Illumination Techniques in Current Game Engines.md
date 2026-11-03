# Etapa 6 Leitura e fichamento

## Identificação do artigo

- Referência completa: LAMBRU, C.; MORAR, A.; MOLDOVEANU, F.; ASAVEI, V.; MOLDOVEANU, A. Comparative Analysis of Real-Time Global Illumination Techniques in Current Game Engines. **IEEE Access**, v. 9, p. 125158-125183, 2021.
- DOI ou URL: (https://doi.org/10.1109/ACCESS.2021.3109663) , (https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9527241)
- Base de origem: IEEE Xplore
- Leitor responsável: Augusto da Silva Domingues 
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
O elevado custo computacional das técnicas de iluminação global (GI) em tempo real baseadas no pipeline de rasterização. O artigo investiga como o desempenho (FPS) de quatro classes de técnicas (RSM, DOM/LPV, Voxel Cone Tracing e espaço de tela/SSDO) varia conforme a resolução da tela, a resolução das estruturas intermediárias e o tamanho do conjunto de amostras.

### Objetivo do estudo
Descrever quatro classes de técnicas de GI em tempo real baseadas em rasterização, implementar uma técnica representativa de cada classe em um mesmo framework (C++ com OpenGL 4.6) e compará-las sob os mesmos parâmetros externos (cena, materiais e câmera) por critérios qualitativos e quantitativos (taxa de quadros).

### Método utilizado
Implementação unificada em arquitetura multi-pass de quatro técnicas:
1. Reflective Shadow Map (RSM) com amostragem estocástica e interpolação em espaço de tela;
2. Light Propagation Volumes (LPV);
3. Voxel Cone Tracing;
4. Screen Space Directional Occlusion (SSDO).
As medições quantitativas (Tabela 2, p. 125178) avaliaram o FPS considerando o cálculo da iluminação difusa indireta, sombras e oclusão de ambiente nas resoluções 1280×720 e 1920×1080.

### Contexto, amostra ou dados
Hardware: GPU NVIDIA GTX 1070. Cena de teste: Sponza Atrium, com contagem fixa de 262 mil triângulos (p. 125177). Parâmetros variados: resolução do RSM (512² e 1024²) e amostras (100 a 400); resolução do LPV (32³ e 64³); resolução do volume de voxels (64³ a 512³) com voxelização contínua ligada ou desligada; e amostras no SSDO (100 a 400).

### Principais resultados
- No RSM (a 1920×1080, 100 amostras), o desempenho cai de 122 FPS (512²) para 109 FPS (1024²), e chega a 58 FPS com 400 amostras em 1024². Os autores explicam que resoluções maiores do RSM e conjuntos maiores de amostras aumentam as falhas de cache (cache misses) na Texture Mapping Unit (TMU) da GPU (p. 125178-125179).
- No Voxel Cone Tracing (a 1920×1080), o FPS cai de 145 (grade 64³) para 89 (grade 512³) com voxelização contínua desligada, e de 138 (64³) para 52 FPS (512³) com voxelização contínua ligada, evidenciando o peso da recriação do volume a cada quadro e das amostragens adicionais ao longo do cone (p. 125178-125179).
- No SSDO (a 1920×1080), o desempenho vai de 36 FPS (100 amostras) a 11,6 FPS (400 amostras) devido à severa sobrecarga no cache da TMU ao acumular iluminação de grandes distâncias (p. 125178-125179).

### Limitações apresentadas
A análise restringe-se a técnicas baseadas no pipeline de rasterização, não implementando técnicas desenhadas inteiramente para o pipeline de ray tracing (p. 125158). Além disso, utiliza apenas uma cena com contagem fixa de triângulos (não testando a escalabilidade geométrica de polígonos) e a arquitetura multi-pass do framework impõe overhead de gerenciamento de alto nível (p. 125168).

### Contribuição para o nosso artigo
Fornece evidência experimental controlada sobre o custo de estruturas matriciais (RSM e G-buffers no espaço de tela) e volumétricas (LPV e voxels) dentro do pipeline de rasterização. Demonstra que o custo das estruturas matriciais cresce fortemente com a resolução e sofre com falhas de cache na TMU, mesmo mantendo fixa a contagem de polígonos.

### Comentário crítico
O ponto forte do estudo é isolar o impacto da resolução das estruturas de dados e do número de amostras em um mesmo framework e hardware. Contudo, como a contagem de triângulos permanece fixa em 262 mil e o ray tracing em hardware é abordado apenas de forma contextual (Seção III-F), os resultados devem ser usados na revisão para fundamentar os limites de memória e cache (TMU) das estruturas matriciais e de voxels, sem extrapolá-los como medição direta de BVH.

### Citação literal opcional
> "The caching mechanism of the TMU has more misses when the sampling texture, the RSM, has a higher resolution. All those misses have a negative impact on performance and this impact is even more visible when the sample set is larger and there are more cache misses."

Página: 125179

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página.
