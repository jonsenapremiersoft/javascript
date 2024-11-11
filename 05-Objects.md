# Objetos

## 1. Introdução
Os objetos são estruturas fundamentais em JavaScript que permitem armazenar coleções de dados e funcionalidades relacionadas. Eles são compostos por pares de chave-valor, onde cada valor pode ser qualquer tipo de dado, incluindo outros objetos ou funções.

## 2. Criação e Manipulação de Objetos

### 2.1 Criando Objetos

Existem três formas principais de criar objetos:

```javascript
// 1. Notação literal (mais comum)
const pessoa = {
    nome: "João",
    idade: 25
};

// 2. Construtor Object
const carro = new Object();
carro.marca = "Toyota";
carro.modelo = "Corolla";

// 3. Função construtora
function Animal(especie, nome) {
    this.especie = especie;
    this.nome = nome;
}
const cachorro = new Animal("cachorro", "Rex");
```

### 2.2 Manipulando Propriedades

```javascript
const usuario = {
    nome: "Maria",
    idade: 30
};

// Adicionando propriedades
usuario.email = "maria@email.com";
usuario["telefone"] = "123456789";

// Modificando propriedades
usuario.idade = 31;

// Removendo propriedades
delete usuario.telefone;

// Verificando se uma propriedade existe
console.log("nome" in usuario); // true
console.log(usuario.hasOwnProperty("email")); // true
```

## 3. Propriedades e Métodos

### 3.1 Métodos em Objetos

```javascript
const calculadora = {
    valor1: 0,
    valor2: 0,
    // Método tradicional
    somar: function() {
        return this.valor1 + this.valor2;
    },
    // Sintaxe abreviada (ES6+)
    multiplicar() {
        return this.valor1 * this.valor2;
    }
};

calculadora.valor1 = 5;
calculadora.valor2 = 3;
console.log(calculadora.somar()); // 8
```

### 3.2 Getters e Setters

```javascript
const conta = {
    _saldo: 0,
    
    get saldo() {
        return `R$ ${this._saldo.toFixed(2)}`;
    },
    
    set saldo(valor) {
        if (valor >= 0) {
            this._saldo = valor;
        } else {
            console.log("Valor inválido");
        }
    }
};

conta.saldo = 150.50;
console.log(conta.saldo); // "R$ 150.50"
```

## 4. Object Destructuring

### 4.1 Destructuring Básico

```javascript
const produto = {
    nome: "Notebook",
    preco: 3000,
    especificacoes: {
        ram: "8GB",
        armazenamento: "256GB"
    }
};

// Destructuring simples
const { nome, preco } = produto;
console.log(nome); // "Notebook"

// Renomeando variáveis
const { nome: nomeProduto, preco: precoProduto } = produto;
console.log(nomeProduto); // "Notebook"

// Destructuring aninhado
const { especificacoes: { ram, armazenamento } } = produto;
console.log(ram); // "8GB"
```

### 4.2 Valores Padrão

```javascript
const config = {
    tema: "claro"
};

const { tema, idioma = "pt-BR" } = config;
console.log(idioma); // "pt-BR"
```

## 5. Exercícios Práticos

### Exercício 1: Criação e Manipulação
```javascript
/* 
Crie um objeto chamado 'biblioteca' que contenha os seguintes dados:
- nome
- livros (array de objetos com título, autor e ano)
- adicionarLivro (método para adicionar novo livro)
- listarLivros (método para listar todos os livros)
*/

// Solução
const biblioteca = {
    nome: "Biblioteca Central",
    livros: [],
    adicionarLivro(titulo, autor, ano) {
        this.livros.push({ titulo, autor, ano });
    },
    listarLivros() {
        this.livros.forEach(livro => 
            console.log(`${livro.titulo} - ${livro.autor} (${livro.ano})`)
        );
    }
};
```

### Exercício 2: Destructuring
```javascript
/* 
Dado o objeto abaixo, use destructuring para extrair:
- nome e idade em variáveis normais
- rua e número em variáveis chamadas enderecoRua e enderecoNumero
- telefone celular em uma variável chamada celular (com valor padrão 'não informado')
*/

const cliente = {
    nome: "Ana Silva",
    idade: 28,
    endereco: {
        rua: "Rua das Flores",
        numero: 123
    },
    telefones: {
        fixo: "11 2222-3333"
    }
};

// Solução
const { nome, idade } = cliente;
const { endereco: { rua: enderecoRua, numero: enderecoNumero } } = cliente;
const { telefones: { celular = 'não informado' } } = cliente;
```

## 6. Boas Práticas

1. **Nomeação Clara**
   - Use nomes descritivos para propriedades e métodos
   - Siga as convenções de nomenclatura (camelCase)

2. **Organização**
   - Mantenha propriedades relacionadas juntas
   - Agrupe métodos de forma lógica

3. **Imutabilidade**
   - Prefira `const` para declaração de objetos
   - Use métodos que não modificam o objeto original

4. **Encapsulamento**
   - Use getters e setters para controlar acesso a dados
   - Prefixe propriedades privadas com underscore (_)

5. **Destructuring**
   - Use destructuring para extrair múltiplas propriedades
   - Defina valores padrão quando apropriado

6. **Métodos Concisos**
   - Use a sintaxe de método abreviada do ES6
   - Mantenha métodos pequenos e focados

7. **Validação**
   - Valide dados em setters
   - Verifique a existência de propriedades antes de usá-las

## Conclusão

Objetos são fundamentais em JavaScript e dominá-los é essencial para programação eficiente. Pratique os conceitos apresentados e sempre consulte a documentação para aprofundamento.
