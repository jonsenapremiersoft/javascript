# Expressões Regulares (Regex) em JavaScript

## 1. Introdução
Expressões Regulares são padrões utilizados para encontrar combinações de caracteres em strings. Em JavaScript, podemos criar uma regex de duas formas:

```javascript
// Usando o construtor
const regex1 = new RegExp('padrão');

// Usando literal (mais comum)
const regex2 = /padrão/;
```

## 2. Caracteres Especiais Básicos
Vamos praticar com os caracteres mais comuns:

```javascript
// . - qualquer caractere (exceto quebra de linha)
let texto = "gato, guto, goto";
console.log(texto.match(/g.to/g)); // ['gato', 'guto', 'goto']

// [] - conjunto de caracteres
let palavras = "cat, bat, rat";
console.log(palavras.match(/[cbr]at/g)); // ['cat', 'bat', 'rat']

// ^ - início da string
let frase = "JavaScript é incrível";
console.log(/^Java/.test(frase)); // true

// $ - fim da string
console.log(/ível$/.test(frase)); // true
```

## 3. Quantificadores
Vamos ver como definir quantidades:

```javascript
// * - 0 ou mais ocorrências
let texto1 = "ca cat caat caaat";
console.log(texto1.match(/ca*t/g)); // ['ct', 'cat', 'caat', 'caaat']

// + - 1 ou mais ocorrências
console.log(texto1.match(/ca+t/g)); // ['cat', 'caat', 'caaat']

// ? - 0 ou 1 ocorrência
let texto2 = "color colour";
console.log(texto2.match(/colou?r/g)); // ['color', 'colour']

// {n} - exatamente n ocorrências
// {n,} - n ou mais ocorrências
// {n,m} - entre n e m ocorrências
let numeros = "1 12 123 1234 12345";
console.log(numeros.match(/\d{3}/g)); // ['123', '123', '123']
```

## 4. Exercício Prático
Vamos criar um validador de e-mail simples:

```javascript
function validarEmail(email) {
    const regex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
    return regex.test(email);
}

// Testando
console.log(validarEmail('teste@email.com')); // true
console.log(validarEmail('teste@.com')); // false
console.log(validarEmail('teste@dominio')); // false
```

## 5. Métodos Importantes
JavaScript oferece vários métodos para trabalhar com regex:

```javascript
const texto = "O rato roeu a roupa do rei de Roma";

// test() - retorna true/false
const temRato = /rato/.test(texto);
console.log(temRato); // true

// match() - retorna um array com as correspondências
const palavrasComR = texto.match(/r\w+/g);
console.log(palavrasComR); // ['rato', 'roeu', 'roupa', 'rei', 'Roma']

// replace() - substitui as correspondências
const novoTexto = texto.replace(/r/g, 'l');
console.log(novoTexto); // "O lato loeu a loupa do lei de loma"
```



## 6. Dicas Importantes
1. Use a flag `g` para busca global
2. Use a flag `i` para busca case-insensitive
3. Use a flag `m` para busca multilinha
4. Teste suas regex em sites como regex101.com

Quer praticar algum desses conceitos ou tem alguma dúvida específica?
