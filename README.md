#### Proyecto y tecnologías que usaremos
En este curso realizaremos una aplicación muy parecida a Instagram, llamada petgram. Tendremos nuestras rutas, gestión de usuarios y likes.

##### Utilizaremos como empaquetador y transpilador:

Webpack, Babel
##### Estilado con CSS en JS con:

styled-components
##### Como linter utilizaremos:

Standard JS
##### Para fetching (obtención) de datos:

GraphQL, React Apollo
##### Para el enrutado de la SPA utilizaremos:

Reach Router
##### Para las buenas prácticas utilizaremos:

Lighthouse, Cypress
##### Haremos SEO, PWA y Deploy con:

React Helmet, Workbox, Progressive Web App, Deply con Now

#### Clonando el repositorio e instalando Webpack
Pasos para iniciar nuestro proyecto:

Paso 1: Vamos a clonar el repositorio desde github.com/midudev/curso-platzi-react-avanzado usando git clone URL_DEL_REPO en nuestra consola.
Paso 2: Vamos a instalar webpack y webpack-cli como dependencias de desarrollo con:
```
 	npm i webpack webpack-cli --save-dev.
```
Paso 3: Crearemos una carpeta llama src y dentro de ella un archivo index.js en el cual colocaremos solo un 
```
	console.log('Empezamos el curso!').
```
Paso 4: Crearemos en el root de nuestro proyecto un archivo 
```
	webpack.config.js el cual tendrá toda la configuración de webpack
```
Paso 5: Instalaremos html-webpack-plugin con: 
```
	npm i html-webpack-plugin --save-dev.
```
Paso 6: Instalaremos webpack-dev-server con: 
```
	npm i webpack-dev-server --save-dev.
```
Paso 7: Añadiremos un nuevo script llamado dev: 
```
	"dev": "webpack-dev-server".
```

```
	// webpack.config.js
	const HtmlWebpackPlugin = require("html-webpack-plugin")

	module.exports = {
		output: {
			filename: 'app.bundle.js'
		},
		plugins: [
			new HtmlWebpackPlugin()
		]
	}
```

#### Instalación de React y Babel
En esta clase vamos a configurar React instalando las dependencias 
```
	npm i react react-dom 
```
y Babel para poder transpilar código jsx a JavaScript Vanilla con: 
```
	npm i @babel/core @babel/preset-env babel-loader @babel/preset-react --save-dev.
```
Ahora añadiremos en nuestro webpack.config.js lo siguiente:

// webpack.config.js

{/*...*/}
module.exports = {
	{/*...*/}
	module: {
		rules: [
			{
				test: /\.js$/,
				exclude: /node_modules/,
				use: {
					loader: 'babel-loader',
					options: {
						presets: [
							'@babel/preset-env',
							'@babel/preset-react'
						]
					}
				}
			}
		]
	}
}

#### Linter, extensiones y deploy con Now
En esta clase haremos que el desarrollo sea más ágil y correcto siguiendo los siguientes pasos:

Vamos a instalar StandardJS como dependencia de desarrollo con: 
```
	npm i standard --save-dev
```
StandardJS nos va a servir de Linter para una mejor escritura de JavaScript/React.
Agregaremos un nuevo script en nuestro package.json: 
```
	"lint": "standard".
```
Ahora vamos a ignorar aquellos archivos que no queremos que el Linter arregle, añadiremos en nuestro package.json lo siguiente:
```
	"standard": {
		"ignore": [
			"/api/**"
		]
	}
```
Ahora, queremos que nuestro Linter nos detecte los errores a medida que vamos escribiendo, para hacer esto añadimos lo siguiente a nuestro package.json:
```
	"eslintConfig": {
		"extends": [
			"./node_modules/standard/eslintrc.json"
		]
	}
```
Ahora debemos tener lo siguiente en nuestro editor de código para que funcione todo al pie de la letra:
	Tener instalada la extensión ESLint
	Si quieres que al guardar los cambios se formatee tu código deberás tener instalada la extensión Prettier
	Tener las siguientes configuraciones en VSCode:	
		Format On Save: false
		Prettier: Eslint Integration: true
		Eslint: Auto Fix On Save: true
Ahora utilizaremos Now para hacer el deploy de nuestro proyecto.
Descargaremos e instalaremos Now para que nos registre de una manera mucho más fácil los tokens de acceso y podamos continuar con el curso.
Entraremos a la carpeta de api y notaremos que ya tiene un archivo now.json que preparamos para ti con toda la configuración necesaria para hacer el deploy.
Para desplegar el proyecto del backend haremos lo siguiente en nuestra terminar:
	cd api
	Cambiamos el name de la aplicación en el now.json
	Finalmente ejecutamos now
Ahora para desplegar nuestro front haremos lo siguiente:
	Crearemos un archivo now.json en el root de nuestro proyecto con lo siguiente:
```
	{
		""version"": 2,
		""name"": ""petgram"",
		""builds"": [
			{
				""use"": ""@now/static-build"",
				""src"": ""package.json""
			}
		],
		""routes"": [
			{
				""src"": ""(.*).js"",
				""dest"": ""/$1.js""
			},
			{
				""src"": ""(.*).json"",
				""dest"": ""/$1.json""
			},
			{
				""src"": ""/.*"",
				""dest"": ""index.html""
			}
		]
	}
```
En nuestro package.json añadiremos el siguiente script: 
```
	""now-build"": ""npm run build"".
```
Finalmente en la raíz de nuestro proyecto ejecutaremos now para que nos dé una URL en la que se verá nuestro proyecto."