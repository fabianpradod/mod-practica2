# Práctica 2 - Generación de Variables Aleatorias Continuas

> Transcripción completa del PDF original a Markdown.
> Revisada página por página para conservar ejercicios, fórmulas, algoritmos y material de apoyo.


---

# Página 1

Universidad del Valle de Guatemala
Facultad de Ingeniería
Ciencia de la Computación y Tecnologías de la información
CC2017 - Modelación y Simulación
Ciclo 2, 2026
Ejercicio 1
Sea X una variable aleatoria exponencial con media 1. Proporcione un algoritmo eficiente para
simular una variable aleatoria cuya distribución es la distribución condicional de X dado que X <
0,05. Es decir, su función de densidad es
f(x) =
e−x
1 −e−0,05 ,
0 < x < 0,05.
Genere 1000 de estas variables y utilícelas para estimar E[X | X < 0,05]. Luego determine el
valor exacto de E[X | X < 0,05].
Ejercicio 2 (Método de composición)
Suponga que es relativamente fácil generar variables aleatorias a partir de cualquiera de las dis-
tribuciones Fi, i = 1, . . . , n. ¿Cómo podríamos generar una variable aleatoria con función de dis-
tribución
F(x) =
n
∑︂
i=1
piFi(x)
donde pi, i = 1, . . . , n, son números no negativos cuya suma es 1?
Ejercicio 3
Utilizando el resultado del Ejercicio 2, proporcione algoritmos para generar variables aleatorias a
partir de las siguientes distribuciones.
(a) F(x) = x + x3 + x5
3
,
0 ≤x ≤1
(b) F(x) =
⎧
⎪
⎪
⎨
⎪
⎪
⎩
1 −e−2x + 2x
3
0 < x < 1
3 −e−2x
3
1 < x < ∞
(c) F(x) =
n
∑︂
i=1
αixi,
0 ≤x ≤1,
donde αi ≥0,
n
∑︂
i=1
αi = 1
Ejercicio 4
Una compañía de seguros contra siniestros tiene 1000 asegurados, cada uno de los cuales pre-
sentará una reclamación en el próximo mes de manera independiente con probabilidad 0.05. Su-
poniendo que los montos de las reclamaciones son variables aleatorias exponenciales indepen-
dientes con media $800, utilice simulación para estimar la probabilidad de que la suma de estas
reclamaciones exceda $50,000.
Página 1

---

# Página 2

Universidad del Valle de Guatemala
Facultad de Ingeniería
Ciencia de la Computación y Tecnologías de la información
CC2017 - Modelación y Simulación
Ciclo 2, 2026
Ejercicio 5
Escriba un programa que genere variables aleatorias normales utilizando el método del Ejemplo
5f (método de rechazo con una distribución exponencial de tasa 1).
Ejercicio 6
Escriba un programa que genere las primeras T unidades de tiempo de un proceso de Poisson
con tasa λ.
Ejercicio 7
(a) Escriba un programa que utilice el algoritmo de adelgazamiento (thinning) para generar las
primeras 10 unidades de tiempo de un proceso de Poisson no homogéneo con función de
intensidad
λ(t) = 3 +
4
t + 1
(b) Proponga una manera de mejorar el algoritmo de adelgazamiento para este ejemplo.
Ejercicio 8
Escriba un programa para generar los puntos de un proceso de Poisson bidimensional dentro de
un círculo de radio R, y ejecute el programa para λ = 1 y R = 5. Grafique los puntos obtenidos.
Material de apoyo: Ejemplo 5f — Generación de una variable aleatoria normal
Para generar una variable aleatoria normal estándar Z (es decir, con media 0 y varianza 1), se
observa primero que el valor absoluto de Z tiene función de densidad
f(x) =
√︃
2
π e−x2/2,
0 < x < ∞.
Esta densidad se genera usando el método de rechazo, tomando como densidad auxiliar g la
exponencial de media 1, es decir g(x) = e−x, 0 < x < ∞. Entonces
f(x)
g(x) =
√︁
2/π e x−x2/2,
cuyo máximo ocurre en x = 1, lo que da la constante
c = máx
x
f(x)
g(x) = f(1)
g(1) =
√︁
2e/π.
Página 2

---

# Página 3

Universidad del Valle de Guatemala
Facultad de Ingeniería
Ciencia de la Computación y Tecnologías de la información
CC2017 - Modelación y Simulación
Ciclo 2, 2026
Como f(x)
c g(x) = exp
{︃
−(x −1)2
2
}︃
, se obtiene el siguiente algoritmo para generar el valor absoluto
de una normal estándar:
Paso 1: Genere Y , una exponencial con tasa 1.
Paso 2: Genere un número aleatorio U.
Paso 3: Si U ≤exp{−(Y −1)2/2}, haga X = Y . En caso contrario, regrese al Paso 1.
Una vez generado X (que se distribuye como el valor absoluto de una normal estándar), se ob-
tiene Z haciendo que sea igualmente probable que valga X o −X (esto se decide con un número
aleatorio adicional: si U ≤1/2 entonces Z = X; si no, Z = −X).
Puede demostrarse además que la condición de aceptación del Paso 3 es equivalente a −log U ≥
(Y −1)2/2, y como −log U es exponencial de tasa 1, se obtiene la siguiente versión equivalente,
que genera simultáneamente una normal estándar y — como subproducto — una exponencial
independiente de tasa 1:
Paso 1: Genere Y1, exponencial con tasa 1.
Paso 2: Genere Y2, exponencial con tasa 1.
Paso 3: Si Y2 −(Y1 −1)2/2 > 0, haga Y = Y2 −(Y1 −1)2/2 y continúe al Paso 4. En caso
contrario, regrese al Paso 1.
Paso 4: Genere un número aleatorio U y haga
Z =
{︄
Y1
si U ≤1/2
−Y1
si U > 1/2
Z (normal estándar) e Y (exponencial de tasa 1) resultan independientes. Dado que c =
√︁
2e/π ≈
1,32, en promedio el algoritmo requiere generar 1,64 exponenciales y calcular 1,32 cuadrados por
cada normal generada. (Si se desea una normal de media µ y varianza σ2, basta con tomar µ+σZ.)
Ejercicio 9
Explique el método polar para generar variables aleatorias normales. Su explicación debe incluir:
(a) En qué consiste el método (idea general y algoritmo paso a paso).
(b) Para qué sirve (qué problema resuelve y por qué es preferible frente al uso directo de las
transformaciones de Box–Muller).
(c) Un ejemplo numérico: elija valores de U1 y U2 y aplique el algoritmo paso a paso hasta
obtener el par de normales X, Y (si el primer par (V1, V2) cae fuera del círculo unitario, elija
un segundo par y continúe).
Página 3

---

# Página 4

Universidad del Valle de Guatemala
Facultad de Ingeniería
Ciencia de la Computación y Tecnologías de la información
CC2017 - Modelación y Simulación
Ciclo 2, 2026
Ejercicio 10
Explique el proceso de Poisson bidimensional y el algoritmo para simularlo dentro de una región
circular. Su explicación debe incluir:
(a) En qué consiste (definición formal del proceso y el algoritmo de simulación paso a paso).
(b) Para qué sirve (qué tipo de fenómenos se pueden modelar con este proceso y por qué es
útil poder simularlo).
(c) Un ejemplo numérico: para λ = 1 y r = 2, elija valores de X1, X2, . . . (o de los números
aleatorios necesarios para generarlos) y aplique el algoritmo paso a paso hasta obtener las
coordenadas polares de los puntos simulados.
Página 4