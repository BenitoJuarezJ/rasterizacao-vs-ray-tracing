# Análise Comparativa entre Rasterização e Ray Tracing

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Pesquisa](https://img.shields.io/badge/modalidade-pesquisa%20bibliográfica-blue)
![Licença](https://img.shields.io/badge/licença-MIT-green)

## Resumo

Este projeto apresenta uma análise comparativa da complexidade assintótica, do desempenho computacional e da qualidade visual dos algoritmos de renderização gráfica tridimensional, com ênfase nas técnicas de rasterização e ray tracing.

A pesquisa busca relacionar os fundamentos teóricos da complexidade de algoritmos às aplicações práticas da computação gráfica, considerando o equilíbrio entre eficiência computacional e fidelidade visual.

## Objetivo geral

Analisar e comparar a rasterização e o ray tracing quanto ao custo computacional, à complexidade algorítmica, ao desempenho e à eficácia visual em aplicações de computação gráfica tridimensional.

## Objetivos específicos

- Apresentar os fundamentos teóricos da rasterização e do ray tracing;
- Identificar as principais etapas computacionais de cada método;
- Examinar a complexidade e os custos computacionais envolvidos;
- Comparar o desempenho das técnicas em aplicações gráficas;
- Analisar as diferenças relacionadas à qualidade visual;
- Investigar as limitações e possibilidades de utilização em tempo real;
- Relacionar a evolução das GPUs à adoção do ray tracing em aplicações modernas.

## Tema delimitado

> Análise comparativa da complexidade assintótica e do desempenho entre os algoritmos de renderização gráfica 3D: rasterização versus ray tracing.

| Delimitação | Descrição |
|---|---|
| Área geral | Complexidade de algoritmos e análise de desempenho em computação gráfica 3D |
| Tema amplo | Complexidade de algoritmos |
| Tema específico | Comparação do custo computacional e da eficácia visual entre rasterização e ray tracing |
| Modalidade | Pesquisa bibliográfica e análise comparativa |

## Fundamentação inicial

### Rasterização

A rasterização é uma técnica de renderização que converte objetos tridimensionais em fragmentos e pixels exibidos em uma superfície bidimensional. Por apresentar elevado desempenho, é amplamente utilizada em jogos digitais, simulações e outras aplicações que exigem geração de imagens em tempo real.

Entretanto, determinados efeitos visuais, como sombras, reflexos e iluminação indireta, precisam ser aproximados por meio de técnicas complementares.

### Ray tracing

O ray tracing é uma técnica que simula o percurso dos raios de luz em uma cena virtual. Seu funcionamento permite representar, de maneira mais próxima do comportamento físico da luz, efeitos como reflexos, refrações, sombras e iluminação global.

Apesar da maior fidelidade visual, o método costuma apresentar maior custo computacional, especialmente em cenas complexas e aplicações que exigem renderização em tempo real.

### Comparação inicial

| Critério | Rasterização | Ray Tracing |
|---|---|---|
| Princípio de funcionamento | Projeção e conversão de primitivas gráficas em pixels | Simulação do percurso dos raios de luz |
| Desempenho | Geralmente mais elevado | Geralmente mais exigente |
| Custo computacional | Comparativamente menor | Comparativamente maior |
| Qualidade visual | Depende de aproximações e técnicas adicionais | Maior fidelidade na simulação da luz |
| Uso em tempo real | Amplamente consolidado | Em expansão com o desenvolvimento de hardware especializado |
| Principais aplicações | Jogos, interfaces gráficas e simulações | Cinema, visualização científica, arquitetura e jogos modernos |

## Justificativa

O tema apresenta relevância acadêmica e mercadológica por abordar o equilíbrio entre eficiência computacional e fidelidade visual, questão central no desenvolvimento de sistemas gráficos.

A transição de modelos baseados predominantemente em rasterização para soluções híbridas ou baseadas em ray tracing acompanha a evolução das unidades de processamento gráfico e a introdução de componentes especializados.

O estudo interessa às áreas de desenvolvimento de jogos, produção cinematográfica, simulação, visualização científica e computação gráfica. No contexto acadêmico, permite relacionar a análise de algoritmos aos desafios práticos da renderização em tempo real.

## Metodologia

O projeto será desenvolvido por meio de uma pesquisa bibliográfica, de natureza exploratória e abordagem qualitativa, acompanhada de análise comparativa.

As principais etapas metodológicas serão:

1. Levantamento de artigos, trabalhos acadêmicos, livros e documentos técnicos;
2. Estudo dos fundamentos da rasterização e do ray tracing;
3. Identificação das principais operações executadas por cada técnica;
4. Análise da complexidade e dos custos computacionais;
5. Comparação das características de desempenho;
6. Comparação da qualidade e da eficácia visual;
7. Sistematização dos resultados encontrados;
8. Elaboração das considerações finais.

## Integrantes

| Integrante | Perfil no GitHub |
|---|---|
| Benito Juarez Jesus Viana Aguiar | [@BenitoJuarezJ](https://github.com/BenitoJuarezJ) |
| Renan Vears de Andrade | [@renanvras987](https://github.com/renanvras987) |
| Augusto Domingues da Silva | [@augustodasilvadomingues](https://github.com/augustodasilvadomingues) |
| Thiago de Luca Fernandes | [@Thiago13721](https://github.com/Thiago13721) |

## Informações acadêmicas

| Campo | Informação |
|---|---|
| Curso | Ciência da Computação |
| Modalidade | Projeto de pesquisa bibliográfica |
| Área de estudo | Complexidade de algoritmos e computação gráfica 3D |
| Orientadora | Andreia Ono Sakai |
| Branch principal | `main` |
| Status | Em desenvolvimento |

## Organização do repositório

```text
.
├── README.md
├── LICENSE
├── referencias/
├── documentos/
└── resultados/- **Modalidade:** Projeto de pesquisa bibliográfica
- **Orientadora:** Andreia Ono Sakai
- **Branch principal:** `main`
"referencias/"| Referências e materiais bibliográficos autorizados
"documentos/"| Documentos produzidos durante a pesquisa
"resultados/"| Análises, comparações e resultados obtidos

Referências iniciais

1. BIKKER, Jacco. Ray Tracing in Real-time Games. 2012. Disponível em: "https://jbikker.github.io/literature/Ray%20Tracing%20in%20Real-time%20Games%20-%202012.pdf" (https://jbikker.github.io/literature/Ray%20Tracing%20in%20Real-time%20Games%20-%202012.pdf).

2. UNIVERSIDADE FEDERAL DE UBERLÂNDIA. Repositório Institucional. Disponível em: "https://repositorio.ufu.br/handle/123456789/49252" (https://repositorio.ufu.br/handle/123456789/49252).

3. Custo e Fotorrealismo: análise. Artigo acadêmico. Disponível em: "https://share.google/P6pUni1OqHWQGSmEZ" (https://share.google/P6pUni1OqHWQGSmEZ).

4. UNIVERSIDADE FEDERAL DE PERNAMBUCO. Repositório Institucional. Disponível em: "https://repositorio.ufpe.br/bitstream/123456789/2746/1/arquivo6997_1.pdf" (https://repositorio.ufpe.br/bitstream/123456789/2746/1/arquivo6997_1.pdf).

5. UNIVERSIDADE FEDERAL DE SANTA CATARINA. Repositório Institucional. Disponível em: "https://repositorio.ufsc.br/bitstream/handle/123456789/202673/TCC.pdf?sequence=1" (https://repositorio.ufsc.br/bitstream/handle/123456789/202673/TCC.pdf?sequence=1).

Status do projeto

O projeto encontra-se em desenvolvimento. A etapa atual contempla:

- [x] Escolha e delimitação do tema;
- [x] Elaboração da justificativa;
- [x] Verificação inicial de viabilidade;
- [x] Levantamento bibliográfico preliminar;
- [x] Identificação dos integrantes;
- [ ] Revisão bibliográfica completa;
- [ ] Análise da complexidade dos algoritmos;
- [ ] Comparação dos métodos;
- [ ] Organização dos resultados;
- [ ] Elaboração das considerações finais.

Licença

Este projeto está licenciado sob os termos da MIT License.

A licença permite o uso, a cópia, a modificação, a distribuição e a publicação deste material, desde que o aviso de direitos autorais e o texto da licença sejam preservados.

Para mais informações, consulte o arquivo ""LICENSE"" (LICENSE).

---

Projeto desenvolvido para fins acadêmicos no curso de Ciência da Computação.
