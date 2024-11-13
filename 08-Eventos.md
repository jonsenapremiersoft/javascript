# Eventos

## 1. Introdução aos Eventos

Os eventos são ações ou ocorrências que acontecem em um sistema web, seja por interação do usuário (como cliques ou digitação) ou por mudanças no estado do navegador (como o carregamento da página). Eles são fundamentais para criar aplicações web interativas e responsivas.

### Por que eventos são importantes?

- **Interatividade**: Permitem que sua aplicação responda às ações do usuário em tempo real
- **Experiência do Usuário**: Criam interfaces mais naturais e intuitivas
- **Dinamismo**: Possibilitam atualizar conteúdo sem recarregar a página
- **Feedback**: Permitem informar o usuário sobre o resultado de suas ações

## 2. Tipos de Eventos

### 2.1 Eventos de Mouse

Eventos que ocorrem quando o usuário interage com o mouse:

- `click`: Disparado quando um elemento é clicado (pressionar e soltar o botão do mouse)
- `dblclick`: Ocorre após dois cliques rápidos consecutivos
- `mouseenter`: Disparado quando o cursor do mouse entra na área do elemento
- `mouseleave`: Ocorre quando o cursor sai da área do elemento
- `mousemove`: Ativado continuamente enquanto o mouse se move sobre o elemento
- `mousedown`: Ocorre no momento em que o botão do mouse é pressionado
- `mouseup`: Disparado quando o botão do mouse é solto

Exemplo prático de diferentes eventos de mouse:

```html
<div id="mouse-events" style="width: 200px; height: 200px; background: #f0f0f0;">
    Área de teste de eventos do mouse
</div>

<div id="log"></div>
```

```javascript
const mouseArea = document.getElementById('mouse-events');
const log = document.getElementById('log');

function logEvent(eventName) {
    log.innerHTML = `Último evento: ${eventName} - ${new Date().toLocaleTimeString()}`;
}

// Registrando diferentes eventos de mouse
mouseArea.addEventListener('click', () => logEvent('click'));
mouseArea.addEventListener('dblclick', () => logEvent('dblclick'));
mouseArea.addEventListener('mouseenter', () => logEvent('mouseenter'));
mouseArea.addEventListener('mouseleave', () => logEvent('mouseleave'));
mouseArea.addEventListener('mousemove', () => logEvent('mousemove'));
mouseArea.addEventListener('mousedown', () => logEvent('mousedown'));
mouseArea.addEventListener('mouseup', () => logEvent('mouseup'));
```

### 2.2 Eventos de Teclado

Eventos disparados quando o usuário interage com o teclado:

- `keydown`: Ocorre quando uma tecla é pressionada
- `keyup`: Disparado quando uma tecla é solta
- `keypress`: Ocorre quando uma tecla que produz um caractere é pressionada (deprecated)

Exemplo de monitoramento de teclas:

```html
<input type="text" id="keyboard-input" placeholder="Digite algo aqui">
<div id="key-log"></div>
```

```javascript
const input = document.getElementById('keyboard-input');
const keyLog = document.getElementById('key-log');

input.addEventListener('keydown', (event) => {
    keyLog.innerHTML = `
        Tecla: ${event.key}<br>
        Código: ${event.code}<br>
        Ctrl pressionado: ${event.ctrlKey}<br>
        Shift pressionado: ${event.shiftKey}<br>
        Alt pressionado: ${event.altKey}
    `;
});
```

### 2.3 Eventos de Formulário

Eventos relacionados à interação com formulários:

- `submit`: Disparado quando um formulário é enviado
- `reset`: Ocorre quando o formulário é resetado
- `change`: Ativado quando o valor de um campo muda e perde o foco
- `focus`: Ocorre quando um elemento recebe foco
- `blur`: Disparado quando um elemento perde o foco

Exemplo completo de formulário com diferentes eventos:

```html
<form id="user-form">
    <div>
        <label for="name">Nome:</label>
        <input type="text" id="name" required>
    </div>
    <div>
        <label for="email">Email:</label>
        <input type="email" id="email" required>
    </div>
    <div>
        <label for="age">Idade:</label>
        <input type="number" id="age" min="0" max="150">
    </div>
    <button type="submit">Enviar</button>
    <button type="reset">Limpar</button>
</form>

<div id="form-log"></div>
```

```javascript
const form = document.getElementById('user-form');
const formLog = document.getElementById('form-log');
const nameInput = document.getElementById('name');
const emailInput = document.getElementById('email');
const ageInput = document.getElementById('age');

function logFormEvent(event, message) {
    const time = new Date().toLocaleTimeString();
    formLog.innerHTML += `<div>${time}: ${event} - ${message}</div>`;
}

// Eventos do formulário
form.addEventListener('submit', (e) => {
    e.preventDefault();
    logFormEvent('submit', 'Formulário enviado!');
});

form.addEventListener('reset', () => {
    logFormEvent('reset', 'Formulário resetado!');
});

// Eventos dos campos
nameInput.addEventListener('focus', () => {
    logFormEvent('focus', 'Campo nome focado');
});

nameInput.addEventListener('blur', () => {
    logFormEvent('blur', 'Campo nome perdeu foco');
});

emailInput.addEventListener('change', (e) => {
    logFormEvent('change', `Email alterado para: ${e.target.value}`);
});

// Validação em tempo real
ageInput.addEventListener('input', (e) => {
    const age = e.target.value;
    if (age < 0 || age > 150) {
        ageInput.setCustomValidity('Idade deve estar entre 0 e 150');
    } else {
        ageInput.setCustomValidity('');
    }
});
```

### 2.4 Eventos de Documento/Janela

Eventos relacionados ao documento HTML e à janela do navegador:

- `load`: Disparado quando a página e todos seus recursos terminam de carregar
- `DOMContentLoaded`: Ocorre quando o HTML é totalmente carregado, sem esperar por CSS, imagens etc.
- `resize`: Ativado quando a janela é redimensionada
- `scroll`: Ocorre quando a página ou elemento é rolado

Exemplo prático:

```html
<div id="scroll-area" style="height: 2000px;">
    <div id="scroll-indicator" style="position: fixed; top: 10px; right: 10px;">
        Scroll: 0%
    </div>
</div>
```

```javascript
const scrollIndicator = document.getElementById('scroll-indicator');

// Monitorando carregamento
document.addEventListener('DOMContentLoaded', () => {
    console.log('DOM carregado!');
});

window.addEventListener('load', () => {
    console.log('Página totalmente carregada!');
});

// Monitorando scroll
window.addEventListener('scroll', () => {
    const maxScroll = document.documentElement.scrollHeight - window.innerHeight;
    const currentScroll = window.scrollY;
    const scrollPercentage = (currentScroll / maxScroll * 100).toFixed(0);
    scrollIndicator.textContent = `Scroll: ${scrollPercentage}%`;
});

// Monitorando redimensionamento
window.addEventListener('resize', () => {
    console.log(`Nova dimensão: ${window.innerWidth}x${window.innerHeight}`);
});
```

## 3. Event Handlers

Existem três maneiras de adicionar event handlers (manipuladores de eventos) em JavaScript. Cada uma tem seus próprios benefícios e limitações:

### 3.1 Atributo HTML (não recomendado)
Esta é a forma mais antiga e menos flexível. O código JavaScript é misturado com HTML, o que não é uma boa prática.

```html
<button onclick="handleClick()">Clique Aqui</button>

<script>
function handleClick() {
    alert('Botão clicado!');
}
</script>
```

### 3.2 Propriedade do DOM
Melhor que a primeira opção, mas ainda tem limitações, como não poder ter múltiplos handlers para o mesmo evento.

```html
<button id="myButton">Clique Aqui</button>

<script>
const btn = document.getElementById('myButton');
btn.onclick = function() {
    alert('Botão clicado!');
};
</script>
```

### 3.3 addEventListener (método recomendado)
A forma mais moderna e flexível de adicionar event listeners.

```html
<button id="myButton">Clique Aqui</button>

<script>
const btn = document.getElementById('myButton');

// Podemos adicionar múltiplos handlers
btn.addEventListener('click', function(event) {
    console.log('Primeiro handler:', event);
});

btn.addEventListener('click', function(event) {
    console.log('Segundo handler:', event);
});

// Podemos remover handlers quando necessário
function temporaryHandler() {
    console.log('Este handler será removido em 5 segundos');
}

btn.addEventListener('click', temporaryHandler);

setTimeout(() => {
    btn.removeEventListener('click', temporaryHandler);
    console.log('Handler removido!');
}, 5000);
</script>
```

## 4. Event Bubbling e Capturing

### 4.1 Event Bubbling (Borbulhamento)
É o processo onde um evento dispara primeiro no elemento mais interno e depois "borbulha" até os elementos pai.

```html
<div id="avo" style="padding: 20px; background: #f0f0f0;">
    Avô
    <div id="pai" style="padding: 20px; background: #e0e0e0;">
        Pai
        <div id="filho" style="padding: 20px; background: #d0d0d0;">
            Filho
        </div>
    </div>
</div>

<div id="log"></div>
```

```javascript
const log = document.getElementById('log');

function logEvent(elemento, fase) {
    log.innerHTML += `<div>Elemento: ${elemento} - Fase: ${fase}</div>`;
}

// Demonstração de Bubbling (terceiro parâmetro false ou omitido)
document.getElementById('filho').addEventListener('click', function() {
    logEvent('Filho', 'Bubbling');
});

document.getElementById('pai').addEventListener('click', function() {
    logEvent('Pai', 'Bubbling');
});

document.getElementById('avo').addEventListener('click', function() {
    logEvent('Avô', 'Bubbling');
});
```

### 4.2 Event Capturing
É o processo oposto ao bubbling, onde o evento é primeiro capturado pelo elemento mais externo e depois desce até o elemento alvo.

```javascript
// Demonstração de Capturing (terceiro parâmetro true)
document.getElementById('avo').addEventListener('click', function() {
    logEvent('Avô', 'Capturing');
}, true);

document.getElementById('pai').addEventListener('click', function() {
    logEvent('Pai', 'Capturing');
}, true);

document.getElementById('filho').addEventListener('click', function() {
    logEvent('Filho', 'Capturing');
}, true);
```

## 5. Event Delegation

Event delegation é uma técnica onde, em vez de adicionar event listeners a cada elemento filho, adicionamos um único listener ao elemento pai. Isso é possível graças ao bubbling dos eventos.

Exemplo completo de uma lista de tarefas usando event delegation:

```html
<div id="todo-app">
    <input type="text" id="new-task" placeholder="Nova tarefa">
    <button id="add-task">Adicionar</button>
    
    <ul id="task-list">
        <li>
            Tarefa 1
            <button class="delete">X</button>
            <button class="edit">✎</button>
        </li>
        <li>
            Tarefa 2
            <button class="delete">X</button>
            <button class="edit">✎</button>
        </li>
    </ul>
</div>

<style>
.completed {
    text-decoration: line-through;
    color: #888;
}
.delete, .edit {
    margin-left: 10px;
    padding: 2px 5px;
}
</style>
```

```javascript
const todoApp = document.getElementById('todo-app');
const newTask = document.getElementById('new-task');
const taskList = document.getElementById('task-list');

// Adicionar tarefa
document.getElementById('add-task').addEventListener('click', function() {
    if (newTask.value.trim() === '') return;
    
    const li = document.createElement('li');
    li.innerHTML = `
        ${newTask.value}
        <button class="delete">X</button>
        <button class="edit">✎</button>
    `;
    taskList.appendChild(li);
    newTask.value = '';
});

// Event delegation para toda a lista
taskList.addEventListener('click', function(e) {
    const target = e.target;
    
    // Clique no item da lista
    if (target.tagName === 'LI') {
        target.classList.toggle('completed');
    }
    // Clique no botão deletar
    else if (target.classList.contains('delete')) {
        target.parentElement.remove();
    }
    // Clique no botão editar
    else if (target.classList.contains('edit')) {
        const li = target.parentElement;
        const currentText = li.firstChild.textContent.trim();
        const newText = prompt('Editar tarefa:', currentText);
        
        if (newText !== null && newText.trim() !== '') {
            li.firstChild.textContent = newText;
        }
    }
});

// Demonstração de por que event delegation é melhor
console.log('Número de event listeners sem delegation:', document.querySelectorAll('li').length);
console.log('Número de event listeners com delegation: 1');
```
