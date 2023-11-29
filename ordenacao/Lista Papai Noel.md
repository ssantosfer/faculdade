# Exercício - Ordenando a Lista de Crianças do Papai Noel
Papai Noel está nos preparativos finais para a entrega dos presentes para as crianças do mundo todo pois o natal está chegando mais uma vez. Olhando suas novas listas de crianças que irão ganhar presentes neste ano ele percebeu que o duende estagiário (que havia ficado responsável por fazer as listas) não havia colocado os nomes em ordem alfabética.

Como o Papai Noel é um homem muito organizado ele deseja que cada lista de crianças possua, no seu final, o total de crianças que foram bem comportadas neste ano e um total das que não foram. Assim ele pode comparar a quantidade de crianças que se comportam este ano com as dos anos anteriores.

Para ajudar o bom velhinho, seu dever é criar um programa que leia todos os nomes da lista e imprima os mesmos nomes em ordem alfabética. No final da lista, você deve imprimir o total de crianças que foram e não foram comportadas neste ano.

## Entrada
A entrada é composta por vários nomes. O primeiro valor N (0 ≤ N ≤ 100), indica quantos nomes tem na lista. As N linhas seguintes, contem um caracter especial correspondente ao comportamento da criança (+ indica que a criança foi bem comportada, - indica que a criança não foi bem comportada). Após o caracter especial, segue o nome da criança com no máximo 20 caracteres.

## Saída
Para cada lista de crianças, você deve imprimir os nomes em ordem alfabética. Após imprimir os nomes das crianças, você deve mostrar o total de crianças que se comportaram bem ou mal durante o ano.


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

qtd_nomes = int(input())
comportada = 0
incomportada = 0

nomes = []
for i in range(qtd_nomes):
    nome = input()
    nomes.append(nome[2:])
    if nome[0] == '+':
        comportada +=1
    else:
        incomportada +=1

def exibe_nomes(nomes):
    qsort(nomes)
    for i in nomes:
        print(i)
    print(f'Se comportaram: {comportada} | Nao se comportaram: {incomportada}')

exibe_nomes(nomes)
```

### Exemplo de Entrada

```python
16
+ Tininha
+ Dudinha
- Carlinhos
- Marquinhos
+ Joaozinho
+ Bruninha
- Leandrinho
- Fernandinha
+ Rafinha
- Pedrinho
+ Aninha
- Tamirinha
- Gaguinho
- Zezinho
- Luquinhas
+ Julhinha
```

### Exemplo de Saída

```python
Aninha
Bruninha
Carlinhos
Dudinha
Fernandinha
Gaguinho
Joaozinho
Julhinha
Leandrinho
Luquinhas
Marquinhos
Pedrinho
Rafinha
Tamirinha
Tininha
Zezinho

Se comportaram: 7 | Nao se comportaram: 9
```