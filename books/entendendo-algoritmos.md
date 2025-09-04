# Entendendo Algoritmos — Aditya Y. Bhargava

**Categoria:** Algorithms & Data Structures  
**Avaliação pessoal:** ★★★★★  

---

## Capítulo 1 — Introdução a algoritmos
- Algoritmo = conjunto de instruções.  
- Pesquisa binária: O(log n), vs busca linear: O(n).  
- Notação Big O descreve crescimento do custo.  
**Resumo IA:** O capítulo mostra como a pesquisa binária reduz drasticamente o número de operações e introduz a notação Big O para comparar algoritmos.

---

## Capítulo 2 — Ordenação por seleção (arrays e listas encadeadas)
- Arrays: acesso aleatório O(1), inserções caras.  
- Listas: inserções baratas, acesso aleatório O(n).  
- Ordenação por seleção: O(n²).  
**Resumo IA:** Compara arrays vs listas encadeadas e introduz ordenação por seleção como motivação para algoritmos mais rápidos.

---

## Capítulo 3 — Recursão
- Definir caso-base e caso recursivo.  
- Pilha de chamadas consome memória.  
**Resumo IA:** Recursão simplifica o raciocínio, mas deve ser usada com cuidado por conta do consumo de pilha.

---

## Capítulo 4 — Quicksort (Dividir para conquistar)
- Divide e conquista = subproblemas menores + combinação.  
- Quicksort: médio O(n log n), pior caso O(n²).  
**Resumo IA:** Algoritmo rápido na prática; escolha do pivô define eficiência.

---

## Capítulo 5 — Tabelas hash
- Funções hash para mapear chaves.  
- Colisões (encadeamento, open addressing).  
- Fator de carga influencia desempenho.  
**Resumo IA:** Estrutura poderosa para buscas rápidas, mas depende de uma boa função hash.

---

## Capítulo 6 — Pesquisa em largura (BFS)
- Grafos: nós + arestas.  
- BFS encontra caminho mais curto em grafos não ponderados.  
- Complexidade: O(V+E).  
**Resumo IA:** Algoritmo simples que garante o menor número de arestas entre dois nós.

---

## Capítulo 7 — Algoritmo de Dijkstra
- Caminho mínimo em grafos ponderados (pesos não-negativos).  
- Estruturas influenciam desempenho (heap).  
**Resumo IA:** Essencial em grafos ponderados; ineficaz com pesos negativos.

---

## Capítulo 8 — Algoritmos gulosos
- Escolhem sempre a opção localmente ótima.  
- Funcionam em alguns problemas (interval scheduling, mochila fracionária).  
- Aproximações em problemas NP-completos.  
**Resumo IA:** Estratégia prática e rápida, mas não garante sempre a solução ótima.

---

## Capítulo 9 — Programação dinâmica
- Resolve subproblemas sobrepostos.  
- Problema da mochila, LCS como exemplos.  
**Resumo IA:** Constrói soluções complexas a partir de tabelas de subproblemas, transformando exponencial em polinomial.

---

## Capítulo 10 — K-vizinhos mais próximos (KNN)
- Classificação e regressão baseadas em proximidade.  
- Importância das features e da normalização.  
**Resumo IA:** Método intuitivo e versátil, mas pesado para consultas grandes.

---


# Exemplos de código (Python)

A seguir, algumas implementações simplificadas dos algoritmos mais importantes apresentados no livro:

### Pesquisa binária
```python
def pesquisa_binaria(lista, item):
    baixo, alto = 0, len(lista) - 1
    while baixo <= alto:
        meio = (baixo + alto) // 2
        chute = lista[meio]
        if chute == item:
            return meio
        if chute > item:
            alto = meio - 1
        else:
            baixo = meio + 1
    return None
```

### Ordenação por seleção
```python
def busca_menor(arr):
    menor = arr[0]
    menor_indice = 0
    for i in range(1, len(arr)):
        if arr[i] < menor:
            menor = arr[i]
            menor_indice = i
    return menor_indice

def ordenacao_por_selecao(arr):
    novo_arr = []
    for _ in range(len(arr)):
        menor = busca_menor(arr)
        novo_arr.append(arr.pop(menor))
    return novo_arr
```

### Quicksort
```python
def quicksort(arr):
    if len(arr) < 2:
        return arr
    else:
        pivo = arr[0]
        menores = [i for i in arr[1:] if i <= pivo]
        maiores = [i for i in arr[1:] if i > pivo]
        return quicksort(menores) + [pivo] + quicksort(maiores)
```

### Pesquisa em largura (BFS)
```python
from collections import deque

def pesquisa_em_largura(grafo, inicio):
    fila = deque()
    fila += grafo[inicio]
    visitados = set()
    while fila:
        pessoa = fila.popleft()
        if pessoa not in visitados:
            print(pessoa)
            fila += grafo.get(pessoa, [])
            visitados.add(pessoa)
```

### Dijkstra
```python
def dijkstra(grafo, inicio):
    custos = {n: float("inf") for n in grafo}
    custos[inicio] = 0
    pais = {}
    processados = set()

    nodo = inicio
    while nodo is not None:
        custo = custos[nodo]
        vizinhos = grafo[nodo]
        for v in vizinhos:
            novo_custo = custo + vizinhos[v]
            if novo_custo < custos[v]:
                custos[v] = novo_custo
                pais[v] = nodo
        processados.add(nodo)
        nodo = min(
            (n for n in custos if n not in processados),
            key=custos.get,
            default=None
        )
    return custos, pais
```

### Programação dinâmica — Problema da mochila
```python
def mochila(capacidade, pesos, valores, n):
    if n == 0 or capacidade == 0:
        return 0
    if pesos[n-1] > capacidade:
        return mochila(capacidade, pesos, valores, n-1)
    else:
        return max(
            valores[n-1] + mochila(capacidade - pesos[n-1], pesos, valores, n-1),
            mochila(capacidade, pesos, valores, n-1)
        )
```

### K-vizinhos mais próximos (KNN — versão simplificada)
```python
import math
from collections import Counter

def distancia_euclidiana(p1, p2):
    return math.sqrt(sum((x - y) ** 2 for x, y in zip(p1, p2)))

def knn(dados, consulta, k=3):
    distancias = [(distancia_euclidiana(consulta, ponto[:-1]), ponto[-1]) for ponto in dados]
    distancias.sort(key=lambda x: x[0])
    vizinhos = [rotulo for _, rotulo in distancias[:k]]
    return Counter(vizinhos).most_common(1)[0][0]
```

