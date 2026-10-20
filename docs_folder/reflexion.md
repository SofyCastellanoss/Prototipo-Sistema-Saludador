# Reflexión sobre la práctica de laboratorio:

La verdad esta práctica se veía fácil: un sistema que le saluda por tu nombre y te dice la edad. En papel son como tres pasos. 
El estudiante da clic en solicitar saludo, el programa pide nombre, edad, hora y si es AM o PM, uno lo llena y ya  saluda, nada del otro mundo. 
Ya cuando te pones a armarlo en JavaFX uno se da cuenta de que “prototipo” no es solo el mensaje bonito.

Lo primero que me trabó no fue el saludo, fue correrlo, tener Java instalado no significa que se pueda compilar JavaFX. 
A veces está el JRE 8, no el JDK, no aparece Maven, y JavaFX ya ni viene metido en el JDK. Ahí me sorprendió que una práctica 
tan corta dependa tanto de librerías y de cómo la ejecuta. No es un System.out.println y ya.

Otra cosa que no tenía tan clara era para qué pedir la hora y el AM/PM si al final lo importante es el nombre y la edad, primero pensé que sobraba
Después tiene sentido: eso es lo que el sistema le solicita al estudiante, y además sirve para no saludar 
igual a las 8 de la mañana que a las 8 de la noche. Aunque el resultado se centre en “hola, fulano, tienes X años”, esos datos sí forman parte del flujo.

En la interfaz también hay detalles que uno no piensa. No se puede mostrar todo junto: primero el botón, luego el formulario, luego el resultado. 
Si se oculta un panel mal, se queda el hueco. El spinner de la edad también me la hizo: si se escribe el número a mano y no se “confirma” el valor,
el programa se queda con el anterior y parece que no hizo caso. Esas cosas no salen en el enunciado y uno se las come cuando lo prueba.

De estructura, aunque el programa sea chiquito, se siente raro meter la lógica del saludo pegada al botón. Una cosa es el clic y otra validar 
que la hora esté entre 1 y 12, que pongan AM o PM, y armar el texto. Separarlo (pantalla / datos / saludo) se entiende mejor. FXML se ve ordenado, 
pero al inicio no me queda tan claro eso de los fx:id y el @FXML; si le pifias al nombre, no carga y no sabes por qué. Hacerlo todo en una clase 
es más largo, pero al menos ves todo junto y es más fácil copiarlo.

Lo que todavía no termino de cachar bien es lo de los módulos, el module-info y por qué a veces hay que tener un Launcher aparte 
para que JavaFX arranque. Lo usas porque “así corre”, no porque lo hayas entendido del todo. Igual con Maven y javafx:run: cuando funciona 
está bien, cuando no, el error parece de tu código y a veces es el entorno.

Al final me quedó que el prototipo sirve si puedes hacer el paso a paso de verdad: clic, llenar datos, ver el saludo con tu nombre y tu edad. 
Lo demás (librerías, comandos, pantallas, validaciones) es lo que convierte un ejercicio de enunciado en software, aunque el sistema nada más te esté saludando.
