# Web Storage em JavaScript: localStorage e sessionStorage

## Introdução
O Web Storage é uma API do HTML5 que permite armazenar dados no navegador do usuário de forma mais organizada e eficiente que os cookies. Existem dois mecanismos principais:
- **localStorage**: armazena dados sem data de expiração
- **sessionStorage**: mantém dados apenas durante a sessão do navegador

## Por que usar Web Storage?
- Armazenamento local de preferências do usuário
- Dados de formulários não enviados
- Histórico de ações do usuário
- Cache de dados para melhor performance
- Estado da aplicação

## localStorage vs sessionStorage

### localStorage
- Persiste mesmo após fechar o navegador
- Compartilhado entre todas as abas/janelas do mesmo domínio
- Limite de armazenamento maior (geralmente 5-10MB)
- Ideal para: preferências do usuário, dados de login, temas, configurações

### sessionStorage
- Dados disponíveis apenas durante a sessão
- Isolado por aba/janela do navegador
- Mesmo limite de armazenamento que localStorage
- Ideal para: dados temporários, estado de formulários, dados sensíveis temporários

## Métodos Principais

```javascript
// Armazenar dados
localStorage.setItem('chave', 'valor');
sessionStorage.setItem('chave', 'valor');

// Recuperar dados
const valor = localStorage.getItem('chave');
const valor = sessionStorage.getItem('chave');

// Remover item específico
localStorage.removeItem('chave');
sessionStorage.removeItem('chave');

// Limpar todo o storage
localStorage.clear();
sessionStorage.clear();

// Verificar quantidade de itens
localStorage.length;
sessionStorage.length;
```

## Exemplos Práticos

### 1. Tema Dark/Light
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Exemplo Tema Dark/Light</title>
    <style>
        .light {
            background-color: #fff;
            color: #333;
        }
        .dark {
            background-color: #333;
            color: #fff;
        }
        .container {
            padding: 20px;
            text-align: center;
        }
    </style>
</head>
<body class="light">
    <div class="container">
        <h1>Exemplo de Tema</h1>
        <button onclick="alternarTema()">Alternar Tema</button>
    </div>

    <script>
        function alternarTema() {
            const temaAtual = localStorage.getItem('tema') || 'light';
            const novoTema = temaAtual === 'light' ? 'dark' : 'light';
            
            localStorage.setItem('tema', novoTema);
            aplicarTema();
        }

        function aplicarTema() {
            const tema = localStorage.getItem('tema') || 'light';
            document.body.className = tema;
        }

        // Aplicar tema ao carregar a página
        aplicarTema();
    </script>
</body>
</html>
```

### 2. Carrinho de Compras
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Carrinho de Compras</title>
    <style>
        .container { padding: 20px; }
        .produto { margin: 10px 0; }
        #carrinho { margin-top: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Carrinho de Compras</h1>
        
        <div class="produto">
            <h3>Produto 1 - R$ 50,00</h3>
            <button onclick="adicionarAoCarrinho({id: 1, nome: 'Produto 1', preco: 50})">
                Adicionar ao Carrinho
            </button>
        </div>

        <div class="produto">
            <h3>Produto 2 - R$ 30,00</h3>
            <button onclick="adicionarAoCarrinho({id: 2, nome: 'Produto 2', preco: 30})">
                Adicionar ao Carrinho
            </button>
        </div>

        <div id="carrinho">
            <h2>Seu Carrinho</h2>
            <ul id="lista-carrinho"></ul>
            <p>Total: R$ <span id="total">0,00</span></p>
            <button onclick="limparCarrinho()">Limpar Carrinho</button>
        </div>
    </div>

    <script>
        function adicionarAoCarrinho(produto) {
            let carrinho = JSON.parse(sessionStorage.getItem('carrinho')) || [];
            carrinho.push(produto);
            sessionStorage.setItem('carrinho', JSON.stringify(carrinho));
            atualizarCarrinho();
        }

        function limparCarrinho() {
            sessionStorage.removeItem('carrinho');
            atualizarCarrinho();
        }

        function atualizarCarrinho() {
            const carrinho = JSON.parse(sessionStorage.getItem('carrinho')) || [];
            const listaEl = document.getElementById('lista-carrinho');
            const totalEl = document.getElementById('total');
            
            listaEl.innerHTML = '';
            let total = 0;

            carrinho.forEach(produto => {
                const li = document.createElement('li');
                li.textContent = `${produto.nome} - R$ ${produto.preco},00`;
                listaEl.appendChild(li);
                total += produto.preco;
            });

            totalEl.textContent = total.toFixed(2);
        }

        // Atualizar carrinho ao carregar a página
        atualizarCarrinho();
    </script>
</body>
</html>
```

### 3. Formulário com Auto-save
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Formulário com Auto-save</title>
    <style>
        .form-group { margin: 15px 0; }
        .form-group label { display: block; margin-bottom: 5px; }
        .form-group input, .form-group textarea {
            width: 100%;
            max-width: 300px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Formulário com Auto-save</h1>
        <form id="meuForm" onsubmit="enviarFormulario(event)">
            <div class="form-group">
                <label for="nome">Nome:</label>
                <input type="text" id="nome" onchange="salvarProgresso(event)">
            </div>

            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" id="email" onchange="salvarProgresso(event)">
            </div>

            <div class="form-group">
                <label for="mensagem">Mensagem:</label>
                <textarea id="mensagem" onchange="salvarProgresso(event)"></textarea>
            </div>

            <button type="submit">Enviar</button>
            <button type="button" onclick="limparFormulario()">Limpar</button>
        </form>
    </div>

    <script>
        function salvarProgresso(evento) {
            const campo = evento.target;
            sessionStorage.setItem(`form_${campo.id}`, campo.value);
        }

        function recuperarProgresso() {
            const campos = document.querySelectorAll('input, textarea');
            campos.forEach(campo => {
                const valorSalvo = sessionStorage.getItem(`form_${campo.id}`);
                if (valorSalvo) campo.value = valorSalvo;
            });
        }

        function limparFormulario() {
            document.getElementById('meuForm').reset();
            Object.keys(sessionStorage).forEach(key => {
                if (key.startsWith('form_')) {
                    sessionStorage.removeItem(key);
                }
            });
        }

        function enviarFormulario(evento) {
            evento.preventDefault();
            alert('Formulário enviado!');
            limparFormulario();
        }

        // Recuperar dados ao carregar a página
        recuperarProgresso();
    </script>
</body>
</html>
```

## Casos de Uso Reais

1. **E-commerce**
   - Carrinho de compras temporário (sessionStorage)
   - Lista de desejos persistente (localStorage)
   - Últimos produtos vistos (localStorage)

2. **Blog/Portal de Notícias**
   - Preferências de visualização (localStorage)
   - Histórico de artigos lidos (localStorage)
   - Rascunhos de comentários (sessionStorage)

3. **Aplicativo de Tarefas**
   - Lista de tarefas offline (localStorage)
   - Filtros e ordenação (localStorage)
   - Estado atual da edição (sessionStorage)

## Boas Práticas

1. **Sempre verifique o suporte**
```javascript
if (typeof(Storage) !== "undefined") {
    // Código usando Web Storage
} else {
    // Fallback
}
```

2. **Trate erros de quota excedida**
```javascript
try {
    localStorage.setItem('chave', 'valor');
} catch (e) {
    if (e.name === 'QuotaExceededError') {
        alert('Storage cheio! Libere espaço para continuar.');
    }
}
```

3. **Use JSON para objetos complexos**
```javascript
const usuario = {
    nome: 'João',
    idade: 25,
    preferencias: ['música', 'esportes']
};

localStorage.setItem('usuario', JSON.stringify(usuario));
const usuarioSalvo = JSON.parse(localStorage.getItem('usuario'));
```



## Recursos Adicionais
- [MDN Web Storage API](https://developer.mozilla.org/pt-BR/docs/Web/API/Web_Storage_API)
- [Can I Use - Web Storage](https://caniuse.com/?search=webstorage)
- [W3Schools - Web Storage API](https://www.w3schools.com/html/html5_webstorage.asp)
