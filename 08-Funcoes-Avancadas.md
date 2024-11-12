# Funções Avançadas

## 1. Arrow Functions
As arrow functions são uma forma moderna e mais concisa de escrever funções em JavaScript, introduzida no ES6. Elas não só tornam o código mais limpo, mas também têm comportamentos específicos que as tornam ideais para certas situações.

### Sintaxe Básica
```javascript
// Função tradicional
function soma(a, b) {
    return a + b;
}

// Arrow function equivalente
const soma = (a, b) => a + b;
```

### Casos de Uso Práticos
Imagine que você está desenvolvendo um e-commerce e precisa filtrar produtos:

```javascript
const produtos = [
    { nome: 'Notebook', preco: 3000 },
    { nome: 'Smartphone', preco: 1500 },
    { nome: 'Tablet', preco: 800 }
];

// Usando arrow function para filtrar produtos
const produtosCaros = produtos.filter(produto => produto.preco > 1000);

// Usando arrow function para formatar preços
const precosFormatados = produtos.map(produto => `R$ ${produto.preco},00`);
```

### Vantagens
- Código mais conciso
- Melhor legibilidade em funções de callback
- Não possui seu próprio 'this' (herda do contexto pai)

## 2. Callbacks
Callbacks são funções passadas como argumentos para outras funções. Elas são fundamentais para programação assíncrona e manipulação de eventos.

### Exemplo Prático - Sistema de Notificações
Imagine um sistema de notificações para um aplicativo de delivery:

```javascript
function prepararPedido(numeroPedido, callback) {
    console.log(`Preparando pedido #${numeroPedido}`);
    
    // Simulando tempo de preparo
    setTimeout(() => {
        const pedido = {
            numero: numeroPedido,
            status: 'pronto'
        };
        callback(pedido);
    }, 3000);
}

function notificarCliente(pedido) {
    console.log(`🔔 Pedido #${pedido.numero} está ${pedido.status}!`);
}

// Usando o callback
prepararPedido(123, notificarCliente);
```

### Uso Comum de Callbacks
- Manipulação de eventos de clique
- Requisições AJAX
- Operações assíncronas
- Processamento de arrays (map, filter, reduce)

## 3. Closures
Closures são funções que "lembram" o ambiente em que foram criadas, mantendo acesso às variáveis desse ambiente mesmo após sua execução.

### Exemplo Prático - Contador de Visitas
```javascript
function criarContadorVisitas() {
    let visitas = 0;
    
    return {
        registrarVisita: function() {
            visitas++;
            return visitas;
        },
        obterTotalVisitas: function() {
            return visitas;
        }
    };
}

const contadorBlog = criarContadorVisitas();
console.log(contadorBlog.registrarVisita()); // 1
console.log(contadorBlog.registrarVisita()); // 2
console.log(contadorBlog.obterTotalVisitas()); // 2
```

### Aplicações Práticas de Closures
- Encapsulamento de dados
- Funções de fábrica
- Memoização (cache de resultados)
- Módulos privados

## 4. This Keyword
A palavra-chave 'this' refere-se ao objeto que está executando a função atual. Seu valor pode mudar dependendo do contexto de execução.

### Contextos Comuns do 'this'

1. **Método de Objeto**
```javascript
const usuario = {
    nome: 'João',
    idade: 25,
    apresentar() {
        console.log(`Olá, eu sou ${this.nome} e tenho ${this.idade} anos`);
    }
};

usuario.apresentar(); // this refere-se ao objeto usuario
```

2. **Eventos DOM**
```javascript
class CarrinhoCompras {
    constructor() {
        this.itens = [];
        
        // Usando arrow function para manter o this
        document.getElementById('btnAdicionar').addEventListener('click', () => {
            this.adicionarItem('Produto');
        });
    }
    
    adicionarItem(produto) {
        this.itens.push(produto);
        console.log('Item adicionado ao carrinho');
    }
}
```

### Dicas para Usar o 'this'
- Use arrow functions quando quiser preservar o this do contexto externo
- Em métodos de objetos, use funções regulares para acessar o objeto atual
- Em event handlers, bind o this ou use arrow functions
- Em classes, os métodos regulares mantêm o this referenciando a instância

### Exemplo Prático - Sistema de Perfil
```javascript
class PerfilUsuario {
    constructor(nome) {
        this.nome = nome;
        this.posts = [];
        
        // Arrow function mantém o this corretamente
        this.publicarPost = () => {
            this.posts.push(`Post de ${this.nome}`);
        };
    }
    
    // Método regular da classe
    listarPosts() {
        return this.posts.map(post => `- ${post}`).join('\n');
    }
}

const perfil = new PerfilUsuario('Maria');
perfil.publicarPost();
console.log(perfil.listarPosts());
```

## Exercícios Práticos Sugeridos

1. Crie um sistema de carrinho de compras usando closures para manter o estado dos itens
2. Implemente um debounce function para otimizar chamadas de API
3. Desenvolva um sistema de eventos personalizado usando callbacks
4. Crie uma classe de reprodutor de mídia usando this e arrow functions

## Dicas de Boas Práticas

1. Use arrow functions para callbacks curtos e quando precisar manter o this
2. Evite callbacks aninhados (callback hell) - prefira Promises ou async/await
3. Use closures para encapsulamento de dados privados
4. Seja consistente com o uso de this - use bind, arrow functions ou métodos de classe conforme apropriado
