
# Frustum-Traced Irregular Z-Buffers: Fast, Sub-pixel Accurate Hard Shadows
## Etapa 6 Leitura e fichamento
**Classificação:** Fundamentação
### Identificação do artigo

- Referência completa: WYMAN, C.; HOETZLEIN, R.; LEFOHN, A. Frustum-Traced Irregular Z-Buffers: Fast, Sub-pixel Accurate Hard Shadows. *IEEE Transactions on Visualization and Computer Graphics*, v. 22, n. 4, 2016.
- DOI ou URL: https://doi.org/10.1109/TVCG.2016.2572689
- Base de origem: IEEE Xplore / NVIDIA Research
- Texto consultado: https://research.nvidia.com/sites/default/files/pubs/2015-02_Frustum-Traced-Raster-Shadows/ftizb_cameraReady.pdf
- Leitor responsável: Thiago de Luca Fernandes
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
As limitações estruturais e de memória inerentes à rasterização convencional (matrizes bidimensionais) em capturar dados analíticos e de profundidade. A natureza $O(W \times H)$ do Z-buffer apresenta gargalos severos de mapeamento ao processar listas irregulares sob alta oclusão geométrica.

### Objetivo do estudo
Revisitar a arquitetura do Irregular Z-Buffer (IZB), propondo uma implementação de varredura conservativa (frustum tracing) baseada em listas conectadas dinamicamente (linked lists), visando contornar os limites da grade bidimensional regular na GPU.

### Método utilizado
A proposta subverte a lógica da rasterização padrão substituindo as alocações da matriz de profundidade ($Z$) por listas conectadas (linked lists) por pixel. A renderização acontece em passos, realizando interseções puramente entre o frustum (geometria da câmera) e a geometria 3D bruta de forma matricial contígua, mas empilhando as colisões analiticamente. Os autores executaram análises de tempo (ms) contra métodos de ray tracing como NVIDIA OptiX.

### Contexto, amostra ou dados
O sistema processou a visibilidade analítica num conjunto geométrico de alta carga. Avaliado em uma GPU GeForce GTX 980, manipulando buffers e listas não ordenadas e estressando a capacidade atômica dos núcleos CUDA em gerenciar múltiplas alocações de memória por pixel.

### Principais resultados
Ao forçar a rasterização a armazenar mais do que apenas a profundidade mais próxima (natureza do Z-buffer padrão), o consumo de VRAM e o tempo de *overhead* atômico sobem exponencialmente. Cenários massivamente densos custaram até 162 ms por frame em casos de alta desordem. No entanto, o custo final da arquitetura baseada em IZB conseguiu ficar na mesma ordem de grandeza competitiva de complexidade algorítmica de soluções espaciais focadas em árvores.

### Limitações apresentadas
A construção de estruturas não ordenadas (linked lists) diretamente na memória contígua da GPU gera gargalos intermitentes devido a "atomics contention" (contenção atômica) quando muitos primitivos caem na mesma região. As listas podem crescer descontroladamente esgotando os recursos, configurando a transição de um problema puramente computacional $O(N)$ para um limite de armazenamento.

### Contribuição para o nosso artigo
Essencial para exemplificar o limite extremo da Rasterização. O artigo fundamenta o projeto ao demonstrar o que ocorre quando tentamos expandir o array de Z-buffer para realizar buscas profundas: o custo da rasterização, que teoricamente seria vantajoso, implode devido à limitação física de gerenciar ponteiros de memória em arquiteturas matriciais.

### Comentário crítico
Ótima peça analítica de algoritmos de baixo nível. Wyman prova na matemática que o Z-buffer é excelente porque é simples e acessado contiguamente na memória cache. Assim que introduzimos "listas" dentro dele (para tentar replicar a fidelidade do Ray Tracing), a Rasterização perde sua maior vantagem: a coerência de dados de acesso em memória $O(1)$ constante por pixel, tornando a complexidade espacial impraticável.

### Citação literal opcional
> "Irregular Z-buffers fundamentally change the rendering problem from point sampling to analytic visibility tracking using per-pixel linked lists."
Página: 2

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página.