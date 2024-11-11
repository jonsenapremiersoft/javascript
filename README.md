# Introdução ao JavaScript

## História e evolução

O JavaScript foi criado em 1995 por Brendan Eich enquanto trabalhava na Netscape Communications Corporation. Originalmente chamado de Mocha e depois LiveScript, o nome JavaScript foi adotado por questões de marketing, aproveitando a popularidade da linguagem Java na época.

Pontos importantes da história:
- 1996: Padronização pela ECMA International (ECMAScript)
- 2009: ECMAScript 5 (ES5) trouxe importantes atualizações
- 2015: ECMAScript 2015 (ES6) revolucionou a linguagem com novas funcionalidades
- Atualizações anuais desde então, trazendo melhorias constantes

Hoje, o JavaScript é uma das linguagens mais populares do mundo, sendo fundamental para:
- Desenvolvimento web front-end
- Desenvolvimento back-end (Node.js)
- Desenvolvimento mobile (React Native, Ionic)
- Desenvolvimento desktop (Electron)

## Engine JavaScript

A Engine JavaScript é o programa que interpreta e executa o código JavaScript. Cada navegador tem sua própria engine:

- V8: Utilizada pelo Google Chrome e Node.js
- SpiderMonkey: Utilizada pelo Firefox
- JavaScriptCore: Utilizada pelo Safari
- Chakra: Utilizada pelo Internet Explorer e Edge (versões antigas)

### Como funciona a Engine

1. Parsing:
   - O código é analisado e transformado em uma árvore de sintaxe abstrata (AST)
   - Verifica erros de sintaxe

2. Compilação:
   - O código é compilado para bytecode
   - Otimizações são aplicadas

3. Execução:
   - O bytecode é executado
   - Gerenciamento de memória (Garbage Collection)
   - Just-In-Time (JIT) compilation para código de máquina

## JavaScript in-browser: Capacidades e Limitações

### O que pode fazer:
- Manipular o DOM (HTML e CSS)
- Fazer requisições HTTP (AJAX/Fetch)
- Armazenar dados localmente (localStorage/sessionStorage)
- Manipular cookies
- Acesso a APIs do navegador:
  - Geolocalização
  - Web Audio
  - Canvas
  - WebGL
  - Web Storage
  - Web Workers

### O que não pode fazer:
- Acessar arquivos do sistema diretamente
- Acessar hardware do computador
- Executar programas nativos
- Modificar configurações do navegador
- Acessar outros domínios sem permissão (Same-origin policy)

## Diferenciais do JavaScript

1. Versatilidade:
   - Única linguagem que roda nativamente em todos os navegadores
   - Pode ser usada em todas as camadas de desenvolvimento (full-stack)
   - Grande variedade de frameworks e bibliotecas

2. Assíncrono por natureza:
   - Event Loop
   - Promises
   - Async/Await
   - Callbacks

3. Tipagem dinâmica e flexível:
   - Tipos de dados são determinados em tempo de execução
   - Conversão automática de tipos
   - Prototypal inheritance

4. Comunidade ativa:
   - Maior repositório de pacotes (npm)
   - Abundância de recursos e documentação
   - Constante evolução

## Principais Casos de Uso

1. Desenvolvimento Web Front-end:
   - Interatividade em páginas web
   - Single Page Applications (SPA)
   - Validação de formulários
   - Animações e efeitos visuais

2. Desenvolvimento Back-end (Node.js):
   - APIs RESTful
   - Microserviços
   - Servidores em tempo real
   - Ferramentas de linha de comando

3. Desenvolvimento Mobile:
   - Aplicativos híbridos
   - PWAs (Progressive Web Apps)
   - React Native
   - Ionic

4. Desenvolvimento Desktop:
   - Electron
   - NW.js

5. Internet das Coisas (IoT):
   - Johnny-Five
   - Node-RED


## Configuração do Ambiente

Para começar a programar em JavaScript, você precisa de:

1. Um editor de código
   - Visual Studio Code (recomendado)
   - Sublime Text
   - Atom

2. Um navegador moderno
   - Google Chrome (recomendado)
   - Mozilla Firefox
   - Microsoft Edge

3. Node.js (opcional, mas recomendado)
   - Baixe em: nodejs.org
   - Permite executar JavaScript fora do navegador

### Configurando o VS Code
1. Baixe e instale o VS Code
2. Instale extensões recomendadas:
   - Live Server
   - JavaScript (ES6) code snippets
   - ESLint
   - Prettier

## Console e Ferramentas do Desenvolvedor

### Abrindo o Console
- Chrome/Edge: F12 ou Ctrl + Shift + I
- Firefox: F12 ou Ctrl + Shift + K
- Mac: Cmd + Option + I

### Principais recursos do Console:
```javascript
// Imprimindo mensagens
console.log("Mensagem básica");
console.info("Informação");
console.warn("Aviso");
console.error("Erro");

// Agrupando mensagens
console.group("Grupo de logs");
console.log("Log 1");
console.log("Log 2");
console.groupEnd();

// Medindo tempo
console.time("Timer");
// ... código ...
console.timeEnd("Timer");

// Criando tabelas
console.table(["Item 1", "Item 2", "Item 3"]);
```

### Outras ferramentas do desenvolvedor:
1. Elements: Inspeção e manipulação do HTML/CSS
2. Sources: Debugger e arquivos fonte
3. Network: Monitoramento de requisições
4. Application: Armazenamento local e recursos
5. Performance: Análise de desempenho
6. Memory: Gerenciamento de memória

### Primeiro código
```javascript
// Crie um arquivo index.html
<!DOCTYPE html>
<html>
<head>
    <title>Primeira Página JavaScript</title>
</head>
<body>
    <h1>Olá, JavaScript!</h1>
    <script>
        console.log("Meu primeiro código JavaScript!");
        alert("Bem-vindo ao JavaScript!");
    </script>
</body>
</html>
```

### Executando JavaScript em arquivo separado
```javascript
// arquivo: script.js
console.log("JavaScript em arquivo separado!");

// arquivo: index.html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Externo</title>
</head>
<body>
    <h1>JavaScript em arquivo separado</h1>
    <script src="script.js"></script>
</body>
</html>
```




## Configurando o Prettier

O Prettier é uma ferramenta de formatação de código que ajuda a manter um estilo consistente em todo o projeto. Ele reformata automaticamente o código seguindo regras predefinidas.

### Instalação
```bash
# Instalação local no projeto
npm install --save-dev prettier

# Ou globalmente
npm install -g prettier
```

### Configuração
Crie um arquivo `.prettierrc` na raiz do projeto:

```json
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "printWidth": 80,
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "auto",
  "bracketSameLine": false,
  "jsxSingleQuote": false
}
```

Explicação das configurações:
- `trailingComma`: Adiciona vírgula no último item de objetos/arrays
- `tabWidth`: Define o tamanho da indentação
- `semi`: Adiciona ponto e vírgula no final das declarações
- `singleQuote`: Usa aspas simples em vez de duplas
- `printWidth`: Comprimento máximo da linha
- `bracketSpacing`: Espaços entre chaves em objetos literais
- `arrowParens`: Parênteses em arrow functions com um único parâmetro
- `endOfLine`: Tipo de quebra de linha
- `bracketSameLine`: Coloca a > do JSX na próxima linha
- `jsxSingleQuote`: Tipo de aspas em atributos JSX

### Ignorando Arquivos
Crie um arquivo `.prettierignore`:
```
# Arquivos e diretórios ignorados pelo Prettier
node_modules
dist
build
coverage
*.min.js
```

### Integração com VS Code
1. Instale a extensão "Prettier - Code formatter"
2. Configure o VS Code para formatar ao salvar:
```json
// settings.json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```
