# Exercício - Fila do Recreio
Na escola onde você estuda, a hora do recreio é a mais aguardada pela grande maioria dos alunos. Não só porque as vezes as aulas são cansativas, mas sim porque a merenda servida é muito boa, preparada por um chefe italiano muito caprichoso.

Quando bate o sinal para a hora do recreio, todos os alunos saem correndo da sua sala para chegar o mais cedo possível na cantina, tanta é a vontade de comer. Um de seus professores notou, porém, que havia ali uma oportunidade.

Utilizando um sistema de recompensa, seu professor de matemática disse que a ordem da fila para se servir será dada não pela ordem de chegada, mas sim pela soma das notas obtidas em sala de aula. Assim, aqueles com maior nota poderão se servir antes daqueles que tem menor nota.

Sua tarefa é simples: dada a ordem de chegada dos alunos na cantina, e as suas respectivas notas na matéria de matemática, reordene a fila de acordo com as notas de matemática, e diga quantos alunos não precisaram trocar de lugar nessa reordenação.

## Entrada
A primeira linha contém um inteiro N, indicando o número de casos de teste a seguir.

Cada caso de teste inicia com um inteiro M (1 ≤ M ≤ 1000), indicando o número de alunos. Em seguida haverá M inteiros distintos Pi (1 ≤ Pi ≤ 1000), onde o i-ésimo inteiro indica a nota do i-ésimo aluno.

Os inteiros acima são dados em ordem de chegada, ou seja, o primeiro inteiro diz respeito ao primeiro aluno a chegar na fila, o segundo inteiro diz respeito ao segundo aluno, e assim sucessivamente.

## Saída
Para cada caso de teste imprima uma linha, contendo um inteiro, indicando o número de alunos que não precisaram trocar de lugar mesmo após a fila ser reordenada.


# Solução

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


def casos_testes():
    numero_de_alunos = int(input())
    notas = input().split()
    notas_int = []
    for i in notas:
        notas_int.append(int(i))
    notas_ordenadas = notas_int[:]
    bubble_sort(notas_ordenadas)

    nao_precisaram_trocar = 0
    for i in range(numero_de_alunos):
        if notas_int[i] == notas_ordenadas[i]:
            nao_precisaram_trocar += 1

    return nao_precisaram_trocar

def final():
    resultados = []
    numero_casos = int(input())
    for _ in range(numero_casos):
        resultado = casos_testes()
        resultados.append(resultado)
    for i in resultados:
        print(i)

final()
```

### Exemplo de Entrada

```python
3
3
100 80 90
4
100 120 30 50
4
100 90 30 25
```

### Exemplo de Saída

```python
1
0
4
```