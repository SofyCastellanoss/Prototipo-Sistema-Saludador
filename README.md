# Prototipo-Sistema-Saludador

# Descrición: 
Sistema Saludador

El Sistema Saludador es un prototipo de software de escritorio hecho en JavaFX. Su objetivo es saludar al estudiante por su nombre y mencionar su edad. No gestiona usuarios, bases de datos ni historial: solo cubre el caso de uso “Solicitar saludo”.

Actor El único actor es el estudiante. Interactúa con una ventana gráfica: pulsa botones y escribe datos.

Objetivo Que, al terminar el flujo, el sistema muestre un saludo personalizado que:

se dirija al estudiante por su nombre;
indique su edad.
Datos que usa el sistema

Nombre
Edad
Hora en formato de 12 horas (por ejemplo 10:30)
Periodo AM o PM
La hora y el AM/PM se piden porque forman parte de lo que el sistema solicita. En el prototipo también sirven para elegir el momento del día (buenos días, buenas tardes o buenas noches). El resultado obligatorio sigue siendo el saludo con nombre y edad.

Cómo se ejecuta el software

Paso 1. Inicio Al abrir la aplicación aparece la pantalla inicial con el título “Sistema Saludador” y el botón “Solicitar saludo”. El estudiante hace clic en “Solicitar saludo”. Eso es la petición del caso de uso: el estudiante pide que el sistema lo salude.

Paso 2. Solicitud de datos El sistema cambia a un formulario y pide:

Nombre
Edad
Hora
Si esa hora es AM o PM
Hasta que el estudiante no complete y confirme, no se genera el saludo.

Paso 3. Ingreso de datos El estudiante escribe el nombre, indica la edad, escribe la hora (hh:mm) y elige AM o PM. Luego pulsa “Confirmar”. Si falta un dato o el formato no es válido (nombre vacío, hora mal escrita, hora fuera de 1–12, etc.), el sistema muestra un mensaje de error y se queda en el formulario. El estudiante corrige y vuelve a confirmar.

Paso 4. Saludo Si los datos son correctos, el sistema genera el saludo y muestra una pantalla de resultado. Ahí saluda al estudiante por su nombre y menciona su edad. Ejemplo: “¡Buenos días, Sofía. Tienes 18 años.”

Flujo resumido Estudiante pulsa Solicitar saludo → el sistema pide nombre, edad, hora y AM/PM → el estudiante ingresa esos datos y confirma → el sistema saluda por nombre y menciona la edad.

Pantallas

Inicio: solo la acción de solicitar el saludo.
Formulario: captura de datos.
Resultado: mensaje de saludo.
Desde el resultado se puede pedir otro saludo (vuelve al formulario) o volver al inicio.

Comportamiento del software

Es una aplicación de una sola ventana.
El flujo es secuencial: no se salta el formulario.
No guarda la información después de cerrar.
El saludo se calcula en el momento, con los datos que acaba de ingresar el estudiante.
