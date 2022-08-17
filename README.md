# FirstAppNodeJS

Este paso lo guiará para crear su primer módulo de Node.js. Su módulo contendrá un grupo de colores en una matriz y proporcionará una función para obtener uno al azar. Usaremos la propiedad **exports** incorporada de Node.js para permitir que la función y la matriz estén disponibles para programas externos.

Primero, comenzaremos por decidir qué datos sobre colores se almacenarán en su módulo. Cada color será un objeto que contiene una propiedad name que los seres humanos pueden identificar fácilmente y una propiedad code, que es una string que contiene un código de color HTML.

Luego, debe definir los colores que desea admitir en su módulo. Su módulo contendrá una matriz llamada allColors que contendrá seis colores. Su módulo también incluirá una función llamada getRandomColor() que seleccionará un color de su matriz de forma aleatoria y lo mostrará.

En su terminal, cree una nueva carpeta llamada colors y posiciónese en ella:

~~~ 
mkdir colors
cd colors 
~~~

