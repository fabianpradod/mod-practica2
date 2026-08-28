# mod-practica2

Práctica 2 de **CC2017 Modelación y Simulación** — Ciclo 2, 2026. Universidad del Valle de Guatemala.

## Contenido

| Archivo | Descripción |
|---|---|
| [`Practica_2_Generacion_de_Variables_Aleatorias_Continuas.ipynb`](Practica_2_Generacion_de_Variables_Aleatorias_Continuas.ipynb) | Solución de los 10 ejercicios de variables aleatorias **continuas**, ejecutado. |
| [`Practica_2_Generacion_de_Variables_Aleatorias_Continuas.md`](Practica_2_Generacion_de_Variables_Aleatorias_Continuas.md) | Enunciado original de la práctica de continuas (transcripción del PDF). |
| [`Practica_2_Generacion_Variables_Aleatorias_Discretas.ipynb`](Practica_2_Generacion_Variables_Aleatorias_Discretas.ipynb) | Práctica de variables aleatorias **discretas**, usada como referencia de formato. |

## Ejercicios de la práctica continua

| # | Tema | Referencia exacta contra la que se valida |
|---|---|---|
| 1 | Exponencial truncada por transformación inversa | $E[X\mid X<0.05]=\frac{1-1.05e^{-0.05}}{1-e^{-0.05}}$ |
| 2 | Método de composición | $P(X\le x)=\sum_i p_iF_i(x)$ |
| 3 | Composición aplicada: polinomios y mezcla Exp/Uniforme | $E[X]=\tfrac{25}{36}$, $\tfrac12$, $\sum_i\alpha_i\tfrac{i}{i+1}$ |
| 4 | Riesgo agregado de una cartera de seguros | $P(S>50{,}000)=0.1070977$ (mezcla binomial–gamma) |
| 5 | Normal por rechazo con exponencial (Ejemplo 5f) | $c=\sqrt{2e/\pi}$, aceptación $1/c$ |
| 6 | Proceso de Poisson homogéneo | $N(T)\sim\text{Poisson}(\lambda T)$ |
| 7 | Poisson no homogéneo por adelgazamiento y mejoras | $m(10)=30+4\log 11$ |
| 8 | Proceso de Poisson bidimensional en un círculo | $E[N]=\lambda\pi R^2=25\pi$ |
| 9 | Método polar para normales | aceptación $\pi/4$, $4/\pi$ pares |
| 10 | Proceso de Poisson bidimensional: teoría y ejemplo | $N(A)\sim\text{Poisson}(\lambda\lvert A\rvert)$ |

## Metodología

Cada ejercicio sigue la misma estructura: **Método** (derivación y algoritmo paso a paso) → **código** con aserciones → **Respuesta**. Toda estimación Monte Carlo se contrasta contra su valor exacto —forma cerrada cuando existe, cuadratura de alta precisión en caso contrario— y se reporta la desviación en unidades de error estándar, además de pruebas de bondad de ajuste (Kolmogórov–Smirnov, chi-cuadrado) donde corresponde. Las simulaciones usan una semilla global fija, así que el notebook es reproducible.

## Ejecución

Requiere `numpy`, `scipy`, `pandas`, `matplotlib` y `jupyter`:

```
pip install numpy scipy pandas matplotlib jupyter
jupyter notebook Practica_2_Generacion_de_Variables_Aleatorias_Continuas.ipynb
```
