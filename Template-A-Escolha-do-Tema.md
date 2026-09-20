# Etapa (a) — Escolha do Tema

## 1. Identificação do Grupo

| Campo | Informação |
|---|---|
| Curso / Disciplina | Ciência da Computação / Computabilidade e Complexidade de Algoritmos |
| Projeto de Pesquisa / IC | Análise comparativa entre rasterização e ray tracing |
| Orientador(a) | Andrea Ono Sakai |
| Data de entrega desta etapa | 20/09/2026 |
| Integrantes do grupo | Benito Juarez Jesus Viana Aguiar, Renan Veras de Andrade, Augusto da Silva Domingues, Thiago de Luca Fernandes |

## 2. Tema Escolhido

### 2.1 Área geral de interesse
Complexidade de algoritmos, uso de estruturas de dados e análise de desempenho em computação gráfica 3D.

### 2.2 Tema delimitado (versão final)
> **Tema:** Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização tradicional via Z-buffer e o Ray Tracing acelerado por Bounding Volume Hierarchy (BVH) em cenários de alta contagem de polígonos.

### 2.3 Do amplo ao específico

| Tema amplo (ponto de partida) | Tema delimitado (ponto de chegada) |
|---|---|
| Complexidade de algoritmos | Análise comparativa do custo computacional e da complexidade assintótica entre a rasterização (Z-buffer) e o Ray Tracing (BVH). |

## 3. Justificativa da Escolha

### 3.1 Relevância
O tema possui alta relevância para a engenharia de software gráfico e otimização de hardware. Ao passo que a transição de algoritmos lineares para árvores estruturadas se torna um padrão no mercado, é necessário investigar o comportamento teórico de algoritmos de $O(N)$ (como a rasterização simples) em comparação a algoritmos $O(\log N)$ para interseção espacial de raios (BVH). 

### 3.2 Viabilidade

| Critério | Avaliação (Sim/Parcial/Não) | Observação |
|---|---|---|
| Tempo disponível é suficiente | Sim | O projeto recorta variáveis subjetivas (qualidade visual) focando estritamente na complexidade teórica. |
| Há acesso a fontes/dados necessários | Sim | As bases científicas (IEEE Xplore, ACM, NVIDIA) fornecem vasta literatura revisada por pares sobre o tema. |
| O grupo já tem domínio mínimo do tema | Sim | O grupo domina os conceitos de renderização, tempo de execução e busca por grafos/árvores na computação. |
| Recursos técnicos necessários estão disponíveis | Sim | O trabalho é uma pesquisa bibliográfica qualitativa baseada em literatura de referência. |

### 3.3 Originalidade / Não-redundância
Ao contrário de comparações generalistas que enfocam fotorealismo, a pesquisa inova ao concentrar-se nas estruturas de dados (matriz bidimensional de profundidade vs árvores hierárquicas espaciais) e como seus custos de memória se comportam sob estresse.

## 4. Validação com o Orientador

| Campo | Informação |
|---|---|
| Data da conversa/validação | 15/09/2026 |
| Tema aprovado pelo orientador? | Sim com ajustes |
| Observações ou ajustes solicitados pelo orientador | A orientadora solicitou restringir a pesquisa à complexidade algorítmica e custo, deixando a qualidade visual como fator estritamente secundário. |

## 5. Contribuição Individual dos Integrantes

### Integrante 1 — Thiago de Luca Fernandes
- **O que fez nesta etapa:** Estruturei a delimitação do tema introduzindo o comparativo técnico (Z-buffer vs BVH) e desenvolvi a justificativa sobre complexidade espacial.
- **Tempo dedicado (aprox.):** 7h
- **Evidência da contribuição:** Escrita do detalhamento algorítmico inserido no repositório principal.

### Integrante 2 — Renan Veras de Andrade
- **O que fez nesta etapa:** Realizei o alinhamento da justificativa perante os ajustes solicitados pelo parecer, validando o recorte operacional.
- **Tempo dedicado (aprox.):** 4h
- **Evidência da contribuição:** Rascunhos compartilhados em grupo evidenciando o ajuste fino do escopo.

### Integrante 3 — Benito Juarez Jesus Viana Aguiar
- **O que fez nesta etapa:** Avaliei a viabilidade de execução do trabalho mediante o tempo restante e acesso às bases de dados ACM, IEEE e NVIDIA.
- **Tempo dedicado (aprox.):** 6h
- **Evidência da contribuição:** Levantamento primário da disponibilidade de artigos em plataformas acadêmicas.

### Integrante 4 — Augusto da Silva Domingues 
- **O que fez nesta etapa:** Compilei os quadros lógicos do template e revisei a fluidez narrativa das justificativas baseadas no modelo da disciplina.
- **Tempo dedicado (aprox.):** 6h
- **Evidência da contribuição:** Organização final do documento `.md` e validação do checklist final.

### 5.1 Quadro-resumo de participação

| Integrante | Contribuição principal | % estimado de participação nesta etapa |
|---|---|---|
| Thiago de Luca Fernandes | Escopo algorítmico e foco em Z-buffer/BVH | 30% |
| Renan Veras de Andrade | Ajustes conforme parecer da orientadora | 20% |
| Benito Juarez Jesus Viana Aguiar | Mapeamento de bases (ACM/IEEE/NVIDIA) e viabilidade | 30% |
| Augusto da Silva Domingues  | Revisão e formatação estrutural do template | 20% |

## 6. Checklist Final da Etapa

- [x] Tema delimitado e redigido em 1-2 frases
- [x] Justificativa de relevância escrita
- [x] Viabilidade avaliada pelo grupo
- [x] Verificação preliminar de originalidade realizada
- [x] Tema validado com o orientador
- [x] Contribuição individual de cada integrante registrada
- [x] Quadro-resumo de participação preenchido (soma = 100%)