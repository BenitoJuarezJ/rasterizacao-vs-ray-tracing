# Template de Definição de Objetivos da Pesquisa Científica
### Computabilidade e Complexidade de Algoritmos

---

## Identificação do Grupo

| Campo | Informação |
|---|---|
| Curso / Disciplina | Ciência da Computação / Computabilidade e Complexidade de Algoritmos |
| Projeto de Pesquisa / IC | Análise comparativa entre rasterização e ray tracing |
| Orientador(a) | Andrea Ono Sakai |
| Data de entrega desta etapa | 20/09/2026 |
| Integrantes do grupo | Benito Juarez Jesus Viana Aguiar, Renan Veras de Andrade, Augusto da Silva Domingues , Thiago de Luca Fernandes |
| Tema (da etapa "a") | Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização (Z-buffer) e o Ray Tracing (BVH) em cenários de alta contagem de polígonos. |

## PARTE 1 — DEFINIR O OBJETIVO GERAL

### 1.1 Tema específico do grupo

**Pergunta:** Qual foi o tema específico que o grupo definiu?

> Resposta: Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH).

### 1.2 Passo a passo para chegar ao objetivo geral

**Passo 1 — Delimitação do tema**
> Resposta: Delimitamos a pesquisa ao contexto das análises assintóticas estruturais ($O(N)$ vs $O(\log N)$) focando unicamente nos algoritmos de oclusão e espaciais (Z-buffer vs BVH).

**Passo 2 — Formulação da problemática**
> Resposta: Como a complexidade algorítmica e a eficiência de memória se diferenciam entre implementações de renderização com Z-buffer versus Ray Tracing baseado em BVH à medida que se eleva a complexidade topológica (quantidade de polígonos) de uma cena gráfica em tempo real?.

**Passo 3 — Transformar a pergunta em objetivo geral**
> Resposta: Investigar e quantificar as divergências de complexidade algorítmica e custo estrutural da memória entre a renderização via Z-buffer e o Ray Tracing em BVH, visando identificar os gargalos matemáticos de cada abordagem.

**Passo 4 — Ajustes finais**
- [x] É claro, direto e mensurável?
- [x] Evitei verbos fracos como "estudar" ou "conhecer"?
- [x] Usei um verbo forte (explorar, analisar, investigar, compreender, avaliar, propor, desenvolver, aplicar, identificar)?

### 1.3 Respostas finais da Parte 1

**1) Qual a problemática?**
> Resposta: A ausência de clareza matemática exata no custo-benefício computacional durante o ponto de virada (quando a quantidade de polígonos torna a travessia de árvores logarítmicas mais eficiente que o mapeamento matricial de pixels) entre Z-buffer e BVH.

**2) Qual o objetivo geral?**
> Resposta: Analisar comparativamente a complexidade assintótica (Big-O) e o custo de memória (footprint) gerado pelas estruturas Z-buffer e Bounding Volume Hierarchy (BVH) em pipelines de computação gráfica de renderização estressada.

---

## PARTE 2 — DEFININDO OS OBJETIVOS ESPECÍFICOS

### 2.1 Objetivo geral pesquisado

> Resposta: Analisar comparativamente a complexidade assintótica (Big-O) e o custo de memória (footprint) gerado pelas estruturas Z-buffer e Bounding Volume Hierarchy (BVH) em pipelines de computação gráfica de renderização estressada.

### 2.2 Assuntos da pesquisa

**Assuntos do grupo:**
1. Resposta: Os fundamentos teóricos e matemáticos do mapeamento via Z-Buffer.
2. Resposta: A matemática subjacente e montagem de estruturas Bounding Volume Hierarchy (BVH).
3. Resposta: A transposição do crescimento exponencial de polígonos na notação assintótica Big-O.
4. Resposta: A carga de memória requerida pelas duas estruturas (matriz bidimensional vs árvore gráfica de travessia).
5. Resposta: Cruzamento de gargalos de desempenho focados no contexto temporal e custo de processamento.

### 2.3 Estrutura básica do artigo

**Estrutura do grupo:**
- Introdução
- Resposta: Fundamentação teórica de Rasterização e Estrutura Z-Buffer
- Resposta: Arquitetura de Espaço e Travessia no Ray Tracing via Bounding Volume Hierarchy
- Resposta: Análise e projeção assintótica de tempo e complexidade Big-O
- Resposta: Comparação de Consumo de Memória (Matriz de profundidade vs Árvores de Oclusão)
- Considerações finais

### 2.4 Objetivos específicos classificados

**Objetivos específicos do grupo:**

- **Objetivos Conceituais**
  - Resposta: Conceituar a arquitetura e a mecânica das listas de oclusão por profundidade (Z-buffer).
  - Resposta: Detalhar a elaboração da estrutura de dados Bounding Volume Hierarchy em hardware de processamento gráfico.

- **Objetivos Técnicos**
  - Resposta: Mensurar o comportamento de tempo de execução da rasterização sob a métrica Big-O ao escalar primitivas geométricas em tela.
  - Resposta: Estruturar a diferença formal de peso no preenchimento do *cache* de memória da GPU entre as duas abordagens.
  - Resposta: Determinar o ponto de intersecção em que o uso do Ray Tracing sobrepassa a eficiência da varredura baseada em Rasterização.

---

## CHECKLIST FINAL DO GRUPO

- [x] O tema específico está delimitado (área, tempo, espaço ou aplicação)
- [x] A problemática está formulada como pergunta
- [x] O objetivo geral está no infinitivo, claro e mensurável
- [x] Foram listados de 4 a 5 assuntos do artigo
- [x] A estrutura do artigo foi definida (introdução, desenvolvimento, considerações finais)
- [x] Os objetivos específicos foram classificados em Conceituais e Técnicos