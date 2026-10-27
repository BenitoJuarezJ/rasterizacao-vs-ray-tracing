# Etapa 9 Normalização e revisão final

## Solicitação

Revise o conteúdo, as citações, as referências e a formatação antes da entrega.

## Identificação

- Título do artigo: Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos
- Versão revisada: 2
- Data: 25/10/2026
- Responsável pela conferência final: Renan Veras de Andrade

## Revisão científica

- [x] Tema, problema e objetivos estão alinhados. *(Conferi que as Etapas 1 a 3 e a introdução do artigo são coerentes entre si.)*
- [x] As conclusões respondem ao problema. *(Reformulei a conclusão sobre a memória como fator limitante, que não era sustentada por Woop, Wyman nem Ritschel; ver registro, itens 1, 5, 12 e 13.)*
- [x] Não existem afirmações sem fonte quando a fonte é necessária. *(Corrigi as afirmações atribuídas a artigos que não as continham; ver registro.)*
- [x] As limitações do trabalho foram reconhecidas. *(O artigo admite o tamanho reduzido do conjunto, a ausência do ponto de virada e a distância entre iluminação global e visibilidade primária.)*
- [x] Não foram incluídos resultados inexistentes. *(Retirei ou substituí as citações literais e os resultados dos fichamentos que não apareciam nos artigos originais; ver registro, itens 1, 2, 4, 5, 8, 9 e 11.)*

## Citações e referências

- [x] Toda obra citada aparece nas referências. *(Conferi: Crassin, Lambru, Ritschel, Woop e Wyman.)*
- [x] Toda referência listada foi citada no texto. *(Conferi.)*
- [x] Citações diretas contêm página. *(O artigo não tem citações diretas. Nos fichamentos, corrigi as citações com problema; ver registro, itens 2, 4 e 11.)*
- [x] Autores, títulos, anos, DOI e links foram conferidos. *(Corrigi volume, número e páginas de Wyman e conferi os DOIs; ver registro, itens 3 e 6.)*
- [x] O padrão exigido foi aplicado de forma consistente. *(Apliquei o padrão exigido a todas as referências; ver registro, item 16.)*

## Escrita

- [x] O texto possui sequência lógica.
- [x] Os parágrafos apresentam uma ideia principal.
- [x] Foram corrigidos ortografia e concordância. *(Fiz a revisão ortográfica completa do texto.)*
- [x] Repetições e frases vagas foram eliminadas. *(Reescrevi a síntese crítica e as considerações finais para eliminar a repetição sobre a memória.)*
- [x] O texto diferencia descrição de análise crítica. *(Há seção própria de síntese crítica.)*

## Formatação

- [x] O template institucional foi respeitado.
- [x] Títulos e subtítulos estão padronizados. *(Ver registro, item 15.)*
- [x] Tabelas e figuras possuem identificação e fonte. *(O artigo não tem tabelas nem figuras; não se aplica.)*
- [x] Margens, fonte, espaçamento e paginação foram conferidos.

## Registro das correções

| Seção | Problema encontrado | Correção realizada | Responsável |
|---|---|---|---|
| [1] Artigo, Eixo 2 (Woop et al., 2006) | O texto dizia que os autores concluem que o ray tracing é limitado pela memória, que o desempenho depende de o cache L2 abrigar a árvore e que a reconstrução da árvore a cada quadro é cara. O artigo não diz isso. O Update Processor da DRPU só atualiza os limites da B-KD tree (os ciclos de atualização ficam cerca de duas ordens de grandeza abaixo dos de renderização), os caches de primeiro nível têm acerto acima de 90% na maioria das cenas e a banda de DRAM medida é baixa (73 a 210 MB/s, Tabela 2). A restrição declarada pelos autores é que só movimentos coerentes são tratados com eficiência. A B-KD tree é descrita pelos autores como um tipo de BVH com limites unidimensionais. | Reescrevi o parágrafo com esses achados e retirei "L2", "limitado pela memória" e "reconstrução a cada quadro". | Benito Juarez Jesus Viana Aguiar e Renan Veras de Andrade |
| [2] Ficha de Woop (e Etapas 5 e 7) | A citação literal ("Performance of interactive ray tracing is highly dependent on caching...", p. 13) não aparece no texto do artigo. A ficha também dizia que o estudo comprova que o ray tracing é memory-bound, o que contradiz a baixa banda medida. O cenário de "8 unidades SP" são, na verdade, 8 cópias da DRPU no ASIC (estimativa de 80 a 290 fps a 1024 × 768). A afirmação de que o estudo "levou aos núcleos RTX" não tem apoio no artigo. | Retirei a citação literal do fichamento (campo opcional, marcado como não utilizada). Corrigi o problema investigado, os resultados e o comentário crítico, e retirei do texto a indicação de nm do ASIC, que aparecia com valores diferentes nos materiais do grupo. | Benito Juarez Jesus Viana Aguiar e Renan Veras de Andrade |
| [3] Ficha de Wyman, texto consultado | O PDF indicado é o artigo da conferência I3D 2015 ("Frustum-Traced Raster Shadows: Revisiting Irregular Z-Buffers"), e não o artigo da TVCG 2016 que está na referência. | Registrei no fichamento e na Metodologia do artigo que a leitura foi feita na versão da conferência I3D (2015) do mesmo trabalho. | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [4] Ficha de Wyman e Artigo, Eixo 1 | O IZB guarda, por texel do espaço da luz, uma lista encadeada dos pontos de amostra vistos pela câmera, e o foco é sombra dura. A ficha o descrevia como lista de profundidades por pixel que "expande o Z-buffer". A citação literal (p. 2) não aparece no texto de 2015. As conclusões "a coerência de memória se perde" e "a rasterização implode" não são dos autores, que mostram um sistema interativo. | Reescrevi problema, método e comentário. Retirei a citação literal do fichamento (campo opcional, marcado como não utilizada). | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [5] Ficha de Wyman, Etapas 5 e 7 e Artigo, Eixo 1 | "Consumo de VRAM e overhead atômico sobem exponencialmente" contradiz o artigo: o desempenho escala de forma aproximadamente linear com triângulos e pixels, e sublinear com a resolução (1080p para 2160p custa cerca de 2× e não 4×). Os 162 ms são da cena GeeBee Plane (11,7 milhões de triângulos, 32 amostras por pixel, Tabela 1) e não de "alta desordem". Os autores concluem que reconstroem a estrutura em menos de 2 ms por quadro. | Corrigi os números e o contexto. Incorporei a Seção 3.1, que dá a complexidade O(N) com N = fragmentos de triângulos × comprimento médio das listas, porque responde diretamente à pergunta de pesquisa. | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [6] Referências (Wyman) | Constava "v. 22, n. 4, 2016". Os dados corretos são v. 22, n. 10, p. 2249-2261. | Corrigi volume, número e páginas e conferi o DOI. | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [7] Etapa 5 e ficha de Lambru, Eixo 3 | A Etapa 5 dizia que Lambru compara rasterização e ray tracing. O resumo do artigo diz que a análise cobre apenas técnicas baseadas no pipeline de rasterização e que as técnicas feitas para ray tracing ficam de fora. A ficha também usava o estudo para "justificar o BVH", o que ele não testa. | Corrigi a justificativa da Etapa 5. Passei a usar Lambru como evidência sobre o custo de estruturas matriciais e de volume em rasterização. | Augusto Domingues da Silva e Renan Veras de Andrade |
| [8] Ficha de Lambru | A contagem de polígonos é fixa no experimento, então o estudo não testa a escala de polígonos. "O(N²)" e "colapsam" eram interpretações do grupo, e não resultados do artigo. O link em "texto consultado" apontava para a página de resumo da IEEE Xplore. | Conferi números e citação no PDF completo, atualizei o link para o documento integral e removi "O(N²)". | Augusto Domingues da Silva e Renan Veras de Andrade |
| [9] Ficha de Crassin, Etapa 7 e Artigo, Eixo 2 | Os 11,4 FPS são de uma janela de 1024 × 768 com 3 cones difusos e 1 especular, e não de objetos dinâmicos "quebrando a árvore". Os outros valores medidos são 20 FPS (512², com cone especular) e 30 FPS (sem cone especular). O resumo do artigo anuncia 25 a 70 FPS e desempenho "quase independente da cena". A atualização de um objeto dinâmico (mão com 16 mil triângulos) custa cerca de 5,5 ms por quadro e a octree estática é construída uma vez (cerca de 280 ms). A ficha afirmava "gargalo imenso" na atualização, o que não está no texto. O artigo também não declara O(log N). A limitação de memória (cerca de 1 GB) está correta. | Corrigi os números e o contexto e mantive a limitação de memória. Separei o que é do artigo do que é interpretação do grupo. | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [10] Etapa 5 (Crassin) | A justificativa dizia que o artigo "contrapõe o Z-buffer". A comparação feita no artigo é com o LPV (Light Propagation Volumes). | Corrigi a justificativa. | Thiago de Luca Fernandes e Renan Veras de Andrade |
| [11] Ficha de Ritschel (versão do grupo) e Etapa 5 | A ficha chamava o estudo de "revisão sistemática". É uma revisão narrativa, sem protocolo de busca. A citação literal (p. 161) não aparece no artigo. O artigo não menciona BVH nem Z-buffer, então "demonstra textualmente a transição Z-buffer para BVH" é falso. O limite "RT Cores não existiam" é uma observação do grupo, e não dos autores. | Substituí a ficha pela versão revisada (06_leitura_e_fichamento_Ritschel2012_FINAL_v2.md, com citação e página conferidas) e corrigi a justificativa da Etapa 5. | Renan Veras de Andrade |
| [12] Artigo, Eixo 2 (Ritschel) | O texto atribuía ao survey o "alto custo de atualização estrutural em cenas totalmente dinâmicas" e a ideia de que estruturas hierárquicas são necessárias para escalar. Isso não consta. O survey fala de divergência de threads na GPU quando a iluminação fica complexa. | Reescrevi o parágrafo apenas com o que o survey diz. | Renan Veras de Andrade |
| [13] Artigo, Síntese crítica, Considerações finais e Resumo, e Etapa 7 (síntese provisória) | "A memória é o principal fator limitante nos dois paradigmas" não se sustenta. Wyman aponta contenção atômica e divergência, Ritschel aponta divergência, Woop mostra baixa banda e Crassin aponta consumo de memória e custo de atualização. | Reformulei: os estudos apontam gargalos diferentes (acesso à memória, atualização da estrutura, contenção e divergência), sem convergir em um único. Ajustei também o resumo. | Renan Veras de Andrade |
| [14] Artigo, Metodologia | Em alguns fichamentos iniciais, o campo de URL registrava a página de metadados/resumo da base indexadora em vez do link direto para o PDF integral efetivamente lido. | Padronizei a descrição na Metodologia e nos fichamentos: cada artigo foi atribuído a um integrante, fichado a partir da leitura integral do PDF e auditado na revisão final, registrando que a leitura de Wyman foi realizada na versão I3D (2015). | Augusto Domingues da Silva e Renan Veras de Andrade |
| [15] Artigo, formatação | Os títulos tinham marcadores de modelo ("`[Eixo 1]`", "`[Eixo 2]`", sem espaço antes do texto). As palavras-chave terminavam em ponto e vírgula. O Resumo vinha depois das Considerações finais. As strings de busca estavam em linhas soltas, sem marcadores. | Removi os marcadores, ajustei a pontuação, movi o Resumo para antes da Introdução e formatei a lista de strings. | Augusto Domingues da Silva e Renan Veras de Andrade |
| [16] Referências | O estilo das referências estava inconsistente: a citação no texto seguia a ABNT, mas os títulos dos periódicos estavam sem destaque. | Apliquei o padrão exigido pela professora a todas as referências. | Augusto Domingues da Silva e Renan Veras de Andrade |
| [17] Artigo, Síntese crítica (Limitações e Lacunas) e Etapa 7 (Eixo 3) | O texto afirmava que os experimentos usam resoluções baixas ou médias e apontava como lacuna a falta de avaliações em resoluções como 4K. Wyman et al. relatam a passagem de 1080p para 2160p (item 5). | Retirei a afirmação sobre resoluções baixas ou médias e reformulei a lacuna: entre os estudos, só Wyman et al. chegam a 2160p, e com uma estrutura irregular, não com o Z-buffer convencional. | Renan Veras de Andrade |