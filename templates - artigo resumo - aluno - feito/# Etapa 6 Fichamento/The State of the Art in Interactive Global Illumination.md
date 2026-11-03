# Etapa 6 Leitura e fichamento

## Identificação do artigo

- Referência completa: RITSCHEL, Tobias; DACHSBACHER, Carsten; GROSCH, Thorsten; KAUTZ, Jan. The State of the Art in Interactive Global Illumination. **Computer Graphics Forum**, v. 31, n. 1, p. 160-188, 2012.
- DOI ou URL: [https://doi.org/10.1111/j.1467-8659.2012.02093.x](https://doi.org/10.1111/j.1467-8659.2012.02093.x)
- Base de origem: Eurographics Digital Library
- Leitor responsável: Renan Veras de Andrade
- Data da leitura: 08/10/2026

## Fichamento

### Problema investigado
A simulação do transporte de luz (iluminação global, GI) é cara por causa da natureza física do problema e do caráter global das interações entre as superfícies da cena. Já existia um grande volume de métodos que trocam exatidão por velocidade, o que tornava necessário reunir, organizar e comparar a extensa literatura sobre os que alcançam tempos interativos.

### Objetivo do estudo
Revisar, classificar e comparar métodos de GI interativa, isto é, que geram a imagem em menos de 1 segundo, com solução exata ou plausível do transporte de luz. Também apresentar a teoria de base, comparar pontos fortes e fracos por fenômeno visual, destacar padrões de projeto e listar problemas em aberto.

### Método utilizado
Revisão narrativa da literatura (survey) organizada em quatro eixos:
1. Teoria: equação de renderização, equação de renderização volumétrica e notação de caminhos de luz (L, D, S, V, E).
2. Abordagens: elementos finitos/radiosidade, ray tracing de Monte Carlo, photon mapping, instant radiosity, many-lights, GI baseada em pontos, métodos de ordenadas discretas, pré-computação (PRT) e caching.
3. Fenômenos: oclusão ambiental, iluminação natural, um quique, cáusticas, múltiplos quiques e espalhamento.
4. Estratégias: rasterização, importance sampling, espaço de tela, surfels/hierarquias/clusters, splatting, upsampling e percepção.

A comparação final (Seção 6) pontua técnicas selecionadas em seis critérios (velocidade, qualidade, dinamismo, escalabilidade, adequação à GPU e esforço de implementação). As notas foram dadas individualmente por cada autor e depois calculadas pela média. Não há protocolo sistemático de busca e seleção reproduzível (bases, strings, critérios de inclusão e exclusão).

### Contexto, amostra ou dados
Não há amostra empírica. O corpus é a literatura de computação gráfica até cerca de 2011, com foco em técnicas que rodam em hardware contemporâneo da época. Os autores observam que os artigos costumam testar em cenas pequenas e médias (Cornell box, Sponza, Sibenik).

### Principais resultados
- Define "interativo" como menos de 1 s por imagem e organiza o campo em duas visões complementares: abordagens (Seção 3) e estratégias (Seção 5).
- Aponta limitações típicas por família: métodos em espaço de tela são independentes da complexidade geométrica na etapa de pós-processamento, mas trabalham com informação incompleta devido ao recorte e à oclusão do framebuffer; já o Monte Carlo ray tracing renderiza todos os caminhos de luz, mas exige muitos raios e perde desempenho na GPU à medida que os raios secundários divergem (incoerência e divergência de threads).
- Conclui que nenhum método é "a solução definitiva" e lista problemas em aberto: escalabilidade para cenas grandes, filtragem, coerência temporal, múltiplos quiques especulares (glossy), volumes, luzes complexas e ajuste manual de parâmetros.

### Limitações apresentadas
- As notas da comparação são, nas palavras dos autores, necessariamente subjetivas, e nem todos os métodos podiam ser testados no hardware da época (a comparação cobre cerca de uma década de trabalhos).
- O limiar de 1 s é uma escolha arbitrária reconhecida pelos autores.
- Ficam fora do escopo: modelagem e medição de reflectância, métodos de visibilidade e sombras primárias (remetidos a outros surveys) e abordagens não usadas em aplicações interativas.

### Contribuição para o nosso artigo
Serve como fundamentação teórica e contextualização: explica por que técnicas puramente em espaço de tela operam com informação espacial incompleta e por que o traçado de raios em GPUs sofre queda de eficiência quando há incoerência e divergência de execução (threads/raios divergentes), além de contextualizar o papel da rasterização e do ray tracing em GPU na época (cerca de 100 milhões de raios por segundo).

### Comentário crítico
Pontos fortes: cobertura ampla e bem organizada, critérios de comparação explícitos (incluindo adequação à GPU e coerência de memória/código) e lista objetiva de problemas em aberto. Fragilidades: retrata o cenário tecnológico de 2011/2012, as pontuações comparativas são subjetivas e trata-se de revisão narrativa sem protocolo sistemático reproduzível.

### Citação literal opcional
> "Interactive GI is usually based on certain simplifications and making tradeoffs"

Página: 2 (versão do autor, com paginação 1-27; p. 161 na paginação do periódico)

## Checklist
- [x] O artigo foi lido além do resumo.
- [x] O método e os resultados foram identificados.
- [x] As limitações foram registradas.
- [x] A conexão com o tema foi explicada.
- [x] Toda citação literal contém página.
