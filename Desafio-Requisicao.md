# Desafio: API de Países

Este exemplo demonstra o uso de async/await com fetch para consumir a API pública RestCountries. A aplicação permite buscar países e exibir informações como bandeira, capital, população e região.

## Recursos Implementados
- Async/await com fetch para chamadas à API
- Debounce na busca para otimizar requisições 
- Loading state durante as requisições
- Tratamento de erros
- Interface responsiva com Bootstrap
- Cards interativos com efeito hover

## Código Completo
```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Buscador de Países</title>
   <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
   <style>
       .country-card {
           transition: transform 0.3s;
       }
       .country-card:hover {
           transform: translateY(-5px);
       }
       .flag-img {
           height: 150px;
           object-fit: cover;
       }
   </style>
</head>
<body class="bg-light">
   <div class="container py-5">
       <h1 class="text-center mb-4">Buscador de Países</h1>
       
       <div class="row justify-content-center mb-4">
           <div class="col-md-6">
               <input type="text" id="searchInput" class="form-control" placeholder="Digite o nome do país...">
           </div>
       </div>

       <div id="countriesContainer" class="row g-4"></div>
       
       <div id="loading" class="text-center d-none">
           <div class="spinner-border text-primary" role="status">
               <span class="visually-hidden">Carregando...</span>
           </div>
       </div>
   </div>

   <script>
       const searchInput = document.getElementById('searchInput');
       const countriesContainer = document.getElementById('countriesContainer');
       const loading = document.getElementById('loading');

       async function searchCountries(searchTerm) {
           try {
               loading.classList.remove('d-none');
               const response = await fetch(`https://restcountries.com/v3.1/name/${searchTerm}`);
               
               if (!response.ok) {
                   throw new Error('País não encontrado');
               }

               const data = await response.json();
               return data;
           } catch (error) {
               console.error('Erro:', error);
               return [];
           } finally {
               loading.classList.add('d-none');
           }
       }

       function createCountryCard(country) {
           return `
               <div class="col-md-4">
                   <div class="card country-card h-100">
                       <img src="${country.flags.png}" class="card-img-top flag-img" alt="Bandeira ${country.name.common}">
                       <div class="card-body">
                           <h5 class="card-title">${country.name.common}</h5>
                           <p class="card-text">
                               <strong>Capital:</strong> ${country.capital?.[0] || 'N/A'}<br>
                               <strong>População:</strong> ${country.population.toLocaleString()}<br>
                               <strong>Região:</strong> ${country.region}
                           </p>
                       </div>
                   </div>
               </div>
           `;
       }

       let debounceTimeout;
       searchInput.addEventListener('input', (e) => {
           clearTimeout(debounceTimeout);
           debounceTimeout = setTimeout(async () => {
               const searchTerm = e.target.value.trim();
               if (searchTerm.length >= 2) {
                   const countries = await searchCountries(searchTerm);
                   countriesContainer.innerHTML = countries
                       .map(country => createCountryCard(country))
                       .join('');
               } else {
                   countriesContainer.innerHTML = '';
               }
           }, 300);
       });
   </script>
</body>
</html>
```

## Desafio para Prática
### Adicione as seguintes features ao projeto:

### Tema Escuro/Claro

- Implemente um botão para alternar entre modo claro e escuro
- Altere cores do fundo, cards e textos
- Persista a preferência do usuário no localStorage


### Filtro por Região

- Adicione um dropdown para filtrar países por região
- Use o endpoint: https://restcountries.com/v3.1/region/{region}
- Combine com a busca por nome se necessário


### Modal de Detalhes

- Ao clicar em um país, abra um modal com informações adicionais
- Mostre moeda, idiomas e países vizinhos
- Implemente navegação entre países vizinhos
