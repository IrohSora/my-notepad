# React
Una librería creada por Facebook para optimizar el desarrollo Front.

# Virtual DOM
Es una copia del DOM en la cuál podemos identificar qué elementos del DOM cambia para no re renderizar todo el DOM, sino solo la sección en la que está contenida el elemento cambiante.

# Create React App
Con el siguiente comando podremos generar un boilerpalte con toda la configuraicón un proyecto react para empezar a trabajar:
```bash
npx create-react-app [name]
```

Para ejecutarlo, entramos a la carpeta generada y ejecutamos `npm run start`, nos abrirá un navegador con el proyecto inicializado (solo una imagen y un enlace a la documentación de React).

# Tipos de componentes
* **Componente stateful**. Es conocido como *estructura de clases*, nos permite manejar ciclo de vida y estado, es el componente más poderoso de React, su estructura básica es la siguiente:
```jsx
import React, {Component} from 'react';

class Stateful extends Component {
  constructor(props) {
    super(props);
    this.state = {
      hello: 'Hola mundo!'
    }
  }
  // parte visual de nuestro componente
  render() {
    return(
      <h1>{this.state.hello}</h1>
    )
  }
}

export default Stateful;
```

* **Componente stateless**. No depende de un estado ni de un ciclo de vida, solamente la parte lógica. Estos componentes son muy usados actualmente pues se enfocan en ciertas partes de la funcionalidad. Esta es su estructura:
```javascript
import React from 'react';

const Stateless = () => {
  return(
    <h1>Hola mundo</h1>
  );
}

export default Stateless;
```

* **Componente presentacional**. No contiene ninguna lógica ni estado, solamente la parte visual, estructura básica:
```javascript
import React from 'react';

const Presentacional = () => <h1>Hola mundo!</h1>

export default Presentacional;
```

# JSX
Es una extensión que podemos usar para nuestros componentes React, que nos brina una interfaz con utilidades en tiempo de desarrollo, si bien mantiene el resaltado de JS, también nos permite escribir más fácilmente nuestros componentes de React así como auxiliares de linteo, veamos un ejemplo de un componente con jsx:
```jsx
import React from 'react'

const HolaMundo = () => {
  const Hello = 'Hola mundo!'
  const isTrue = true
  return(
    <div className="HolaMundo">
      <h1>{Hello}</h1>
      <h2>Curso de React</h2>
      <input type="text"/>
      {isTrue ? <h4>Esto es verdadero</h4> : <h4>Soy falso</h4>}
      {isTrue && <h4>Soy verdadero</h4>}
    </div>
  )
}

export default HolaMundo;
```
> Tomar en cuenta que las etiquetas que no tienen cierre, se tiene que indicar ejemplo <input type="text"/>

# Props: comunicación entre componentes
Nuestros componentes se pueden alimentar de información desde el exterior mediante los argumentos que reciben al crearlos, por definición es bueno mandarlos mediante un argumento llamado `props``
```jsx
import React from 'react'

const Button = props => {
  const {text} =  props
  return(
    <div>
      <button type="button">{text}</button>
    </div>
  )
};

export default Button;
```

> Nótese que resulta simple utilzar `text` de manera simple ya que hemos destructurado el objeto props.


La implementación se vería algo así:
```javascript
ReactDOM.render(
  <Button text="Click 2" />,
  document.getElementById('root')
);
```

# Ciclo de vida de los componentes React
Los componentes pasan por una serie de fases de ciclo de vida. Algunos serán toda una sección del componente y otros se pueden mandar llamar para asignar actividades según las necesidades, las fases se pueden clasificar de la siguiente manera:

* Montaje. El componete se crea junto a la lógica y los componentes internos, luego son insertados en el DOM. Métodos:
  * **constructor()** es el primer método llamado, aquí se inicializan métodos, controladores y eventos del estado.
  * **getDerivedStateFromProps()** se llama antes de presentarse en el DOM, nos permite actualizar el estado interno en respuesta a un cambio en las propiedades.
  * **render()** se llama para representar los elementos del DOM e implementar su lógica
  * **componentdidMount()** se llama cuando el componente ha sido montado en el DOM, aquí se trabajan los eventos que permiten interactuar con el componente.
* Actualización. Nuestro componente está pendiente de los cambios que pueden presentarse en el state o las props para hacer los cambios que sean necesarios.
  * **getDerivedStateFromProps()** es el primero en ejecutarse en la fase de actualización y funciona de la misma forma que en el montaje
  * **shouldComponentUpdate()** en él se puede controlar la fase de actualización, retornamos un booleano para proceder o no con la actualización, se usa para optimización.
  * **render()** se llama para representar los cambios en el DOM
  * **componentDidUpdate()** es invocado inmediatamente después de que el componente se actualiza y recibe compo argumentos las propiedades y el estado.
* Demsontaje. Nuestro componente "muere" cuando no necesitamos más un elemento de nuestra aplicación, esto es, sacarlo del DOM.
  * **componentWillUnmount()** se llama justo antes de que el componente sea eliminaddo del DOM
* Manejo de errores. Cuando se sucita algún error en el código de la aplicación, se entra en esta fase para entender qué está ocurriendo.
  * **getDerivedStateFromError()** se llama tan pronto se sucita un error, recibe como argumento el error.
  * **componentDidCatch()** se llama después de lanzarse un error, recibe como argumento el error

En la siguiente [liga](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/), encontramos un diagrama ilustrativo de las primeras tres:

# Instlación y configuración de un proyecto
Para empezar a configurar un proyecto desde cero, creamos nuestra carpeta, inicializamos nuestro repo local e inicializamos npm:
```bash
mkdir [project]
git init
npm init
```

Con lo cuál tendremos solamente nuestro `package`, vamos a crear la estrucutra básica nuestro proyecto:
```bash
project/
--- public/
--- --- index.html
--- src/
--- --- components/
--- --- index.js
```

Ahora instalamos las dependencias react y react-dom con el siguiente comando:
```bash
npm install react react-dom
```

## Agregando componentes al proyecto
Dentro de la carpeta `components, creamos un archivo llamado `HelloWorld.jsx` con la siguiente estructura:
```jsx
import React from 'react'

const HelloWorld = () => (
  <h1>hola mundo!</h1>
)

export default HelloWorld
```

## Agregando el entrypoint de nuestro proyecto
El entrypoint es el primer archivo que será leído en nuestro proyecto, como su njombre lo dice: punto de entrada, en él haremos uso de React DOM, que nos permitirá implementar nuestro código jsx en el proyecto. Todo esto lo haremos en el archivo `index.js`:
```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import Helloworld from './components/HelloWorld'
// La función render, recib el componente a mostrar y el nodo en el cuál se va indexar
ReactDOM.render(<Helloworld />, document.getElementById('app'))
```

## Agregando el html de nuestro proyecto
Este será el markup principal de nuestro proyecto, donde generaremos el elemento donde será renderizada uestra aplicación:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Project</title>
</head>
<body>
  <div id="app"></div>
</body>
</html>
```

## Agregando compatibilidad con Babel
Babel es una herramienta que utilizaremos para trnaspilar nuestro código moderno de javascript a código que todos los navegadores puesan soportar.

Primeramente instalamos las dependencias que necesitamos para babel como dependencias de desarrollo:
```bash
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
```

Creamos el archivo `.babelrc` en la raíz de nuestro proyecto con la siguiente configuración:
```json
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

## Configurando webpack
Webpack nos ayudará a preparar nuestro proyecto para el entorno de desarrollo local y eventualmente para su despliegue a producción: reunirá nuestros archivos y los optimizará.

Primeramente instalamos las siguientes dependencias de desarrollo:
```bash
npm install webpack webpack-cli html-webpack-plugin html-loader --save-dev
```

Ahora generamos en la raíz de nuestro proyecto el archivo `webpack.config.js` con la siguiente estructura:
```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: {
          loader: "html-loader"
        }
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
      filename: './index.html'
    })
  ]
}
```

Donde:
* ´entry´ contiene información sobre el punto de acceso
* ´output´ de donde ubicará y cómo nombrará los archivos resultado del proceso de compilación
* ´resolve´ para indicar las extensiones que se resolverán
* ´module´ contiene las reglas que seguirá nuestro proyecto

Posteriormente agregaremos un nuevo script a nuestro ´package´:
```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --mode production"
  },
```

Ahora corremos la compilación con
```bash
npm run build
```
> Nótese que esta configuración es útil para generar un bundle de nuestro proyecto para producción.


Ahora veremos como resultado nuestra carpeta dist con todo nuestro proyecto preparado para producción en la carpeta de `dist`.

### Webpack dev server
Para poder probar lo que estamos construyendo también nos apoyaremos de WebPack para generar un server local en donde podamos ejecutar nuestro proyecto para develop.

Primeramente instalamos la dependencia:
```bash
npm install webpack-dev-server --save-dev
```

Generaremos otro script en nuestro `package`:
```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --mode production",
    "start": "webpack serve --mode development --env development"
  },
```

Corremos el comando con:
```bash
npm run start
```

Con esto ya podremos ver nuestro proyecto en un entorno de desarrollo local que se actualizará cada que hagamos un cambio.

## Configurando sass
Para configurar sass en nuestro proyecto tenemos que llevar a cabo la siguiente configuración:

Instalamos las siguientes dependencias de desarollo:
```bash
npm install mini-css-extract-plugin css-loader node-sass sass-loader --save-dev
```

Agregamos una nueva dependencia `MiniCssExtractPlugin`, así como una nueva regla y un nuevo plugin en nuestro archivo `webpack.config.js`:
```javascript
...
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  module: {
    rules: [
      ...
      {
        test: /\.(s*)css$/,
        use: [
          {
            loader: MiniCssExtractPlugin.loader,
          },
          'css-loader',
          'sass-loader'
        ]
      }
    ],
    plugins: [
      ...
      new MiniCssExtractPlugin({
        filename: 'assets/[name].css'
      })
    ]
  }
}
```

Adicionalmente agregaremos a nuestro proyecto una llamada `assets` dentro de la carpeta `src`, que será donde vivirán nuestros archivos `sass` así como cualquier recurso que se use en nuestro proyecto.
```bash
--- src/
--- assets/
--- --- App.scss
```

Inicialmente vamos a crear también un archivo llamado `App.scss` para generar nuestros primero estilos:
```scss
body {
  margin: 0;
  background: red;
}
```

Para implementarlo en nuestro componente tendríamos que importarlo
```jsx
// HelloWorld.jsx
import '../assets/styles/App.scss'
```

Con sto ya podríamos generar nuestros estilos en archivos sass para que luego sean agregados en la compilación de webpack.





