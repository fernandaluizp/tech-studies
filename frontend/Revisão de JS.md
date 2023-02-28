# Revisão de JS

## CommonJS and ESModules

<br>

### CommonJS

- mod1.js

```bash
const mod1Function = () => console.log('Mod1 is alive!')
const mod1Function2 = () => console.log('Mod1 is rolling, baby!')

module.exports = { mod1Function, mod1Function2 }
```

- main.js

```bash
({ mod1Function, mod1Function2 } = require('./mod1.js'))

const testFunction = () => {
    console.log('Im the main function')
    mod1Function()
    mod1Function2()
}

testFunction()
```

<br>

### ESModules

#### Uso comum

- mod.js

```bash
const mod1Function = () => console.log('Mod1 is alive!')
export { mod1Function }
```

- main.js

```bash
import { mod1Function } from './mod1.js'

const testFunction = () => {
    console.log('Im the main function')
    mod1Function()
}

testFunction()
```

#### Exportando mais de um componente

```bash
// mod1.js
const mod1Function = () => console.log('Mod1 is alive!')
const mod1Function2 = () => console.log('Mod1 is rolling, baby!')

export { mod1Function, mod1Function2 }
```

```bash
// main.js
import { mod1Function, mod1Function2 } from './mod1.js'

const testFunction = () => {
    console.log('Im the main function')
    mod1Function()
    mod1Function2()
}

testFunction()
```
#### Export default

- mod.js

```bash
// mod1.js
const mod1Function = () => console.log('Mod1 is alive!')
const mod1Function2 = () => console.log('Mod1 is rolling, baby!')

export default mod1Function
export { mod1Function2 }
```

- main.js

```bash
// main.js
import mod1Function, { mod1Function2 } from './mod1.js'

const testFunction = () => {
    console.log('Im the main function')
    mod1Function()
    mod1Function2()
}

testFunction()
```

<br>
<hr>
<br>

## Destructuring


### Destructuring de Array

```bash
const [ valorA, valorB, ..valorC ] = [ 10, 20, 30, 40, 50, 60 ]

  console.log(valorA) // 10
  console.log(valorB) // 20
  console.log(valorC) // [ 30, 40, 50, 60 ]
```


### Destructuring de Object

```bash
const usuario = { idade: 18, temFilhos: true, xpto: '1123' }

  const { nome = 'Pedro', idade, ...resto } = usuario

  console.log(nome) // Pedro
  console.log(idade) // 18
  console.log(resto) // { temFilhos: true, xpto: '1123' }
```

<br>
<hr>
<br>

## Function vs Lambda Function vs Função Construtora


###  Função Anônima
```bash

var anon = function (a, b) { return a + b };

ou

var anon = (a, b) => { return a + b };

ou

- Usando função normal
[1,2,3,4].filter(function (value) {return value % 2 === 0});

- Usando função anônima
[1,2,3,4].filter(value => value % 2 === 0);

```

### Lambda Function

```bash
function traverseArray(arr, func) {
    let result = '';
    for (const value of arr) {
        result += func(value) + ' ';
    }
    console.log(result);
}

const arr = [1, 2, 3, 4, 5];
const doubler = value => value * 2;

traverseArray(arr, doubler);
//result: 2 4 6 8 10

```
- Diferença maior entre função anonima e lambda é que a lambda pode ser nomeada


```bash
function traverseArray(arr, func) {
    let result = '';
    for (const value of arr) {
        result += func(value) + ' ';
    }
    console.log(result);
}

const arr = [1, 2, 3, 4, 5];

traverseArray(arr, function doubler(value) {
    return value * 2;
});
//result: 2 4 6 8 10
```

### Função Construtora

```bash
function Cachorro(nome, idade) {
    this.nome = nome
    this.idade = idade
}

const cachorro = new Cachorro('Rex', 1)
```
Ao executar a função Cachorro com new, estamos fazendo quatro coisas:

1. Criando um novo objeto ({}).
2. Definindo o construtor do objeto cachorro como Cachorro.
3. Definindo o protótipo do objeto cachorro como Cachorro.prototype.
4. Executando a função Cachorro dentro do escopo do novo objeto, criando assim, uma nova instância.

<br>
<hr>
<br>


## Closure / IIFE
- Closure em JavaScript é uma forma de lexical scoping usado para perservar variáveis do escopo externo de uma função no escopo interno de uma função. Lexical scoping é o processo usado para definir o escopo de uma variável pela posição do source code.

### Closure

```bash

function buildGreeting() {
    let message = 'Hello';

    function greetUser() {
        console.log(message);
    }

    return greetUser;
}
let hello = buildGreeting();
hello();

```

### Immediately Invoked Function Expressions (IIFE)

```bash
(function (name) {
    console.log(name);
})("Tom")
```

```bash
for (var id = 1; id <= 3; id ++) {
    (function (id) {
        setTimeout(function () {
            console.log('seconds: ' + id);
        }, id* 1000);
    })(id);
}
```

<br>
<hr>
<br>

## First-Class Function e callbacks

### First-Class Function

- Entende-se que uma linguagem de programação tem Função First-class quando suas funções são tratadas como qualquer outra variável

```bash
    const foo = function() {
    console.log("foobar");
    }
    // Chamar a função usando a variável
    foo();
```

### Função Callback

```bash
function sayHello() {
   return "Hello, ";
}
function greeting(helloMessage, name) {
  console.log(helloMessage() + name);
}
// Passar `sayHello` como um argumento pra função `greeting`
greeting(sayHello, "JavaScript!");
```
- Nós estamos passando a função sayHello() como um argumento pra função greeting(), isso explica como estamos tratando a função como um valor.
sayHello é uma função Callback

<br>
<hr>
<br>


## Class/prototype

```bash
var Reptile = function(name, canItSwim) {
  this.name = name;
  this.canItSwim = canItSwim;
}

Reptile.prototype.doesItDrown = function() {
  if (this.canItSwim) {
    console.log(`${this.name} can swim`);
  } else {
    console.log(`${this.name} has drowned`);
  }
};

// for this example consider alligators can swim and crocs cannot
let alligator = new Reptile("alligator", true);
alligator.doesItDrown(); // alligator can swim

let croc = new Reptile("croc", false);
croc.doesItDrown(); // croc has drowned
```