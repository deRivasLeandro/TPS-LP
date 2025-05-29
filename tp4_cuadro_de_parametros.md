# Cuadro de Parámetros

| **Tipo de parámetro**       | **Estático** | **Dinámico** | **Ejemplo dinámico**                             |
|-----------------------------|--------------|--------------|------------------------------------------------------------------|
| **Por valor**               | ✔️           | ❌           | `f(x)`, donde `x = 5` se copia al parámetro formal.              |
| **Por referencia**          | ✔️           | ⚠️ Algunos lenguajes lo implementan en tiempo de ejecución | `f(&x)` o `f(ref x)` modifica directamente `x`. |
| **Por nombre**              | ❌           | ✔️           | Utilizado en ALGOL; la expresión se reevalúa cada vez que se accede. |
| **Por resultado**           | ✔️           | ⚠️           | Similar a por referencia, pero el valor se copia al final de la función. |
| **Por valor-resultado**     | ✔️           | ⚠️           | Se pasa una copia, y al terminar se copia de vuelta (Ada, Pascal). |
| **Parámetros predeterminados** | ✔️       | ❌           | `def f(x=3)` en Python; el valor se resuelve en el entorno de definición. |
| **Parámetros variables (varargs)** | ✔️     | ✔️           | `def f(*args)` en Python, `void f(int... x)` en Java.            |
