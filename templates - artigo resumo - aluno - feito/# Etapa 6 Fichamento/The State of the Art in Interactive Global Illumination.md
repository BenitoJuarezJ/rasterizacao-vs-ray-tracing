# The State of the Art in Interactive Global Illumination

## Etapa 6 Leitura e fichamento
**Classificação:** Contextualização
### Identificação do artigo

- Referência completa: RITSCHEL, Tobias; DACHSBACHER, Carsten; GROSCH, Thorsten; KAUTZ, Jan. The State of the Art in Interactive Global Illumination. *Computer Graphics Forum*, v. 31, n. 1, p. 160-188, 2012.
- DOI ou URL: https://doi.org/10.1111/j.1467-8659.2012.02093.x
- Base de origem: Eurographics Digital Library (ACM/Scopus)
- Texto consultado: https://www.semanticscholar.org/paper/The-State-of-the-Art-in-Interactive-Global-Ritschel-Dachsbacher/fc442a3076abc2217058b5651c255e1aa54f00b9
- Leitor responsável: Renan Veras de Andrade
- Data da leitura: 09/10/2026

## Fichamento

### Problema investigado
A alta complexidade assintótica exigida para simular o transporte físico de luz. O estudo investiga o gargalo computacional em alcançar renderizações em tempo real utilizando algoritmos de complexidade linear e polinomial tradicionais da rasterização.

### Objetivo do estudo
Revisar e categorizar algoritmos de renderização interativa focando nos limites estruturais de hardware e software que forçam as metodologicas a trocar exatidão matemática por velocidade de acesso à memória.

### Método utilizado
Revisão sistemática do estado da arte baseada na taxonomia de estruturas de dados e formulação matemática. A pesquisa examina as estratégias sob o viés do tempo de execução: varredura no espaço de tela (Z-buffer e rasterização), hierarquias espaciais (clusters/árvores) e métodos de Monte Carlo (Ray Tracing).

### Contexto, amostra ou dados
O estudo analisa uma década de evolução algorítmica, validando como as GPUs da época processavam a taxa de transferência de dados, com menção específica à capacidade do Ray Tracing em lançar cerca de 100 milhões de raios por segundo sob aceleração de hardware estruturado.

### Principais resultados
- Define-se que métodos em espaço de tela (como o Z-buffer) operam com dados espacialmente incompletos.
- Demonstra que abordagens puras de Ray Tracing exigem avaliação extensiva da árvore de cena, causando divergência severa nos ramos de execução da GPU (branch divergence), o que destrói o desempenho.
- O estudo pontua que o futuro exige "estruturas hierárquicas" (árvores) para escalar problemas que seriam $O(N)$ na varredura tradicional, mas alerta para o alto custo de atualização estrutural quando a cena é totalmente dinâmica.

### Limitações apresentadas
A análise temporal refere-se ao hardware de 2011/2012, onde RT Cores dedicados ainda não existiam comercialmente. A comparação de desempenho entre métodos carece de testes unitários empíricos, baseando-se no cruzamento da literatura analisada. 

### Contribuição para o nosso artigo
O artigo apoia a premissa teórica central do nosso trabalho. A taxonomia formulada demonstra textualmente a transição do paradigma de Z-buffer para a necessidade de hierarquias de volume delimitação (como o BVH) a fim de reduzir o esforço de processamento de oclusão de $O(N)$ para comportamentos logarítmicos.

### Comentário crítico
Excelente para conceituação histórica dos gargalos da complexidade algorítmica. Os autores expõem como os "atalhos" da rasterização deixaram de escalar bem à medida que a complexidade geométrica das cenas (polígonos) explodiu na indústria. Isso justifica por que a transição de um algoritmo de preenchimento de matriz (Raster) para uma travessia de árvore (Ray Tracing/BVH) tornou-se mandatória sob a ótica da Engenharia de Computação.

### Citação literal opcional
> "The rendering equation is typically solved numerically using Monte Carlo integration [...] To reduce noise, a large number of rays need to be traced, creating a bottleneck."
Página: 161

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página.