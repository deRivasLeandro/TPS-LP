Descripción en Lenguaje Natural
LDR es un lenguaje de programación de propósito general, simple y estructurado.

Las variables se escriben con letras mayúsculas (A–Z) seguidas opcionalmente de un número.
Ejemplos: X, Z1, VAR99.

Las sentencias se escriben en mayúscula y finalizan con punto y coma ;.

Un programa inicia con la palabra clave INICIO y finaliza con FIN.

Tipos de datos primitivos: NUM (número entero), CAR (carácter), ARR (arreglo).

Sentencias válidas:

Declaración: VAR tipo;
Ejemplo: X NUM;

Asignación: VAR = valor;
Ejemplo: X = 10;

VAR tipo = valor;

Condicional:

SI condición ENTONCES
  sentencias
SINO
  sentencias
FINSI;

Iteración:

MIENTRAS condición HACER
  sentencias
FINMIENTRAS;

(similar a un console.log())
Impresión: IMPRIMIR VAR;

(Agregar sobrecarga de operadores en ARR y entre NUM y CAR - con posibilidad de usar CAR+NUM donde el valor de CAR es su valor ASCII y en los ARR poder concatenarlos usando +, por ejemplo [1] + ["A"] = [1, "A"] y también poder multiplicarlos con *, por ej. [1]*3 = [1, 1, 1])

📘 Gramática en BNF de LDR

<programa> ::= "INICIO" <sentencias> "FIN"

<sentencias> ::= <sentencia> <sentencias> | λ

<sentencia> ::= <declaracion>";"
              | <asignacion>";"
              | <impresion>";"
              | <condicional>";"
              | <iteracion>";"

<declaracion> ::= <variable> <tipo> 

<asignacion> ::= <variable> "=" <expresion>

<impresion> ::= "IMPRIMIR" <variable>

<condicional> ::= "SI" <condicion> "ENTONCES" <sentencias> "SINO" <sentencias> "FINSI" 

<iteracion> ::= "MIENTRAS" <condicion> "HACER" <sentencias> "FINMIENTRAS"

<tipo> ::= "NUM" | "CAR" | "ARR"

<expresion> ::= <valor>
              | <expresion> <operador> <expresion>

<operador> ::= "+" | "-" | "*" | "/" | "==" | "!=" | "<" | ">" | "<=" | ">="

<valor> ::= <numero> 
          | <caracter> 
          | <array> 
          | <variable>

<array> ::= "[" <array-content> "]"

<array-content> ::= <item> "," <array-content> | <item> | λ

<item> ::= <numero> | <caracter>

<numero> ::= [0-9]+

<caracter> ::= "'" [A-Za-z] "'"

<variable> ::= [A-Z]+ [0-9]?

📘 Reglas Semánticas para Operaciones sobrecargadas
1. 🔤 CAR con NUM
Los caracteres se interpretan según su código ASCII entero.

✅ Operaciones permitidas:
CAR + NUM

NUM + CAR

CAR - NUM

NUM - CAR

CAR * NUM

NUM * CAR

CAR / NUM

NUM / CAR

🧠 Regla general:
Para cualquier operación entre un valor de tipo CAR y otro de tipo NUM, el valor del carácter se convierte implícitamente a su código ASCII (entero) antes de operar.

📌 Ejemplos:
Expresión	Evaluación Intermedia	Resultado
'A' + 1	65 + 1	66
1 + 'A'	1 + 65	66
'C' - 1	67 - 1	66
2 * 'B'	2 * 66	132
'D' / 2	68 / 2	34

2. 🧱 ARR con ARR y ARR con NUM
✅ Operaciones permitidas:

ARR + ARR
ARR * NUM

🧠 Reglas semánticas:
Concatenación (+):
Si ambos operandos son de tipo ARR, se concatenan en el orden dado.

[1] + ["A"] → [1, "A"]
Multiplicación (*):
Si se multiplica un ARR por un NUM (positivo), se repite el contenido del array esa cantidad de veces.

[1] * 3 → [1, 1, 1]
["X"] * 2 → ["X", "X"]
🔎 Tipo de resultado: en ambos casos, el resultado es de tipo ARR.

📌 Ejemplos:
Expresión	Evaluación	Resultado
[1] + ["A"]	Concatenación	[1, "A"]
[1, 2] + [3, 4]	Concatenación	[1, 2, 3, 4]
[1] * 3	Repetición	[1, 1, 1]
["X", "Y"] * 2	Repetición	["X", "Y", "X", "Y"]

🧾 Clasificación de LDR (Cuadro extendido de características)
Características	                             LDR
Paradigma	                                   Imperativo, estructurado
Tipos de datos	Primitivos:                  NUM, CAR
Compuestos:                                  ARR
Asignación	                                 Sí (<variable> = <valor>)
Iteración	                                   Sí (MIENTRAS <condición> HACER ... FINMIENTRAS)
Condicional	                                 Sí (SI <condición> ENTONCES ... SINO ... FINSI)
Tipado	                                     Estático (tipos definidos en tiempo de declaración)
Sistema de Tipos	                           Fuerte (requiere compatibilidad explícita o conversión permitida)
Conversión de Tipos	                         Implícita para operaciones válidas (CAR a NUM por ASCII)
Sobre carga de operadores	                   Parcial: +, -, *, / sobre NUM y CAR, + y * sobre ARR
Nivel de abstracción	                       Medio
Independencia de la máquina	                 Sí (lenguaje de alto nivel)
Orientación a objetos	                       No
Sensible a mayúsculas	                       Sí (identificadores X y x son diferentes)
Control de flujo	                           Secuencia, selección, iteración, subprogramas
Subprogramas	                               No definidos explícitamente (versión actual)
Funciones anidadas / Closures	               No
Polimorfismo	                               Limitado: por sobrecarga de operadores (no por herencia)
Paso de parámetros	                         No soportado actualmente (no hay subprogramas parametrizados)
Manejo de errores / excepciones	             No implementado
Eventos	                                     No
Recursividad	                               No soportada explícitamente (no hay funciones aún)
Evaluación de expresiones	                   Estricta (evaluación inmediata de operandos)
Expresiones soportadas	                     Infijas con paréntesis opcionales
Ámbito de las variables	                     Global (no hay bloques ni funciones locales)
Tiempo de ligadura de tipos	                 Estático (definido al declarar la variable)
Valores por defecto	                         No
Inicialización implícita	                   No
Mutabilidad	                                 Sí (las variables pueden reasignarse)
Representación interna de CAR	               Código ASCII
Compatibilidad de tipos	                     Por conversión (estructural implícita limitada)
Evaluación de condiciones	                   Booleana implícita con comparación de valores (NUM, CAR)
Forma de comentario	                         No definida explícitamente (se puede definir con // o #, por convención)
Representación de arrays	                   Secuencia de elementos entre corchetes ([1, 'A'])
Longitud de identificadores	                 Alfabéticos en mayúsculas ([A-Z]+[0-9]?)
Constantes	                                 Numéricas o caracteres literales (3, 'A')

-----------------------------------------------------------------------
EJEMPLOS DE PROGRAMAS:

Este programa declara un número X, le asigna el valor 7, y verifica si es positivo. Si lo es, lo imprime; si no, imprime el carácter 'N':

INICIO
  X NUM;
  X = 7;
  
  SI X > 0 ENTONCES
    IMPRIMIR X;
  SINO
    IMPRIMIR 'N';
  FINSI;
FIN

----------------------------------------------------------------------
Este programa declara variables de los tres tipos (NUM, CAR, ARR), realiza asignaciones y operaciones con sobrecarga (NUM + CAR), recorre un arreglo e imprime sus elementos, y evalúa una condición final:

INICIO
  A NUM;
  B NUM;
  C CAR;
  D NUM;
  LISTA ARR;

  A = 5;
  B = 10;
  C = 'A';
  
  D = A + B;         // Suma de números
  IMPRIMIR D;

  D = D + C;         // Suma con sobrecarga: 'A' tiene valor 65 (ASCII), D = 15 + 65 = 80
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