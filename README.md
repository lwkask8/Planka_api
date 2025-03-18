# Planka_api
Documentação da API Planka
Esta API permite interagir com o Planka, um sistema de gerenciamento de projetos e tarefas. Ela oferece operações para gerenciar projetos, quadros (boards), listas e cartões.

URL Base
A URL base da API é configurada pela variável de ambiente BASE_URL. Exemplo:

https://Baseurl

Autenticação
Todas as requisições devem incluir um token de autenticação no cabeçalho Authorization. O token é gerado automaticamente ao instanciar a classe PlankaAPI.

Formato do cabeçalho:
Copy
Authorization: Bearer <token>
Endpoints
Endpoint Principal
Método: POST

URL: https://Baseurl/api/execute

Descrição: Executa uma ação no Planka com base nas instruções fornecidas.

Corpo da Requisição (JSON):

json
Copy
{
  "action": "<nome_da_acao>",
  "outros_parametros": "valor"
}
action: Nome da ação a ser executada (obrigatório).

outros_parametros: Parâmetros adicionais dependendo da ação.

Ações Suportadas
1. Projetos
a) Listar Projetos
Ação: get_projects

Descrição: Retorna a lista de todos os projetos.

Exemplo de Requisição:

json
Copy
{
  "action": "get_projects"
}
b) Obter Projeto por ID
Ação: get_project_by_id

Parâmetros:

project_id (obrigatório): ID do projeto.

Exemplo de Requisição:

json
Copy
{
  "action": "get_project_by_id",
  "project_id": "12345"
}
c) Criar Projeto
Ação: create_project

Parâmetros:

name (obrigatório): Nome do projeto.

description (opcional): Descrição do projeto.

Exemplo de Requisição:

json
Copy
{
  "action": "create_project",
  "name": "Novo Projeto",
  "description": "Descrição do novo projeto"
}
d) Atualizar Projeto
Ação: update_project

Parâmetros:

project_id (obrigatório): ID do projeto.

name (opcional): Novo nome do projeto.

description (opcional): Nova descrição do projeto.

Exemplo de Requisição:

json
Copy
{
  "action": "update_project",
  "project_id": "12345",
  "name": "Projeto Atualizado",
  "description": "Nova descrição"
}
e) Deletar Projeto
Ação: delete_project

Parâmetros:

project_id (obrigatório): ID do projeto.

Exemplo de Requisição:

json
Copy
{
  "action": "delete_project",
  "project_id": "12345"
}
2. Quadros (Boards)
a) Listar Quadros de um Projeto
Ação: get_boards

Parâmetros:

project_id (obrigatório): ID do projeto.

Exemplo de Requisição:

json
Copy
{
  "action": "get_boards",
  "project_id": "12345"
}
b) Obter Quadro por ID
Ação: get_board_by_id

Parâmetros:

board_id (obrigatório): ID do quadro.

Exemplo de Requisição:

json
Copy
{
  "action": "get_board_by_id",
  "board_id": "67890"
}
3. Listas
a) Listar Listas de um Quadro
Ação: get_lists

Parâmetros:

board_id (obrigatório): ID do quadro.

Exemplo de Requisição:

json
Copy
{
  "action": "get_lists",
  "board_id": "67890"
}
b) Obter Lista por ID
Ação: get_list_by_id

Parâmetros:

list_id (obrigatório): ID da lista.

Exemplo de Requisição:

json
Copy
{
  "action": "get_list_by_id",
  "list_id": "54321"
}
4. Cartões
a) Listar Cartões de uma Lista
Ação: get_cards

Parâmetros:

list_id (obrigatório): ID da lista.

Exemplo de Requisição:

json
Copy
{
  "action": "get_cards",
  "list_id": "54321"
}
b) Obter Cartão por ID
Ação: get_card_by_id

Parâmetros:

card_id (obrigatório): ID do cartão.

Exemplo de Requisição:

json
Copy
{
  "action": "get_card_by_id",
  "card_id": "98765"
}
c) Mover Cartão para Outra Lista
Ação: move_card

Parâmetros:

card_id (obrigatório): ID do cartão.

list_id (obrigatório): ID da lista de destino.

Exemplo de Requisição:

json
Copy
{
  "action": "move_card",
  "card_id": "98765",
  "list_id": "54321"
}
d) Atualizar Cartão
Ação: update_card

Parâmetros:

card_id (obrigatório): ID do cartão.

name (opcional): Novo nome do cartão.

description (opcional): Nova descrição do cartão.

Exemplo de Requisição:

json
Copy
{
  "action": "update_card",
  "card_id": "98765",
  "name": "Cartão Atualizado",
  "description": "Nova descrição"
}
Exemplos de Uso
Exemplo 1: Listar Projetos
bash
Copy
curl -X POST https://baseurl/api/execute \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer meu_token_secreto" \
     -d '{"action": "get_projects"}'
Exemplo 2: Criar Projeto
bash
Copy
curl -X POST https://baseurl/api/execute \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer meu_token_secreto" \
     -d '{
           "action": "create_project",
           "name": "Meu Novo Projeto",
           "description": "Descrição do projeto"
         }'
Exemplo 3: Mover Cartão
bash
Copy
curl -X POST https://baseurl/api/execute \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer meu_token_secreto" \
     -d '{
           "action": "move_card",
           "card_id": "98765",
           "list_id": "54321"
         }'
Respostas da API
Sucesso: Retorna um JSON com os dados solicitados.

Erro: Retorna um JSON com uma mensagem de erro e um código de status HTTP.

Exemplo de resposta de sucesso:

json
Copy
{
  "item": [
    {
      "id": "12345",
      "name": "Projeto 1",
      "description": "Descrição do Projeto 1"
    }
  ]
}
Exemplo de resposta de erro:

json
Copy
{
  "error": "Token inválido ou ausente"
}
