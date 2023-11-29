# Exercício - Exame Geral
Todo ano bissexto é realizado o exame geral de matemática da Nlogônia. Todos os cidadãos da nação são avaliados a fim de se estudar o desenvolvimento lógico e matemático do país ao longo dos anos.

Após as correções, os cidadãos são ordenadados de acordo com suas notas (quanto maior, melhor) e recebem descontos no imposto de renda de acordo com sua qualificação.

O Escritório Central de Estatística (ECE) é encarregado de processar os dados das notas obtidas no exame. Entretanto este ano, Vasya, um dos responsáveis, está internado no hospital com gripe H1N1 e você foi contratado para realizar o seu trabalho.

Escreva um programa que dado o número de habitantes da Nlogônia e todas as notas obtidas, responda as consultas para retornar a nota do cidadão que ficou em determinada posição.

## Entrada
A entrada contém vários casos de teste. A primeira linha de cada caso contém dois inteiros N (1 ≤ N ≤ 100), Q (1 ≤ Q ≤ 100), o número de habitantes do país e o número de consultas, respectivamente.

As N linhas seguintes contém, cada uma, a nota ni obtida pelo i-ésimo cidadão (0 ≤ ni ≤ 30000).

As próximas Q linhas contém cada uma uma consulta, a posição pi (1 ≤ pi ≤ N) a qual a ECE está interessada em saber a nota.

A entrada termina com fim-de-arquivo (EOF).

## Saída
Para cada caso de teste, imprima, para cada consulta, uma linha contendo a nota do cidadão que ficou classificado na posição pi


## Solução

```python
def troca(L, i, j):
    temp = L[i]
    L[i] = L[j]
    L[j] = temp

def empurra(L, n):
    i = 0
    while i < n-1:
        if L[i] < L[i+1]:
            troca(L, i, i+1)
        i += 1

def bubble_sort(L):
    n = len(L)
    while n > 1:
        empurra(L, n)
        n -= 1

def resultado():
    try:
        while True:
            N, Q = input().split()
            N, Q = int(N), int(Q)
            notas = []

            for i in range(N):
                nota = int(input())
                notas.append(nota)

            bubble_sort(notas)
            consultas = []

            for i in range(Q):
                consulta = int(input())
                consultas.append(consulta)

            for i in consultas:
                print(notas[i-1])
    except:
        pass

resultado()
```

### Exemplo de Entrada

```python
6 5
30
30
40
250
100
15
1
5
3
2
4
```

### Exemplo de Saída

```python
250
30
40
100
30
```