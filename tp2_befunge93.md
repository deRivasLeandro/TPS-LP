
# 🧠 Befunge-93

**Befunge** es un lenguaje de programación esotérico **bidimensional**, en el que el flujo del programa se mueve dentro de una grilla. Su conjunto de instrucciones permite manipular una pila, realizar operaciones matemáticas, moverse por la grilla y más.

---

## 🔸 Instrucciones válidas

### ▸ Direcciones  
`>`  ` < `  ` ^ `  ` v `

### ▸ Manipulación de pila  
`0`–`9` (push número)  
`:` (duplicar)  
`$` (pop)

### ▸ Aritmética  
`+` `-` `*` `/` `%`

### ▸ Lógica  
`!` (not)  
`` ` `` (mayor que)

### ▸ Control de flujo  
`_` `|` `#` `@`

### ▸ Entrada / Salida  
`.` (número → salida)  
`,` (carácter → salida)  
`&` (leer número)  
`~` (leer carácter)

### ▸ Modo cadena  
`"` (activa modo cadena)

### ▸ Otros  
`g` (get)  
`p` (put)  
`?` (dirección aleatoria)  
` ` (espacio vacío)

---

## 🔹 GIC - Befunge93

Formalización del lenguaje como una **Gramática Independiente del Contexto (GIC)**:

```
G = (∑N, ∑T, S, P)
```

- **∑N** = {Programa, Instrucción, Digito}  
- **∑T** = { `>`, `<`, `^`, `v`, `+`, `-`, `*`, `/`, `%`, `!`, `` ` ``, `_`, `|`, `"`, `:`, `$`, `#`, `@`, `.`, `,`, `&`, `~`, `g`, `p`, `?`, `'0'..'9'`, ` ` }  
- **S** = `Programa`

### Producciones:

```
Programa     → Instrucción Programa | Instrucción
Instrucción  → Dirección | Operación | Control | IO | Stack | Caracter
Dirección    → > | < | ^ | v
Operación    → + | - | * | / | %
Control      → ! | ` | _ | | | # | @ | ?
IO           → . | , | & | ~
Stack        → : | $
Caracter     → " | g | p | Dígito | espacio
Dígito       → '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
```

---

## 🔹 BNF - Befunge93

```bnf
<Programa>    ::= <Instruccion> | <Instruccion> <Programa>
<Instruccion> ::= <Direccion> | <Operacion> | <Control> | <IO> | <Stack> | <Caracter>
<Direccion>   ::= ">" | "<" | "^" | "v"
<Operacion>   ::= "+" | "-" | "*" | "/" | "%"
<Control>     ::= "!" | "`" | "_" | "|" | "#" | "@" | "?"
<IO>          ::= "." | "," | "&" | "~"
<Stack>       ::= ":" | "$"
<Caracter>    ::= """ | "g" | "p" | <Digito> | " "
<Digito>      ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
```

---

## 🔹 EBNF - Befunge93

```ebnf
Programa     = { Instruccion } ;
Instruccion  = Direccion | Operacion | Control | IO | Stack | Caracter ;
Direccion    = ">" | "<" | "^" | "v" ;
Operacion    = "+" | "-" | "*" | "/" | "%" ;
Control      = "!" | "`" | "_" | "|" | "#" | "@" | "?" ;
IO           = "." | "," | "&" | "~" ;
Stack        = ":" | "$" ;
Caracter     = """ | "g" | "p" | Digito | " " ;
Digito       = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
```

---

## 🔹 ABNF - Befunge93

```abnf
Programa     = *(Instruccion)

Instruccion  = Direccion / Operacion / Control / IO / Stack / Caracter
Direccion    = ">" / "<" / "^" / "v"
Operacion    = "+" / "-" / "*" / "/" / "%"
Control      = "!" / "`" / "_" / "|" / "#" / "@" / "?"
IO           = "." / "," / "&" / "~"
Stack        = ":" / "$"
Caracter     = DQUOTE / "g" / "p" / Digito / SP
Digito       = "0" / "1" / "2" / "3" / "4" / "5" / "6" / "7" / "8" / "9"
```
