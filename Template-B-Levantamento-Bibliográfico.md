# Etapa (b) — Levantamento Bibliográfico

## 1. Identificação do Grupo

| Campo | Informação |
|---|---|
| Curso / Disciplina | Ciência da Computação / Computabilidade e Complexidade de Algoritmos |
| Projeto de Pesquisa / IC | Análise comparativa entre rasterização e ray tracing |
| Orientador(a) | Andrea Ono Sakai |
| Data de entrega desta etapa | 20/09/2026 |
| Integrantes do grupo | Benito Juarez Jesus Viana Aguiar, Renan Veras de Andrade, Augusto da Silva Domingues , Thiago de Luca Fernandes |
| Tema (da etapa "a") | Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos. |

---

## FASE 1 — Planejamento da Busca

### Passo 1 — Pergunta de pesquisa e palavras-chave

**1.1 Problema/pergunta de pesquisa (versão de trabalho)**
> Como a complexidade assintótica e o consumo de memória divergem entre a rasterização (com Z-buffer) e o Ray Tracing (com aceleração BVH) ao escalar exponencialmente o número de primitivas e polígonos em sistemas gráficos de tempo real?

**1.2 Conceitos-chave e sinônimos**

| Conceito-chave | Sinônimos / termos relacionados (PT) | Sinônimos / termos relacionados (EN) |
|---|---|---|
| Computação Gráfica | Renderização, processamento gráfico | Rendering, computer graphics |
| Rasterização | Conversão de varredura, Z-buffer | Rasterization, Z-buffer, raster graphics |
| Ray Tracing | Traçado de raios, BVH | Ray tracing, Bounding Volume Hierarchy, BVH |
| Complexidade | Custo computacional, desempenho | Complexity, asymptotic complexity, performance |

*Responsável por este passo: Thiago de Luca Fernandes*

---

### Passo 2 — Strings de busca

| Nº | String de busca | Base(s) em que será usada | Elaborada por |
|---|---|---|---|
| 1 | `("Ray tracing" OR "BVH") AND ("Rasterization" OR "Z-buffer") AND ("Complexity" OR "Performance")` | IEEE Xplore, ACM DL, NVIDIA | Renan Veras de Andrade |
| 2 | `("Real-time rendering") AND ("asymptotic complexity" OR "computational cost") AND ("Ray tracing")` | IEEE Xplore, Scopus, NVIDIA | Renan Veras de Andrade |
| 3 | `("Bounding Volume Hierarchy" OR "BVH") AND ("Z-buffer" OR "Rasterization") AND "Performance"` | ACM DL, Scopus, NVIDIA | Renan Veras de Andrade |

---

### Passo 3 — Bases de dados escolhidas

| Base de dados | Por que foi escolhida | Responsável pela busca nesta base |
|---|---|---|
| IEEE Xplore | Reúne os principais artigos revisados por pares em Computação e Engenharia de Hardware gráfico. | Benito Juarez Jesus Viana Aguiar |
| ACM DL / Eurographics | Maior acervo do mundo sobre computação, contemplando especificamente papers originais da SIGGRAPH. | Benito Juarez Jesus Viana Aguiar |
| Scopus | Excelente base para indexação de artigos científicos de impacto focado em algoritmos e ciência da computação. | Benito Juarez Jesus Viana Aguiar |

---

### Passo 4 — Critérios de inclusão e exclusão

**Critérios de inclusão:**
- Artigos publicados em revistas e conferências científicas reconhecidas.
- Textos disponíveis integralmente (PDF ou HTML).
- Trabalhos revisados por pares (peer-reviewed).
- Publicações em inglês focadas especificamente em engenharia de algoritmos de renderização.

**Critérios de exclusão:**
- Trabalhos de Conclusão de Curso (TCC), links de repositórios não validados (share.google).
- Artigos cujo foco seja puramente a direção de arte e qualidade visual.
- Publicações sem abstract ou de fontes desconhecidas sem DOI válido.

*Definidos em conjunto por: Augusto da Silva Domingues *

---

## FASE 2 — Execução da Busca e Triagem

### Passo 5 — Execução das buscas e registro dos resultados

| Base | String usada (nº) | Data da busca | Nº de resultados | Executada por |
|---|---|---|---|---|
| IEEE Xplore | 1 | 16/09/2026 | 215 | Thiago de Luca Fernandes |
| ACM DL | 3 | 16/09/2026 | 134 | Renan Veras de Andrade |
| Scopus | 2 | 16/09/2026 | 82 | Thiago de Luca Fernandes |

**Total de resultados brutos (soma de todas as buscas):** 431
**Gerenciador de referências utilizado:** Zotero
**Formato de exportação:** BibTeX

---

### Passo 6 — Triagem por título e resumo (1ª filtragem)

| Item de controle | Quantidade |
|---|---|
| Total de resultados antes da triagem | 431 |
| Duplicatas removidas | 42 |
| Classificados como "Incluir" | 18 |
| Classificados como "Excluir" | 340 |
| Classificados como "Dúvida" | 31 |

**Como as dúvidas foram resolvidas?** O grupo avaliou os abstracts de forma conjunta com foco em remover artigos focados 100% no visual em detrimento da matemática/complexidade. O método de filtragem PRISMA foi aplicado no Zotero.

*Responsável(is) por esta triagem: Benito Juarez Jesus Viana Aguiar e Augusto da Silva Domingues *

---

### Passo 7 — Triagem por leitura completa (2ª filtragem)

| Item de controle | Quantidade |
|---|---|
| Total de artigos que entraram nesta filtragem | 18 |
| Aprovados (conjunto definitivo para fichamento) | 5 |
| Excluídos nesta etapa | 13 |

**Principais motivos de exclusão nesta filtragem:**
- Foco exacerbado no fotorrealismo invés de algoritmos.
- Falta de métricas palpáveis de memória e tempo de renderização.

*Responsável(is) por esta triagem: Thiago de Luca Fernandes e Benito Juarez Jesus Viana Aguiar*

---

## 3. Lista Final de Artigos Selecionados (Conjunto Definitivo)

1. WYMAN, C. et al. Frustum-Traced Irregular Z-Buffers: Fast, Sub-pixel Accurate Hard Shadows. IEEE Transactions on Visualization and Computer Graphics, v. 22, n. 4, 2016. DOI: 10.1109/TVCG.2016.2572689. Disponível em: https://research.nvidia.com/sites/default/files/pubs/2015-02_Frustum-Traced-Raster-Shadows/ftizb_cameraReady.pdf. Acesso em: 17 set. 2026.
2. LAMBRU, C. et al. Comparative Analysis of Real-Time Global Illumination Techniques in Current Game Engines. IEEE Access, v. 9, p. 125158-125183, 2021. DOI: 10.1109/ACCESS.2021.3109663. Disponível em: https://ieeexplore.ieee.org/abstract/document/9527241. Acesso em: 17 set. 2026.
3. WOOP, S.; BRUNVAND, E.; SLUSALLEK, P. Estimating Performance of a Ray-Tracing ASIC Design. In: 2006 IEEE SYMPOSIUM ON INTERACTIVE RAY TRACING, 2006, Salt Lake City. Proceedings... IEEE, 2006. p. 7-14. DOI: 10.1109/RT.2006.280209. Disponível em: https://www.researchgate.net/publication/228767166_Estimating_Performance_of_a_Ray-Tracing_ASIC_Design. Acesso em: 17 sep. 2026.
4. RITSCHEL, T. et al. The State of the Art in Interactive Global Illumination. Computer Graphics Forum, v. 31, n. 1, p. 160-188, 2012.  DOI: 10.1111/j.1467-8659.2012.02093.x. Disponível em: https://www.semanticscholar.org/paper/The-State-of-the-Art-in-Interactive-Global-Ritschel-Dachsbacher/fc442a3076abc2217058b5651c255e1aa54f00b9. (O DOI leva para a página original, porém achei o artigo/PDF nesse site). Acesso em: 17 sep. 2026.
5. CRASSIN, C. et al. Interactive Indirect Illumination Using Voxel Cone Tracing. Computer Graphics Forum, v. 30, n. 7, p. 1921-1930, 2011. DOI: 10.1111/j.1467-8659.2011.02063.x. Disponível em: https://research.nvidia.com/publication/2011-09_interactive-indirect-illumination-using-voxel-cone-tracing?utm_source=gemini. Acesso em: 17 sep. 2026

---

## 4. Contribuição Individual dos Integrantes

### Integrante 1 — Thiago de Luca Fernandes
- **Passo(s) em que atuou:** Passos 1, 5 e 7
- **O que fez em cada passo:** Determinei a problemática de restrição algorítmica focado em Z-buffer e BVH (Passo 1), executei queries na base IEEE e Scopus (Passo 5) e conduzi a leitura completa final para eliminar as literaturas fracas (Passo 7).
- **Tempo dedicado (aprox.):** 7h
- **Evidência da contribuição:** Planilha `.csv` exportada e notas teóricas de avaliação do BVH inseridas no controle do Zotero.

### Integrante 2 — Renan Veras de Andrade
- **Passo(s) em que atuou:** Passos 2 e 5
- **O que fez em cada passo:** Estruturei e apliquei as condicionais lógicas (booleanas) de busca e realizei o cruzamento de pesquisas avançadas na ACM DL.
- **Tempo dedicado (aprox.):** 4h
- **Evidência da contribuição:** Operadores booleanos de pesquisa validados e documentados em ata do grupo de estudo.

### Integrante 3 — Benito Juarez Jesus Viana Aguiar
- **Passo(s) em que atuou:** Passos 3, 6 e 7
- **O que fez em cada passo:** Escolhi e fundamentei as bases acadêmicas confiáveis para remediar o erro da entrega anterior, além de realizar filtragem grossa via Resumo/Abstract (Passo 6) e leitura técnica de aprovação (Passo 7).
- **Tempo dedicado (aprox.):** 6h
- **Evidência da contribuição:** Print screens do fluxo de aprovação de referências via software de triagem PRISMA.

### Integrante 4 — Augusto da Silva Domingues 
- **Passo(s) em que atuou:** Passos 4 e 6
- **O que fez em cada passo:** Delimitei os hard stops (critérios de exclusão severos, removendo TCCs), apliquei a peneira fina em títulos nas importações em lote e cuidei da formatação final para garantir a qualidade metodológica.
- **Tempo dedicado (aprox.):** 6h
- **Evidência da contribuição:** Configuração padronizada das referências metodológicas do Zotero, consolidação do arquivo markdown.

### 4.1 Quadro-resumo de participação por passo

| Passo | Responsável(is) | % estimado de participação de cada um |
|---|---|---|
| 1. Pergunta e palavras-chave | Thiago | 100% |
| 2. Strings de busca | Renan | 100% |
| 3. Bases de dados | Benito | 100% |
| 4. Critérios de inclusão/exclusão | Augusto | 100% |
| 5. Execução das buscas | Thiago (50%), Renan (50%) | 100% |
| 6. Triagem título/resumo | Benito (50%), Augusto (50%) | 100% |
| 7. Triagem texto completo | Thiago (50%), Benito (50%) | 100% |

### 4.2 Quadro-resumo geral de participação na etapa

| Integrante | % estimado de participação total nesta etapa |
|---|---|
| Thiago de Luca Fernandes | 30% |
| Renan Veras de Andrade | 20% |
| Benito Juarez Jesus Viana Aguiar | 30% |
| Augusto da Silva Domingues  | 20% |

---

## 5. Checklist Final da Etapa

**Fase 1 — Planejamento**
- [x] Pergunta de pesquisa de trabalho definida
- [x] Conceitos-chave e sinônimos (PT/EN) listados
- [x] Strings de busca elaboradas com operadores booleanos
- [x] Bases de dados escolhidas e justificadas
- [x] Critérios de inclusão e exclusão definidos

**Fase 2 — Execução e triagem**
- [x] Buscas executadas e resultados registrados por base/string
- [x] Referências exportadas para o gerenciador de referências
- [x] Triagem por título/resumo concluída (com duplicatas removidas)
- [x] Triagem por texto completo (introdução/conclusão) concluída
- [x] Conjunto definitivo de artigos para fichamento compilado

**Documentação**
- [x] Contribuição individual de cada integrante registrada por passo
- [x] Quadro-resumo de participação preenchido (soma = 100%)