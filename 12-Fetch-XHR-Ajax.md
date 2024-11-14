# Requisições HTTP, Ajax, XHR

## 1. Métodos HTTP: Os métodos HTTP são as ações que podemos realizar ao fazer requisições para um servidor.

### **GET**: Solicita dados do servidor
   - Usado para leitura de dados
   - Não deve modificar dados no servidor
   
```javascript
// Exemplo usando a API pública do GitHub para buscar dados de um usuário
fetch('https://api.github.com/users/github')
    .then(response => response.json())
    .then(data => {
        console.log('Dados do usuário:', data);
        // Aqui você terá acesso a: data.login, data.avatar_url, data.name, etc.
    })
    .catch(error => console.error('Erro:', error));
```

### **POST**: Envia dados para o servidor
   - Usado para criar novos recursos
   
```javascript
// Exemplo usando a JSONPlaceholder API para criar um post
fetch('https://jsonplaceholder.typicode.com/posts', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        title: 'Novo Post',
        body: 'Conteúdo do post',
        userId: 1
    })
})
.then(response => response.json())
.then(data => console.log('Post criado:', data))
.catch(error => console.error('Erro:', error));
```

### **PUT**: Atualiza dados existentes
   - Substitui completamente um recurso

```javascript
// Exemplo usando JSONPlaceholder para atualizar um post completo
fetch('https://jsonplaceholder.typicode.com/posts/1', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        id: 1,
        title: 'Post Atualizado',
        body: 'Conteúdo atualizado',
        userId: 1
    })
})
.then(response => response.json())
.then(data => console.log('Post atualizado:', data))
.catch(error => console.error('Erro:', error));
```

### **PATCH**: Atualiza dados parcialmente
   - Modifica apenas alguns campos

```javascript
// Exemplo usando JSONPlaceholder para atualizar apenas o título de um post
fetch('https://jsonplaceholder.typicode.com/posts/1', {
    method: 'PATCH',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        title: 'Apenas Título Atualizado'
    })
})
.then(response => response.json())
.then(data => console.log('Post parcialmente atualizado:', data))
.catch(error => console.error('Erro:', error));
```

### **DELETE**: Remove dados
   - Exclui um recurso

```javascript
// Exemplo usando JSONPlaceholder para deletar um post
fetch('https://jsonplaceholder.typicode.com/posts/1', {
    method: 'DELETE'
})
.then(response => {
    if (response.ok) {
        console.log('Post deletado com sucesso');
    }
})
.catch(error => console.error('Erro:', error));
```

## 2. Manipulação de JSON

### Exemplo Prático com Dados do OpenWeather API:
```javascript
// Exemplo de objeto JavaScript
const dadosClimaticos = {
    cidade: "São Paulo",
    temperatura: 25.6,
    condicoes: ["ensolarado", "parcialmente nublado"],
    vento: {
        velocidade: 12,
        direcao: "nordeste"
    }
};

// Convertendo para JSON
const jsonString = JSON.stringify(dadosClimaticos);
console.log('JSON:', jsonString);
// Resultado: {"cidade":"São Paulo","temperatura":25.6,"condicoes":["ensolarado","parcialmente nublado"],"vento":{"velocidade":12,"direcao":"nordeste"}}

// Convertendo JSON de volta para objeto
const objetoConvertido = JSON.parse(jsonString);
console.log('Objeto:', objetoConvertido.cidade); // São Paulo
console.log('Temperatura:', objetoConvertido.temperatura); // 25.6
```

## 3. AJAX com Fetch API

- AJAX (Asynchronous JavaScript and XML) é uma técnica de desenvolvimento web que permite fazer requisições ao servidor e atualizar partes de uma página web sem recarregá-la por completo. Hoje em dia, apesar do nome incluir "XML", é muito mais comum usar JSON como formato de dados.

### Principais características do AJAX:
- Assíncrono: não bloqueia a execução do resto do código
- Dinâmico: permite atualizações parciais da página
- Melhor experiência do usuário: não precisa recarregar a página inteira

### Exemplo usando a API do CatFact (Fatos sobre Gatos):
```javascript
// Função assíncrona para buscar fatos sobre gatos
async function buscarFatoGato() {
    try {
        const response = await fetch('https://catfact.ninja/fact');
        const data = await response.json();
        console.log('Fato sobre gato:', data.fact);
    } catch (error) {
        console.error('Erro ao buscar fato:', error);
    }
}

// Exemplo com tratamento de erros e headers personalizados
fetch('https://api.thecatapi.com/v1/images/search', {
    headers: {
        'x-api-key': 'sua-chave-api'  // Exemplo de header personalizado
    }
})
.then(response => {
    if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
})
.then(data => console.log('Imagem de gato:', data[0].url))
.catch(error => console.error('Erro:', error));
```

## 4. XMLHttpRequest

### Exemplo usando a API do JSONPlaceholder:
```javascript
function buscarPost() {
    const xhr = new XMLHttpRequest();
    
    xhr.onreadystatechange = function() {
        if (xhr.readyState === XMLHttpRequest.DONE) {
            if (xhr.status === 200) {
                const data = JSON.parse(xhr.responseText);
                console.log('Post:', data);
            } else {
                console.error('Erro:', xhr.status);
            }
        }
    };

    // Exemplo de monitoramento do progresso
    xhr.onprogress = function(event) {
        if (event.lengthComputable) {
            const percentComplete = (event.loaded / event.total) * 100;
            console.log(`Progresso: ${percentComplete}%`);
        }
    };

    xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts/1');
    xhr.send();
}

// Exemplo de POST com XMLHttpRequest
function criarPost() {
    const xhr = new XMLHttpRequest();
    xhr.open('POST', 'https://jsonplaceholder.typicode.com/posts');
    
    xhr.setRequestHeader('Content-Type', 'application/json');
    
    xhr.onload = function() {
        if (xhr.status === 201) {
            const response = JSON.parse(xhr.responseText);
            console.log('Post criado:', response);
        }
    };

    const data = {
        title: 'Novo Post XMLHttpRequest',
        body: 'Conteúdo do post',
        userId: 1
    };

    xhr.send(JSON.stringify(data));
}
```

## 5. Exemplo Prático Completo

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokedex</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            background-color: #f5f5f5;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }

        h1 {
            text-align: center;
            color: #e3350d;
            margin-bottom: 20px;
        }

        .search-container {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        input {
            flex: 1;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }

        button {
            padding: 10px 20px;
            background-color: #e3350d;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #b82d0d;
        }

        .pokemon-card {
            background-color: #fff;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            display: none;
        }

        .pokemon-card.active {
            display: block;
        }

        .pokemon-image {
            width: 200px;
            height: 200px;
            margin: 20px auto;
        }

        .pokemon-info {
            margin-top: 20px;
        }

        .pokemon-types {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin: 10px 0;
        }

        .type-badge {
            padding: 5px 15px;
            border-radius: 20px;
            color: white;
            font-size: 14px;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 20px;
        }

        .stat-item {
            background-color: #f5f5f5;
            padding: 10px;
            border-radius: 5px;
        }

        .loading {
            display: none;
            text-align: center;
            margin: 20px 0;
        }

        .error-message {
            color: #e3350d;
            text-align: center;
            margin: 20px 0;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Pokedex</h1>
        
        <div class="search-container">
            <input 
                type="text" 
                id="pokemonInput" 
                placeholder="Digite o nome do Pokémon ou número"
            >
            <button onclick="buscarPokemon()">Buscar</button>
        </div>

        <div id="loading" class="loading">Carregando...</div>
        <div id="errorMessage" class="error-message"></div>

        <div id="pokemonCard" class="pokemon-card">
            <h2 id="pokemonName"></h2>
            <img id="pokemonImage" class="pokemon-image" src="" alt="Pokemon">
            
            <div class="pokemon-info">
                <div id="pokemonTypes" class="pokemon-types"></div>
                
                <div class="stats-container">
                    <div class="stat-item">
                        <strong>Altura:</strong>
                        <span id="pokemonHeight"></span>
                    </div>
                    <div class="stat-item">
                        <strong>Peso:</strong>
                        <span id="pokemonWeight"></span>
                    </div>
                    <div class="stat-item">
                        <strong>Habilidades:</strong>
                        <span id="pokemonAbilities"></span>
                    </div>
                    <div class="stat-item">
                        <strong>Experiência Base:</strong>
                        <span id="pokemonBaseExp"></span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Cores para os tipos de Pokémon
        const typeColors = {
            normal: '#A8A878',
            fire: '#F08030',
            water: '#6890F0',
            electric: '#F8D030',
            grass: '#78C850',
            ice: '#98D8D8',
            fighting: '#C03028',
            poison: '#A040A0',
            ground: '#E0C068',
            flying: '#A890F0',
            psychic: '#F85888',
            bug: '#A8B820',
            rock: '#B8A038',
            ghost: '#705898',
            dragon: '#7038F8',
            dark: '#705848',
            steel: '#B8B8D0',
            fairy: '#EE99AC'
        };

        // Adicionar evento de tecla Enter no input
        document.getElementById('pokemonInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                buscarPokemon();
            }
        });

        async function buscarPokemon() {
            const input = document.getElementById('pokemonInput');
            const pokemonCard = document.getElementById('pokemonCard');
            const loading = document.getElementById('loading');
            const errorMessage = document.getElementById('errorMessage');

            // Limpar mensagens anteriores
            errorMessage.style.display = 'none';
            loading.style.display = 'block';
            pokemonCard.classList.remove('active');

            try {
                const pokemonName = input.value.toLowerCase().trim();
                if (!pokemonName) {
                    throw new Error('Por favor, digite o nome de um Pokémon');
                }

                const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemonName}`);
                
                if (!response.ok) {
                    throw new Error('Pokémon não encontrado!');
                }

                const data = await response.json();
                mostrarPokemon(data);
                
            } catch (error) {
                errorMessage.textContent = error.message;
                errorMessage.style.display = 'block';
            } finally {
                loading.style.display = 'none';
            }
        }

        function mostrarPokemon(data) {
            // Atualizar informações básicas
            document.getElementById('pokemonName').textContent = 
                data.name.charAt(0).toUpperCase() + data.name.slice(1);
            document.getElementById('pokemonImage').src = 
                data.sprites.other['official-artwork'].front_default || data.sprites.front_default;
            document.getElementById('pokemonHeight').textContent = `${data.height / 10}m`;
            document.getElementById('pokemonWeight').textContent = `${data.weight / 10}kg`;
            document.getElementById('pokemonBaseExp').textContent = `${data.base_experience || 'N/A'}`;
            
            // Atualizar habilidades
            const abilities = data.abilities
                .map(ability => ability.ability.name.replace('-', ' '))
                .map(str => str.charAt(0).toUpperCase() + str.slice(1))
                .join(', ');
            document.getElementById('pokemonAbilities').textContent = abilities;

            // Atualizar tipos
            const typesContainer = document.getElementById('pokemonTypes');
            typesContainer.innerHTML = '';
            
            data.types.forEach(type => {
                const typeElement = document.createElement('span');
                typeElement.className = 'type-badge';
                typeElement.textContent = type.type.name.toUpperCase();
                typeElement.style.backgroundColor = typeColors[type.type.name] || '#777';
                typesContainer.appendChild(typeElement);
            });

            // Mostrar card
            document.getElementById('pokemonCard').classList.add('active');
        }
    </script>
</body>
</html>
```
