<div align="center">
  <img alt="starknet logo" src="./assets/Starknet.png" width="200" >
  <h1 align="center">StarknetEs Basecamp - Maths Starks</h1>
  <p align="center">
</div>

# Traducción Starknet Basecamp - Stark Maths

Puede encontrar las notas originales [aquí](https://bit.ly/starkmaths2023)

## Temas

- [Matemáticas de base](#matemáticas-de-base)
    - [Aritmética modular](#aritmética-modular)
    - [Campos finitos](#campos-finitos)
    - [Polinomios](#polinomios)
- [Sistemas de comprobación ZK](#sistemas-de-comprobación-ZK)
    - [Sistema de comprobación idealizado para la integridad computacional](#sistema-de-comprobación-idealizado-para-laintegridad-computacional)
    - [Uso de polinomios y restricciones](#uso-de-polinomios-y-restricciones)
- [Integridad computacional](#integridad-computacional)
- [Starks](#starks)
    - [Visión general del proceso stark](#visión-general-del-proceso-stark)
    - [Aritmetización](#aritmetización)
    - [FRI](#fri)
    - [Cairo y el no determinismo](#cairo-y-el-no-determinismo)

### Matemáticas de base
#### Terminología
* El conjunto de los números enteros se designa `Z`, por ejemplo, con {⋯,-4,-3,-2,-1,0,1,2,3,4,⋯}.
* El conjunto de los números racionales se designa `Q`, por ejemplo, con {...1,3/2,2,22/7...}.
* El conjunto de los Números Reales se designa `R` por ejemplo. {2, -4, 613, π, √ 2, ...}.

Los fields se denotan por `F`, si son un campo finito o `K` para un campo de números reales o complejos
también usamos `Z∗p` para representar un campo finito de enteros mod prime p con inversos multiplicativos.

Utilizamos campos finitos para la criptografía, porque los elementos tienen representaciones "cortas", exactas y propiedades útiles.

#### Aritmética modular
[Véase esta introducción](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)

![Graph](/im%C3%A1genes/AritemticaModular.png)

Cuando escribimos n mod k nos referimos simplemente al resto cuando n se divide por k. Así:

```bash
25 mod 3 = 1
15 mod 4 = 3
```
El resto debe ser positivo.

### Teoría de grupos y campos
#### Campos Finitos
Un grupo es un conjunto de elementos {a,b,c,...} (nos referimos a grupos de números, pero pueden ser cualquier cosa) más una operación binaria, que aquí representamos como `•`. 

Para ser considerada un grupo, esta combinación debe tener ciertas propiedades

1. Cierre.
    * Para todo a, b en G,  el resultado de la operación, a • b, también está en G
2. Asociatividad.
    * Para todos los a, b y c en G, (a • b) • c = a • (b • c)
3. Elementos de identidad.
    * Existe un elemento e en G tal que, para cada elemento a en G, la ecuación e • a = a • e = a. Tal elemento es único y por lo tanto se habla del elemento identidad.
4. Elemento inverso.
    * Para cada a en G, existe un elemento b en G, comúnmente denotado a-1 (o -a, si la operación se denota "+"), tal que a • b = b • a = e, donde e es el elemento identidad.

#### Subgrupos
Si un subconjunto de los elementos de un grupo también satisface las propiedades del grupo, entonces es un subgrupo del grupo original.

#### Grupos cíclicos y generadores
Un grupo finito puede ser cíclico. Esto significa que tiene un elemento generador. Si se empieza en un punto cualquiera y luego se aplica la operación de grupo con el generador como argumento un cierto número de veces, se da la vuelta a todo el grupo y se termina en el mismo sitio, véase más abajo.

#### Encontrar una inversa
Del pequeño teorema de Fermat

```
a elevado -1 ≡ a elevado p -2(modp)
```
![Graph](/im%C3%A1genes/inver.png)
Sea p = 7 y a = 2. Podemos calcular la inversa de a como:

```
a elevado p -2 = 2 elevado 5 = 32 ≡ 4 mod 7.
```
![Graph](/im%C3%A1genes/inver2.png)

Esto es fácil de verificar: 2 x 4 ≡ 1 mod 7.