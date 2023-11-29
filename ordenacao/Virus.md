# Exercício - Vírus
A secretaria de saúde pública da Nlogônia acabou de emitir um alerta. Um vírus está contagiando toda a população.

Após muitos estudos, os pesquisadores do país determinaram que, após infiltrarem o corpo hospedeiro, os virus se juntam dois a dois para tornarem-se letais. O nível de letalidade de uma infecção é determinado pela soma da diferença da idade, em dias, dos vírus pareados. Os vírus sem pares não influenciam no nível.

Desta forma, se existem 4 vírus no corpo hospedeiro com idades (em dias), iguais a

4, 10, 9, 43

E eles se paream da seguinte forma:

4 com 9, 43 com 10

Então nível de letalidade seria (9 - 4) + (43 - 10) = 38.

A secretaria de saúde pública da Nlogônia pediu para que você escrevesse um programa que, dado a contagem de vírus em um corpo e a idade de cada um deles, calcule o nível máximo de letalide que a infecção pode assumir.

## Entrada
A entrada contém vários casos de teste. A primeira linha de cada caso contém um inteiro N (1 ≤ N ≤ 1000), a quantidade de vírus no corpo hospedeiro. A linha seguinte contém N números inteiros ai (0 ≤ ai ≤ 1000) separados por espaços, as idades (em dias) de todos os vírus no corpo.

A entrada termina com fim-de-arquivo (EOF).

## Saída
Para cada caso de teste, imprima uma única linha contendo o nível de letalidade máximo que a infecção pode assumir.


## Solução

```python
from random import randint

def troca(L, i, j):
    temp = L[i]
    L[i] = L[j]
    L[j] = temp

def particiona(L, inicio, fim):
    sorteado = randint(inicio, fim)
    troca(L, inicio, sorteado)
    pivo = inicio
    i = inicio+1
    j = fim
    while i < j:
        while i < j and L[i] < L[pivo]: i += 1
        while L[j] > L[pivo]: j -= 1
        if i < j:
            troca(L, i, j)
            i += 1
            j -= 1
    pf = i if L[i] <= L[pivo] else i-1
    troca(L, pivo, pf)
    return pf

def quick_sort(L, inicio, fim):
    if inicio >= fim: return
    pivo = particiona(L, inicio, fim)
    quick_sort(L, inicio, pivo-1)
    quick_sort(L, pivo+1, fim)

def qsort(L):
    quick_sort(L, 0, len(L)-1)
    
def calc_letalidade():
    final = []
    try:
        while True:
            N = int(input())
            idades = input().split()
            idades_int = []
            for i in idades:
                idades_int.append(int(i))
            qsort(idades_int)
            inicio = 0
            fim = N -1
            letalidades = []
            while fim > inicio:
                idade_fim = idades_int[fim]
                idade_inicio = idades_int[inicio]
                letalidade = idade_fim - idade_inicio
                letalidades.append(letalidade)
                inicio +=1
                fim -=1
            somador = 0
            for i in letalidades:
                somador = somador + i
            final.append(somador)
    except:
        pass
    for i in final:
        print(i)

calc_letalidade()
```

### Exemplo de Entrada

```python
4
4 9 43 10
3
0 100 50
```

### Exemplo de Saída

```python
40
100
```