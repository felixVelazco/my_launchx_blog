
title: "Jest sir!"
date: 2022-04-02
description: 'Pruebas unitarias con Jest'


Hola a todos los que lean esto! En el post anterior hablé de manera general sobre la definición y la utilidad de las muestras unitarias en la creación de 
software, ahora toca ver la versión práctica del código, así que vamos a darle!

## Requisitos
- Javascript
- npm
- Node JS
- Jest

## Requerimientos de la aplicación
Para este ejercicio, debemos de crear una clase `Mascota`, la cual al instanciar un objeto, recibirá de parámetros `name`, `age`, `race`, `canSwim`, `favoriteFoods` 
y debe tener los métodos `getName`, `setAge`. 

## Pasos
### Crear la carpeta de tu proyecto 
Para este proyecto crearé una carpeta llamada <kbd>Mascota</kbd> donde estará la raiz de nuestro proyecto

### Crear nuestro `package.json`
En la raiz de nuestro proyecto, abriremos una terminal, donde ejecutaremos el siguiente comando:

```console
felix@bar:mascota$ npm init
```

Te aparecerán después varias preguntas que puedes responder u omitir simplemente presionando <kbd>Enter</kbd> en cada una, y listo!

Si abrimos nuestro archivo package.json, veremos algo como esto:

```json
{
  "name": "mascota",
  "version": "1.0.0",
  "description": "\"Clase para crear una mascota\"",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "felix velazco",
  "license": "ISC"
}
```

### Agregar `Jest` a nuestro `package.json`
Para eso ejecutaremos el comando:

```console
felix@bar:mascota$ npm install --save-dev jest
```
Este comando lo que hace es descargar la carpeta `node_modules` en nuestro proyecto, y especifica que el `node_module` jest será utilizado como 
devDependencies (es decir, son dependencias que sirven solo cuando el proyecto está en desarrollo, pero no para el producto final, como lo son las 
pruebas unitarias)

Y si nos metemos nuevamente a nuestro archivo `package.json` vemos que este a sido modificado, agregando nuestras `devDependencies`.

```json
{
  "name": "mascota",
  "version": "1.0.0",
  "description": "\"Clase para crear una mascota\"",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "felix velazco",
  "license": "ISC",
  "devDependencies": {
    "jest": "^27.5.1"
  }
}
```
Ya por último, modificamos la línea de `"test": "echo \"Error: no test specified\" && exit 1"` por `"test": "node ./node_modules/jest/bin/jest"`

```
NOTA: esta sintaxis solo aplica para windows, para sistemas Linux/Unix usar `"test": "node ./node_modules/.bin/jest"`
```
Y así nuestro `package.json` quedó listo

### Creación de nuestras carpetas y archivos
Pasamos a crear dos carpetas llamadas <kbd>app</kbd> y <kbd>test</kbd>. En la primer carpeta crearemos un archivo llamado <kbd>mascota.js</kbd>, mientras que en
la segunda un archivo <kbd>mascota.test.js</kbd>. Debe de quedar una distribución similar a la siguiente:

![Directorio con todos los archivos](https://user-images.githubusercontent.com/79220309/164637006-56f750f7-d55d-4482-b2ab-d78a3a93de68.png)

### Aplicar el TDD
En el post anterior había mencionado que el TDD es una técnica que ayuda a crear código en base a pruebas, y que consta de 3 pasos.

#### 1. Hacer una prueba que falle

Abrimos el archivo `mascota.test.js` y creamos el siguiente código

```js
//Con esto importamos la clase mascota
const Mascota = require("./../app/mascota");

//Crea una suite donde estarán todas tus pruebas
describe('Unit test suite para Clase Mascota',() =>{
//Aqui se pone la primera prueba, que consiste en crear un objeto de la clase mascota
  test('1) Crear un objeto', () => {
    //Se crea el objeto con los atributos que queramos
    const perro = new Mascota('doggy', 2, 'shiba', false, ['croquetas', 'sobres', 'platano']);

    //en expect ponemos la variable que queremos analizar
    //toBe nos dice que a lo que tiene que ser igual (existen mas funciones ademas de toBe)
    expect(perro.name).toBe("doggy");
  })
})
```
Guardamos cambios, nos vamos a nuestra consola y corremos la prueba

```console
felix@bar:mascota/test$ npm test mascota.test.js

> mascota@1.0.0 test
> node ./node_modules/jest/bin/jest "test/mascota.test.js"

 FAIL  test/mascota.test.js
  Unit test suite para Clase Mascota
    × 1) Crear un objeto (1 ms)

  ● Unit test suite para Clase Mascota › 1) Crear un objeto

    TypeError: Mascota is not a constructor

       7 |   test('1) Crear un objeto', () => {
       8 |     //Se crea el objeto con los atributos que queramos
    >  9 |     const perro = new Mascota('doggy', 2, 'shiba', false, ['croquetas', 'sobres', 'platano']);
         |                   ^
      10 |
      11 |     //en expect ponemos la variable que queremos analizar
      12 |     //toBe nos dice que a lo que tiene que ser igual (existen mas funciones ademas de toBe)

      at Object.<anonymous> (test/mascota.test.js:9:19)

Test Suites: 1 failed, 1 total
Tests:       1 failed, 1 total
Snapshots:   0 total
Time:        0.696 s, estimated 1 s
Ran all test suites matching /test\\mascota.test.js/i.
```
La prueba tronó, como debería de ser, debido a que aún no tenemos nada de código hecho. Una vez que tienes lo que debes de recibir





