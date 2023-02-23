<div align="center">
  <img alt="starknet logo" src="./assets/Starknet.png" width="200" >
  <h1 align="center">StarknetEs Basecamp - Maths Starks</h1>
  <p align="center">
</div>

# Traducción Starknet Basecamp - Stark Maths

Puede encontrar las notas originales [aquí](https://bit.ly/starkmaths2023)

## Temas

- [Matemáticas de base](#matemáticas-de-base)
    - [Terminología](#terminología)
    - [Aritmética modular](#aritmética-modular)
    - [Teoría de grupos y campos](#teoría-de-grupos-y-campos)
    - [Subgrupos](#subgrupos)
    - [Grupos cíclicos y generadores](#grupos-cíclicos-y-generadores)
    - [Encontrar una inversa](#encontrar-una-inversa)
    - [Campos](#campos)
    - [Campos finitos y generadores](#campos-finitos-y-generadores)
    - [Polinomios](#polinomios)
    - [Lemma de Schwartz-Zippel](#lemma-de-schwartz-zippel)
    - [Interpolación de Lagrange](#interpolación-de-lagrange)
- [Sistemas de prueba de conocimiento cero](#sistemas-de-prueba-de-conocimiento-cero)
    - [¿Qué es una prueba de conocimiento cero?](#qué-es-una-prueba-de-conocimiento-cero)
    - [Actores en un sistema a prueba de conocimiento cero](#actores-en-un-sistema-a-prueba-de-conocimiento-cero)
    - [Sistema de comprobación idealizado para la integridad computacional](#sistema-de-comprobación-idealizado-para-laintegridad-computacional)
    - [Uso de polinomios y restricciones](#uso-de-polinomios-y-restricciones)
- [Integridad computacional](#integridad-computacional)
- [Starks](#starks)
    - [Visión general del proceso stark](#visión-general-del-proceso-stark)
    - [Aritmetización](#aritmetización)
    - [FRI](#fri)
    - [Cairo y el no determinismo](#cairo-y-el-no-determinismo)

## Matemáticas de base
### Terminología
* El conjunto de los números enteros se designa `ℤ`, por ejemplo, con {⋯,-4,-3,-2,-1,0,1,2,3,4,⋯}.
* El conjunto de los números racionales se designa `ℚ`, por ejemplo, con {...1,3/2,2,22/7...}.
* El conjunto de los Números Reales se designa `ℝ` por ejemplo. {2, -4, 613, π, √ 2, ...}.

Los fields se denotan por `𝔽`, si son un campo finito o `𝕂` para un campo de números reales o complejos
también usamos `ℤ*ₚ` para representar un campo finito de enteros mod prime p con inversos multiplicativos.

Utilizamos campos finitos para la criptografía, porque los elementos tienen representaciones "cortas", exactas y propiedades útiles.

### Aritmética modular
[Véase esta introducción](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)

![Graph](/im%C3%A1genes/AritemticaModular.png)

Cuando escribimos n mod k nos referimos simplemente al resto cuando n se divide por k. Así:

```bash
25 mod 3 = 1
15 mod 4 = 3
```
El resto debe ser positivo.

### Teoría de grupos y campos
Un grupo es un conjunto de elementos {a,b,c,...} (nos referimos a grupos de números, pero pueden ser cualquier cosa) más una operación binaria, que aquí representamos como `•`. 

Para ser considerada un grupo, esta combinación debe tener ciertas propiedades

1. Cierre.
    * Para todo a, b en G,  el resultado de la operación, a • b, también está en G
2. Asociatividad.
    * Para todos los a, b y c en G, (a • b) • c = a • (b • c)
3. Elementos de identidad.
    * Existe un elemento e en G tal que, para cada elemento a en G, la ecuación e • a = a • e = a. Tal elemento es único y por lo tanto se habla del elemento identidad.
4. Elemento inverso.
    * Para cada a en G, existe un elemento b en G, comúnmente denotado α⁻¹ (o -a, si la operación se denota "+"), tal que a • b = b • a = e, donde e es el elemento identidad.

### Subgrupos
Si un subconjunto de los elementos de un grupo también satisface las propiedades del grupo, entonces es un subgrupo del grupo original.

### Grupos cíclicos y generadores
Un grupo finito puede ser cíclico. Esto significa que tiene un elemento generador. Si se empieza en un punto cualquiera y luego se aplica la operación de grupo con el generador como argumento un cierto número de veces, se da la vuelta a todo el grupo y se termina en el mismo sitio, véase más abajo.

### Encontrar una inversa
Del pequeño teorema de Fermat

![Graph](/im%C3%A1genes/inver.png)

Sea p = 7 y a = 2. Podemos calcular la inversa de a como:

![Graph](/im%C3%A1genes/inver2.png)

Esto es fácil de verificar: 2 x 4 ≡ 1 mod 7.

### Campos
Un campo es un conjunto de números enteros junto con dos operaciones llamadas suma y multiplicación.

Un ejemplo de campo son los números reales sometidos a adición y multiplicación, otro es un conjunto de números enteros mod un número primo con adición y multiplicación. 

Se requiere que las operaciones de campo satisfagan los siguientes axiomas de campo. En estos axiomas, a, b y c son elementos arbitrarios del campo `𝔽`.

1. Asociatividad de la suma y la multiplicación: `a + (b + c) = (a + b) + c` y `a • (b • c) = (a • b) • c`.
2. Conmutatividad de la suma y la multiplicación: `a + b = b + a` y `a • b = b • a`
3. Identidad aditiva y multiplicativa: existen dos elementos diferentes 0 y 1 en `𝔽` tales que `a + 0 = a` y `a • 1 = a`.
4. Inversos aditivos: para cada a en F, existe un elemento en F, denotado -a, llamado inverso aditivo de a, tal que `a + (-a) = 0`.
5. Inversos multiplicativos: para cada a ≠ 0 en F, existe un elemento en F, denotado por α⁻¹, llamado inverso multiplicativo de a, tal que `a•α⁻¹ = 1`.
6. Distributividad de la multiplicación sobre la suma: `a•(b + c) = (a•b) + (a•c)`.

### Campos finitos y generadores
Un campo finito es un campo con un conjunto finito de elementos, como el conjunto de enteros mod p donde p es un primo.

Para probar operaciones en campos finitos, [consulte aquí](https://asecuritysite.com/encryption/finite)

El orden del campo es el número de elementos del conjunto del campo.

Un elemento puede representarse como un número entero mayor o igual que 0 y menor que el orden del campo: {0, 1, ..., p-1} en un campo simple.

Todo campo finito tiene un generador. Un generador es capaz de generar todos los elementos del conjunto exponenciando el generador.
Así que para el generador g podemos tomar g⁰, g¹ ,g² y finalmente esto nos dará todos los elementos del grupo.

Por ejemplo, si tomamos el conjunto de los números enteros y el primo p = 5, obtenemos el grupo ℤ*₅ = {0,1,2,3,4}. 
En el grupo ℤ*₅ las operaciones se realizan en módulo 5; por lo
5 tanto, no tenemos 3 × 4 = 12 sino 3 × 4 = 2, porque 12 mod 5 = 2.

ℤ*₅ es cíclico y tiene dos generadores, 2 y 3, porque `2¹ = 2, 2² = 4, 2³ = 3, 2⁴ = 1`, y `3¹ = 3, 3² = 4, 3³ = 2, 3⁴ = 1`

En un campo finito de orden 𝔮, el polinomio X elevado 𝔮 - X tiene todos los q elementos del campo finito como raíces.

### Polinomios
Un polinomio es una ecuación de la forma

![Graph](/im%C3%A1genes/poli.png)

Donde los valores a son constantes, y x es una variable, si nuestro polinomio tiene una sola variable, se llama polinomio univariante.

Un hecho básico sobre los polinomios y sus raíces es que si `p(x)` es un polinomio, entonces `p(a) = 0` para algún valor específico `𝔞`

Si y sólo si existe un polinomio `q(x)` tal que `(x-a)q(x) = p(x)`, y por lo tanto 

![Graph](/im%C3%A1genes/poli2.png)

Esto es válido para todas las raíces, volveremos sobre ello más adelante.

### Lemma de Schwartz-Zippel
"diferentes polinomios son diferentes en la mayoría de los puntos".

Los polinomios tienen una propiedad ventajosa, a saber, si tenemos dos polinomios no iguales de grado como máximo `d`, no pueden intersecarse en más de `d` puntos.

![Graph](/im%C3%A1genes/Zippel2.png)

### Interpolación de Lagrange
Si tienes un conjunto de puntos, al hacer una interpolación de Lagrange en esos puntos obtienes un polinomio que pasa por todos esos puntos.
Si tienes dos puntos en un plano, puedes definir una única recta que pase por ambos, para 3 puntos, una única curva de 2º grado `(por ejemplo, 5x2 + 2x + 1)` pasará por ellos, etc.
Para `n` puntos, puedes crear un polinomio de grado `n-1` que pase por todos los puntos.

![Graph](/im%C3%A1genes/Lagrange.png)

## Sistemas de prueba de conocimiento cero
### Qué es una prueba de conocimiento cero
#### Una definición imprecisa
Es una prueba de que existe o de que sabemos algo, más un aspecto de conocimiento cero,es decir, la persona que verifica la prueba sólo obtiene una información: que la prueba es válida o inválida.

### Actores en un sistema a prueba de conocimiento cero
* Creador - opcional, puede combinarse con el prover
* Prover
* Verificador

El prover creará una prueba para convencer al verificador de que conoce un valor secreto (el testigo) o de que un cálculo se ha realizado correctamente.

El sistema de comprobación puede ser interactivo, en el que el comprobador y el verificador intercambian mensajes para verificar la prueba, o puede consistir únicamente en que el comprobador envíe la prueba al verificador, que puede aceptarla o rechazarla en un solo paso.

A menudo, la verificación será automática, realizada por un contrato inteligente en Ethereum, por ejemplo.

### Tipos de sistema ZK
![Graph](/im%C3%A1genes/zk.png)