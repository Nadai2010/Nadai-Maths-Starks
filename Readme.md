<div align="center">
  <img alt="starknet logo" src="./assets/Starknet.png" width="200" >
  <h1 align="center">StarknetEs Basecamp - Maths Starks</h1>
  <p align="center">
</div>

# Traducción Starknet Basecamp - Stark Maths

Puede encontrar las notas originales [aquí](https://bit.ly/starkmaths2023)

## Temas

- [Matemáticas de base](#matemáticas-de-base)
    - [Aritmética modular / Campos finitos](#aritmética-modular-/-campos-finitos)
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
también usamos `Z*p` para representar un campo finito de enteros mod prime p con inversos multiplicativos.

Utilizamos campos finitos para la criptografía, porque los elementos tienen representaciones "cortas", exactas y propiedades útiles.





