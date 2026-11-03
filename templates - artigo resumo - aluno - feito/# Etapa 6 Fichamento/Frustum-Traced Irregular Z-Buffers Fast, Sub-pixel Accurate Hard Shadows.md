# Etapa 6 Leitura e fichamento

## Identificação do artigo

- Referência completa: WYMAN, Chris; HOETZLEIN, Rama; LEFOHN, Aaron. Frustum-Traced Irregular Z-Buffers: Fast, Sub-pixel Accurate Hard Shadows. **IEEE Transactions on Visualization and Computer Graphics**, v. 22, n. 10, p. 2249-2261, 2016.
- DOI ou URL: [https://doi.org/10.1109/TVCG.2016.2572689](https://doi.org/10.1109/TVCG.2016.2572689) (Texto integral consultado na versão da conferência I3D 2015 do mesmo trabalho: [https://research.nvidia.com/sites/default/files/pubs/2015-02_Frustum-Traced-Raster-Shadows/ftizb_cameraReady.pdf](https://research.nvidia.com/sites/default/files/pubs/2015-02_Frustum-Traced-Raster-Shadows/ftizb_cameraReady.pdf))
- Base de origem: IEEE Xplore / NVIDIA Research
- Leitor responsável: Thiago de Luca Fernandes
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
Os artefatos de serrilhamento espacial e temporal (aliasing) dos shadow maps regulares decorrentes da incompatibilidade de amostragem entre o espaço da câmera e o espaço da luz, bem como a baixa escalabilidade e a alta variação de desempenho entre quadros nas implementações anteriores de Irregular Z-Buffers (IZBs) (Seções 1 e 2).

### Objetivo do estudo
Apresentar um sistema em tempo real que renderiza sombras duras antisserrilhadas com precisão subpixel (1 e 32 amostras por pixel) utilizando Irregular Z-Buffers (IZBs) acelerados pelo pipeline gráfico de rasterização (rasterização conservativa e early-z culling).

### Método utilizado
O algoritmo constrói uma grade no espaço da luz em que cada texel armazena um ponteiro para uma lista encadeada (linked list) dos pontos de amostra visíveis pela câmera que se projetam naquele texel (Seção 3). Os triângulos da cena são então rasterizados de forma conservativa no espaço da luz, e cada fragmento percorre a lista encadeada do seu texel realizando testes de interseção frustum-triângulo. O estudo mede o tempo de cada etapa e compara a contagem de testes de interseção com um ray tracer baseado em BVH (NVIDIA OptiX).

### Contexto, amostra ou dados
Avaliado em uma GPU NVIDIA GeForce GTX 980 (OpenGL 4.4) utilizando 9 cenas de jogos e modelos CAD (de 89 mil triângulos em Chalmers Villa até 12,3 milhões de triângulos em UNC Powerplant), em 1920×1080 (e testes de escala até 3840×2160) com 4 cascatas de 2048² (Seção 7, Tabela 1).

### Principais resultados
- Na Seção 3.1, os autores formalizam a complexidade algorítmica como $O(N)$ para $N$ testes de visibilidade, onde $N = t_f \langle l_{izb} \rangle$, sendo $t_f$ o número de fragmentos de triângulos no espaço da luz e $\langle l_{izb} \rangle$ o comprimento médio das listas do IZB percorridas por cada fragmento.
- A estrutura do IZB é reconstruída do zero em cerca de 0,6 a 2,1 ms por quadro (Tabela 1).
- Em 1920×1080 com 32 amostras por pixel (Tabela 1), o tempo total varia de 7,6 ms (Chalmers Villa, 89k triângulos) a 162,9 ms (GeeBee Plane, 11,7M triângulos) e 75,6 ms (UNC Powerplant, 12,3M triângulos).
- A passagem de 1080p para 2160p (4K) escala de forma sublinear, aumentando o custo em cerca de 2× em vez dos 4× esperados, graças à remoção antecipada de nós já totalmente ocluídos (Seção 7, Figura 8).
- Comparado a um ray tracer com BVH no estado da arte (Figura 10), o IZB realiza entre 0,3× e 2,6× o número de testes de interseção por pixel.

### Limitações apresentadas
O principal gargalo na etapa de testes de visibilidade decorre da divergência de threads na GPU quando listas adjacentes possuem comprimentos muito diferentes, além da contenção em operações atômicas ao atualizar as máscaras de visibilidade (Seções 5.5, 6.7 e 7). Para modelos com muitos triângulos pequenos (como GeeBee Plane), a eficiência do descarte (culling) cai e a rasterização conservativa dilata proporcionalmente mais os fragmentos. Além disso, a aproximação unidimensional usada para 32 amostras pode gerar vazamento de luz (light leaking) em pequenos oclusores distantes (Seções 6.1 e 8).

### Contribuição para o nosso artigo
Responde diretamente à questão da complexidade e dos gargalos de estruturas baseadas em rasterização quando estendidas para visibilidade exata: formaliza a complexidade $O(t_f \langle l_{izb} \rangle)$, fornece a única comparação direta de número de interseções por pixel contra uma BVH (Figura 10) e é o único estudo do conjunto que mede o comportamento de escala até a resolução 2160p (4K).

### Comentário crítico
O estudo demonstra que o Irregular Z-Buffer reconstrói sua estrutura em menos de 2 ms por quadro (muito mais rápido que reconstruir uma BVH completa do zero), mas evidencia que substituir a escrita direta de profundidade do Z-buffer clássico por listas encadeadas introduz contenção atômica e divergência de threads quando o comprimento das listas varia.

### Citação literal opcional
Não utilizada. O fichamento emprega paráfrases conferidas nas Seções 3, 5, 6, 7 e 8 e na Tabela 1.

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página — não se aplica: nenhuma foi utilizada.
