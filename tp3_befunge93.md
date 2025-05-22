# Árboles Sintácticos en Befunge93

## 🔗 Diagrama sintáctico (Conway)

Diagrama sintáctico (Conway):
👉 [Ver Mapa Conceptual](https://www.mermaidchart.com/app/projects/ce7befff-14ab-49aa-bde9-41ec8ad8fd5e/diagrams/2197df75-fdbf-4ea7-b862-0e06679ca427/version/v0.1/edit)

---

## 🌱 Ejemplo 1: Suma simple

### Código Befunge93:

23+.

### Descripción:

- `2` → Push 2 en la pila  
- `3` → Push 3 en la pila  
- `+` → Suma los dos valores anteriores (2 + 3) y apila el resultado  
- `.` → Muestra el resultado (5)

### Árbol Sintáctico:

Programa
│
├── Instrucción: PUSH 2
├── Instrucción: PUSH 3
├── Instrucción: ADD
│ ├── Operando1: POP (3)
│ └── Operando2: POP (2)
├── Instrucción: OUTPUT
│ └── Operando: POP (5)


---

## 🌿 Ejemplo 2: Multiplicación, resta y salida

### Código Befunge93:

42*51-+.


### Descripción paso a paso:

- `4` → Push 4  
- `2` → Push 2  
- `*` → Multiplica 4 * 2 = 8 → push 8  
- `5` → Push 5  
- `1` → Push 1  
- `-` → Resta 5 - 1 = 4 → push 4  
- `+` → Suma 8 + 4 = 12 → push 12  
- `.` → Muestra el resultado (12)

### Árbol Sintáctico:

Programa
│
├── Instrucción: PUSH 4
├── Instrucción: PUSH 2
├── Instrucción: MUL
│ ├── Operando1: POP (2)
│ └── Operando2: POP (4)
│ └── Resultado: PUSH (8)
├── Instrucción: PUSH 5
├── Instrucción: PUSH 1
├── Instrucción: SUB
│ ├── Operando1: POP (1)
│ └── Operando2: POP (5)
│ └── Resultado: PUSH (4)
├── Instrucción: ADD
│ ├── Operando1: POP (4)
│ └── Operando2: POP (8)
│ └── Resultado: PUSH (12)
├── Instrucción: OUTPUT
│ └── Operando: POP (12)