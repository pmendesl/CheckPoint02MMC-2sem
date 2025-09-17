# Integrantes: Pedro Mendes RM: 562242 / Leonardo Augusto RM: 565564 / Alexandre RM: 563346

# Checkpoint 02 - Modelagem Matemática e Computacional

## Pergunta 1: Aplicação de Sistemas de Equações Lineares

**Área do Conhecimento:** Engenharia Elétrica

**Aplicação:** Análise de Circuitos Elétricos em Corrente Contínua, utilizando as Leis de Ohm e as Leis de Kirchhoff para determinar as correntes em um circuito.

**Referência:**

*   Santos, W. V. D., & Primo, A. S. (2017). **APLICAÇÃO DA ÁLGEBRA LINEAR NA ENGENHARIA ELÉTRICA: ANÁLISE DE CIRCUITOS ELÉTRICOS EM CORRENTE CONTÍNUA**. *Cadernos de Graduação - Ciências Exatas e Tecnológicas*, 4(2), 25-36. Disponível em: [https://periodicos.set.edu.br/cadernoexatas/article/download/4017/2461/13810](https://periodicos.set.edu.br/cadernoexatas/article/download/4017/2461/13810)

## Pergunta 2: Significado dos Componentes do Sistema Ax=b

Para a aplicação de análise de circuitos elétricos, o sistema de equações lineares é representado na forma **Ax = b**, onde:

*   **Matriz A (Coeficientes):** Esta matriz é composta pelos valores das **resistências** dos componentes do circuito e pelos coeficientes que representam as relações entre as correntes, conforme estabelecido pelas Leis de Kirchhoff (Lei das Correntes e Lei das Tensões) e a Lei de Ohm. As unidades de medida para os elementos de A são Ohms (Ω).

*   **Vetor x (Incógnitas):** O vetor x representa as **correntes elétricas** desconhecidas que fluem através das diferentes malhas ou ramos do circuito. A resolução do sistema Ax=b nos fornece os valores dessas correntes. As unidades de medida para as incógnitas x são Ampères (A).

*   **Vetor b (Termos Constantes):** O vetor b é formado pelos valores das **fontes de tensão** (ou fontes de força eletromotriz) presentes no circuito. Estes são os termos independentes das equações. As unidades de medida para os termos constantes b são Volts (V).

**Significado Físico e Unidades de Medida:**

Ao resolver o sistema Ax=b, obtemos os valores das correntes elétricas (x) que circulam no circuito. Esses valores têm um **significado físico direto**, pois indicam a intensidade e a direção do fluxo de elétrons em cada parte do circuito. As unidades de medida são Ampères (A) para as correntes, Ohms (Ω) para as resistências (na matriz A) e Volts (V) para as tensões (no vetor b).

**Número de Equações e Incógnitas:**

O número de equações e incógnitas em um sistema linear derivado da análise de circuitos depende da complexidade do circuito. Geralmente, para cada malha independente ou nó do circuito, uma equação pode ser formulada. No exemplo do artigo de referência, um circuito com três correntes desconhecidas (I1, I2, I3) resulta em um sistema de **3 equações e 3 incógnitas**.


## Pergunta 3: Exemplo Numérico em Python

Para demonstrar a resolução de um sistema de equações lineares para o circuito elétrico, utilizaremos um exemplo numérico em Python com a biblioteca NumPy.

**Sistema de Equações (baseado no artigo de referência):**

Considerando o circuito base do artigo, as equações das malhas podem ser representadas como:

1.  `22*I1 - 10*I2 = 9`
2.  `-10*I1 + 57*I2 - 47*I3 = 0`
3.  `-47*I2 + 47*I3 = 9`

Onde I1, I2 e I3 são as correntes nas malhas. Este sistema pode ser escrito na forma matricial Ax=b:

```
A = [[22, -10, 0],
     [-10, 57, -47],
     [0, -47, 47]]

b = [[9],
     [0],
     [9]]
```

**Código Python:**

```python
import numpy as np

# Matriz A dos coeficientes (resistências)
A = np.array([
    [22, -10, 0],
    [-10, 57, -47],
    [0, -47, 47]
])

# Vetor b dos termos constantes (tensões)
b = np.array([
    [9],
    [0],
    [9]
])

print("Matriz A:")
print(A)
print("\nVetor b:")
print(b)

# Resolvendo o sistema Ax = b para x (correntes)
x = np.linalg.solve(A, b)

print("\nSolução (Vetor x - Correntes I1, I2, I3 em Ampères):")
print(x)
```

**Saída do Código:**

```
Matriz A:
[[ 22 -10   0]
 [-10  57 -47]
 [  0 -47  47]]

Vetor b:
[[9]
 [0]
 [9]]

Solução (Vetor x - Correntes I1, I2, I3 em Ampères):
[[1.5       ]
 [2.4       ]
 [2.59148936]]
```

As correntes calculadas são aproximadamente I1 = 1.5 A, I2 = 2.4 A e I3 = 2.59 A.

## Pergunta 4: Solução Exata ou Aproximada?

Foi possível obter uma **solução exata** para o sistema de equações lineares. A função `numpy.linalg.solve` é projetada para encontrar a solução exata de um sistema linear do tipo Ax=b, desde que a matriz A seja invertível (não singular). Em um ambiente computacional, os resultados são apresentados como números de ponto flutuante, que são representações aproximadas de números reais. No entanto, o algoritmo subjacente busca a solução analítica precisa.

**Justificativa:**

Sistemas de equações lineares, como o que representa o circuito elétrico, possuem uma solução única e exata se a matriz dos coeficientes (A) for não singular. O método utilizado pelo NumPy (`np.linalg.solve`) emprega algoritmos numéricos (como a decomposição LU) que, em teoria, fornecem a solução exata. Quaisquer pequenas variações nos resultados são devido à **precisão finita da representação de números de ponto flutuante** em computadores, e não a uma busca por uma solução inerentemente aproximada (como seria o caso em métodos iterativos para sistemas muito grandes ou mal-condicionados). O problema em questão é bem-condicionado e de pequeno porte, permitindo uma solução direta e precisa.
