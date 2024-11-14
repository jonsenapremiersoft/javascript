# Async/Await

## Introdução
Async/await é uma forma moderna de lidar com programação assíncrona em JavaScript, tornando o código mais limpo e fácil de entender em comparação com callbacks e Promises.

## Conceitos Fundamentais

### 1. Funções Assíncronas
Uma função assíncrona é declarada usando a palavra-chave `async`:

```javascript
async function minhaFuncao() {
    // código assíncrono aqui
}

// Com arrow function
const minhaFuncao = async () => {
    // código assíncrono aqui
};
```

### 2. A palavra-chave await
- Só pode ser usada dentro de funções async
- Pausa a execução até que a Promise seja resolvida
- Retorna o valor resolvido da Promise

```javascript
async function buscarUsuario() {
    const response = await fetch('https://api.exemplo.com/usuario/1');
    const usuario = await response.json();
    return usuario;
}
```

## APIs que Utilizaremos
- JSONPlaceholder (Posts e Usuários)
- PokeAPI (Dados de Pokémon)

## 1. Conceitos Básicos com JSONPlaceholder

### Buscando Posts
```javascript
async function buscarPosts() {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const posts = await response.json();
        return posts;
    } catch (erro) {
        console.error('Erro ao buscar posts:', erro);
        throw erro;
    }
}

// Teste
buscarPosts().then(posts => console.log('Posts:', posts.slice(0, 3)));
```

### Buscando Post e Comentários
```javascript
async function buscarPostEComentarios(postId) {
    try {
        // Buscas paralelas
        const [post, comentarios] = await Promise.all([
            fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`).then(r => r.json()),
            fetch(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`).then(r => r.json())
        ]);

        return { post, comentarios };
    } catch (erro) {
        console.error('Erro ao buscar post e comentários:', erro);
        throw erro;
    }
}

// Teste
buscarPostEComentarios(1).then(dados => console.log('Post e Comentários:', dados));
```

## 2. Trabalhando com a PokeAPI

### Sistema de Cache com Pokémon
```javascript
class PokemonService {
    constructor() {
        this.cache = new Map();
    }

    async buscarPokemon(nome) {
        // Verifica cache
        if (this.cache.has(nome)) {
            console.log('Retornando do cache');
            return this.cache.get(nome);
        }

        try {
            const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${nome.toLowerCase()}`);
            if (!response.ok) throw new Error('Pokémon não encontrado');
            
            const pokemon = await response.json();
            
            // Salva no cache
            this.cache.set(nome, pokemon);
            
            return pokemon;
        } catch (erro) {
            console.error('Erro ao buscar Pokémon:', erro);
            throw erro;
        }
    }
}

// Teste
const pokemonService = new PokemonService();
async function testarPokemon() {
    const pikachu = await pokemonService.buscarPokemon('pikachu');
    console.log('Pikachu:', {
        nome: pikachu.name,
        altura: pikachu.height,
        peso: pikachu.weight,
        tipos: pikachu.types.map(t => t.type.name)
    });
}

testarPokemon();
```
