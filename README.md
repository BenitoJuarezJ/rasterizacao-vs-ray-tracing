# Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos

![Status](https://img.shields.io/badge/status-concluído-brightgreen)
![Pesquisa](https://img.shields.io/badge/modalidade-pesquisa%20bibliográfica-blue)
![Licença](https://img.shields.io/badge/licença-MIT-green)

## Resumo

Este projeto apresenta uma análise comparativa da complexidade assintótica e do custo computacional e de memória envolvendo as duas principais estruturas de dados utilizadas na renderização gráfica em tempo real: matrizes bidimensionais de profundidade para rasterização (Z-buffer) e hierarquias de volumes de delimitação para Ray Tracing (*Bounding Volume Hierarchy* - BVH). A pesquisa isola parâmetros subjetivos de estética visual e fotorrealismo para aprofundar-se estritamente na fundamentação algorítmica e arquitetural do gerenciamento de recursos perante o aumento exponencial de primitivas geométricas.

## Objetivo geral

Analisar comparativamente a complexidade assintótica (notação Big-O) e o custo estrutural de memória (*footprint*) associados à varredura matricial no Z-buffer versus o particionamento espacial e interseções logarítmicas em estruturas hierárquicas BVH sob estresse geométrico.

## Objetivos específicos

- Conceituar e modelar matematicamente a Rasterização (Z-buffer) e o Ray Tracing (BVH) em termos de algoritmos e estruturas de dados;
- Examinar a complexidade assintótica ($O(N)$ vs. $O(\log N)$) e os custos de processamento envolvidos;
- Isolar a análise em métricas de processamento, cache e acesso à memória (evitando comparações estéticas subjetivas);
- Investigar os gargalos impostos pela memória de vídeo (VRAM), cache de texturas (TMU), contenção atômica e divergência de execução nas GPUs.

## Tema delimitado

> Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos.

| Delimitação | Descrição |
|---|---|
| Área geral | Complexidade de algoritmos e desempenho de estruturas de dados em computação gráfica 3D |
| Tema amplo | Complexidade e Estruturas de Dados na Computação Gráfica |
| Tema específico | Comparação da complexidade espacial e temporal entre rasterização (Z-buffer) e Ray Tracing (BVH) |
| Modalidade | Pesquisa bibliográfica qualitativa e comparativa baseada em artigos científicos revisados por pares |

## Metodologia

O projeto foi desenvolvido por meio de uma revisão bibliográfica qualitativa e comparativa com busca estruturada (fluxo PRISMA) nas bases **IEEE Xplore**, **ACM Digital Library** e **Scopus** (executada em 16/09/2026). A partir de 431 registros iniciais, removeram-se 42 duplicatas e triaram-se 389 estudos no gerenciador Zotero, selecionando-se 18 artigos para leitura integral e aprovando-se um corpus definitivo de 5 estudos fundamentais auditados integralmente.

## Integrantes

| Integrante | Perfil no GitHub |
|---|---|
| Augusto da Silva Domingues | [@augustodasilvadomingues](https://github.com/augustodasilvadomingues) |
| Benito Juarez Jesus Viana Aguiar | [@BenitoJuarezJ](https://github.com/BenitoJuarezJ) |
| Renan Veras de Andrade | [@renanvras987](https://github.com/renanvras987) |
| Thiago de Luca Fernandes | [@Thiago13721](https://github.com/Thiago13721) |

## Informações acadêmicas

| Campo | Informação |
|---|---|
| Instituição | Centro Universitário Braz Cubas |
| Curso | Ciência da Computação |
| Disciplina / Área | Computabilidade e Complexidade de Algoritmos |
| Modalidade | Projeto de pesquisa bibliográfica |
| Orientadora | Profa. Andrea Ono Sakai |
| Branch principal | `main` |
| Status | Concluído |

## Organização do repositório

```text
.
├── templates - artigo resumo - aluno - feito/
│   ├── # Etapa 6 Fichamento/
│   │   ├── Comparative Analysis of Real-Time Global...
│   │   ├── Estimating Performance of a Ray-Tracing...
│   │   ├── Frustum-Traced Irregular Z-Buffers Fast, Sub...
│   │   ├── Interactive Indirect Illumination Using Voxel...
│   │   └── The State of the Art in Interactive Global...
│   ├── # Etapa 1 Tema e delimitação.md
│   ├── # Etapa 2 Problema de pesquisa.md
│   ├── # Etapa 3 Objetivo geral e objetivos esp.md
│   ├── # Etapa 4 Planejamento da busca bibliogr.md
│   ├── # Etapa 5 Busca e triagem dos artigos.md
│   ├── # Etapa 7 Matriz de síntese e organização.md
│   ├── # Etapa 8 Redação do Artigo.md
│   ├── # Etapa 9 Normalização e revisão final.md
│   ├── # Etapa 10 Preparação da apresentação.md
│   ├── # 10_apresentacao_GRUPO8_FINAL.pptx
│   ├── 00_LEIA-ME.md
│   └── RESUMO_FINAL_GRUPO_8.docx
├── Artigos.zip
├── documentacao.zip
├── a_Escolha_do_Tema.md
├── b_Levantamento_Bibliografico_Preliminar.md
├── c_objetivo_geral_e_especificos.md
├── triagem_final_zotero.csv
├── triagem_final_zotero.xlsx
├── LICENSE
└── README.md
