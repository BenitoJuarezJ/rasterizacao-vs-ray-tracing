# Etapa 7 Matriz de síntese e organização da revisão

## Eixos da revisão

1. Limitações Logísticas e de Memória da Rasterização (Z-buffer)
2. Escalabilidade e Gargalos de Travessia em Estruturas Hierárquicas Espaciais (BVH/Árvores)
3. O Ponto de Interseção do Desempenho Algorítmico (Matriz vs Árvore)

## Matriz de síntese

| Eixo | Artigos relacionados | Convergências | Divergências | Limitações | Lacunas |
|---|---|---|---|---|---|
| 1. Rasterização e Memória | Wyman et al. (2016); Ritschel et al. (2012); Lambru et al. (2021) | A rasterização possui tempo de acesso O(1) por pixel, mas seu escalonamento linear O(N) colapsa sob alta complexidade geométrica, esgotando a largura de banda. | Wyman et al. (2016) indicam que estruturar listas (linked lists) dentro do Z-buffer resolve falhas de varredura, enquanto Lambru et al. (2021) apontam que essa sobrecarga colapsa o hardware. | As avaliações de Rasterização focam principalmente no limite das matrizes bidimensionais, carecendo de testes híbridos massivos. | A literatura não define o limiar exato em que a contagem de polígonos satura a Texturing Mapping Unit (TMU) na leitura contígua. |
| 2. Árvores e BVH | Woop et al. (2006); Crassin et al. (2011) | O particionamento logarítmico O(log N) poupa a GPU de cálculos brutos, isolando o custo algorítmico do volume total de geometria na cena. | A origem técnica do gargalo varia: Woop indica que o problema é a leitura (DRAM) na travessia das árvores; Crassin foca no altíssimo custo de inicialização dos ponteiros. | Os estudos modelam o comportamento via simulações (ASIC/FPGA) ou uso de estruturas aproximadas (octrees esparsas). | Falta quantificar empiricamente o "imposto logístico" cobrado para realocar o BVH ou a Octree quadro a quadro em cenas dinâmicas. |
| 3. Comparativo Matriz x Árvore | Lambru et al. (2021); Ritschel et al. (2012) | O Z-buffer é superior pela localidade de cache e acesso contíguo rápido. Árvores espaciais reinam na geometria pesada, porém exigem hardware de aceleração para manter o tempo real. | Lambru aloca a falha de desempenho aos limites de memória cache, enquanto Ritschel dá ênfase à divergência de instruções (branch divergence) nos shaders da GPU. | Mapeamento testado historicamente em baixas resoluções, mascarando como a expansão vetorial de 4K pressionaria o Z-buffer. | Inexistência de um equacionamento matemático absoluto definindo o ponto de virada onde construir a árvore compensa a varredura linear. |

## Roteiro da revisão da literatura

### Eixo 1 - Limitações Logísticas e de Memória da Rasterização (Z-buffer)
- Ideia principal: A rasterização clássica ($O(N)$) e a matriz bidimensional não conseguem escalar de forma analítica frente à explosão de primitivas sem estressar a memória (VRAM e TMU).
- Evidências que serão usadas: A severa degradação de FPS sob alta resolução relatada por Lambru (2021); o alto custo registrado por Wyman (2016) ao forçar o "Irregular Z-buffer" a realizar operações de sobreposição atômica pesadas (162 ms).
- Comparação entre estudos: Ritschel (2012) aborda o limite conceitual do espaço de tela pela falta de dados globais, enquanto Wyman (2016) prova empiricamente que tentar burlar isso funde os recursos do barramento da placa gráfica.
- Ligação com o problema: Explica a base teórica de que o paradigma bidimensional (Z-buffer) é matematicamente incapaz de sobreviver a altos níveis de complexidade geométrica (Oclusão e Sombras), forçando a busca por soluções 3D.

### Eixo 2 - Escalabilidade e Gargalos de Travessia em Estruturas Espaciais
- Ideia principal: Estruturas hierárquicas como o BVH e Octrees resolvem as equações de interseção em velocidade vertiginosa ($O(\log N)$), mas transferem o gargalo computacional para a reconstrução de listas encadeadas.
- Evidências que serão usadas: A projeção de Woop (2006) de que a travessia logarítmica esgota o cache L2, exigindo unidades lógicas dedicadas (DRPU); e os testes de Crassin (2011) relatando quedas severas de *frame rate* (11,4 FPS) quando objetos dinâmicos quebram a árvore de volume pré-construída.
- Comparação entre estudos: Ambos corroboram a teoria de que o "calcanhar de Aquiles" do Ray Tracing mudou dos cálculos de geometria (interseção) para a latência de transferência de dados (Memory Bandwidth).
- Ligação com o problema: Complementa a análise mostrando que o BVH ganha assintoticamente, mas tem um custo pesado para ser estruturado na memória, compondo a balança principal da pesquisa.

## Síntese crítica provisória

A literatura revela uma clara dicotomia algorítmica: a rasterização (baseada no armazenamento matricial do Z-buffer) garante excelente coerência de memória e consultas de complexidade constante $O(1)$ por pixel, mas apresenta degradação catastrófica de forma linear ($O(N)$) ao esbarrar no limite físico da banda de leitura (TMU) em casos de alta sobreposição. Em contrapartida, estruturas espaciais hierárquicas, como o BVH e as Octrees, contornam a saturação de pixels por meio de varreduras logarítmicas ($O(\log N)$). No entanto, essas tecnologias tridimensionais exigem um salto substancial na largura de banda (DRAM) para acomodar as requisições de travessia do grafo, acarretando uma imensa penalidade de desempenho na reconstrução e alocação dinâmica dos *pointers* a cada quadro. Conclui-se, portanto, que a restrição de renderização em alta performance deixou de ser apenas a capacidade processual geométrica, passando a residir nos limites sistémicos de acesso à memória *cache* entre matrizes e árvores.

## Checklist

- [x] Os artigos foram agrupados por ideias.
- [x] Há comparações entre estudos.
- [x] As divergências foram registradas.
- [x] As lacunas são específicas e sustentadas pelas leituras.