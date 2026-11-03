# Etapa 6 Leitura e fichamento

## Identificação do artigo

- Referência completa: CRASSIN, Cyril; NEYRET, Fabrice; SAINZ, Miguel; GREEN, Simon; EISEMANN, Elmar. Interactive Indirect Illumination Using Voxel Cone Tracing. **Computer Graphics Forum**, v. 30, n. 7, p. 1921-1930, 2011.
- DOI ou URL: [https://doi.org/10.1111/j.1467-8659.2011.02063.x](https://doi.org/10.1111/j.1467-8659.2011.02063.x) https://research.nvidia.com/publication/2011-09_interactive-indirect-illumination-using-voxel-cone-tracing?utm_source=gemini
- Base de origem: Wiley Online Library / Eurographics Digital Library
- Leitor responsável: Benito Juarez Jesus Viana Aguiar
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
O elevado custo computacional de calcular iluminação indireta em tempo real em cenas complexas com milhões de triângulos e materiais difusos e especulares (glossy), evitando etapas lentas de pré-computação (Seção 1, p. 1921).

### Objetivo do estudo
Apresentar um algoritmo em tempo real na GPU baseado em uma representação hierárquica de octree esparsa de voxels (Sparse Voxel Octree - SVO) construída e atualizada dinamicamente, combinada com traçado aproximado de cones (voxel cone tracing) (p. 1921-1922).

### Método utilizado
O algoritmo opera em três passos (Seções 3 e 4):
1. Voxelização da malha poligonal usando o pipeline de rasterização da GPU para construir e atualizar a octree esparsa na memória de vídeo, seguida de injeção de fótons a partir da visão da fonte de luz;
2. Filtragem (MIP-mapping) dos valores de irradiância e direções nos níveis superiores da octree usando voxels anisotrópicos;
3. Renderização a partir da câmera lançando um pequeno número de cones pelo espaço 3D pré-filtrado para acumular visibilidade e iluminação indireta.
Os autores comparam o desempenho e a qualidade com Light Propagation Volumes (LPV) e com referências offline (Mental Ray e NVIDIA OptiX).

### Contexto, amostra ou dados
Implementado em uma GPU NVIDIA GTX 480 com CPU Intel Core 2 Duo E6850. A avaliação principal utiliza a cena Sponza (280 mil triângulos) com uma octree de 9 níveis (resolução virtual de $512^3$) e um objeto dinâmico inserido na cena (malha da mão de Wald, com 16 mil triângulos), nas resoluções de tela $512^2$ e $1024 \times 768$ (Seção 10, p. 1928).

### Principais resultados
- O resumo informa taxas gerais de 25 a 70 FPS e desempenho quase independente da complexidade da malha por evitar testar diretamente os triângulos durante o cone tracing.
- Na Seção 10 (p. 1928), a criação inicial da octree para a parte estática da cena Sponza leva cerca de 280 ms; a atualização interativa da octree para o objeto dinâmico (16k triângulos) leva cerca de 5,5 ms por quadro (tempo que depende do tamanho e do número de partes dinâmicas); e a injeção e filtragem da luz leva cerca de 16 ms quando a luz se move.
- Com um objeto dinâmico e luz móvel em Sponza, o método alcança média de 30 FPS sem cone especular e 20 FPS com um cone especular em viewport de $512^2$, caindo para 11,4 FPS em resolução $1024 \times 768$ (três cones difusos e um especular) (p. 1928).

### Limitações apresentadas
A principal limitação declarada pelos autores na Seção 10 (p. 1928) é o consumo relativamente elevado de memória de vídeo, mesmo utilizando uma estrutura esparsa, alocando cerca de 1024 MB (1 GB) de VRAM. Além disso, o custo de atualização dinâmica cresce com o tamanho e a quantidade de objetos móveis, e a discretização espacial pode gerar vazamento de luz (light leaking) ou superestimação de oclusão em cones largos.

### Contribuição para o nosso artigo
Documenta quantitativamente o compromisso das estruturas hierárquicas tridimensionais na GPU: ao substituir a malha poligonal por uma árvore pré-filtrada (octree esparsa, estrutura parente da BVH), a consulta torna-se quase independente da contagem de triângulos estáticos, mas impõe alto consumo de memória (~1 GB de VRAM) e custos adicionais de construção inicial (280 ms) e atualização por objeto dinâmico (5,5 ms).

### Comentário crítico
É importante distinguir os números do resumo (25 a 70 FPS) das medições detalhadas na Seção 10 (11,4 FPS em 1024×768 com cones difusos e especular). O artigo sustenta com precisão o peso da pegada de memória (1 GB) e o tempo de atualização de objetos móveis em árvores espaciais na GPU, embora compare diretamente sua proposta com LPV e OptiX, e não com o Z-buffer de visibilidade primária.

### Citação literal opcional
Não utilizada. O fichamento emprega paráfrases conferidas nas Seções 1, 3, 4, 9, 10 e 11 e nas Tabelas 1 e 2 (p. 1921-1929).

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página — não se aplica: nenhuma foi utilizada.
