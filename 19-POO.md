# Programação Orientada a Objetos (POO) em JavaScript

## **1. Introdução à POO**
A Programação Orientada a Objetos é um paradigma que organiza o código em **objetos**. Cada objeto possui:
- **Propriedades** (dados que ele armazena).
- **Métodos** (funções que ele pode executar).

### **Principais Conceitos**
- **Classe**: Modelo para criar objetos.
- **Objeto**: Instância de uma classe.
- **Encapsulamento**: Esconde detalhes internos do objeto.
- **Herança**: Permite que uma classe herde propriedades e métodos de outra.
- **Polimorfismo**: Capacidade de usar métodos de diferentes formas.

---

## **2. Classes e Objetos**
Em JavaScript, usamos o comando `class` para definir uma classe.

### **Exemplo de Classe**
```javascript
class Pessoa {
    constructor(nome, idade) {
        this.nome = nome; // Propriedade
        this.idade = idade;
    }
}

// Criando um objeto
const pessoa1 = new Pessoa("João", 30);
console.log(pessoa1.nome); // João
console.log(pessoa1.idade); // 30
```

---

## **3. Construtores e Propriedades**
- O **construtor** é um método especial usado para inicializar os objetos.
- As **propriedades** são atributos que armazenam dados nos objetos.

### **Exemplo**
```javascript
class Carro {
    constructor(marca, modelo, ano) {
        this.marca = marca;
        this.modelo = modelo;
        this.ano = ano;
    }
}

const meuCarro = new Carro("Toyota", "Corolla", 2022);
console.log(meuCarro.marca); // Toyota
```

---

## **4. Métodos de Classe**
Os **métodos** são funções que pertencem a uma classe.

### **Exemplo**
```javascript
class Calculadora {
    somar(a, b) {
        return a + b;
    }

    subtrair(a, b) {
        return a - b;
    }
}

const calc = new Calculadora();
console.log(calc.somar(5, 3)); // 8
console.log(calc.subtrair(5, 3)); // 2
```

---

## **5. Herança**
A **herança** permite que uma classe derive de outra, reutilizando suas propriedades e métodos.

### **Exemplo**
```javascript
class Animal {
    constructor(nome) {
        this.nome = nome;
    }

    fazerSom() {
        console.log("Som genérico");
    }
}

class Cachorro extends Animal {
    fazerSom() {
        console.log("Au au");
    }
}

const animal = new Animal("Genérico");
animal.fazerSom(); // Som genérico

const cachorro = new Cachorro("Rex");
cachorro.fazerSom(); // Au au
```

---

## **6. Encapsulamento**
Usamos o encapsulamento para restringir o acesso a certas partes do código. Propriedades ou métodos privados são precedidos por `#`.

### **Exemplo**
```javascript
class ContaBancaria {
    #saldo = 0;

    depositar(valor) {
        this.#saldo += valor;
    }

    sacar(valor) {
        if (valor <= this.#saldo) {
            this.#saldo -= valor;
        } else {
            console.log("Saldo insuficiente");
        }
    }

    mostrarSaldo() {
        console.log(`Saldo: R$${this.#saldo}`);
    }
}

const minhaConta = new ContaBancaria();
minhaConta.depositar(100);
minhaConta.sacar(50);
minhaConta.mostrarSaldo(); // Saldo: R$50
```

---

## **7. Polimorfismo**
O polimorfismo ocorre quando diferentes classes implementam o mesmo método de formas distintas.

### **Exemplo**
```javascript
class Forma {
    calcularArea() {
        console.log("Área genérica");
    }
}

class Quadrado extends Forma {
    constructor(lado) {
        super();
        this.lado = lado;
    }

    calcularArea() {
        return this.lado ** 2;
    }
}

class Circulo extends Forma {
    constructor(raio) {
        super();
        this.raio = raio;
    }

    calcularArea() {
        return Math.PI * this.raio ** 2;
    }
}

const formas = [new Quadrado(4), new Circulo(3)];

formas.forEach(forma => console.log(forma.calcularArea()));
// 16
// 28.274333882308138
```

---

## **8. Exercícios Práticos**

### **Exercício 1**
Crie uma classe `Produto` com as propriedades `nome` e `preco`. Adicione um método para aplicar desconto ao preço.

### **Exercício 2**
Implemente uma classe `Funcionario` com as propriedades `nome` e `salario`. Crie uma subclasse `Gerente` que adicione um bônus ao salário.

### **Exercício 3**
Desenvolva uma classe `Biblioteca` com métodos para adicionar e listar livros. Use encapsulamento para proteger a lista de livros.

---

## **Resumo**
- A POO organiza o código em classes e objetos.
- Utilizamos **construtores**, **propriedades** e **métodos** para definir comportamentos e estados.
- Com **herança**, reutilizamos código. Com **encapsulamento**, protegemos dados. E com **polimorfismo**, aumentamos a flexibilidade.
