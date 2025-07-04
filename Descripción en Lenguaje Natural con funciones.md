## 📘 Documentación del Lenguaje LDR

---

### 📌 Descripción en Lenguaje Natural
LDR es un lenguaje de programación de propósito general, simple y de paradigma imperativo estructurado.

- Las variables se escriben con letras mayúsculas (A–Z) seguidas opcionalmente de uno o más números.  
  Ejemplos: `X`, `Z1`, `VAR99`.
- Las sentencias, incluyendo bloques de control de flujo, se escriben en mayúscula y finalizan con punto y coma ;.
- Un programa inicia con la palabra clave `INICIO` y finaliza con `FIN`.
- La identación no es obligatoria, pero se recomienda para mejorar la claridad del programa.

### Tipos de datos
- **Primitivos:** `NUM` (número entero), `CAR` (carácter).
- **Compuestos:** `ARR` (arreglo).

### Sentencias válidas:
- **Declaración:**
  - `VAR tipo;`  
  - Ejemplo: `X NUM;`
  - También se permite declarar e inicializar: `VAR tipo = valor;`

- **Asignación:**
  - `VAR = valor;`  
  - Ejemplo: `X = 10;`
  - La reasignación funciona de la misma manera

- **Condicional:**
```ldr
SI condición ENTONCES
  sentencias
SINO
  sentencias
FINSI;
```

- **Iteración:**
```ldr
MIENTRAS condición HACER
  sentencias
FINMIENTRAS;
```

- **Impresión:** (similar a `console.log()`)
  - `IMPRIMIR VAR;`

- **Funciones/Subprogramas:**
  - Se pueden invocar con `NOMBRE(ARGUMENTOS);`

```ldr
FUNCION NOMBRE(PARAMS)
  sentencias
FINFUNCION
```

---

## 📘 Gramática en BNF de LDR
```bnf
<programa> ::= "INICIO" <bloque> "FIN"

<bloque> ::= <definiciones_funcion> <sentencias>

<definiciones_funcion> ::= <definicion_funcion> <definiciones_funcion> | λ

<definicion_funcion> ::= "FUNCION" <nombre> "(" <parametros>* ")" <sentencias> "FINFUNCION"

<parametros> ::= <parametro> ("," <parametro>)*

<parametro> ::= <variable> <tipo>

<sentencias> ::= <sentencia> <sentencias> | λ

<sentencia> ::= <declaracion> ";"
              | <asignacion> ";"
              | <impresion> ";"
              | <condicional> ";"
              | <iteracion> ";"
              | <llamado_funcion> ";"

<tipo> ::= "NUM" | "CAR" | "ARR"

<declaracion> ::= <variable> <tipo> | <variable> <tipo> "=" <valor>

<asignacion> ::= <variable> "=" <valor>

<impresion> ::= "IMPRIMIR" (<variable> | <valor>)

<condicional> ::= "SI" <condicion> "ENTONCES" <sentencias> "SINO" <sentencias> "FINSI"

<condicion> ::= <valor> <operador_comparacion> <valor> | "(" <condicion> ")" | <condicion> "&&" <condicion> | <condicion> "||" <condicion> | "!(" <condicion> ")"

<operador_comparacion> ::= "<" | ">" | "==" | "<=" | ">=" | "!="

<iteracion> ::= "MIENTRAS" <condicion> "HACER" <sentencias> "FINMIENTRAS"

<valor> ::= <numero> | <caracter> | <array> | <operacion> | <variable>

<operacion> ::= <valor> <operador> <valor>

<operador> ::= "+" | "-" | "*" | "/"

<llamado_funcion> ::= <nombre> "(" <argumentos>* ")"

<argumentos> ::= <valor> ("," <valor>)*

<array> ::= "[" <array-content> "]"

<array-content> ::= <item> "," <array-content> | <item>

<item> ::= <numero> | <caracter>

<numero> ::= [0-9]+ 

<caracter> ::= "'" <cualquier_caracter> "'"
<cualquier_caracter> ::= [A-Za-z0-9!@#$%^&*()_+-=\[\]{}|;:'",.<>/?`~] | " "

<variable> ::= [A-Z]+[0-9]*

<nombre> ::= [A-Z]+
```

---

## 📘 Reglas Semánticas para Operaciones Sobrecargadas

### 1. 🔤 CAR con NUM
Los caracteres se interpretan como su código ASCII.

**Operaciones permitidas:** `+`, `-`, `*`, `/` entre `CAR` y `NUM` (en cualquier orden).

**Regla:** Convertir `CAR` a su valor ASCII (entero), luego operar.

**Ejemplos:**
| Expresión | Resultado |
|-----------|-----------|
| `'A' + 1` | 66        |
| `1 + 'A'` | 66        |
| `'C' - 1` | 66        |
| `2 * 'B'` | 132       |
| `'D' / 2` | 34        |

### 2. 🧱 ARR con ARR y ARR con NUM

**Operaciones permitidas:**
- `ARR + ARR`: concatenación.
- `ARR * NUM`: repetición.

**Ejemplos:**
| Expresión             | Resultado                |
|----------------------|--------------------------|
| `[1] + ['A']`         | `[1, 'A']`               |
| `[1,2] + [3,4]`       | `[1,2,3,4]`              |
| `[1]*3`               | `[1,1,1]`                |
| `['X','Y']*2`         | `['X','Y','X','Y']`      |

---

## 🎯 Semántica de Funciones

- Más que funciones son procedimientos, puesto que no tienen un return.
- Las funciones se definen con `FUNCION <nombre>(<parametros>)` y terminan con `FINFUNCION`.
- No devuelven valores (procedimientos), pero pueden usar `IMPRIMIR`.
- Los parámetros son **ligados posicionalmente**, y son **variables locales**.

### Reglas de Tipos
| Situación                                     | Regla                            |
|----------------------------------------------|----------------------------------|
| Llamado con cantidad incorrecta de argumentos | ❌ Error de aridad               |
| Tipos incompatibles                           | ❌ Error de tipo                 |
| Variables locales                             | ✔️ Solo accesibles en la función |
| Parámetros duplicados                         | ❌ Error de declaración          |

---

## 🧾 Clasificación de LDR (Cuadro extendido de características)

| Características                     | LDR                                                                 |
|-------------------------------------|----------------------------------------------------------------------|
| Paradigma                           | Imperativo, estructurado                                             |
| Tipos de datos                      | Primitivos: NUM, CAR<br>Compuestos: ARR                              |
| Asignación                          | Sí (`<variable> = <valor>`)                                          |
| Iteración                           | Sí (`MIENTRAS <condición> HACER ... FINMIENTRAS`)                   |
| Condicional                         | Sí (`SI <condición> ENTONCES ... SINO ... FINSI`)                   |
| Tipado                              | Estático (en tiempo de declaración)                                 |
| Sistema de Tipos                    | Fuerte                                                              |
| Conversión de Tipos                 | Implícita para CAR -> NUM (ASCII)                                     |
| Sobrecarga de operadores            | Parcial: `+`, `-`, `*`, `/` sobre NUM y CAR;<br>`+`, `*` sobre ARR    |
| Nivel de abstracción                | Alto                                                                |
| Independencia de la máquina         | Sí                                                                  |
| Orientación a objetos               | No                                                                  |
| Sensible a mayúsculas               | Sí (`X` y `x` son diferentes). No aplica para identificadores de variables (solo se permiten mayúsculas).         |
| Control de flujo                    | Secuencia, selección, iteración, subprogramas                       |
| Subprogramas                        | Sí (funciones definidas con parámetros)                             |
| Funciones anidadas / Closures       | No                                                                  |
| Polimorfismo                        | Limitado: por sobrecarga de operadores                              |
| Paso de parámetros                  | Sí (posicional, con tipo explícito)                                 |
| Ámbito de variables                 | Global y local (funciones tienen su propio entorno local)           |
| Recursividad                        | No soportada explícitamente                                         |
| Evaluación de expresiones           | Estricta                                                            |
| Expresiones soportadas              | Infijas (`a + b`), con paréntesis opcionales                        |
| Evaluación de condiciones           | Booleana con comparación de NUM y CAR                               |
| Tiempo de ligadura de tipos         | Estático                                                            |
| Valores por defecto                 | No                                                                  |
| Inicialización implícita            | No                                                                  |
| Mutabilidad                         | Sí (las variables pueden reasignarse)                               |
| Representación interna de CAR       | Código ASCII                                                        |
| Compatibilidad de tipos             | Por nombre, con conversión limitada semánticamente                  |
| Representación de arrays            | Corchetes: `[1, 'A']`                                               |
| Operaciones con arrays              | `+` (concat), `*` (repetir con NUM)                                 |
| Longitud de identificadores         | [A-Z]+[0-9]?                                                        |
| Constantes                          | Numéricas (`3`), caracteres (`'A'`)                                 |
| Manejo de errores / excepciones     | No                                                                  |
| Eventos                             | No                                                                  |
| Forma de comentario                 | No definida (convención: `//`, `#` a implementar)                          |
---

## 🧪 Ejemplos de Programas

### Ejemplo 1: Condicional simple
```ldr
INICIO
  X NUM;
  X = 7;
  SI X > 0 ENTONCES
    IMPRIMIR X;
  SINO
    IMPRIMIR 'N';
  FINSI;
FIN
```

### Ejemplo 2: Arrays, operaciones y sobrecarga
```ldr
INICIO
  A NUM;
  B NUM;
  C CAR;
  D NUM;
  LISTA ARR;

  A = 5;
  B = 10;
  C = 'A';
  D = A + B;
  IMPRIMIR D;
  D = D + C;
  IMPRIMIR D;

  LISTA = [1, 2, 3, 4, 5];
  I NUM;
  I = 0;

  MIENTRAS I < 5 HACER
    IMPRIMIR LISTA[I];
    I = I + 1;
  FINMIENTRAS;

  SI D > 50 ENTONCES
    IMPRIMIR 'S';
  SINO
    IMPRIMIR 'N';
  FINSI;
FIN
```

### Ejemplo 3: Uso de función SUMAR
```ldr
INICIO
  FUNCION SUMAR(X NUM, Y NUM)
    RES NUM;
    RES = X + Y;
    IMPRIMIR RES;
  FINFUNCION

  A NUM;
  B NUM;
  A = 5;
  B = 7;
  SUMAR(A, B);
FIN
```

---

- Posibles mejoras/extensiones para el lenguaje:
  - Incorporar un tipo de dato booleano.
  - Agregar manejo de errores.
  - Permitir realizar comentarios en el código.
  - Agregar funciones (que tengan un return).
  - Ver de manejar los enteros cuando tienen 0s a la izquierda.