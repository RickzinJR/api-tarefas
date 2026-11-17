# API de Tarefas

API REST para gerenciamento de tarefas, construída em Node.js e Express seguindo o padrão MVC.

Projeto desenvolvido durante o curso de Análise e Desenvolvimento de Sistemas na FECAP, com foco em entender na prática como uma API REST funciona: rotas, verbos HTTP, códigos de status e separação de responsabilidades.

## Funcionalidades

A API expõe um CRUD completo sobre o recurso `tarefas`:

| Método | Rota | Descrição | Status de sucesso |
|---|---|---|---|
| `GET` | `/tarefas` | Lista todas as tarefas | `200 OK` |
| `POST` | `/tarefas` | Cria uma nova tarefa | `201 Created` |
| `PUT` | `/tarefas/:id` | Atualiza uma tarefa existente | `200 OK` |
| `DELETE` | `/tarefas/:id` | Remove uma tarefa | `204 No Content` |

Quando o `id` informado não existe, a API responde `404 Not Found`.

## Tecnologias

- **Node.js** — ambiente de execução
- **Express** — roteamento e tratamento de requisições
- **Postman** — coleção de testes incluída no repositório

## Arquitetura

O projeto segue o padrão **MVC**, separando responsabilidades em camadas:

```
tarefas-api/
├── src/
│   ├── routes/         # Define as rotas e os verbos HTTP
│   ├── controllers/    # Recebe a requisição e devolve a resposta
│   ├── models/         # Guarda e manipula os dados
│   ├── app.js          # Configura o Express e os middlewares
│   └── server.js       # Sobe o servidor
├── postman_collection.json
└── package.json
```

A rota não sabe como o dado é guardado e o model não sabe que existe HTTP. Essa separação facilita trocar a camada de dados depois, por exemplo substituindo o armazenamento em memória por um banco, sem mexer nos controllers.

## Como executar

Requer Node.js instalado.

```bash
git clone https://github.com/RickzinJR/api-tarefas.git
cd api-tarefas/tarefas-api
npm install
npm run dev
```

O servidor sobe em `http://localhost:3000`.

## Exemplos de uso

**Listar tarefas**

```bash
curl http://localhost:3000/tarefas
```

**Criar uma tarefa**

```bash
curl -X POST http://localhost:3000/tarefas \
  -H "Content-Type: application/json" \
  -d '{ "titulo": "Estudar Node", "concluida": false }'
```

**Atualizar uma tarefa**

```bash
curl -X PUT http://localhost:3000/tarefas/1 \
  -H "Content-Type: application/json" \
  -d '{ "titulo": "Estudar Node.js", "concluida": true }'
```

**Remover uma tarefa**

```bash
curl -X DELETE http://localhost:3000/tarefas/1
```

### Testando no Postman

O arquivo `postman_collection.json` está na pasta `tarefas-api`. Importe-o no Postman para ter todas as requisições prontas.

## Próximos passos

- [ ] Persistir os dados em banco (MySQL) no lugar do armazenamento em memória
- [ ] Validar os dados de entrada
- [ ] Autenticação com JWT
- [ ] Testes automatizados

## Autor

**Ricardo Oliveira** — Estudante de Análise e Desenvolvimento de Sistemas na FECAP

[LinkedIn](https://linkedin.com/in/ricardoojunior) · [GitHub](https://github.com/RickzinJR)
