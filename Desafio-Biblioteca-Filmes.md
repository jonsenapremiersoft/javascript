# Desafio: Biblioteca de Filmes 🎬

## Parte 1: Configuração do Projeto

1. Crie uma nova pasta para o projeto
2. Abra o terminal e execute:
```bash
npm create vite@latest movie-library -- --template vanilla
cd movie-library
npm install
```

3. Instale as dependências necessárias:
```bash
npm install bootstrap axios
```

4. Substitua o conteúdo do `index.html`:
```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Biblioteca de Filmes</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body>
    <nav class="navbar navbar-dark bg-dark mb-4">
      <div class="container">
        <span class="navbar-brand">🎬 Biblioteca de Filmes</span>
        <div class="d-flex">
          <input type="search" id="searchInput" class="form-control me-2" placeholder="Buscar filme...">
          <button id="searchButton" class="btn btn-outline-light">Buscar</button>
        </div>
      </div>
    </nav>

    <main class="container">
      <div id="moviesList" class="row g-4">
        <!-- Os cards dos filmes serão inseridos aqui -->
      </div>
    </main>

    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

5. Crie a estrutura base dos arquivos JavaScript:

`src/main.js`:
```javascript
import { searchMovies } from './services/api.js';
import { renderMovies } from './components/movieCard.js';

// TODO: Implementar a lógica de busca
document.getElementById('searchButton').addEventListener('click', () => {
  // Sua implementação aqui
});

// Carregar alguns filmes iniciais
searchMovies('marvel').then(movies => {
  renderMovies(movies);
});
```

`src/services/api.js`:
```javascript
const API_KEY = 'SUA_CHAVE_OMDB_AQUI'; // Você pode usar: 'trilogy'
const BASE_URL = 'https://www.omdbapi.com';

export async function searchMovies(query) {
  // TODO: Implementar a busca usando fetch ou axios
  // Retornar um array de filmes da API
}
```

`src/components/movieCard.js`:
```javascript
export function renderMovies(movies) {
  const moviesList = document.getElementById('moviesList');
  moviesList.innerHTML = ''; // Limpa a lista atual

  // TODO: Para cada filme, criar um card usando Bootstrap
  // Dica: Use as classes 'col-md-4 mb-4' para o container do card
}

export function createMovieCard(movie) {
  // TODO: Criar e retornar o HTML do card do filme
  // Dica: Use as classes do Bootstrap para criar um card bonito
}
```

`src/styles/custom.css`:
```css
/* TODO: Adicionar estilos personalizados */
.movie-card {
  transition: transform 0.2s;
}

.movie-card:hover {
  /* Adicionar efeito hover */
}
```

## Parte 2: O Desafio

### Objetivos:
1. Implementar a função `searchMovies` usando a API do OMDB (http://www.omdbapi.com/)
2. Criar o layout dos cards dos filmes usando Bootstrap
3. Implementar a funcionalidade de busca
4. Adicionar alguns efeitos CSS personalizados

### Bônus (se houver tempo):
- Adicionar loading state durante a busca
- Implementar paginação
- Adicionar um modal com mais detalhes do filme ao clicar no card

### APIs Sugeridas:
- OMDB API (http://www.omdbapi.com/) - API de filmes, fácil de usar
- Chave da API: 'trilogy' (limitada, mas funcional para o exercício)

### Dicas:
- Use async/await para as chamadas à API
- Lembre-se de tratar erros nas requisições
- Mantenha o código organizado em módulos
- Use as classes do Bootstrap para agilizar o layout
