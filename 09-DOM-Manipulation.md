# Manipulação do DOM

## Introdução
O DOM (Document Object Model) é uma interface que representa documentos HTML e XML como uma estrutura em árvore, onde cada elemento é um nó. Através do JavaScript, podemos manipular essa estrutura de forma dinâmica, alterando conteúdo, estilo e estrutura da página.

## 1. Seletores
Os seletores nos permitem encontrar e selecionar elementos HTML no documento.

### Métodos principais:
```javascript
// Selecionar por ID
const elemento = document.getElementById('meuId');

// Selecionar por classe
const elementos = document.getElementsByClassName('minhaClasse');

// Selecionar por tag
const paragrafos = document.getElementsByTagName('p');

// Seletor CSS (retorna primeiro elemento)
const primeiroElemento = document.querySelector('.minhaClasse');

// Seletor CSS (retorna todos os elementos)
const todosElementos = document.querySelectorAll('.minhaClasse');
```

### Exemplo prático:
```javascript
// HTML:
// <div id="usuario" class="card">
//   <h2>João Silva</h2>
//   <p class="email">joao@email.com</p>
// </div>

const cartao = document.getElementById('usuario');
const email = document.querySelector('.email');
console.log(email.textContent); // joao@email.com
```

## 2. Criação e Remoção de Elementos

### Criando elementos:
```javascript
// Criar novo elemento
const novoParagrafo = document.createElement('p');

// Adicionar texto ao elemento
novoParagrafo.textContent = 'Novo parágrafo';

// Adicionar elemento ao DOM
document.body.appendChild(novoParagrafo);
```

### Removendo elementos:
```javascript
// Remover elemento
elemento.remove();

// Remover elemento filho
pai.removeChild(filho);
```

### Exemplo prático - Lista de tarefas:
```javascript
function adicionarTarefa(texto) {
    const lista = document.getElementById('listaTarefas');
    const novaTarefa = document.createElement('li');
    novaTarefa.textContent = texto;
    
    const botaoRemover = document.createElement('button');
    botaoRemover.textContent = 'Remover';
    botaoRemover.onclick = () => novaTarefa.remove();
    
    novaTarefa.appendChild(botaoRemover);
    lista.appendChild(novaTarefa);
}
```

## 3. Modificação de Conteúdo e Atributos

### Modificando conteúdo:
```javascript
// Modificar texto
elemento.textContent = 'Novo texto';

// Modificar HTML
elemento.innerHTML = '<strong>Texto em negrito</strong>';
```

### Modificando atributos:
```javascript
// Definir atributo
elemento.setAttribute('class', 'novaClasse');

// Obter valor do atributo
const valor = elemento.getAttribute('class');

// Remover atributo
elemento.removeAttribute('class');

// Trabalhar com classes
elemento.classList.add('novaClasse');
elemento.classList.remove('velhaClasse');
elemento.classList.toggle('ativar');
```

### Exemplo prático - Toggle tema escuro:
```javascript
function toggleTemaEscuro() {
    const body = document.body;
    body.classList.toggle('tema-escuro');
    
    const botao = document.getElementById('botaoTema');
    const estaEscuro = body.classList.contains('tema-escuro');
    botao.textContent = estaEscuro ? 'Modo Claro' : 'Modo Escuro';
}
```

## 4. Navegação no DOM

### Relações entre elementos:
```javascript
// Elemento pai
const pai = elemento.parentElement;

// Elementos filhos
const filhos = elemento.children;
const primeiroFilho = elemento.firstElementChild;
const ultimoFilho = elemento.lastElementChild;

// Elementos irmãos
const proximoIrmao = elemento.nextElementSibling;
const irmaoAnterior = elemento.previousElementSibling;
```

### Exemplo prático - Navegação em árvore:
```javascript
function mostrarCaminhoAteRaiz(elemento) {
    let caminho = [];
    let atual = elemento;
    
    while (atual !== null) {
        caminho.push(atual.tagName);
        atual = atual.parentElement;
    }
    
    return caminho.join(' > ');
}
```

## Exercícios Práticos

1. **Lista de Contatos**
Crie uma aplicação que permita:
- Adicionar novos contatos (nome e email)
- Remover contatos existentes
- Marcar contatos como favoritos
- Filtrar contatos por nome

2. **Editor de Notas**
Desenvolva um editor que permita:
- Criar notas com título e conteúdo
- Formatar texto (negrito, itálico)
- Mudar cor do texto
- Salvar e excluir notas

3. **Menu Dinâmico**
Implemente um menu que:
- Expanda/recolha submenus ao clicar
- Destaque item atual
- Adicione/remova itens dinamicamente
- Salve estado de expansão

### Exemplo de solução para o exercício 1:
```javascript
// HTML:
// <div id="app">
//   <input id="nome" placeholder="Nome">
//   <input id="email" placeholder="Email">
//   <button onclick="adicionarContato()">Adicionar</button>
//   <ul id="listaContatos"></ul>
// </div>

function adicionarContato() {
    const nome = document.getElementById('nome').value;
    const email = document.getElementById('email').value;
    
    if (!nome || !email) return;
    
    const lista = document.getElementById('listaContatos');
    const contato = document.createElement('li');
    
    contato.innerHTML = `
        <span>${nome} (${email})</span>
        <button onclick="this.parentElement.classList.toggle('favorito')">
            ★
        </button>
        <button onclick="this.parentElement.remove()">
            Excluir
        </button>
    `;
    
    lista.appendChild(contato);
    
    // Limpar campos
    document.getElementById('nome').value = '';
    document.getElementById('email').value = '';
}
```

## Dicas Importantes:
1. Use `querySelector` e `querySelectorAll` para seletores mais complexos
2. Prefira `textContent` a `innerHTML` quando não precisar inserir HTML
3. Considere performance ao manipular muitos elementos
4. Use delegação de eventos para listas dinâmicas
5. Mantenha referências a elementos frequentemente acessados
