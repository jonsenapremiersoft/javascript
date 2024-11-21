# Desafio: Sistema de Biblioteca com POO em JavaScript

## Objetivo
Criar um sistema de gerenciamento de biblioteca usando Programação Orientada a Objetos (POO) em JavaScript, implementando operações básicas como adicionar livros e gerenciar empréstimos.

## Requisitos Funcionais
- Cadastrar novos livros com título, autor e número de páginas
- Visualizar lista de livros cadastrados
- Gerenciar empréstimos/devoluções de livros
- Interface responsiva usando Bootstrap

## Estrutura de Classes
1. `Livro`: Gerencia dados e estado do livro
2. `Biblioteca`: Mantém a coleção de livros
3. `UI`: Controla a interface do usuário

## Desafios Extra
1. Criar classe `Categoria` para classificação de livros
2. Implementar sistema de busca e filtros

## Tecnologias
- HTML5
- CSS3 (Bootstrap 5)
- JavaScript (POO)

## Critérios de Avaliação
- Uso correto dos conceitos de POO
- Organização do código
- Interface responsiva
- Tratamento de erros
- Funcionalidades extras implementadas

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Biblioteca POO</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
    <div class="container py-5">
        <h1 class="text-center mb-4">Gerenciador de Biblioteca</h1>
        
        <div class="row">
            <div class="col-md-6">
                <div class="card mb-4">
                    <div class="card-header">
                        Adicionar Livro
                    </div>
                    <div class="card-body">
                        <form id="livroForm">
                            <div class="mb-3">
                                <input type="text" class="form-control" id="titulo" placeholder="Título" required>
                            </div>
                            <div class="mb-3">
                                <input type="text" class="form-control" id="autor" placeholder="Autor" required>
                            </div>
                            <div class="mb-3">
                                <input type="number" class="form-control" id="paginas" placeholder="Número de Páginas" required>
                            </div>
                            <button type="submit" class="btn btn-primary">Adicionar Livro</button>
                        </form>
                    </div>
                </div>
            </div>
            
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header">
                        Lista de Livros
                    </div>
                    <div class="card-body">
                        <ul id="listaLivros" class="list-group"></ul>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        class Livro {
            constructor(titulo, autor, paginas) {
                this.titulo = titulo;
                this.autor = autor;
                this.paginas = paginas;
                this.emprestado = false;
            }

            emprestar() {
                if (!this.emprestado) {
                    this.emprestado = true;
                    return true;
                }
                return false;
            }

            devolver() {
                if (this.emprestado) {
                    this.emprestado = false;
                    return true;
                }
                return false;
            }
        }

        class Biblioteca {
            static livros = [];

            static adicionarLivro(livro) {
                this.livros.push(livro);
            }

            static listarLivros() {
                return this.livros;
            }
        }

        class UI {
            static exibirLivros() {
                const listaLivros = document.getElementById('listaLivros');
                listaLivros.innerHTML = '';

                Biblioteca.listarLivros().forEach((livro, index) => {
                    const li = document.createElement('li');
                    li.className = 'list-group-item d-flex justify-content-between align-items-center';
                    li.innerHTML = `
                        <div>
                            <h5 class="mb-1">${livro.titulo}</h5>
                            <small>por ${livro.autor}</small>
                            <p class="mb-1">${livro.paginas} páginas</p>
                        </div>
                        <button class="btn btn-sm ${livro.emprestado ? 'btn-warning' : 'btn-success'}" 
                                onclick="UI.toggleEmprestimo(${index})">
                            ${livro.emprestado ? 'Devolver' : 'Emprestar'}
                        </button>
                    `;
                    listaLivros.appendChild(li);
                });
            }

            static adicionarLivro(e) {
                e.preventDefault();

                const titulo = document.getElementById('titulo').value;
                const autor = document.getElementById('autor').value;
                const paginas = document.getElementById('paginas').value;

                const livro = new Livro(titulo, autor, paginas);
                Biblioteca.adicionarLivro(livro);

                UI.limparCampos();
                UI.exibirLivros();
            }

            static toggleEmprestimo(index) {
                const livros = Biblioteca.listarLivros();
                const livro = livros[index];
                
                if (livro.emprestado) {
                    livro.devolver();
                } else {
                    livro.emprestar();
                }

                UI.exibirLivros();
            }

            static limparCampos() {
                document.getElementById('titulo').value = '';
                document.getElementById('autor').value = '';
                document.getElementById('paginas').value = '';
            }
        }

        document.getElementById('livroForm').addEventListener('submit', UI.adicionarLivro);
        UI.exibirLivros();
    </script>
</body>
</html>
```
