# Promises

## 1. Introdução às Promises

Uma Promise é como um "recibo de uma encomenda" no JavaScript. Quando você pede algo que pode demorar para ficar pronto (como buscar dados de uma API, ler um arquivo ou processar uma imagem), você recebe imediatamente uma Promise - que é uma garantia de que você receberá uma resposta no futuro, seja ela positiva ou negativa.

### Analogia da Pizzaria
Imagine pedir uma pizza:
1. Você faz o pedido e recebe um número de protocolo (Promise)
2. A pizza está sendo preparada (Promise pendente)
3. Dois possíveis resultados:
   - A pizza fica pronta (Promise resolvida)
   - Acabou o queijo e não podem fazer sua pizza (Promise rejeitada)

```javascript
// Exemplo da Pizzaria em código
const pedirPizza = new Promise((resolve, reject) => {
    // Simulando o tempo de preparo
    setTimeout(() => {
        const temIngredientes = true;
        
        if (temIngredientes) {
            resolve("🍕 Sua pizza está pronta!");
        } else {
            reject("😢 Desculpe, acabaram os ingredientes");
        }
    }, 2000);
});

// Usando a Promise
pedirPizza
    .then(mensagem => console.log(mensagem))  // Se deu certo
    .catch(erro => console.log(erro));        // Se deu errado
```

## Por que usar Promises?

### Operações Assíncronas
JavaScript é single-thread, ou seja, executa uma coisa por vez. Promises permitem executar operações demoradas sem travar o resto do código.

```javascript
// Sem Promise (código síncrono)
console.log("Início");
const dados = buscarDadosDoBanco(); // Trava aqui até terminar
console.log("Fim");

// Com Promise (código assíncrono)
console.log("Início");
buscarDadosDoBanco()
    .then(dados => console.log(dados))
    .catch(erro => console.log(erro));
console.log("Fim"); // Executa antes dos dados chegarem
```



## Casos práticos de uso

### a. Requisições HTTP
```javascript
// Buscando dados de uma API
fetch('https://api.exemplo.com/dados')
    .then(response => response.json())
    .then(dados => console.log(dados))
    .catch(erro => console.log('Erro:', erro));
```

### b. Leitura de Arquivos
```javascript
// Em Node.js
const fs = require('fs').promises;

fs.readFile('arquivo.txt', 'utf-8')
    .then(conteudo => console.log(conteudo))
    .catch(erro => console.log('Erro na leitura:', erro));
```

### c. Temporizadores
```javascript
const esperar = (segundos) => {
    return new Promise(resolve => {
        setTimeout(resolve, segundos * 1000);
    });
}

// Uso
console.log("Início");
esperar(2)
    .then(() => console.log("Passaram-se 2 segundos"));
```

### d. Carregamento de Imagens
```javascript
function carregarImagem(url) {
    return new Promise((resolve, reject) => {
        const img = new Image();
        img.onload = () => resolve(img);
        img.onerror = () => reject(new Error('Erro ao carregar imagem'));
        img.src = url;
    });
}

// Uso
carregarImagem('foto.jpg')
    .then(img => document.body.appendChild(img))
    .catch(erro => console.log(erro));
```



### 1.1 Estados de uma Promise:
- **Pending**: Estado inicial
- **Fulfilled**: Operação concluída com sucesso
- **Rejected**: Operação falhou

## 2. Métodos .then() e .catch()

### 2.1 .then()
O método `.then()` é usado para tratar o sucesso de uma Promise.

```javascript
const minhaPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Sucesso!");
    }, 1000);
});

minhaPromise
    .then(resultado => {
        console.log(resultado); // "Sucesso!"
    });
```

### 2.2 .catch()
O método `.catch()` é usado para tratar erros.

```javascript
const minhaPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject("Algo deu errado!");
    }, 1000);
});

minhaPromise
    .then(resultado => {
        console.log(resultado);
    })
    .catch(erro => {
        console.error(erro); // "Algo deu errado!"
    });
```

## 3. Promise.all e Promise.race

### 3.1 Promise.all()
Executa múltiplas Promises em paralelo e aguarda todas serem resolvidas.

```javascript
const promise1 = Promise.resolve(3);
const promise2 = new Promise(resolve => setTimeout(() => resolve('foo'), 2000));
const promise3 = fetch('https://api.exemplo.com/dados');

Promise.all([promise1, promise2, promise3])
    .then(valores => {
        console.log(valores); // [3, "foo", Response]
    })
    .catch(erro => {
        console.error('Uma das promises falhou:', erro);
    });
```

### 3.2 Promise.race()
Retorna a primeira Promise que for resolvida ou rejeitada.

```javascript
const promise1 = new Promise(resolve => setTimeout(() => resolve('Primeiro'), 500));
const promise2 = new Promise(resolve => setTimeout(() => resolve('Segundo'), 100));

Promise.race([promise1, promise2])
    .then(resultado => {
        console.log(resultado); // "Segundo"
    });
```

## 4. Comparação com async/await

### 4.1 Usando .then()/.catch()
```javascript
function buscarDados() {
    fetch('https://api.exemplo.com/dados')
        .then(response => response.json())
        .then(dados => console.log(dados))
        .catch(erro => console.error(erro));
}
```

### 4.2 Usando async/await
```javascript
async function buscarDados() {
    try {
        const response = await fetch('https://api.exemplo.com/dados');
        const dados = await response.json();
        console.log(dados);
    } catch (erro) {
        console.error(erro);
    }
}
```

## 5. Casos de Uso

### 5.1 Carregamento Paralelo de Recursos
```javascript
async function carregarRecursos() {
    const [usuarios, produtos, pedidos] = await Promise.all([
        fetch('/api/usuarios').then(r => r.json()),
        fetch('/api/produtos').then(r => r.json()),
        fetch('/api/pedidos').then(r => r.json())
    ]);

    return { usuarios, produtos, pedidos };
}
```

### 5.2 Timeout com Promise.race()
```javascript
function fetchComTimeout(url, timeout = 5000) {
    return Promise.race([
        fetch(url),
        new Promise((_, reject) => 
            setTimeout(() => reject(new Error('Timeout')), timeout)
        )
    ]);
}
```

## 6. Exemplo Completo: Dashboard de Dados

Vamos criar um dashboard que carrega dados de diferentes APIs públicas simultaneamente.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard de Dados</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <h1 class="text-center mb-4">Dashboard de Dados</h1>
        
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Usuários</h5>
                        <div id="usuarios-container">Carregando...</div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Posts</h5>
                        <div id="posts-container">Carregando...</div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Todos</h5>
                        <div id="todos-container">Carregando...</div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="text-center mt-3">
            <button id="atualizar" class="btn btn-primary">Atualizar Dados</button>
        </div>
    </div>

    <script>
        class Dashboard {
            constructor() {
                this.baseUrl = 'https://jsonplaceholder.typicode.com';
                this.inicializar();
            }

            async inicializar() {
                this.bindElements();
                this.bindEvents();
                await this.carregarDados();
            }

            bindElements() {
                this.usuariosContainer = document.getElementById('usuarios-container');
                this.postsContainer = document.getElementById('posts-container');
                this.todosContainer = document.getElementById('todos-container');
                this.btnAtualizar = document.getElementById('atualizar');
            }

            bindEvents() {
                this.btnAtualizar.addEventListener('click', () => this.carregarDados());
            }

            async carregarDados() {
                try {
                    this.mostrarCarregando();
                    
                    const [usuarios, posts, todos] = await Promise.all([
                        fetch(`${this.baseUrl}/users`).then(r => r.json()),
                        fetch(`${this.baseUrl}/posts`).then(r => r.json()),
                        fetch(`${this.baseUrl}/todos`).then(r => r.json())
                    ]);

                    this.renderizarDados(usuarios, posts, todos);
                } catch (erro) {
                    this.mostrarErro(erro);
                }
            }

            mostrarCarregando() {
                [this.usuariosContainer, this.postsContainer, this.todosContainer]
                    .forEach(container => {
                        container.innerHTML = '<div class="spinner-border" role="status"></div>';
                    });
            }

            renderizarDados(usuarios, posts, todos) {
                this.usuariosContainer.innerHTML = `
                    <p>Total de usuários: ${usuarios.length}</p>
                    <ul class="list-group">
                        ${usuarios.slice(0, 5).map(user => 
                            `<li class="list-group-item">${user.name}</li>`
                        ).join('')}
                    </ul>
                `;

                this.postsContainer.innerHTML = `
                    <p>Total de posts: ${posts.length}</p>
                    <ul class="list-group">
                        ${posts.slice(0, 5).map(post => 
                            `<li class="list-group-item">${post.title.slice(0, 30)}...</li>`
                        ).join('')}
                    </ul>
                `;

                this.todosContainer.innerHTML = `
                    <p>Total de todos: ${todos.length}</p>
                    <ul class="list-group">
                        ${todos.slice(0, 5).map(todo => 
                            `<li class="list-group-item ${todo.completed ? 'list-group-item-success' : ''}">${todo.title.slice(0, 30)}...</li>`
                        ).join('')}
                    </ul>
                `;
            }

            mostrarErro(erro) {
                [this.usuariosContainer, this.postsContainer, this.todosContainer]
                    .forEach(container => {
                        container.innerHTML = `
                            <div class="alert alert-danger">
                                Erro ao carregar dados: ${erro.message}
                            </div>
                        `;
                    });
            }
        }

        // Inicializar o dashboard
        new Dashboard();
    </script>
</body>
</html>
```

## 7. Melhores Práticas

1. **Sempre trate erros**: Use `.catch()` ou `try/catch` com async/await.

2. **Evite Promise hell**: Prefira encadeamento ou async/await para melhor legibilidade.
```javascript
// Ruim
promise1()
    .then(valor1 => {
        promise2(valor1)
            .then(valor2 => {
                promise3(valor2)
                    .then(valor3 => {
                        // ...
                    });
            });
    });

// Bom
async function minhaFuncao() {
    const valor1 = await promise1();
    const valor2 = await promise2(valor1);
    const valor3 = await promise3(valor2);
}
```

3. **Use Promise.all() para operações paralelas**: Quando as operações não dependem uma da outra.

4. **Retorne Promises**: Ao criar funções assíncronas, retorne a Promise em vez de criar uma nova.
```javascript
// Ruim
function minhaFuncao() {
    return new Promise((resolve) => {
        fetch('/api/dados')
            .then(resolve);
    });
}

// Bom
function minhaFuncao() {
    return fetch('/api/dados');
}
```

5. **Prefira async/await para código mais limpo**: Mas conheça e entenda Promises para casos específicos.

6. **Use Promise.race() com timeout**: Para evitar operações que demoram muito.

7. **Evite .then() aninhados**: Use o encadeamento de .then() ou async/await.
