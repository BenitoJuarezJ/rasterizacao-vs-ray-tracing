# Análise Comparativa do Custo Computacional: Z-Buffer vs BVH (Ray Tracing)

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Pesquisa](https://img.shields.io/badge/modalidade-pesquisa%20bibliográfica-blue)
![Licença](https://img.shields.io/badge/licença-MIT-green)

## Resumo

Este projeto apresenta uma análise comparativa da complexidade assintótica e do custo computacional e de memória envolvendo as duas principais estruturas de dados utilizadas na renderização gráfica: matrizes bidimensionais de profundidade para rasterização (Z-buffer) e hierarquias de volume delimitação para Ray Tracing (Bounding Volume Hierarchy - BVH). A pesquisa abandona parâmetros de estética visual e fotorealismo para aprofundar-se estritamente na fundamentação algorítmica do esgotamento de recursos perante a escalabilidade exponencial de vértices geométricos.

## Objetivo geral

Analisar comparativamente a complexidade assintótica (Notação Big-O) e o custo logístico em processamento e memória associados à varredura e interpolação no Z-buffer versus o mapeamento espacial e interseções logarítmicas de árvores estruturadas por BVH.

## Objetivos específicos

- Conceituar e modelar matematicamente a Rasterização (Z-buffer) e Ray Tracing (BVH) em termos de algoritmos;
- Examinar a complexidade e os custos de processamento (Notação assintótica) envolvidos;
- Isolar a análise apenas em métricas de processamento e dados espaciais (evitando comparações estéticas);
- Investigar as limitações impostas pela memória no trânsito das estruturas Bounding Volume para a GPU.

## Tema delimitado

> Análise comparativa do custo computacional e complexidade assintótica entre os algoritmos Z-buffer (Rasterização) e BVH (Ray Tracing) em simulações e renderização em tempo real.

| Delimitação | Descrição |
|---|---|
| Área geral | Complexidade de algoritmos e desempenho de estruturas de dados |
| Tema amplo | Complexidade e Estruturas de Algoritmos na Computação Gráfica |
| Tema específico | Comparação da complexidade espacial e temporal entre rasterização (Z-buffer) e Ray Tracing (BVH) |
| Modalidade | Pesquisa bibliográfica qualitativa baseada em artigos acadêmicos |

## Metodologia

O projeto será desenvolvido através de pesquisa sistemática (PRISMA) com busca rigorosa em literatura revisada por pares contida nas bases de dados da IEEE Xplore, ACM DL e Scopus. As considerações focarão na análise matemática do desempenho, ignorando artefatos criados para otimizações subjetivas.

## Integrantes

| Integrante | Perfil no GitHub |
|---|---|
| Benito Juarez Jesus Viana Aguiar | [@BenitoJuarezJ](https://github.com/BenitoJuarezJ) |
| Renan Veras de Andrade | [@renanvras987](https://github.com/renanvras987) |
| Augusto da Silva Domingues  | [@augustodasilvadomingues](https://github.com/augustodasilvadomingues) |
| Thiago de Luca Fernandes | [@Thiago13721](https://github.com/Thiago13721) |

## Informações acadêmicas

| Campo | Informação |
|---|---|
| Curso | Ciência da Computação |
| Modalidade | Projeto de pesquisa bibliográfica |
| Área de estudo | Computabilidade e Complexidade de Algoritmos |
| Orientadora | Andreia Ono Sakai |
| Branch principal | `main` |
| Status | Em desenvolvimento |

## Organização do repositório

```text
.
├── a_Escolha_do_Tema.md
├── b_Levantamento_Bibliografico_Preliminar.md
├── c_objetivo_geral_e_especificos.md
├── README.md
├── LICENSE
├── documentacao/
├── referencias/
└── resultados/