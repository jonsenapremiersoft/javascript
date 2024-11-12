# Fundamentos de Escopo e Hoisting em JavaScript

## 1. Objetivos da Aula
- Compreender os diferentes tipos de escopo em JavaScript
- Entender o mecanismo de hoisting
- Conhecer as diferenças entre var, let e const
- Introduzir arrow functions e seu comportamento com escopo

## 2. Escopo Global e Local

### 2.1 Escopo Global
O escopo global é o contexto mais externo do código. Variáveis declaradas fora de qualquer função são globais.

```javascript
// Variável global
var globalVar = "Sou global";
let globalLet = "Também sou global";

function exemplo() {
    console.log(globalVar); // Acessível
    console.log(globalLet); // Acessível
}
```

⚠️ **Cuidados com o escopo global:**
- Evite poluir o escopo global
- Pode causar conflitos de nomes
- Dificulta a manutenção do código

### 2.2 Escopo Local (Function Scope)
Variáveis declaradas dentro de funções só são acessíveis dentro delas.

```javascript
function exemploLocal() {
    var localVar = "Sou local";
    let localLet = "Também sou local";
    
    console.log(localVar); // OK
    console.log(localLet); // OK
}

// console.log(localVar); // ReferenceError
// console.log(localLet); // ReferenceError
```

## 3. Escopo de Bloco

### 3.1 let vs var
A principal diferença entre `let` e `var` é o escopo de bloco:

```javascript
// Exemplo com var
if (true) {
    var x = 10;
}
console.log(x); // 10 - var não respeita o escopo de bloco

// Exemplo com let
if (true) {
    let y = 20;
}
// console.log(y); // ReferenceError - let respeita o escopo de bloco
```

### 3.2 const
- Similar ao `let` em termos de escopo
- Não pode ser reatribuída
- Mas objetos e arrays podem ser modificados

```javascript
const PI = 3.14;
// PI = 3.15; // TypeError

const usuario = {
    nome: "João"
};
usuario.nome = "Maria"; // OK
// usuario = {}; // TypeError
```

## 4. Hoisting

### 4.1 Hoisting de Variáveis
O JavaScript "eleva" as declarações para o topo do seu escopo.

```javascript
console.log(varExemplo); // undefined
var varExemplo = "teste";

// O código acima é interpretado assim:
var varExemplo;
console.log(varExemplo);
varExemplo = "teste";
```

### 4.2 Hoisting de Funções
Funções declaradas com `function` são completamente elevadas:

```javascript
saudacao(); // "Olá!" - Funciona!

function saudacao() {
    console.log("Olá!");
}

// Mas com função de expressão não funciona:
// bemVindo(); // TypeError
var bemVindo = function() {
    console.log("Bem-vindo!");
};
```

## 5. Introdução às Arrow Functions

### 5.1 Sintaxe Básica
```javascript
// Função tradicional
function soma(a, b) {
    return a + b;
}

// Arrow function
const somaArrow = (a, b) => a + b;

// Com um único parâmetro
const dobrar = x => x * 2;

// Com corpo de função
const saudar = nome => {
    const saudacao = `Olá, ${nome}!`;
    return saudacao;
};
```

## 6. Exercícios Práticos

### Exercício 1: Hoisting
```javascript
// Explique o que será impresso e por quê
console.log(a);
var a = 1;

console.log(b);
let b = 2;

function exemplo() {
    console.log(c);
    var c = 3;
}
```

### Exercício 2: Conversão para Arrow Function
```javascript
// Converta as seguintes funções para arrow functions
function multiplicar(a, b) {
    return a * b;
}

function parOuImpar(numero) {
    if (numero % 2 === 0) {
        return "Par";
    }
    return "Ímpar";
}
```

## 7. Boas Práticas

1. **Preferência por `const` e `let`**
   - Use `const` por padrão
   - Use `let` quando precisar reatribuir
   - Evite `var`

2. **Evite Escopo Global**
   - Encapsule seu código em funções ou módulos

3. **Nomeação Clara**
   - Use nomes descritivos para variáveis e funções
   - Siga uma convenção de nomenclatura consistente

4. **Declarações no Topo**
   - Declare todas as variáveis no topo do seu escopo
   - Evite depender do hoisting
