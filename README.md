# FirstAppNodeJS

Este paso lo guiará para crear su primer módulo de Node.js. Su módulo contendrá un grupo de colores en una matriz y proporcionará una función para obtener uno al azar. Usaremos la propiedad **exports** incorporada de Node.js para permitir que la función y la matriz estén disponibles para programas externos.

Primero, comenzaremos por decidir qué datos sobre colores se almacenarán en su módulo. Cada color será un objeto que contiene una propiedad name que los seres humanos pueden identificar fácilmente y una propiedad code, que es una string que contiene un código de color HTML.

Luego, debe definir los colores que desea admitir en su módulo. Su módulo contendrá una matriz llamada allColors que contendrá seis colores. Su módulo también incluirá una función llamada getRandomColor() que seleccionará un color de su matriz de forma aleatoria y lo mostrará.

En su terminal, cree una nueva carpeta llamada colors y posiciónese en ella:

~~~ 
mkdir colors
cd colors 
~~~

Inicie npm para que otros programas puedan importar este módulo más adelante en el tutorial:

~~~ 
npm init -y
~~~ 

Use el indicador -y para omitir las solicitudes habituales de personalización de su package.json. Si este fuera un módulo que desea publicar en npm, respondería a todas estas preguntas con datos pertinentes

~~~
Output
{
  "name": "colors",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
~~~

Ahora, abra un editor de texto de línea de comandos vim y cree un nuevo archivo para que sirva como punto de entrada para su módulo:

`vim index.js`

Su módulo hará algunas acciones. Primero, definirá una clase Color. Su clase Color se instalará con su nombre y código HTML. Añada las líneas siguientes para crear la clase:

~~~
class Color {
  constructor(name, code) {
    this.name = name;
    this.code = code;
  }
}

const allColors = [
  new Color('brightred', '#E74C3C'),
  new Color('soothingpurple', '#9B59B6'),
  new Color('skyblue', '#5DADE2'),
  new Color('leafygreen', '#48C9B0'),
  new Color('sunkissedyellow', '#F4D03F'),
  new Color('groovygray', '#D7DBDD'),
];

~~~

La palabra clave exports hace referencia a un objeto global disponible en todos los módulos Node.js. Las funciones y los objetos almacenados en el objeto exports de un módulo, en su totalidad, quedan expuestos cuando otros módulos Node.js los importan. Por ejemplo, la función getRandomColor() se creó directamente en el objeto exports. Luego, añada una propiedad allColors al objeto exports que hace referencia a la matriz de constante local allColors creada anteriormente en la secuencia de comandos.

Cuando otros módulos importen este, tanto allColors como getRandomColor() quedarán expuestos y disponibles para su uso.

Guarde el archivo y ciérrelo.

Hasta ahora, creó un módulo que contiene una matriz de colores y una función que muestra uno de forma aleatoria. También exportó la matriz y la función para que los programas externos puedan usarlas. En el siguiente paso, usará su módulo en otras aplicaciones para demostrar los efectos de export.

# Paso 2: Probar su módulo con REPL

Antes de crear una aplicación completa, tómese un momento para confirmar que su módulo funciona. En este paso, usará el REPL para cargar el módulo colors. Mientras se encuentra en el REPL, invoque la función getRandomColor() para ver si se comporta como se espera.

Inicie el REPL de Node.js en la misma carpeta que el archivo index.js:

`node`

Cuando se inicie el REPL, verá el símbolo >. Esto significa que podrá ingresar el código JavaScript que se evaluará de inmediato. 

`colors = require('./index');`

En este comando, require() carga el módulo colors en su punto de entrada. Cuando presione INTRO, obtendrá el siguiente resultado:

~~~
Output
{
  getRandomColor: [Function],
  allColors: [
    Color { name: 'brightred', code: '#E74C3C' },
    Color { name: 'soothingpurple', code: '#9B59B6' },
    Color { name: 'skyblue', code: '#5DADE2' },
    Color { name: 'leafygreen', code: '#48C9B0' },
    Color { name: 'sunkissedyellow', code: '#F4D03F' },
    Color { name: 'groovygray', code: '#D7DBDD' }
  ]
}
~~~

El REPL muestra el valor de colors, que son las funciones y los objetos importados del archivo index.js. Cuando utilice la palabra clave require, Node.js mostrará todos los contenidos dentro del objeto exports de un módulo.

Recuerde que añadió getRandomColor() y allColors a exports en el módulo colors. Por ese motivo, verá a ambos en el REPL cuando se importen.

En el símbolo del sistema, pruebe la función getRandomColor():

`colors.getRandomColor();`

Se le solicitará un color aleatorio:

~~~
Output
Color { name: 'groovygray', code: '#D7DBDD' }
~~~

Debido a que el índice es aleatorio, su resultado puede variar. Ahora que confirmó que el módulo colors está funcionando, cierre el REPL de Node.js

`.exit`

## Paso 3: Guardar su módulo local como dependencia

Al probar su módulo en el REPL, lo importó con una ruta relativa. Esto significa que utilizó la ubicación del archivo index.js en relación con el directorio de trabajo para obtener su contenido. Si bien esto funciona, normalmente la experiencia de programación es mejor si importa los módulos por sus nombres, de modo que la importación no se vea afectada cuando el contexto cambie. En este paso, instalará el módulo colors con la función install del módulo local de npm.

Configure un nuevo módulo Node.js fuera de la carpeta colors. Primero, diríjase al directorio anterior y cree una nueva carpeta:

~~~
cd ..
mkdir really-large-application
~~~

Ahora, posiciónese en su nuevo proyecto:

`cd really-large-application`

Como en el caso del módulo colors, inicie su carpeta con npm:

`npm init -y`

Se generará el siguiente package.json:

~~~
Output
{
  "name": "really-large-application",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
~~~

Ahora, instale su módulo colors y utilice el indicador --save para que se registre en su archivo package.json:

`npm install --save ../colors`

Acaba de instalar su módulo colors en el nuevo proyecto. Abra el archivo package.json para ver la nueva dependencia local:

`vim package.json`

Verá que se agregaron las siguientes:

~~~
{
  "name": "really-large-application",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "colors": "file:../colors"
  }
}
~~~

Cierre el archivo.

El módulo colors se copió a su directorio node_modules. Verifique que esté en él con el siguiente comando:

`ls node_modules`

Utilice su módulo local instalado en este nuevo programa. Vuelva a abrir su editor de texto y cree otro archivo de JavaScript:

`nano index.js`

Su programa importará primero el módulo colors. Luego, elegirá un color de forma aleatoria usando la función getRandomColor() proporcionada por el módulo. Por último, imprimirá un mensaje en la consola que indicará al usuario el color que debe usar.

Introduzca el siguiente código en index.js:

const colors = require('colors');

~~~
const chosenColor = colors.getRandomColor();
console.log(`You should use ${chosenColor.name} on your website. It's HTML code is ${chosenColor.code}`);
~~~

Guarde este archivo y ciérrelo.

Su aplicación ahora indicará al usuario una opción de color aleatorio para un componente del sitio web.

Ejecute esta secuencia de comandos con lo siguiente:

`node index.js`

El resultado será similar a este:

`You should use leafygreen on your website. It's HTML code is #48C9B0`

Con esto, habrá instalado con éxito el módulo colors y podrá administrarlo como cualquier otro paquete de npm utilizado en su proyecto. Sin embargo, si añadiera más colores y funciones a su módulo colors local, debería ejecutar npm update en sus aplicaciones para poder usar las nuevas opciones. En el siguiente paso, usará el módulo local colors de otra forma y obtendrá actualizaciones automáticas cuando el código del módulo cambie.

