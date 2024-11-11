# Aula: Fundamentos de JavaScript - Variáveis e Tipos de Dados

## 1. Declaração de Variáveis (var, let e const)

Em JavaScript, temos três formas de declarar variáveis:

```javascript
// var (forma antiga, evite usar)
var idade = 25;

// let (permite reatribuição)
let nome = "Maria";
nome = "João"; // permitido

// const (não permite reatribuição)
const PI = 3.14159;
// PI = 3.14; // Erro!
```

Principais diferenças:
- `var`: tem escopo de função e pode ser redeclarada
- `let`: tem escopo de bloco e pode ser reatribuída
- `const`: tem escopo de bloco e não pode ser reatribuída

## 2. Tipos de Dados Básicos

### Numbers
```javascript
let idade = 25;          // número inteiro
let altura = 1.75;       // número decimal
let infinito = Infinity; // infinito
let naoNumero = NaN;     // Not a Number
```

### Strings
```javascript
let nome = "Maria";
let sobrenome = 'Silva';
let nomeCompleto = `${nome} ${sobrenome}`; // template string

// Métodos comuns de string
console.log(nome.length);          // 5
console.log(nome.toUpperCase());   // MARIA
console.log(nome.toLowerCase());   // maria
```

### Booleans
```javascript
let estaChovendo = true;
let temSol = false;

// Operadores lógicos
let guardaChuva = estaChovendo && !temSol;  // AND
let diaAgradavel = estaChovendo || temSol;   // OR
```

## 3. null e undefined

```javascript
// undefined - valor não atribuído
let variavelNaoDefinida;
console.log(variavelNaoDefinida); // undefined

// null - ausência intencional de valor
let variavelNula = null;
```

## 4. Conversão de Tipos

```javascript
// String para Number
let numeroTexto = "123";
let numero = Number(numeroTexto);    // 123
let numeroFloat = parseFloat("3.14"); // 3.14
let numeroInt = parseInt("3.14");     // 3

// Number para String
let idade = 25;
let idadeTexto = idade.toString();    // "25"
let idadeTexto2 = String(idade);      // "25"

// Para Boolean
let booleano = Boolean(1);        // true
let booleano2 = Boolean("");      // false
```

## Desafios para Praticar

### Desafio 1: Calculadora de Idade
```javascript
/* 
Crie um programa que:
1. Declare uma constante com o ano atual
2. Declare uma variável com o ano de nascimento
3. Calcule a idade
4. Converta a idade para string e mostre no console
*/

// Sua solução aqui
```

### Desafio 2: Verificador de Tipos
```javascript
/* 
Crie um programa que:
1. Declare variáveis com diferentes tipos de dados
2. Crie uma função que recebe um valor e retorna seu tipo
3. Teste a função com todos os tipos que aprendemos
*/

// Sua solução aqui
```

### Desafio 3: Manipulação de Strings
```javascript
/* 
Crie um programa que:
1. Declare uma string com seu nome completo
2. Separe o nome do sobrenome
3. Conte quantas letras tem cada um
4. Converta o nome para maiúsculas e o sobrenome para minúsculas
*/

// Sua solução aqui
```

### Soluções dos Desafios:

Desafio 1:
```javascript
const anoAtual = 2024;
let anoNascimento = 1995;
let idade = anoAtual - anoNascimento;
let idadeTexto = idade.toString();
console.log(`Você tem ${idadeTexto} anos`);
```

Desafio 2:
```javascript
function verificarTipo(valor) {
    return typeof valor;
}

console.log(verificarTipo(42));        // "number"
console.log(verificarTipo("teste"));   // "string"
console.log(verificarTipo(true));      // "boolean"
console.log(verificarTipo(undefined)); // "undefined"
console.log(verificarTipo(null));      // "object"
```

Desafio 3:
```javascript
let nomeCompleto = "Maria Silva";
let partes = nomeCompleto.split(" ");
let nome = partes[0];
let sobrenome = partes[1];

console.log(`Nome: ${nome} (${nome.length} letras)`);
console.log(`Sobrenome: ${sobrenome} (${sobrenome.length} letras)`);
console.log(`Formatado: ${nome.toUpperCase()} ${sobrenome.toLowerCase()}`);
```

Dúvidas frequentes:
1. Quando usar let vs const?
   - Use `const` sempre que o valor não precisar ser reatribuído
   - Use `let` quando precisar mudar o valor da variável

2. Por que evitar var?
   - `var` tem um comportamento de escopo mais confuso
   - Pode causar bugs difíceis de encontrar
   - `let` e `const` são mais previsíveis e seguros

3. Qual a diferença entre null e undefined?
   - `undefined` é um valor automático para variáveis não inicializadas
   - `null` é um valor que você atribui intencionalmente para indicar ausência de valor

