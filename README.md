# Lista de Tarefas

Essa aplicação é uma simples lista de tarefas desenvolvida com React e utilizando o Vite como ferramenta de build. Nela, você pode adicionar, remover, buscar e filtrar suas tarefas. A lista é salva no LocalStorage, o que permite manter as tarefas mesmo após fechar o navegador.

## Funcionalidades

° Adicionar Tarefas: Adicione novas tarefas com uma descrição e categoria.
° Remover Tarefas: Exclua as tarefas que não são mais necessárias.
° Marcar como Concluída: Marque tarefas como concluídas ou desfaça essa ação.
° Buscar Tarefas: Utilize o campo de busca para encontrar uma tarefa específica.
° Filtrar Tarefas: Filtre as tarefas por status (concluídas ou pendentes).
° Ordenação: Ordene suas tarefas em ordem alfabética ascendente ou descendente.

## Como rodar a aplicação

Para executar a aplicação localmente, siga os passos abaixo:

1 Clone o repositório: git clone https://github.com/seuusuario/nome-do-repositorio.git

2 Instale as dependências: Na pasta do projeto, execute:

° npm install

3 Rode o projeto: Após a instalação, inicie o servidor de desenvolvimento com:

° npm run dev

4 Acesse a aplicação: Abra o navegador e vá para o endereço:

° http://localhost:3000

## Sobre o Template Vite

Este projeto foi configurado usando o Vite, uma ferramenta de build extremamente rápida e moderna para projetos frontend. O Vite oferece um HMR (Hot Module Replacement), o que significa que você pode ver suas mudanças no código refletirem na página imediatamente, sem precisar recarregar o navegador. Isso acelera o desenvolvimento, especialmente com React.

## Explicações sobre o código

Armazenamento de Tarefas no LocalStorage

As tarefas são armazenadas no LocalStorage, permitindo que os dados permaneçam disponíveis mesmo após recarregar a página. Isso é feito no useState, carregando os dados salvos, e no useEffect, que atualiza o LocalStorage toda vez que a lista de tarefas muda.

const [todos, setTodos] = useState(() => {
  const savedTodos = localStorage.getItem("todos");
  return savedTodos ? JSON.parse(savedTodos) : [];
});

useEffect(() => {
  localStorage.setItem("todos", JSON.stringify(todos));
}, [todos]);


## Função addTodo

Esta função permite adicionar novas tarefas à lista. Cada nova tarefa recebe um id gerado aleatoriamente e as demais informações fornecidas pelo usuário.

const addTodo = (text, category) => {
  const newTodos = [
    ...todos,
    {
      id: Math.floor(Math.random() * 10000),
      text,
      category,
      isCompleted: false,
    },
  ];
  setTodos(newTodos);
};


## Função completeTodo

Alterna o status de conclusão de uma tarefa, permitindo que o usuário marque uma tarefa como concluída ou desfaça essa ação.

const completeTodo = (id) => {
  const newTodos = [...todos];
  newTodos.map((todo) =>
    todo.id === id ? (todo.isCompleted = !todo.isCompleted) : todo
  );
  setTodos(newTodos);
};


## Estrutura do Projeto

src/components/Todo.js: Componente responsável por exibir uma única tarefa e seus controles de concluir e remover.
src/components/TodoForm.js: Formulário para adicionar novas tarefas.
src/components/Search.js: Componente para buscar tarefas.
src/components/Filter.js: Filtro para exibir tarefas concluídas ou pendentes.
